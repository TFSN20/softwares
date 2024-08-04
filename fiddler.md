## 下载与设置
- classic：免费下载fiddler classic版本
- https：Tools-Options-Https全勾上
- 移动端抓取：Tools-Options-Connections左侧全部勾选，ipconfig:8888下载证书并安装到移动端
## 证书
- openssl官网下载精简版，管理员打开cmd cd /d d:/openssl bin所在目录
- 计算hash值
  ```
  openssl x509 -inform DER -subject_hash_old -in 证书文件.cer
  ```
- 导处到bin目录下
  ```
  openssl x509 -inform DER -text -in "d:\Downloads\FiddlerRoot.cer" > hash值.0
  ```
# root
- bypass解锁bl
- 下载当前系统的线刷包（如果没有则选择先刷机，即先下载mifash，不是mifash_unloack，进行刷机）
- 下载migisk对boot.img（也有可能是init_boot.img或recovery.img）进行安装修补
- ```
  adb reboot fastboot
  fastboot flash init_boot magisk_patched-27000_3gjhq.img （不同img类型命令不一样boot，recovery）
  fastboot reboot
  ```
# 问题
- migisk非26版本以下不能使用magic_overlayfs模块，会导致root失效，只能刷机。
- 需要在KernelSU对应用赋予root权限，而不是让应用申请，比如shell（就是adb）
- KernelSU解锁system分区https://kernelsu.com/system-rw（至少先安装一个模块，否则没用）
