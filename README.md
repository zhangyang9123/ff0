# CX330-scan

通过网络资产线索（如：域名，IP地址，资产名称等），利用FOFA访问网络空间测绘数据，对资产进行拓展查询

## 0x00 简介

CX330-scan 是一款使用 Go 编写的命令行 FoFa 查询工具，可以对特定资产进行拓展搜索，主要的功能如下：
基本 FoFa 语法查询     Icon Hash 在线查询     URL 证书计算查询    排除蜜罐资产 	更多......

## 0x01 下载

点击 [releases](https://github.com/zhangyang9123/ff0/releases)下载链接 ，按照自己的系统架构选择相应的发行版本下载。

## 0x02 配置

MacOS/Linux/Win

第一次运行程序会在同级目录	生成config.yml配置文件，只需要配置完 `email` 和 `key` 就可以使用

```
DefaultEmail  : 
DefaultAPIKey : 
DefaultSize   : 10000
DefaultOutput : data.xlsx
```

## 0x03 使用方法

直接运行程序会打印出提示信息

```
/ "... an experienced, industrious, ambitious, and often quite often \
| picturesque liar."                                                 |
\                 -- Mark Twain                                      /
 --------------------------------------------------------------------
  \                                  ,+*^^*+___+++_
   \                           ,*^^^^              )
    \                       _+*                     ^**+_
     \                    +^       _ _++*+_+++_,         )
              _+^^*+_    (     ,+*^ ^          \+_        )
             {       )  (    ,(    ,_+--+--,      ^)      ^\
            { (@)    } f   ,(  ,+-^ __*_*_  ^^\_   ^\       )
           {:;-/    (_+*-+^^^^^+*+*<_ _++_)_    )    )      /
          ( /  (    (        ,___    ^*+_+* )   <    <      \
           U _/     )    *--<  ) ^\-----++__)   )    )       )
            (      )  _(^)^^))  )  )\^^^^^))^*+/    /       /
          (      /  (_))_^)) )  )  ))^^^^^))^^^)__/     +^^
         (     ,/    (^))^))  )  ) ))^^^^^^^))^^)       _)
          *+__+*       (_))^)  ) ) ))^^^^^^))^^^^^)____*^
          \             \_)^)_)) ))^^^^^^^^^^))^^^^)
           (_             ^\__^^^^^^^^^^^^))^^^^^^^)
             ^\___            ^\__^^^^^^))^^^^^^^^)\\
                  ^^^^^\uuu/^^\uuu/^^^^\^\^\^\^\^\^\^\
                     ___) >____) >___   ^\_\_\_\_\_\_\)
                    ^^^//\\_^^//\\_^       ^(\_\_\_\)
                      ^^^ ^^ ^^^ ^

Usage:
  [!]./linux_ff0  -q 'host="sdxiehe.edu.cn"' -s 10000 -o data.xlsx
  [!]./linux_ff0  -f query_rules_file.txt -s 10000 -o data.xlsx

Options:
  -h, --help
  -q, --query       [string]          参数字符串 (默认: '')
  -f, --file        [filePath]        批量查询规则文件 (默认: '')
  -s, --size        [int]             到处数据量 (默认: 10000)
  -e, --is_honeypot                   排除蜜罐数据  (仅限FOFA高级会员使用 )
  -o, --output      [string]          输出文件名字 / 绝对路径 (默认: data.xlsx)
  -g, --grammar                       fofa搜索语法帮助表
  -t, --tip         [string]          fofa 搜索关键字提示列表
  -x, --xlsx        [文件路径]        读取生成xlsx文件 (配合 level 参数使用)
  -l, --level       [1/2/3]               读取文件细粒度 (配合 xlsx 参数使用)
  -ih, --iconhash   [string]          计算指定 URL favicon icon_hash


```

#### 查询fofa语法

使用 -g 参数，打印出fofa语法规则

```
./ff0 -g

/ "... an experienced, industrious, ambitious, and often quite often \
| picturesque liar."                                                 |
\                 -- Mark Twain                                      /
 --------------------------------------------------------------------
  \                                  ,+*^^*+___+++_
   \                           ,*^^^^              )
    \                       _+*                     ^**+_
     \                    +^       _ _++*+_+++_,         )
              _+^^*+_    (     ,+*^ ^          \+_        )
             {       )  (    ,(    ,_+--+--,      ^)      ^\
            { (@)    } f   ,(  ,+-^ __*_*_  ^^\_   ^\       )
           {:;-/    (_+*-+^^^^^+*+*<_ _++_)_    )    )      /
          ( /  (    (        ,___    ^*+_+* )   <    <      \
           U _/     )    *--<  ) ^\-----++__)   )    )       )
            (      )  _(^)^^))  )  )\^^^^^))^*+/    /       /
          (      /  (_))_^)) )  )  ))^^^^^))^^^)__/     +^^
         (     ,/    (^))^))  )  ) ))^^^^^^^))^^)       _)
          *+__+*       (_))^)  ) ) ))^^^^^^))^^^^^)____*^
          \             \_)^)_)) ))^^^^^^^^^^))^^^^)
           (_             ^\__^^^^^^^^^^^^))^^^^^^^)
             ^\___            ^\__^^^^^^))^^^^^^^^)\\
                  ^^^^^\uuu/^^\uuu/^^^^\^\^\^\^\^\^\^\
                     ___) >____) >___   ^\_\_\_\_\_\_\)
                    ^^^//\\_^^//\\_^       ^(\_\_\_\)
                      ^^^ ^^ ^^^ ^


[+]                Rule                                   Mark
 ------------------------------------------- --------------------------------
  domain="qq.com"                             搜索根域名带有qq.com的网站
  host=".gov.cn"                              从host中搜索".gov.cn"
  ip="1.1.1.1"                                从ip中搜索包含"1.1.1.1"的网站
  ip="220.181.111.1/24"                       查询IP为"220.181.111.1"的C段资产
  port="6379"                                 查找对应"6379"端口的资产
  title="beijing"                             从标题中搜索"北京"
  status_code="402"                           查询服务器状态为"402"的资产
  protocol="quic"                             查询quic协议资产
  header="elastic"                            从http头中搜索"elastic"
  body="网络空间测绘"                            从html正文中搜索"网络空间测绘"
  os="centos"                                 搜索CentOS资产
  server=="Microsoft-IIS/10"                  搜索IIS10服务器
  app="Microsoft-Exchange"                    搜索Microsoft-Exchange设备
  base_protocol="udp"                         搜索指定udp协议的资产
  banner=users && protocol=ftp                搜索FTP协议中带有users文本的资产
  icp="京ICP证030173号"                        查找备案号为"京ICP证030173号"的网站
  icon_hash="-247388890"                      搜索使用此icon的资产(VIP)
  js_name="js/jquery.js"                      查找网站正文中包含js/jquery.js的资产
  js_md5="82ac3f14327a8b7ba49baa208d4eaa15"   查找js源码与之匹配的资产
  type=service                                搜索所有协议资产，支持subdomain和service两种
  is_domain=true                              搜索域名的资产
  ip_ports="80,161"                           搜索同时开放80和161端口的ip
  port_size="6"                               查询开放端口数量等于"6"的资产(VIP)
  port_size_gt="6"                            查询开放端口数量大于"6"的资产(VIP)
  port_size_lt="12"                           查询开放端口数量小于"12"的资产(VIP)
  is_ipv6=true                                搜索ipv6的资产
  is_fraud=false                              排除仿冒/欺诈数据
  is_honeypot=false                           排除蜜罐数据(VIP)
  country="CN"                                搜索指定国家(编码)的资产
  region="Xinjiang"                           搜索指定行政区的资产
  city="Ürümqi"                               搜索指定城市的资产
  asn="19551"                                 搜索指定asn的资产
  org="Amazon.com,Inc."                       搜索指定org(组织)的资产
  cert="baidu"                                搜索证书(https或者imaps等)中带有baidu的资产
  cert.subject="Oracle Corporation"           搜索证书持有者是OracleCorporation的资产
  cert.issuer="DigiCert"                      搜索证书颁发者为DigiCertInc的资产
  cert.is_valid=true                          验证证书是否有效,true有效,false无效(VIP)
  after="2017" && before="2017-10-01"         限定时间范围

[+] 高级搜索：可以使用括号 () / 和 && / 或 || / 完全匹配 == / 不为 != 等逻辑运算符。
```

#### 基础查询

单条语句查询

```
./ff0  -q '填写相应规则即可' -s 10000  -o data.xlsx
```

多条语句进行文件查询

```
./ff0  -f query_rules_file.txt -s 10000  -o data.xlsx
```

query_rules_file 文件实例

```
  domain="qq.com" 
  host=".gov.cn"
  ip="1.1.1.1" 
  ip="220.181.111.1/24"
  port="6379"
  title="beijing"
  status_code="402"
  protocol="quic"
```

#### 排除蜜罐干扰

-e 参数可排除蜜罐干扰

```
./ff0  -q '填写相应规则即可' -s 10000  -e -o data.xlsx
```

#### iconhash 查询

支持URL favicon Hash 查询资产

```
./ff0  -ih 'https://www.baidu.com/favicon.ico' -s 10000  -o data.xlsx
```

## 0x04 资产数据查看

资产查询结束后，会在当前文件夹下生成xlsx文件

可以使用 -x 参数指定查看的 xlxs 资产文件，并配合 -l / --level 参数指定输出细粒度

**level 1**

```

+-------------------------------+----------------+------+
|             Host              |       Ip       | Port |
+-------------------------------+----------------+------+
|    http://bos.im.baidu.com    | 220.181.111.68 |  80  |
|    http://house.baidu.com     | 180.97.34.232  |  80  |
|   http://apistore.baidu.com   | 103.235.46.238 |  80  |
|   http://yingxiao.baidu.com   | 110.242.68.230 |  80  |
|  https://hiphotos.baidu.com   | 103.235.47.66  | 443  |
| http://trust-static.baidu.com | 112.80.248.190 |  80  |
|    http://koubei.baidu.com    | 112.80.248.190 |  80  |
|     https://vcp.baidu.com     |   42.7.43.35   | 443  |
|  http://nadvideo2.baidu.com   | 101.72.249.35  |  80  |
|     http://vcp.baidu.com      | 182.84.120.35  |  80  |
|     https://ww.baidu.com      | 110.242.68.66  | 443  |
| https://developers.baidu.com  | 112.80.255.42  | 443  |
|     http://cang.baidu.com     | 110.242.68.150 |  80  |
|  http://developers.baidu.com  | 112.80.255.42  |  80  |
|   https://gongyi.baidu.com    | 111.206.209.70 | 443  |
+-------------------------------+----------------+------+
```

**level 2**

```
+-------------------------------+----------------+------+-----------+------------------+
|             Host              |       Ip       | Port |  Domain   |      Title       |
+-------------------------------+----------------+------+-----------+------------------+
|    http://bos.im.baidu.com    | 220.181.*.68 |  80  | baidu.com |                  |
|    http://house.baidu.com     | 180.97.34.232  |  80  | baidu.com |    302 Found     |
|   http://apistore.baidu.com   | 103.235.46.238 |  80  | baidu.com |                  |
|   http://yingxiao.baidu.com   | 110.242.68.230 |  80  | baidu.com |                  |
|  https://hiphotos.baidu.com   | 103.235.47.66  | 443  | baidu.com |  404 Not Found   |
| http://trust-static.baidu.com | 112.80.248.190 |  80  | baidu.com | 百度商家口碑公告 |
|    http://koubei.baidu.com    | 112.80.248.190 |  80  | baidu.com |                  |
|     https://vcp.baidu.com     |   42.7.43.35   | 443  | baidu.com |                  |
|  http://nadvideo2.baidu.com   | 101.72.249.35  |  80  | baidu.com |                  |
|     http://vcp.baidu.com      | 182.84.120.35  |  80  | baidu.com |                  |
|     https://ww.baidu.com      | 110.242.68.66  | 443  | baidu.com |    302 Found     |
| https://developers.baidu.com  | 112.80.255.42  | 443  | baidu.com |                  |
|     http://cang.baidu.com     | 110.242.68.150 |  80  | baidu.com |                  |
|  http://developers.baidu.com  | 112.80.255.42  |  80  | baidu.com |                  |
|   https://gongyi.baidu.com    | 111.206.209.70 | 443  | baidu.com |                  |
+-------------------------------+----------------+------+-----------+------------------+


```

**level** **3**

```

+-------------------------------+----------------+------+-------------------------+-----------+------------------+---------+
|             Host              |       Ip       | Port |         Server          |  Domain   |      Title       | Country |
+-------------------------------+----------------+------+-------------------------+-----------+------------------+---------+
|    http://bos.im.baidu.com    | 220.181.111.68 |  80  | Jetty(9.4.14.v20181114) | baidu.com |                  |   CN    |
|    http://house.baidu.com     | 180.97.34.232  |  80  |         Apache          | baidu.com |    302 Found     |   CN    |
|   http://apistore.baidu.com   | 103.235.46.238 |  80  |                         | baidu.com |                  |   HK    |
|   http://yingxiao.baidu.com   | 110.242.68.230 |  80  |                         | baidu.com |                  |   CN    |
|  https://hiphotos.baidu.com   | 103.235.47.66  | 443  |       JSP3/2.0.14       | baidu.com |  404 Not Found   |   HK    |
| http://trust-static.baidu.com | 112.80.248.190 |  80  |          nginx          | baidu.com | 百度商家口碑公告 |   CN    |
|    http://koubei.baidu.com    | 112.80.248.190 |  80  |                         | baidu.com |                  |   CN    |
|     https://vcp.baidu.com     |   42.7.43.35   | 443  |       JSP3/2.0.14       | baidu.com |                  |   CN    |
|  http://nadvideo2.baidu.com   | 101.72.249.35  |  80  |          nginx          | baidu.com |                  |   CN    |
|     http://vcp.baidu.com      | 182.84.120.35  |  80  |       JSP3/2.0.14       | baidu.com |                  |   CN    |
|     https://ww.baidu.com      | 110.242.68.66  | 443  |      bfe/1.0.8.18       | baidu.com |    302 Found     |   CN    |
| https://developers.baidu.com  | 112.80.255.42  | 443  |                         | baidu.com |                  |   CN    |
|     http://cang.baidu.com     | 110.242.68.150 |  80  |         Apache          | baidu.com |                  |   CN    |
|  http://developers.baidu.com  | 112.80.255.42  |  80  |                         | baidu.com |                  |   CN    |
|   https://gongyi.baidu.com    | 111.206.209.70 | 443  |    Apache-Coyote/1.1    | baidu.com |                  |   CN    |
+-------------------------------+----------------+------+-------------------------+-----------+------------------+---------+

```



## 0x05 结语

如果您有好的建议，就在 Issues 提出来吧！
