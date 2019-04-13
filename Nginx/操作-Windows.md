#  Windows下启动关闭Nginx

* ***使用cmd进入Nginx安装目录***
* 启动Nginx
  * start nginx （建议使用）
  * nginx.exe（不建议使用，会使cmd窗口一直处于命令执行状态，不可执行其他命令）
* 停止Nginx
  * nginx.exe -s quit （完整有序保存停止nginx，保存相关信息）
  * nginx.exe -s stop（快速停止，不保存其他信息）
* 重载Nginx
  * nginx.exe -s reload（配置信息修改后，需要重新载入）
* 重新打开日志文件
  * nginx.exe -s reopen
* 查看nginx版本
  * nginx -V

