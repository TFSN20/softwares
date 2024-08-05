## 下载与设置
- classic：免费下载fiddler classic版本
- https：Tools-Options-Https全勾上
- 移动端抓取：Tools-Options-Connections左侧全部勾选，ipconfig:8888下载证书并安装到移动端
## 证书
- openssl官网下载精简版，管理员打开cmd cd /d d:/openssl bin所在目录
- 计算hash值
  ```
  openssl x509 -inform DER -subject_hash_old -in 证书文件.cer
  openssl x509 -subject_hash_old -in certificate.pem
  ```
- 导处到bin目录下
  ```
  openssl x509 -inform DER -text -in "d:\Downloads\FiddlerRoot.cer" > hash值.0
  ```
- 赋予最高权限
  ```
  chmod 644 /system/etc/security/cacerts/269953fb.0
  ```

# bl，刷机，root，系统分区，系统证书
- bypass解锁bl
- 下载线刷包（一般选择国行版），保存到D盘根目录（防止目录过长）：https://miuiver.com/
- 手机退出小米账号，进入fastboot模式
- XiaoMiFlash.exe：使用XiaoMiFlash.exe 加载设备，选择images上层目录，点击全部删除
- 刷机后：拔出SIM卡开机，开机后插入SIM卡，登陆小米账号，打开开发者模式，打开USB相关，网速显示。
- 给手机传入init_boot.img，kernelSu.apk，一个插件
- 使用KernelSU对boot.img（也有可能是init_boot.img或recovery.img）进行安装修补，将修补img发送到fastboot.exe所在目录
  - 下载：https://github.com/tiann/KernelSU/releases
  - 下载模块：https://www.magiskmodule.com/，以及酷安社区
- ```
  adb reboot fastboot
  fastboot flash init_boot magisk_patched-27000_3gjhq.img （不同img类型命令不一样boot，recovery）
  fastboot reboot
  ```
- 安装插件重启
- 解锁系统分区：在/data/adb/modules/目录下创建.rw文件夹，在.rw文件夹下创建system文件夹，在system文件夹下创建upperdir和workdir文件夹，重启
- 在KernelSu里对mt管理器，shell赋予root。

# 问题
- migisk非26版本以下不能使用magic_overlayfs模块，会导致root失效，只能刷机。
- 需要在KernelSU对应用赋予root权限，而不是让应用申请，比如shell（就是adb）
- KernelSU解锁system分区https://kernelsu.com/system-rw（至少先安装一个模块，否则没用）
