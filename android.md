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
- jd-gui：使用前提有java环境。不同版本查看效果不一样，建议多试试，如低版本1.4.0（需要jre1.7.0的环境（更换JAVA_HOME变量值即可），对应jdk7，7以上安装时没有了jre文件夹，8以下安装时会让选择jre安装位置，直接选择jdk安装位置下面的jre就行，选其他地方会多余（和jdk安装目录下的jre文件夹重复））
  ```
  java -jar '你的jd-gui-1.6.6.jar位置'
  ```
- java环境：bing搜索java jdk，下载window版，设置系统变量：https://blog.csdn.net/qq_38436214/article/details/105071088
- dex2jar：dex装jar，apk解压得到若干dex，下载dex2jar.zip，
  ```
  你的d2j-dex2jar.bat位置 你的classes.dex位置(多个需要分别进行)
  ```
  借助c大批处理：https://bbs.tampermonkey.net.cn/thread-3560-1-1.html
  ```
  rem 这里填d2j-dex2jar路径
  set DEX2JAR="D:\Android\Tools\dex-tools-v2.4\d2j-dex2jar.bat"
  rem 这里填WinRAR路径
  set WINRAR="C:\Program Files\WinRAR\WinRAR.exe"

  for /r %%i in (*.dex) do call %DEX2JAR% "%%i"
  if exist package rd /s /q package
  if exist package.jar del /q package.jar
  md package
  for /r %%i in (*.jar) do %WINRAR% x -o+ "%%i" package
  %WINRAR% a -afzip -df -ep1 -r -m0 package.jar package\
  rd /s /q package
  ```
  在dex所在目录创建此bat运行即可。
- jadx-gui：有时新版本jd-gui某些函数解析不出来，且jadx对apk也生效，非常方便，另外可以右键某个函数进行frida，xposed hook函数赋值。
  ```
  java -jar '你的jadx-1.5.0-all.jar位置'
- blackDex：有32位和64位，选择zip源码自行编译。运行gradlew.bat即可。
  - 会先下载gradle指定版本在C:\Users\Administrator\.gradle。
  - 错误Could not receive a message from the daemon：关闭热点
  - Could not compile settings file 'D:\......\settings.gradle'.：java版本太高，v3.2.0版本使用jre-1.8
  - android sdk：设置用户变量ANDROID_SDK_ROOT为D:\ProgramFiles\Codes\Android\Sdk，之前安装过android studio会简单点。需要ndk21.4.7075529，由于是谷歌源，所以bat下载会失败，去as设置搜索sdk进行下载，需要android sdk platforms 30版本，这个bat就行。

  - 构建项目：
    ```
    gradle build (项目根目录)或
    gradlew.bat build
    ```
- java：
  - jdk需要和jre版本对齐，jdk7，jdk8安装时会向注册表写入东西，但是系统变量优先级更高，不用管注册表，一般只改JAVA_HOME变量即可。
    ```
    where java（查看java位置，由于path中存在%SystemRoot%\system32，而jdk7会在这里留下java.ex，javaw.exe，javaws.exe，删除这三个文件，因为重复了，在%JAVA_HOME%\bin下就有，有影响。jdk会在path中写入C盘符java.exe，也会有影响，删除这个变量。）
    ```
    ```
    java -version（查看jdk，jre版本）
    ```
# 手机必装的app
- aurora store 第三方谷歌商店
- Droid-ify 开源app下载
