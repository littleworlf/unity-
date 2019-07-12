# unity
Unity手游自动化测试心得（GAutomator&AirTest）

GAutomator Unity自动化测试

简介
GAutomator是Tencent WeTest团队的一个开源的项目，对应的测试IDE仍在开发中 ，由于没有集成为一个IDE，所以需要集成SDK到被测APK中，打包成测试APK才能连接测试，需要配合GAutomatorView使用，实现可视化。项目用到了Tencent 开发的wpyscripts(天火),但是wpyscripts我在网上没找到相应的API文档。
GAutomator 是为 Unity 游戏量身定制的自动化测试框架。类似于 UIAutomator 操作 Android 标准控件，GAutomator 通过 Gameobject 为操作单元能够实现对 Unity 手游的自动化 UI 测试，同时支持 NGUI 和 UGUIUI 控件，能够完成包括 click、press、swipe、摇杆和 QQ、微信登录等操作。
上文提及的wpyscripts是Tencent专门为unity开发的一个手游测试Python API库。
GAutomatorView是一个独立的exe程序，可以连接并同步手游的实时画面，获取对应的控件并生成对应树形结构，在这里还可以复制某个component的路径，以及查看component的属性信息，有了这些信息，我们才可以根据这些路径和属性，完成对应的测试脚本的编写。

用法
1.将GAutomator SDK集成到unity游戏项目中，打包成测试用的apk，集成SDK说明文档可参考官方文档，地址
https://github.com/Tencent/GAutomator/blob/master/GAutomatorSdk/docs/Unity%E6%B8%B8%E6%88%8F%E9%9B%86%E6%88%90GAutomator%20SDK.md 
2.clone官方的开源项目到本地，官方开源项目GitHub地址https://github.com/Tencent/GAutomator?from=content_csdnblog
任选一个你喜欢的编辑器，PyCharm、sublime均可，并打开项目，在开源项目中新增自己的测试用例python脚本，推荐放在main.py同一目录下，运行，输出测试结果将实时输出到控制台。
ps:SDK目前只支持Android平台，IOS平台能够编译，但是无效。


AirTest自动化测试
简介
AirTest是网易推出的一套手机游戏自动化测试框架，同样是用python语言，AirTestAPI开源并且有对应的AirtestAPI说明文档，API说明文档：
https://airtest.readthedocs.io/en/latest/all_module/airtest.core.api.html
并且，网易已经开发出自己的AirTestIDE，可以在官网下载并体验，airtest官网http://airtest.netease.com/
使用教程文档http://airtest.netease.com/docs/en/index.html


用法
AirTest Project核心组成是Airtest和Poco两大框架，他们都是Python的第三方库，airtest.core.api中提供了大量的操作，如click、swipe、keyevent等。AirTestIDE是官方提供的集成开发环境，可以连接手机并进行代码等编写测试运行，可以通过点击游戏画面的形式，快速生成图文混合的测试代码，代码简单易懂，对于自动生成的代码，可能有不和心意的地方，经过简单的调整后即可测试运行，运行过程中，控制台会实时打印测试中间过程的结果，最终运行结束后，将以网页的形式生成测试报告。具体的操作教程见上文使用教程文档

总结与思考：
1.GAutomator和AirTest都是通过引入python第三方库的形式调用函数，通过在测试脚本中模拟用户输入，达到测试效果。
2.想要将自动化测试集成到unity中，首先需要对第三方库中的方法进行二次开发，封装成c#方便使用的接口，https请求也好，设法引入第三方库也好，总之进行二次包装。值得一提的是，Tencent已经做过这样的事情，在GAutomator SDK 1.5.0版本中提供了接口，可以调用python注册的函数，类似于远程RPC调用，支持同步/异步调用。
3.AirTestIDE使用简单，上手很容易，但是IDE本身并不开源。因而，要想集成至unity，这两种方式都需要我们自行开发IDE页面。
