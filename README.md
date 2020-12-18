# yescryptr16-wasm-miner
Yescryptr16 WebAssembly based miner

Folder "html" - file for web server (html, wasm file, js file)
Folder "miner" - miner src for compile to wasmminer.wasm
Folder "sample" - sample config for caddy web server
Folder "wsproxy" - proxy src Go lang for working miner

## 1) How to compile wsproxy

```
build wsproxy and run
sudo apt install golang
export GOPATH=~/go
go get github.com/gorilla/websocket
#go get -v -u github.com/gorilla/websocket
git clone https://github.com/ohac/wasmminer.git
cd wsproxy
go build
./wsproxy
```

**update GO on ubuntu 16.04 to last version**

```
#delete old version
sudo apt-get purge golang*

sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go

#check version
go version
```

## 2) How to compile miner

```
#before compiling, you need to install emcc, the version of python is not lower than 3.7
wget 'https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz' | tar xzf -
cd emsdk-portable
#if the previous method does not work
#git clone https://github.com/emscripten-core/emsdk.git
#cd emsdk
./emsdk update
./emsdk install latest
./emsdk activate latest
source ./emsdk_env.sh
```

```
#now we compile the miner for the web
cd miner
./build.sh
cp em.js wasmminer.js wasmminer.wasm worker.js ../../html/js
```

**hints for using python version 3.7**

```
alias python=python3
python -V
python3 -V
sudo update-alternatives --config python
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 5
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2
#cmd for select python version
sudo update-alternatives --config python
```

## 3) Cmd for run caddy

```
#download caddy
wget https://github.com/caddyserver/caddy/releases/download/v2.2.1/caddy_2.2.1_linux_arm64.tar.gz
#run as daemon
./caddy run --environ --config /home/user/caddy/caddy.conf --adapter caddyfile
#run as cmd
./caddy run --config /home/user/caddy/caddy.conf --adapter caddyfile
```

## 4) End...
1) Run wsproxy
2) Test wsproxy
```
curl 192.168.0.123:8088/proxy
```
3) Run caddy (or other webserver)
4) Open site and test mining
