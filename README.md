# dnspodddns4winbat
<code>set /p name=请输入Azure的子域名称:

rem 修改记录(hk01.******.com)
curl -X POST https://dnsapi.cn/Record.Modify -d "login_token=******,b2d899**************8afc5d236&format=json&domain_id=86893762&record_id=1106659812&sub_domain=hk01&value=%name%.eastasia.cloudapp.azure.com.&record_type=CNAME&record_line_id=0"

exit
</code>

~~这个bat记得默认线路的%要转义%% ~~


#DNSPod 查看域名的 domain_id 和 record_id
获取 login_token
DNSPOD / 用户中心 / 安全设置 / API Token

使用英文 , 将 ID 和 Token 连接起来即为下文提到的参数 your_login_token。

举个例子，比如你的 ID 是 12345 ，Token 是 abcd ，那么你的 your_login_token 就是 12345,abcd。

随后请求一下官方提供的 api 就可以了。

获取 domain_id
curl 'https://dnsapi.cn/Domain.List' -d 'login_token=<your_login_token>&format=json'

根据响应的 json 中的 domains 得到域名对应的 domain_id。

获取 record_id
curl 'https://dnsapi.cn/Record.List' -d 'login_token=<your_login_token>&format=json&domain_id=<your_domain_id>'

根据响应 json 中的 records 得到记录对应的 record_id。

获取 sub_domain
sub_domain 是你要进行动态解析的子域名，其实就是你自己在 控制台 设定的 主机记录，详见获取 record_id 时从官网得到的 json 中的 name 参数。
————————————————

