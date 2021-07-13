---
title:  "相信科学 - 一分钟部署 ShadowSocks-Manager"
description: "最近工作需要建立一个 ShadowSocks 平台供内地同事使用，查看了许多第三方库，觉得 [ShadowSocks-Manager](https://github.com/shadowsocks/shadowsocks-manager) 这个库的控制台做得蛮不错的，便想应用部署在 docker swarm 上，没想到遇到不少问题，花了不少时间。"
date: 2018-05-07 10:00:00
categories: [Tech]
tags: [DevOps, ShadowSocks, ShadowSocks-Manager, ansible, docker, swarm]
---
# 相信科学 - 一分钟部署 ShadowSocks-Manager

之前有写一个 ShadowSocks 自动化部署的 Script（[链接](https://www.damonyuan.com/2017/Start-ShadowSocks-in-One-Minute/)），但是只适合程序员自己使用，因为完全没有 Access Control，也无法监控流量。

最近工作需要建立一个 ShadowSocks 平台供内地同事使用，查看了许多第三方库，觉得 [ShadowSocks-Manager](https://github.com/shadowsocks/shadowsocks-manager) 这个库的控制台做得蛮不错的，便想应用部署在 docker swarm 上，没想到遇到不少问题，花了不少时间。

这里将这个库的 docker image 贡献出来，包括了自动化 ansible 部署的代码。直接使用 docker compose/stack file 部署一分钟就可以搞定，只需要改改 `.env.example` 中的环境变量，或者你需要自动化部署 VPC, SG, EC2 等等，也可以自己根据需求改改 ansible 代码。

gitHub repository [链接](https://github.com/damonYuan/DySocksManager)。

--------
# 相信科学，科学上网
--------