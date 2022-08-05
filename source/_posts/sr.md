---
title: 崩坏:星穹铁道（CrepeSR）开源项目搭建实战
date: 2022-08-05 13:30:08
urlname: CrepeSR-linux
---

项目地址 https://github.com/Crepe-Inc/CrepeSR

# 所需组件

一台服务器（仅在Debian11测试通过）

脑子和手！

# 开始

## 安装可能必须的东东

安装nodejs（18.x）
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
sudo apt install -y npm
## 检查
node -v
npm -v
```

安装MongoDB
```
sudo apt install mongodb-org
sudo systemctl enable --now mongod
## 检查
mongod --version
```

安装Python & mitmproxy
```
sudo apt install -y python3 mitmproxy
## 检查
python -V
mitmproxy --version
```

安装libcap
```
sudo apt install libcap2-bin
```

安装git
```
sudo apt install git
```

## 正片

拉取CrepeSR项目和资源
```
git clone https://github.com/Crepe-Inc/CrepeSR --depth=1
git clone https://github.com/memetrollsXD/CrepeSR-Resources CrepeSR/src/data --depth=1
```

安装依赖
```
cd CrepeSR
npm install
```

让node可以走80-443
```
sudo setcap cap_net_bind_service=+eip `readlink -f \`which node\``
```

启动
```
mitmdump -s proxy.py -k --set block_global=false &
npm run start
```

这就完成了Q_Q


