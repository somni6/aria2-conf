# 根据 [Aria2 Manual](https://aria2.github.io/manual/en/html/) 汉化大部分的配置文件  

[汉化的配置文件](https://github.com/lilyvya/aria2-conf/blob/master/aria2.conf.example)  
**请勿直接使用此配置文件，至少需要更改** `rpc-secret=` **的值**  

下载后去掉所有文件 .example 后缀  
要运行还需要 [Aria2.exe](https://github.com/aria2/aria2/releases) (Windows) ，建议和 [webui-aria2](https://github.com/ziahamza/webui-aria2) 搭配使用  

## 下面是 Windows 的启动方式和 Firefox FlashGot 调用  

### Windows  
Windows CMD 启动双击 start.bat ，后台运行双击 HideRun.vbs  

若要自启动又需要管理员权限使用任务计划程序  
1. 打开任务计划程序：控制面板→管理工具→任务计划程序  
2. 创建任务  
3. 常规  
  3.1. 更改用户或组，使用 SYSTEM 账户  
  3.2. 如果你使用 falloc 的文件预分配方式，又有  

>[WARN] Gaining privilege SeManageVolumePrivilege failed.  

的出现，则使用最高权限运行打上勾  

4. 触发器  
  4.1. 新建  
  4.2. 开始任务选择登录时  
  4.3. 可以按需选择延迟任务时间  
  4.4. 已启用务必确认勾选  
5. 操作  
  5.1. 新建  
  5.2. 程序或脚本选择 `\PATH\aria2c.exe`  
  5.3. 添加参数 `--conf=aria2.conf`  
  5.4. 起始于 `PATH\` （aria2c.exe所在目录）  
6. 条件  
  6.1. 勾全部取消，包括黑掉的（ Windows 蜜汁 BUG ，黑掉的有时候也会生效）  
7. 设置  
  7.1. 仅勾选允许按需运行任务  
  7.2. 如果此任务已经运行，以下规则适用：请勿启动新实例  

### Firefox FlashGot 的调用方式  
需要 [Python2](https://www.python.org/downloads/windows/) 环境  
以 Windows 为例  
* 新增一个下载管理  
* 如果你的系统环境不对：  
  * 可执行路径：`PATH\Python2\pythonw.exe`  
  * 参数模板：`PATH\Aria2\run.pyw --secret <SECRET> --dir PATH [--cookie COOKIE] [--output FNAME] [--referer REFERER] [--user-agent UA] [URL]`  
* 如果系统环境正确：  
  * 可执行路径：`PATH\Aria2\run.pyw`  
  * 参数模板： `--secret <SECRET> --dir PATH [--cookie COOKIE] [--output FNAME] [--referer REFERER] [--user-agent UA] [URL]`  
* 参数模板 `--secret <SECRET>` 里的 `<SECRET>` 替换为 `aria2.conf` 里的 `rpc-secret=` 后面的值  
* 如果需要局域网或互联网使用，在参数模板里加上`--rpc http://127.0.0.1:6800/jsonrpc` ，127.0.0.1:6800 替换为你需要的
 IP / 域名和端口  
