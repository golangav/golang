## 1. Go语言特点

go语言达到了既能达到静态编译语言的安全和性能，又打到了动态语言开发维护的高效率。
使用一个表达式来形容go语言：Go=C+Python，说明go语言既有C静态语言程序的运行速度，又能达到python动态语言的快速开发。

```python

1. 从C语言中继承了很多理念，包括表达式语法，控制结构，基础数据类型，调用参数传值，指针等等，也保留了和C语言一样的编译执行方式及弱化的指针。
2. 引入包的概念，用于组织程序结构，Go语言的一个文件都要归属于一个包，而不能单独存在。
3. 垃圾回收机制，内存自动回收，不需开发人员管理。
4. 天然并发（重要特点）
    - 从语言层面支持并发，实现简单。
    - goroutine，轻量级线程，可实现大并发处理，高效利用多核。
    - 给予CPS并发模型（Communicating Sequential Processes）实现
5. 吸收了管道通信机制，形成Go语言特有的管道channel，通过管道channel可以实现不同的goroute之间的相互通信。

```


## 2. mac安装

```
# 下载解压
wget https://dl.google.com/go/go1.11.4.darwin-amd64.tar.gz
tar -xzf go1.11.4.darwin-amd64.tar.gz
mv go /usr/local/

vim ~/.bash_profile
	# go
	export GOROOT=/usr/local/go
	export GOPATH=$HOME/goproject
	export PATH=$PATH:$GOROOT/bin
source ~/.bash_profile

# 测试
go version
```

## 3. 目录结构

```
mkdir -p ~/goproject/src/go_code
mkdir -p ~/goproject/src/go_code/project01
mkdir -p ~/goproject/src/go_code/project01/main/
touch ~/goproject/src/go_code/project01/main/hello.go


# 安装插件

mkdir -p $GOPATH/src/golang.org/x/
cd $GOPATH/src/golang.org/x/
git clone https://github.com/golang/tools.git

cd $GOPATH
go get -u -v github.com/josharian/impl
go get -u -v github.com/mdempsky/gocode
go get -u -v github.com/rogpeppe/godef
go get -u -v github.com/golang/lint/golint
go get -u -v github.com/lukehoban/go-find-references
go get -u -v github.com/lukehoban/go-outline
go get -u -v github.com/sqs/goreturns
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v github.com/tpng/gopkgs
go get -u -v github.com/newhook/go-symbols
go get -v -u github.com/peterh/liner github.com/derekparker/delve/cmd/dlv
go get -u -v golang.org/x/tools/cmd/guru

cd $GOPATH/src/golang.org/x/
git clone https://github.com/golang/lint.git
go install golang.org/x/lint/golint

git clone git@github.com:golang/net.git --depth 1

git clone git@github.com:golang/net.git --depth 1
```




