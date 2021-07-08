
## 概述
一键 HTTPS 是 SSL 证书结合腾讯云 Web 应用防火墙（WAF）服务开发的快速部署 WAF 的 HTTPS 功能。使用该功能，您可以快捷在 [证书管理控制台](https://console.cloud.tencent.com/https) 将您申请到的 SSL 证书接入部署至腾讯云 Web 应用防火墙（WAF）提供的 SaaS 型 WAF 域名接入服务。
SaaS 型 WAF 通过为防护域名分配 CNAME，修改网站的 DNS 解析记录，将网站收到的 Web 请求转发给 WAF，从而对网站进行安全防护。具体详情参见 [Web 应用防火墙产品概述](https://cloud.tencent.com/document/product/627/17470)。
本文将指导您如何在 [证书管理控制台](https://console.cloud.tencent.com/https) 一键添加 WAF 接入域名并配置 HTTPS。

## 前提条件
已在 [证书管理控制台](https://console.cloud.tencent.com/ssl) 申请颁发 SSL 证书。


## 操作指南
### 步骤1：添加一键 HTTPS 域名
1. 登录 [证书管理控制台](https://console.cloud.tencent.com/ssl)，并单击左侧菜单栏【一键 HTTPS】，进入 【一键 HTTPS】管理页面。
2. 在【一键 HTTPS】管理页面中，单击【一键添加】。如下图所示：
>?若您是首次使用，请在弹出的授权窗口中，授予对应权限。
>
![](https://main.qcloudimg.com/raw/e327528f08706299fef120e04c993099.png)
3. 在弹出的 “一键添加” 窗口中，配置相关信息。如下图所示：
![](https://main.qcloudimg.com/raw/5e8f1474ff34ca297f5ccf9f7ae57e6a.png)
 - **填写域名：**请输入您需要进行一键 HTTPS 的域名，支持通配符域名。
 - **选择证书：**请选择已成功申请的证书。
>? 选择的证书需与【填写域名】对应。单域名对应相同域名名称的单域名证书，通配符域名对应相同域名名称的通配符证书，多域名则选择包含该域名名称的多域名证书。
 - **源站地址：**请根据您的实际需求选择【IP】与【域名】。
 - **IP**：请输入需要防护网站的真实 IP 源站地址，即源站的公网 IP 地址。
 - **域名**：请输入需要防护网站的真实源站域名。
 - **强制 HTTPS：**开启该功能，浏览器端的每个 HTTP 请求都会被跳转成 HTTPS 请求。例如，当浏览器使用 HTTP 协议访问 `http://cloud.tencent.com ` 时，将返回302状态码重定向到 HTTPS 协议访问 `https://cloud.tencent.com`。
 - **回源协议：**	开启该功能，腾讯云将使用 HTTP 协议访问源站。例如，当浏览器使用 HTTP 或 HTTPS 协议访问 `cloud.tencent.com` 时，无论 HTTP 或 HTTPS 协议都将使用 HTTP 协议访问源站。
 - **回源端口：**请根据您的实际需求选择回源端口。默认情况下支持443与8443，若您开启回源协议，则为80与8080。
4. 单击【确定】，即可生成配置实例。如下图所示：
![](https://main.qcloudimg.com/raw/2c548a3cf3bc61f73512a57150319cec.png)

### 步骤2：配置 CNAME 记录

>?
>- 添加一键 HTTPS 域名后，还需配置对应的 CNAME 记录后，接入才可正常生效。
>- 配置 CNAME 记录步骤以腾讯云配置 CNAME 记录为例，若您的一键 HTTPS 域名未在 DNSPod 解析解析托管，具体操作请咨询您的域名解析商或将域名托管至 DNSPod DNS 解析后，再进行配置 CNAME 记录。详情请参见 [域名托管至 DNSPod DNS 解析](https://docs.dnspod.cn/dns/60b99ba0e90008112f815bde/)。
>
1. 登录  [DNSPod 管理控制台](https://console.dnspod.cn/dns/list)。
2. 在 “我的域名” 中，选择需要进行一键 HTTPS 域名，单击对应域名，即可进入该域名的【记录管理】页面。如下图所示：
![](https://main.qcloudimg.com/raw/3888e10fc99f01d0cbb0058411f0e662.png)
3. 单击【添加记录】，填写记录信息。如下图所示：
![](https://main.qcloudimg.com/raw/489791e8d992b47ed300e30899050c67.png)
 - **主机记录**：填写子域名。例如，添加 `cs.dnspod.com` 的一键 HTTPS 域名，您在 “主机记录” 处填写 “cs” 即可。
 - **记录类型**：选择 “CNAME”。
 - **线路类型**：选择 “默认” 类型，否则会导致部分用户无法解析。
 - **记录值**：填写证书控制台新增实例提供的 CNAME 域名。如下图所示：
![](https://main.qcloudimg.com/raw/a0cdf6f3df54548fb0c89c594267a9fe.png)
 - **权重**：同一条主机记录相同的线路，可以针对不同的记录值设置权重，解析时将根据设置的权重比例进行返回。输入范围
为0 - 100的整数。
 - **MX 优先级**：不需要填写。
 - **TTL**：为缓存时间，数值越小，修改记录各地生效时间越快，默认为600秒。
4. 单击【确定】，完成添加。
5. 完成添加后，请耐心等待解析生效，解析生效后即可接入成功。
>?一般情况下，解析生效时间与您设置 TTL 值相同。
>











