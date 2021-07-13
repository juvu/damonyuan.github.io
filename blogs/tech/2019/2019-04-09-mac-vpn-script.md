---
title:  "Mac VPN script"
description: "Script to connect/disconnect a VPN"
date: 2019-04-09 15:04:23
categories: [Tech]
tags: [Shell]
---

# Mac VPN script

> * Author: [Damon Yuan](https://www.damonyuan.com)
> * Date: 2019-04-09

Remember to replace `YOUR_VPN_NAME`, `YOUR_USER_NAME`, `YOUR_PASSWD` with what your VPN configuration.

`YOUR_VPN_GATEWAY`, `YOUR_DEFAULT_GATEWAY` need to be changed accordingly if you want to configure the traffic routes in your local machine.

```
#!/bin/bash
# ---------------------------------------------------------------------------
# hsbc_vpn - start or stop vpn

# Copyright 2018,  <damon@Damons-Macbook.local>
# All rights reserved.

# Usage: hsbc_vpn [-h|--help] [-c|--connect] [-d|--disconnect]

# Revision history:
# 2018-09-07 Created by new_script ver. 3.3
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
  echo -e "Usage: $PROGNAME [-h|--help] [-c|--connect] [-d|--disconnect]"
}

help_message() {
  cat <<- _EOF_
  $PROGNAME ver. $VERSION
  start or stop vpn

  $(usage)

  Options:
  -h, --help  Display this help message and exit.
  -c, --connect  connect to vpn
  -d, --disconnect  disconnect from vpn

_EOF_
  return
}

# Trap signals
trap "signal_exit TERM" TERM HUP
trap "signal_exit INT"  INT

connect() {
/usr/bin/env osascript <<-EOF
set vpn_name to "'YOUR_VPN_NAME'"
set user_name to "YOUR_USER_NAME"
set passwd to "YOUR_PASSWD"

tell application "System Events"
        set rc to do shell script "scutil --nc status " & vpn_name
        if rc starts with "Disconnected" then
                do shell script "scutil --nc start " & vpn_name & " --user " & user_name & " --password " & passwd & " --secret " & passwd
                delay 5
                keystroke passwd
                keystroke return
        end if
end tell
EOF
}

disconnect() {
/usr/bin/env osascript <<-EOF
set vpn_name to "'Default'"

tell application "System Events"
        set rc to do shell script "scutil --nc status " & vpn_name
        if rc starts with "Connected" then
                do shell script "scutil --nc stop " & vpn_name
                keystroke return
        end if
end tell
EOF
}

all_traffic() {
  sudo route change default YOUR_VPN_GATEWAY
}

specific_traffic() {
  sudo route change default YOUR_DEFAULT_GATEWAY
}

# Parse command-line
while [[ -n $1 ]]; do
  case $1 in
    -h | --help)
      help_message; graceful_exit ;;
    -c | --connect)
      echo "connect to vpn"; connect ;;
    -d | --disconnect)
      echo "disconnect from vpn"; disconnect ;;
    -a | --all_traffic)
      echo "redirect all traffic";  ;;
    -s | --specific_traffic)
      echo "specific traffic"; ;;
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
