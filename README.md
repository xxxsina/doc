## Doc 

## 概述
- 对日常操作操作的记录文档

### macos新机的一些初始操作

#### macos终端植入ll操作

1. cd ~/     // 进入文件存放位置
2. touch .bash_profile   // 如果没有.bash_profile文件，就创建一个(有则忽略该步骤)
3. open -e .bash_profile     // 文本方式打开文件，也可以用vim，不过有权限问题，要用sudo vim 
  ``` 
   alias ll='ls -alF'   // 然后在.bash_profile文件中添加这一句，保存退出
  ```
4. source .bash_profile  // 载入更新后就可以使用 ll 了
