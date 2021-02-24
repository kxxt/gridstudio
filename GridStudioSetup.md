# Grid Studio 安装配置

## 主要目标

- 在树莓派上免 docker 运行 Grid Studio
- Grid Studio 接入 Sagemath 的函数

## 目前状态

免 docker 运行已经实现, 但是有一些问题:

- 表格无法保存, 即使提示已保存,实际上没有保存 (主要问题)
- 绘制的图表极其不适合在 piculator 上操作
- terminal 无法使用 (不重要, 把 terminal 砍掉也没什么损失..)

## 系统依赖配置

```sh
sudo apt clean
sudo apt update
sudo apt install -y software-properties-common build-essential wget python3-pip locales curl git
python3.7 -m pip install --upgrade pip numpy pandas matplotlib scipy scikit-learn
sudo apt install golang nodejs npm
```

```sh
node -v
v10.23.1
npm -v
5.8.0
go version
go version go1.11.6 linux/arm
```



## 目录结构

```sh
# WORKDIR: gridstudio/grid-app
mkdir -p /home/pi/gridstudio/source
mkdir -p /home/pi/gridstudio/run
mkdir -p /home/pi/gridstudio/userdata
cp -r . /home/pi/gridstudio/source
cp -r ./terminal-server/ /home/pi/gridstudio/run/terminal-server/
```

## 项目依赖配置

```sh
# WORKDIR: ~/gridstudio/run/terminal-server
npm install --nocache
# WORKDIR: ~/gridstudio/source/
go get -d -v ./...
cd proxy
go build manager.go
rm ./manager
```

## 运行

```sh
# WORKDIR: ~/gridstudio/source/proxy
go run manager.go
```

