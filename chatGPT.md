# chatGPT注册流程

`一、网络`
- 需要除开中国大陆以外的VPN节点，可以通过[自建](./v2ray_deploy.md)或者买服务
- 节点需要对接cloudflare warp云网络

`二、账号注册`
- 访问https://chat.openai.com
- 通过邮箱或者google账号等进行注册
- 通过[sms-man](https://sms-man.com)买一个美国或者其他开放chatGPT国家的虚拟手机号进行手机验证

`三、页面使用过程中保持连接`
- 浏览器安装自动刷新页面的插件，如[Just Refresh](https://chrome.google.com/webstore/detail/just-refresh/pgaimkehoiabhliejchbnamlboniofpd)
- 配置插件，配置页面为 chrome-extension://${extensionID}/options.html  
- 开启一个chatgpt同域下的页面，如https://chat.openai.com/404
- 设定刷新时间，一般30s刷新此役即可满足连接要求

`四、chatGPT Plus、API调用`
- 需要绑定一张国外信用卡，openai不对国内、俄罗斯开放
- 注册[nobepay](https://www.nobepay.com/app/home)账号，通过KYC认证
- 充值，推荐人名币充值，手续费1%，且多余可退款(退款未验证)
    - USTD需要从别的平台充值再转入，两边手续费很高，坑很多，且不可提现
- 开卡：556766卡段可绑定成功，充值详情可见卡段描述
- 绑卡前先确定网络环境，确保platform.openai.com、stripe.com均通过代理且代理对接了warp分流
  - 可通过VrayN的全局代理，加上无痕浏览器进行
- 开通plus
    - 充值plus：通过upgrade plan入口绑卡，绑卡成功后会自动扣除月费
- API使用
    - 点击[个人账户](https://platform.openai.com/account/billing/overview),点击create account进行绑卡
    - 绑卡成功后会预扣款5美元
    - 创建[api-key](https://platform.openai.com/account/api-keys),创建成功后需要复制下来，后期不能再复制到了
    - [接口文档](https://platform.openai.com/docs/api-reference/introduction)
- 绑定失败可能的原因
    - 卡段问题，卡段被拒绝，stripe.com的绑卡接口返回的详情中会有相关提示
    - ip问题，stripe.com的绑卡接口返回一般错误，可以尝试更换ip进行
    - 若失败，不要进行太多次数的尝试，可能会触发账号风控，导致原本可使用的账号触发手机验证码等风控验证
