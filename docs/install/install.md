## mac安装

```
# 下载解压
cd go_dev/
wget https://dl.google.com/go/go1.11.4.darwin-amd64.tar.gz
tar xf go1.11.4.darwin-amd64.tar.gz

# 设置环境变量
vim ~/.bash_profile
    export GOROOT=$HOME/go_dev/go
    export GOPATH=$GOROOT/goproject
    export PATH=$PATH:$GOROOT/bin
source ~/.bash_profile

# 测试
go version
```

## VSCode配置

```angularjs
go get github.com/derekparker/delve/cmd/dlv

```

