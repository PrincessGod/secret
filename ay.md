## 安装Shdowsocks服务端

登录阿里云服务器, 执行以下命令

### 安装pip

	yum install python-pip

### 使用pip安装shadowsocks

	pip install shadowsocks

### 配置Shdowsocks服务,并启动

新建 /etc/shadowsocks.json 文件, 并写入以下内容

	{
		"server":"remote-shadowsocks-server-ip-addr",
		"server_port":443,
		"local_address":"127.0.0.1",
		"local_port":1080,
		"password":"your-passwd",
		"timeout":300,
		"method":"aes-256-cfb",
		"fast_open":false,
		"workers":5
	}

注意修改 `server` 和 `password`, `workers` 表示启动的进程数量。
如果专网 `server` 需要设置为内网。

然后使用以下命令启动: `ssserver -c /etc/shadowsocks.json -d start`


启动：# systemctl start firewalld
查看状态：# systemctl status firewalld 或者 firewall-cmd –state
停止：# systemctl disable firewalld
禁用：# systemctl stop firewalld

永久打开一个端口： firewall-cmd --permanent --add-port=8080/tcp
永久关闭一个端口： firewall-cmd --permanent --remove-port=8080/tcp
永久打开某项服务： firewall-cmd --permanent --add-service=http
永久关闭某项服务： firewall-cmd --permanent --remove-service=http
进行端口转发： firewall-cmd --permanent --add-forward-port=port=80:proto=tcp:toport=8080:toaddr=192.0.2.55
允许转发到其他地址： firewall-cmd --permanent --add-masquerade
重新加载防火墙： firewall-cmd --reload

firewall-cmd --zone=public --add-port=8388/tcp --permanent

### git

	yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
	yum install  gcc perl-ExtUtils-MakeMaker

	yum remove git

	wget https://github.com/git/git/archive/v2.9.2.tar.gz

	cd git-2.9.2
	make prefix=/usr/local/git all
	make prefix=/usr/local/git install

	echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc
	source /etc/bashrc # 实时生效
	

[SS-go](https://teddysun.com/392.html)
