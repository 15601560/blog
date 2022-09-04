---
title: Cloudflare偷鸡计划
date: 2022-09-04 10:32:08
urlname: Cloudflare-accelerate
---
# 缘由

众所周知Cloudflare虽然有中国节点，不过不是给free用的，只限于企业

想用友好的境外节点，结果大家一蜂窝挤一个，根本不好用

ip-scanner/cloudflare项目里扫的节点，部分只开了ssl端口，导致80不跳转443，有时候反代噶了还得动手换

# 准备

1.一个可以自定义cname的域名（以前绑定的可以，现在没了）或者用CloudFlare for SaaS

2.请自带备案

# 开凿

---

Cloudflare中国代理（国际走官方）

请备案后解析到  cn.gblz.work

---

Cloudflare未备案代理（国际走官方）

节点参差不齐，效果甚至不如官方，故等我研究方案后再开放

---

所有IP来自 https://github.com/ip-scanner/cloudflare 的项目