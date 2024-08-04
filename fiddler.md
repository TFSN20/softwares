## 下载与设置
- classic：免费下载fiddler classic版本
- https：Tools-Options-Https全勾上
- 移动端抓取：Tools-Options-Connections左侧全部勾选，ipconfig:8888下载证书并安装到移动端
## 证书与root
- openssl官网下载精简版，管理员打开cmd cd /d d:/openssl bin所在目录
- 计算hash值
  ```
  openssl x509 -inform DER -subject_hash_old -in 证书文件.cer
  ```
- 导处到bin目录下
  ```
  openssl x509 -inform DER -text -in "d:\Downloads\FiddlerRoot.cer" > hash值.0
  ```
-
