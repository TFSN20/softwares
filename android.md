# Android Studio
如果之前安装过，则十分建议删除用户名目录下的.android和.gradle文件夹，AS的安装目录，Sdk所在的目录，以及项目目录（很重要）。

安装会在用户名目录下创建.android和.gradle文件夹，其中.gradle\wrapper\dists下存放各种版本的gradle，对应gradle-x.x-bin目录，
每个目录下的一连串数字字母符号下的gradle-x.x文件夹才是bin存放的地方，其中gradle-x.x同级可能存在存在（需要Sync刷新）gradle-x.x-bin.zip.lck和gradle-x.x-bin.zip.ok，gradle-x.x-bin.zip.part文件夹。
AS中gradle版本下载很慢，可以直接把外部下载好的zip放到一连串数字字母符号文件夹下，并解压（也就是说其实zip和解压文件都要有，但是好像这个方法没用，还是用本地代理完成全部下载吧）。
参考：https://blog.csdn.net/u011046452/article/details/107529346

下载完gradle还会下载maven，可以使用本地代理，设置127.0.0.1，v2ray中端口（分为走http和socks端口不一样）是10809，输入网址（https和http不一样）检查是否走了v2ray(然后还要重启AS，会再探出一个代理窗口，用于http和https)。
参考：https://blog.csdn.net/qq_65732918/article/details/134903527
。
USB真机调试：设置——搜索Sdk——SDK Tools——勾选并点击下载Google USB Driver——Android版本要和手机Android版本一致——手机打开开发者调试和安装。
参考：https://www.cnblogs.com/rainbow70626/p/14364552.html，https://cloud.tencent.com/developer/article/1743279

# android 玩机
## 抓包
- blackBox64+justTrustme模块：对未root机ssl校验好使，前提app是64位，androdi版本也不要太高。
- libChecker：能够查看app位数，原生库（比如opencv，极光认证SDK，百度LBS，U-App SDK），服务（极光推送，OPPO Push，MiPush），活动，权限，Dex（好用）。
- VitrualXposed app：不支持高版本android，优点是0.18.0（io.va.exposed）支持32位，可以和0.20.3（io.va.exposed64）版本共存。
- 低版本app：存在未加固，未对证书校验的情况，易于逆向分析。
# 电脑端
- jd-gui：使用前提有java环境。java -jar '你的jd-gui-1.6.6.jar位置'
- java环境：bing搜索java jdk，下载window版，设置系统变量：https://blog.csdn.net/qq_38436214/article/details/105071088