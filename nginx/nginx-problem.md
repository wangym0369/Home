## nginx常见问题



+ **nginx正常启动，要访问的资源存在，访问资源时却返回403状态码**
  + 查看启动用户和nginx工作用户是否一致（`检查配置文件中user指令`）
  + 检查`nginx`是否具有**web根目录**的访问权限