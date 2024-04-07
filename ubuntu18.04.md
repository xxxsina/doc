## ubuntu 18.04

### 修改系统时间
1. 先关闭自动从互联网同步时间 
     ``` 
        timedatectl set-ntp 0  // 关闭命令
        timedatectl set-ntp 1  // 恢复命令
     ```
2. 修改
    ```
        date -s "2019-11-18 12:00:00"
    ```

3. 将硬件时间同步到系统时间
    ```angular2html
        hwclock --hctosys
    ```

4. 将系统时间同步到硬件时间
    ```angular2html
        hwclock --systohc
    ```
5. 显示硬件时间
    ```angular2html
        hwclock --show
    ```