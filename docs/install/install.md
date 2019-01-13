## mac安装

```
# 下载解压
wget https://dl.google.com/go/go1.11.4.darwin-amd64.tar.gz
tar -xzf go1.11.4.darwin-amd64.tar.gz
mv go /usr/local/

vim ~/.bash_profile
	# go
	export GOROOT=/usr/local/go
	export GOPATH=$HOME/go
	export PATH=$PATH:$GOROOT/bin
source ~/.bash_profile

# 测试
go version
```

## VSCode配置

```angularjs
        "go.buildOnSave": "workspace",
        "go.lintOnSave": "package",
        "go.vetOnSave": "package",
        "go.buildTags": "",
        "go.buildFlags": [],
        "go.lintFlags": [],
        "go.vetFlags": [],
        "go.coverOnSave": false,
        "go.useCodeSnippetsOnFunctionSuggest": false,
        "go.formatOnSave": true,
        "go.formatTool": "goreturns",
        "go.goroot": "/usr/local/go",
        "go.gopath": "/Users/shaowei/go",
        "go.gocodeAutoBuild": false

```

