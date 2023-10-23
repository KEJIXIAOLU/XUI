# 【零基础】V2ray 搭建教程，目前最简单、最安全、最稳定的专属节点搭建方法，晚高峰高速稳定，4K秒开的科学上网线路体验


Xray-core 团队推出了 VLESS Vision 和 VLESS Reality 两种新颖的技术方案。它们能够有效地隐藏和保护流量的特征，提高安全性和稳定性。

## 使用X-UI搭建代理服务，具有以下优点：

- 支持系统状态监控：如CPU、内存、硬盘等状态
- 支持多用户多协议，网页可视化操作
- 支持流量统计
- 支持自定义Xray配置模板
- 支持HTTPS访问面板
- 支持面板自定义端口，账号与密码
- 快速生成分享连接或二维码
- 支持CDN套用
- 支持Fallback分流设置

- ## 一、准备工作

  ### 1、一台境外VPS主流系统，例如：Debian/Ubuntu/CentOS

Vultr 购买地址：https://www.vultr.com/?ref=8753714  [点此进入](https://www.vultr.com/?ref=8941832-8H)：按时计费，最低6$/月。

### 2、下载并安装FinalShell SSH工具

Windows版下载地址：http://www.hostbuf.com/downloads/finalshell_install.exe  [点此下载](http://www.hostbuf.com/downloads/finalshell_install.exe)

macOS版下载地址：http://www.hostbuf.com/downloads/finalshell_install.pkg  [点此下载](http://www.hostbuf.com/downloads/finalshell_install.pkg)

## 二、搭建步骤

## 安装更新运行环境

下面环境的安装方式，大家根据自己的系统选择命令安装就好了。
### 1、Debian/Ubuntu系统执行以下命令：
     
    apt update -y && apt install -y curl && apt install -y socat
     
### 2、CentOS系统执行以下命令：

    yum update -y && yum update -y && yum install -y socat
    
## 安装 X-ui 面板

    bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/956bf85bbac978d56c0e319c5fac2d6db7df9564/install.sh) 0.3.4.4


# X-ui 管理面板设置
添加证书和密钥路径，重启面板
通过域名访问x-ui 管理面板：https://域名:54321

注意事项：如果你点了 X-ui 面板设置，第一次进入的时候会自动帮你更改网址路径，点击确认，会自动跳转到新网址，下次再进入面板就需要通过这个新网址才能进入，
建议将其保存为书签，防止忘记了。

## 搭建 Vision 节点申请证书

### 安装证书工具


    curl https://get.acme.sh | sh; apt install socat -y || yum install socat -y; ~/.acme.sh/acme.sh --set-default-ca --server letsencrypt


### 申请证书

    ~/.acme.sh/acme.sh  --issue -d 你的域名 --standalone -k ec-256 --force --insecure

### 安装证书

    ~/.acme.sh/acme.sh --install-cert -d 你的域名 --ecc --key-file /etc/x-ui/server.key --fullchain-file /etc/x-ui/server.crt
    

## 三、各平台客户端
v2rayNG【需要最新版本】

Windows（v2rayN）：https://github.com/2dust/v2rayN/releases/tag/6.23

Android（v2rayNG）：https://github.com/2dust/v2rayNG/releases/tag/1.8.5

IOS（shadowrocket）：https://apps.apple.com/app/shadowrocket/id932747118


## 四、放行端口
放行指令是一样的，只要将端口443为任意端口就可以了。

### 放行 443 端口

    iptables -I INPUT -p tcp --dport 443 -j ACCEPT

### 放行 54321 端口

    iptables -I INPUT -p tcp --dport 54321 -j ACCEPT


## 五、检测端口是否被封
端口被封的原因是多方面的，目前并没有哪一种节点可以保证不被封，本期讲的这三种方式也不例外，所以如果你的节点突然无法使用了，可以用以下方式进行排查。

打开 [ping.pe](https://ping.pe/)

输入 IP 检测 ping 可用

输入 IP:Port 检查端口是否可用

主要是看最后几个是否为绿色

