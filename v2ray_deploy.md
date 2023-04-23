# 自建VPN

`一、购买节点`
- 注册vultr，如果是新用户先在网上搜索一下优惠充值活动，有充值50送50的优惠，其他国际vps都可
- 虚拟机选择debian系统
- 要有一个ipv4的公网ip

`二、域名解析`
- 需要购买一个域名，将域名或者该域名的下级域名解析到购买的服务器上
- 腾讯云、阿里云有此类服务

`三、v2ray配置`
- 通过v2ray-agent自动配置节点，参考https://github.com/mack-a/v2ray-agent
- 登录虚拟机(ssh username@vps_ip)
- 安装vasma
- 运行vasma
    - 选择安装x-ray
    - 其中需要输入绑定的域名
    - 记录安装的x-ray的版本
- warp分流(对接cloudflare warp云网络，可访问openai.com等)
    - 运行vasma，选择warp分流
    - 进行域名添加
    - 目前脚本配置会导致xray启动失败，进入到xray/conf中编辑routing.json，将geosite更改为domain
    - 重启xray即可
- 生成订阅链接或者二维码


`四、手机使用`
- 安装v2rayNG(https://github.com/2dust/v2rayNG/releases)
- 安装apk的xray内核最好和节点上xray内核版本一致


`五、pc使用`
- 安装v2rayN(https://github.com/2dust/v2rayN/releases)
- 自动配置系统代理+全局配置 开启本地全局代理

### **在使用中，选择vless_reality_vision协议进行连接，避免端口被GFW封**
