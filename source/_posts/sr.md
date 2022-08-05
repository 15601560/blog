---
title: 崩坏:星穹铁道（CrepeSR）开源项目搭建实战
date: 2022-08-05 13:30:08
urlname: CrepeSR-linux
---

项目地址 https://github.com/Crepe-Inc/CrepeSR

官方文档 https://github.com/Crepe-Inc/CrepeSR/wiki/%E4%B8%AD%E6%96%87%E7%89%88%E6%95%99%E7%A8%8B

# 所需组件

一台服务器（仅在Debian11测试通过）

脑子和手！

# 开始

## 安装可能必须的东东

安装nodejs（18.x）
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
## 检查
node -v
npm -v
```

安装MongoDB
```
sudo apt install mongodb-org
sudo systemctl enable --now mongod
## 以上报错则
cat <<"EOF" | bash                              
sudo apt update && \
sudo apt install -y dirmngr gnupg apt-transport-https ca-certificates software-properties-common  && \
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add - && \
echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/5.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list && \
sudo apt update && \
sudo apt install -y mongodb-org && \
sudo systemctl enable --now mongod
EOF
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


