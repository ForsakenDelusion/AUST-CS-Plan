---
profileName: FskDe7usion
postId: "75"
postType: post
categories:
  - 7
---

# 安装

[github仓库](https://github.com/maurosoria/dirsearch)

gitclone下来之后进入目录,第一次运行`python3 dirsearch.py -u url`的时候提示缺少环境,所以我先venv了一个虚拟环境

```python
python3 -m venv venv
```

激活虚拟环境

```python
source venv/bin/activate
```

然后再运行一边命令进入dirsearch

# 选项：

- **--version**：显示程序版本号并退出
- **-h, --help**：显示帮助信息并退出

# 必填项：

- **-u URL, --url=URL**：目标 URL，可以使用多个标志
- **-l PATH, --url-file=PATH**：URL 列表文件
- **--stdin**：从标准输入读取 URL
- **--cidr=CIDR**：目标 CIDR
- **--raw=PATH**：从文件加载原始 HTTP 请求（使用 '--scheme' 标志设置方案）
- **-s SESSION_FILE, --session=SESSION_FILE**：会话文件
- **--config=PATH**：配置文件路径（默认：'DIRSEARCH_CONFIG' 环境变量，否则为 'config.ini'）

# 字典设置：

- **-w WORDLISTS, --wordlists=WORDLISTS**：自定义字典文件（用逗号分隔）
- **-e EXTENSIONS, --extensions=EXTENSIONS**：扩展名列表，用逗号分隔（例如 php,asp）
- **-f, --force-extensions**：将扩展名添加到每个字典条目的末尾
- **-O, --overwrite-extensions**：用您的扩展名（通过 `-e` 选择）覆盖字典中的其他扩展名
- **--exclude-extensions=EXTENSIONS**：要排除的扩展名列表，用逗号分隔（例如 asp,jsp）
- **--remove-extensions**：删除所有路径中的扩展名（例如 admin.php -> admin）
- **--prefixes=PREFIXES**：为所有字典条目添加自定义前缀（用逗号分隔）
- **--suffixes=SUFFIXES**：为所有字典条目添加自定义后缀，忽略目录（用逗号分隔）
- **-U, --uppercase**：字典转为大写
- **-L, --lowercase**：字典转为小写
- **-C, --capital**：字典首字母大写

# 一般设置：

- **-t THREADS, --threads=THREADS**：线程数
- **-r, --recursive**：递归暴力破解
- **--deep-recursive**：对每个目录深度执行递归扫描（例如 api/users -> api/）
- **--force-recursive**：对每个找到的路径执行递归暴力破解，而不仅限于目录
- **-R DEPTH, --max-recursion-depth=DEPTH**：最大递归深度
- **--recursion-status=CODES**：执行递归扫描的有效状态码，支持范围（用逗号分隔）
- **--subdirs=SUBDIRS**：扫描给定 URL[s]的子目录（用逗号分隔）
- **--exclude-subdirs=SUBDIRS**：在递归扫描期间排除以下子目录（用逗号分隔）

# 请求设置：

- **-m METHOD, --http-method=METHOD**：HTTP 方法（默认：GET）
- **-d DATA, --data=DATA**：HTTP 请求数据
- **--data-file=PATH**：包含 HTTP 请求数据的文件
- **-H HEADERS, --header=HEADERS**：HTTP 请求头，可以使用多个标志
- **--header-file=PATH**：包含 HTTP 请求头的文件
- **-F, --follow-redirects**：跟随 HTTP 重定向
- **--random-agent**：为每个请求选择随机用户代理
- **--auth=CREDENTIAL**：认证凭据（例如 user:password 或 bearer token）
- **--auth-type=TYPE**：身份验证类型（basic、digest、bearer、ntlm、jwt、oauth2）
- **--cert-file=PATH**：包含客户端证书的文件
- **--key-file=PATH**：包含客户端证书私钥的文件（未加密）
- **--user-agent=USER_AGENT**
- **--cookie=COOKIE**

# 连接设置：

- **--timeout=TIMEOUT**：连接超时时间
- **--delay=DELAY**：请求之间的延迟时间
- **--proxy=PROXY**：代理 URL（HTTP/SOCKS），可以使用多个标志
- **--proxy-file=PATH**：包含代理服务器的文件
- **--proxy-auth=CREDENTIAL**：代理身份验证凭据
- **--replay-proxy=PROXY**：用找到的路径重播的代理
- **--tor**：使用 Tor 网络作为代理
- **--scheme=SCHEME**：原始请求的方案或 URL 中没有方案时的方案（默认：自动检测）
- **--max-rate=RATE**：每秒最大请求数
- **--retries=RETRIES**：失败请求的重试次数
- **--ip=IP**：服务器 IP 地址
- **--interface=NETWORK_INTERFACE**：要使用的网络接口

# 高级设置：

- **--crawl**：在响应中爬取新路径

# 查看设置：

- **--full-url**：输出中显示完整 URL（在安静模式下自动启用）
- **--redirects-history**：显示重定向历史记录
- **--no-color**：无彩色输出
- **-q, --quiet-mode**：安静模式

# 输出设置：

- **-o PATH, --output=PATH**：输出文件
- **--format=FORMAT**：报告格式（可用：simple、plain、json、xml、md、csv、html、sqlite）
- **--log=PATH**：日志文件