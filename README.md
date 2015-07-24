# ass_hole_hunter
Security framework, hunt for ass hole of the web/network, and fuck them!

#update 2015.04.09
工具设计：

存活扫描模块
1.批量扫描，获取可用的WEB站点
2.每次扫描信息存入report目录下单独的子目录下
3.支持附加端口，但需要手动添加，如192.168.1.130:8080(无论域名和IP，如果有https请加上)
4.自动获取banner，读取title，匹配CMS类型或硬件类型，存入扫描名目录下
5.支持一键扫描（参数 -c），存储结果以sqlite存储

CMS识别模块
1.批量识别CMS类型和定向打击CMS两种（模块选择）
2.此模块在开始运行后，如果没有加-nP参数，会无差别先扫描存活网站（先过存活扫描模块）
非存活网站分为两类
（1）没有banner，只有IIS7,apache/Tomcat页面之类的，或者白页（值得商榷）
（2）不能访问的WEB接口
3.匹配CMS类型（硬件类型）可采用“banner/title”+“特殊文件/目录”+匹配MD5值进行匹配，优先级依次降低。
4.获取banner-->telnet nc？获取title-->直接读取
5.如果是定向打击，系统会先展示CMS库，支持tab补全模式
6.匹配结果写入sqlite数据库

C段+同服模块
1.采集shodan.io+fofa.so+oshadan.com的资源，进行同服查询
2.C段即重复爬取
3.可以通过此收取banner或者title
。。。。。。

漏洞扫描模块
1.可follow上面的CMS模块
2.定向漏洞打击，系统会先展示漏洞库，支持tab补全模式（暂定一个）
3.批量盲打漏洞，系统会根据CMS模块收集的信息进行定向盲打，加-m参数可以无差别尝试全部漏洞项（不加参数，如果没有获取到CMS信息就不会尝试）
4.漏洞收录，暂定中高危
5.漏洞扫描结果存入sqlite存储

WAF绕过模块
1.random-http-socket
2....
3.设计第三方接入模块，比如(..还没想出来，代理不用加，直接全局吧)
4.设置全局代理模式，设定配置文件

其他要点
1.每次加载CMS时检查漏洞库和CMS库有没有更新，若有更新，对根目录配置sqlite数据库进行更新
2.数据库文件
（1）扫描临时文件
ID号--|--URL（IP+端口)--|--存活与否--|--banner OR title--|--CMS类型--|--漏洞名字--|--

（2）CMS库
CMS编号--|--CMS名字--|--CMS语言类型--|--

（3）漏洞库
漏洞编号--|--漏洞名字--|--漏洞类型--|--漏洞参考来源--|--

4.附上demo（demo.py）

#update 2015.04.14
1.lib库的function指令集
2.color模块完成
3.撰写功能测试模块--批量获取title/banner

#update 2015.04.16
1.测试模块基本完成
2.尝试构建线程池模块
3.建议加参数进行更新设置，不用自动更新

#update 2015.04.17
1.剔除存活扫描模块(意义不大，nmap都搞不定还搞个鸡毛。。)
2.更迭banner_title获取模块，直接添加一个主调用模块，
3.在主启动器处，采用线程池分配，若采用字典直接在此分离

#update 2015.04.20
1.正式删除一键全程，在主启动器通过线程池分配实现。

#update 2015.04.21

1.更新数据库模块，完成部分
2.添加exploit的demo
3.待续

#update 2015.04.2
1.更新数据库报告部分

#update 2015.04.23
1.修改完成CMS识别的基础模块
2.

#update 2015.05.06
1.shodan:https://shodan.readthedocs.org/en/latest/tutorial.html
2.https://www.oshadan.com/instruction
3.fofa.so挂了

#update 2015.05.12
1.做f同服C段查询测试demo

#upadte 2015.05.20
我草你大爷！！！
1.完成bpg查询模块
2.fofa.so模块暂缺
3.c段的话，支持临时生成ip的字典，通过线程分发，查询得出结果再排序。


#update 2015.06.04
1.fofa已回复，不过似乎可以用
2.更新fofa模块
3.盲打定位模糊

#update 2015.06.05
1.完成测试exp
2.构建测试库

#update 2015.06.30
1.完成cms识别模块的脚本类型
2.需要后期提取去重特征
