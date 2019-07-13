#  Dart环境安装

##  使用Chocolatey安装Dart

在Linux下使用apt-get来安装查询，如今在windows下可以使用chocolatey来快速搭建一个开发环境。

chocolatey的哲学是完全使用命令来安装应用程序，更像一个包管理工具（背后使用nuget）

另外需要说明的是，chocolatey只是把官方的下载路径分装到chocolatey中，所以下载源都是官方路径，所以下载的一定是合法的。单如果是原软件需要licence注册的话，那么chocolatey下载安装好后需要购买注册。

chocolatey官网：<https://chocolatey.org/install>

* 打开cmd命令行

  ~~~~
  @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
  ~~~~

* 执行完毕后，chocolatey就安装好了

* 使用chocolatey安装软件

  ~~~shell
  #安装软件命令
  choco install java
  cinst java
  # 搜索软件
  clist ssh
  choco list ssh
  #卸载软件
  clist ssh
  cuninst ssh
  #其他命令
  cpack
  cpush
  cup
  cver
  ~~~

  