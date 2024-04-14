## Linux

#### 常规操作
```
    // 修改linux下用户密码 start
    # passwd // 修改root账号输入
    # passwd [username] // 修改其他账号
    // 修改linux下用户密码 end

    # sudo -u www-data -s   // 切换用户
    
    # cp -f file1 file2     // 强行复制

    // 建立软链接 start
    # cd /etc/nginx/sites-available // 进入文件夹
    # touch test.open.tt1.com.cn    // 创建文件
    # ln -s /etc/nginx/sites-available/test.open.tt1.com.cn ../sites-enabled/test.open.tt1.com.cn // 创建连接
    // 建立软链接 end

    # find /etc -name '*srm*'   // 查找文件名包含字符串的文件
    
    # ls -l | wc -l // 统计文件总数
    
    # du -sh application/logs/      // 查看文件夹大小

    // 修改服务器时间 start
    # service ntp stop  // 要改时间的话先把ntp服务关了
    # ntpdate ntp1.aliyun.com   // 修改服务器时间
    // 修改服务器时间 end
```

#### php
```
    # service php5-fpm restart    // 重启php
    # nohup /root/test.php &    // 后台启动php进程
```

#### mysql
```
    # grant all on *.* to root@'%' identified by "password";    // 开启mysql远程访问
    # flush privileges;     // 刷新设置
```

#### redis
```
    # pkill redis-server    // 杀死redis
    # ./redis-server /etc/redis.conf    // 启动
```

### 任务案例
```
// 图腾
#*/2 9-23 * * * /usr/bin/php -f /var/website/cli/index.php main/index/borrow/pending >> /home/uploader/cli_pending.log 2>&1
#*/7 9-23 * * * /usr/bin/php -f /var/website/cli/index.php main/index/borrow/fills >> /home/uploader/cli_fills.log 2>&1
*/13 9-23 * * * /usr/bin/php -f /var/website/cli/index.php main/index/uacount
*/16 9-23 * * * /usr/bin/php -f /var/website/cli/index.php main/index/tuhao
#10 1 * * * /usr/bin/php -f /var/website/cli/index.php main/index/repay >> /home/uploader/cli_repay.log 2>&1
#*/26 * * * * /usr/bin/php -f /var/website/cli/index.php main/index/borrow/canceled >> /home/uploader/cli_canceled.log 2>&1
50 15 * * * /usr/bin/php -f /var/v2/cli/index.php common/index/smd_package
#*/15 2-3 * * * /usr/bin/php -f /var/website/cli/index.php monitor/index/yaper/main.index.uacount
#*/20 2-3 * * * /usr/bin/php -f /var/website/cli/index.php monitor/index/tnuocau/nofile/main.index.tuhao
#1 11 * * * /usr/bin/php -f /var/website/cli/index.php lead_report/index
#1 16 * * * /usr/bin/php -f /var/website/cli/index.php lead_report/index
#30 8 * * * /usr/bin/php -f /var/website/cli/index.php recharge_total/index
#30 19 * * * /usr/bin/php -f /var/website/cli/index.php main/index/vip
*/5 8-20 * * * /usr/bin/php -f /var/website/cli/index.php main/index/setcredits
10 0 * * * /usr/bin/php -f /var/website/cli/index.php main/index/user_allow_deny


*/2 9-23 * * * /usr/bin/php -f /var/v2/cli/index.php main/index/borrow/pending >> /home/uploader/v2_cli_pending.log 2>&1
*/7 9-23 * * * /usr/bin/php -f /var/v2/cli/index.php main/index/borrow/fills >> /home/uploader/v2_cli_fills.log 2>&1
*/4 9-23 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/borrowFills >> /home/uploader/v2_cli_borrowFills.log 2>&1

22 10 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/inner_save
40 11 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/inner
20 12 * * * /usr/bin/php -f /var/v2/cli/index.php main/index/repay >> /home/uploader/v2_cli_repay.log 2>&1
30 13 * * * /usr/bin/php -f /var/v2/cli/index.php main/index/sms

10 4 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/moneyFund	//同步货基

*/26 * * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/transfercanceled >> /home/uploader/cli_transfercanceled.log 2>&1

*/3 9-23 * * * /usr/bin/php -f /var/v2/cli/index.php tplan/starTplan >> /home/uploader/v2_cli_tplanStart.log 2>&1
*/6 9-23 * * * /usr/bin/php -f /var/v2/cli/index.php tplan/tplanOut >> /home/uploader/v2_cli_tplanOut.log 2>&1

40 8 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/sinarepay	//统计任务
50 8 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/sinacompany	//统计任务

50 2 18 * * /usr/bin/php -f /var/v2/cli/index.php sina/index/putprops	//每月18号发送
20 1 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/birthday	//生日礼包
30 22 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/upgrade	//升级
20 23 * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/downgrade	//降级

0 1 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/user_info
10 1 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/user_recharge
40 1 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/user_cash
50 1 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/tender
10 2 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/tender_file
30 2 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/tender_payments
0 3 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/tender_transfer
10 3 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/zhaiquanzr
15 3 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/pt_borrow
35 3 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/pt_borrow_repayments
#55 3 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/llz_borrow
#15 4 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/llz_borrow_zhan
#35 4 * * * /usr/bin/php -f /var/v2/cli/index.php ancun/index/llz_borrow_repayments

******手动任务******
//转让标流标
*/26 * * * * /usr/bin/php -f /var/v2/cli/index.php sina/index/transfercanceled

//同步新浪存钱罐收益 某一天
/usr/bin/php -f /var/v2/cli/index.php sina/index/savingpot/20160412

//同步资金
/usr/bin/php -f /var/v2/cli/index.php sina/index/getmoney

//手动补单
/usr/bin/php -f /var/v2/cli/index.php tmp/repay_one_day/5244/20160516

//流标
/usr/bin/php -f /var/v2/cli/index.php main/index/borrow/canceled >> /home/uploader/cli_canceled.log 2>&1

//等级制度调整 上线后只执行一次
/usr/bin/php -f /var/v2/cli/index.php sina/index/setrole
```