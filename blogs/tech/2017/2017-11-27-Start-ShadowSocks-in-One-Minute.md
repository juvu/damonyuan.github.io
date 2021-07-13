---
title:  "Start ShadowSocks in One Minute"
description: "For the reason you know what, it is always difficult to access github or run some command to fetch remote resource from inside China network. One of the solution is to punch a hole in the Great Wall by setting up ShadowSocks proxy to route your traffic through secured tunnel. There are many great articles to introduce the theory of ShadowSocks and the installation of it, but there is none that automate the process of it. Here is a a automation shell script to help start ShadowSocks server and client in a minute, and it is tested on Ubuntu 16.04. Feel free to modify it according to your requirement."
date: 2017-11-27 12:08:00
categories: [Tech]
tags: [DevOps]
---

# Start ShadowSocks in One Minute

> * Author: [Damon Yuan](https://www.damonyuan.com)
> * Date: 2017-11-27

For the reason you know what, it is always difficult to access github or run some command to fetch remote resource from inside China network. One of the solution is to punch a hole in the Great Wall by setting up ShadowSocks proxy to route your traffic through secured tunnel. There are many great articles to introduce the theory of ShadowSocks and the installation of it, but there is none that automate the process of it. Here is a a automation shell script to help start ShadowSocks server and client in a minute, and it is tested on Ubuntu 16.04. Feel free to modify it according to your requirement.

* Theory of ShadowSocks: [你也能写个 ShadowSocks](https://github.com/gwuhaolin/blog/issues/12 "你也能写个 Shadowsocks"); [ShadowSocks 源代码分析](https://loggerhead.me/posts/shadowsocks-yuan-ma-fen-xi-xie-yi-yu-jie-gou.html#fn:router-problem)
* Set proxy for docker: [Docker网络代理设置](http://blog.csdn.net/styshoo/article/details/55657714 "Docker网络代理设置")
* Thanks to this article [为终端设置Shadowsocks代理](http://droidyue.com/blog/2016/04/04/set-shadowsocks-proxy-for-terminal/ "为终端设置Shadowsocks代理"), and the implementation of this script is based on it.

### Script:

```
#!/bin/bash
# ---------------------------------------------------------------------------
# ss_proxy - create shadowsocks server and client

# Copyright 2017,  <damon@Damons-Macbook.local>

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License at <http://www.gnu.org/licenses/> for
# more details.

# Usage: ss_proxy [-h|--help] [-sss|--shadowsocks_server] [-ssc|--shadowsocks_client]

# Revision history:
# 2017-11-27 Created by new_script ver. 3.3
# ---------------------------------------------------------------------------

PROGNAME=${0##*/}
VERSION="0.1"

clean_up() { # Perform pre-exit housekeeping
  return
}

error_exit() {
  echo -e "${PROGNAME}: ${1:-"Unknown Error"}" >&2
  clean_up
  exit 1
}

graceful_exit() {
  clean_up
  exit
}

signal_exit() { # Handle trapped signals
  case $1 in
    INT)
      error_exit "Program interrupted by user" ;;
    TERM)
      echo -e "\n$PROGNAME: Program terminated" >&2
      graceful_exit ;;
    *)
      error_exit "$PROGNAME: Terminating on unknown signal" ;;
  esac
}

usage() {
  echo -e "Usage: $PROGNAME [-h|--help] [-sss|--shadowsocks_server] [-ssc|--shadowsocks_client]"
}

help_message() {
  cat <<- _EOF_
  $PROGNAME ver. $VERSION
  create shadowsocks server and client

  $(usage)

  Options:
  -h, --help  Display this help message and exit.
  -sss, --shadowsocks_server  shadowsocks server
  -ssc, --shadowsocks_client  shadowsocks client

  NOTE: You must be the superuser to run this script.

_EOF_
  return
}

# Trap signals
trap "signal_exit TERM" TERM HUP
trap "signal_exit INT"  INT

# Check for root UID
if [[ $(id -u) != 0 ]]; then
  error_exit "You must be the superuser to run this script."
fi

install_shadowsocks() {
  apt-get update
  apt-get install -y python-pip python-dev build-essential
  pip install --upgrade pip
  pip install --upgrade virtualenv
  pip install shadowsocks
}

shadowsocks_server() {
  echo  -n "What is your shadowsocks server password? "
  read shadowsocks_password
  read -r -d '' json <<- _EOF_
    {
      "server":"0.0.0.0",
      "server_port":8388,
      "local_address":"127.0.0.1",
      "local_port":1080,
      "password":"${shadowsocks_password}",
      "timeout":300,
      "method":"rc4-md5",
      "fast_open": false,
      "workers": 2
    }
_EOF_
  echo $json > /etc/shadowsocks_server.json

  install_shadowsocks
  ssserver -c /etc/shadowsocks_server.json -d start
}

shadowsocks_client() {
  echo  -n "What is your shadowsocks server password? "
  read shadowsocks_password
  echo  -n "What is your shadowsocks server public ip address? "
  read public_ip
  read -r -d '' json <<- _EOF_
    {
      "server":"${public_ip}",
      "server_port":8388,
      "local_address":"127.0.0.1",
      "local_port":1080,
      "password":"${shadowsocks_password}",
      "timeout":300,
      "method":"rc4-md5"
    }
_EOF_
  echo $json > /etc/shadowsocks_client.json

  install_shadowsocks
  sslocal -c /etc/shadowsocks_client.json -d start

  apt-get install polipo
  read -r -d '' polipo <<- _EOF_
  logSyslog = true \n
  logFile = /var/log/polipo/polipo.log \n
  logLevel=4 \n
  socksParentProxy = "localhost:1080" \n
  socksProxyType = socks5 \n
_EOF_
  echo -e $polipo > /etc/polipo/config
  service polipo start

  echo -e "\nalias hp=\"http_proxy=http://localhost:8123 https_proxy=http://localhost:8123\"" >> ~/.bashrc
  echo -e "\ngp=\" --config http.proxy=localhost:8123\""
  source ~/.bashrc

  echo "Logout and ssh login again then you can start proxy by \`hp curl ip.gs\` or \`git clone  https://android.googlesource.com/tools/repo $gp\`"
}

# Parse command-line
while [[ -n $1 ]]; do
  case $1 in
    -h | --help)
      help_message; graceful_exit ;;
    -sss | --shadowsocks_server)
      echo "shadowsocks server"; shadowsocks_server ;;
    -ssc | --shadowsocks_client)
      echo "shadowsocks client"; shadowsocks_client ;;
    -* | --*)
      usage
      error_exit "Unknown option $1" ;;
    *)
      echo "Argument $1 to process..." ;;
  esac
  shift
done

# Main logic

graceful_exit
```
