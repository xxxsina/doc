
#### 开启远程访问
```
    # grant all on *.* to root@'%' identified by "password";    // 开启mysql远程访问
    # flush privileges;     // 刷新设置
```

#### 查看数据库字符集
```
  # show variables like '%char%';
```

#### 查看 MySQL 数据表（table） 的字符集
```
  # show table status from sqlstudy_db like '%countries%';
```
#### 查看 MySQL 数据列（column）的字符集
```
  # show full columns from countries;
```
#### 查看当前安装的 MySQL 所支持的字符集
```
  # show character set
```
#### 修改字段字符集
```
  # ALTER TABLE m_collection CONVERT TO CHARACTER SET utf8
```
#### mysql对自增id重新从1排序
```
  # ALTER TABLE m_games AUTO_INCREMENT=0
```

### 一些日常维护的数据操作案例
```
// 替换操作
UPDATE m_games_packs SET title=REPLACE(title, '安卓', '') WHERE title like "%安卓%";
UPDATE c_comic_episodes SET url=REPLACE(url, 'auto', 'at') WHERE url like "%auto%" and cid=2294 and sid=2;
UPDATE c_comic_gallery_source SET dataId=SUBSTRING(dataId,10)

// 数据去重
  # 检查  
  SELECT  MAX(id) AS id,COUNT(loginId) AS c,loginId FROM m_bind GROUP BY loginId,appId HAVING c>1 ORDER BY c DESC
DELETE FROM m_bind WHERE id IN (SELECT id FROM (SELECT  MAX(id) AS id,COUNT(loginId) AS c FROM m_bind GROUP BY loginId,appId HAVING c>1 ORDER BY c DESC) AS tab )

DELETE FROM c_comic_episodes WHERE id IN (SELECT id FROM (SELECT  MAX(id) AS id,COUNT(1) AS c FROM c_comic_episodes WHERE sid=2 GROUP BY dataId HAVING c>1 ORDER BY c DESC) AS tab )

// 更新comic表status
UPDATE c_comic c INNER JOIN  c_comic_source s ON c.id=s.cid SET c.status=1
UPDATE c_comic_source c INNER JOIN  c_comic_episodes s ON c.cid=s.cid AND c.sid=s.sid AND c.lianzai=s.name SET c.eid=s.id

// 查询group后的总数
SELECT *,COUNT(*) AS c FROM  m_subscribe WHERE del =1 GROUP BY userId HAVING c>9 AND c <15 ORDER BY c DESC

// 去重求和  再也不用group了
SELECT COUNT(DISTINCT article_id) FROM t_article_tag_rel WHERE tag_id IN (SELECT id FROM t_article_tags WHERE alpha='P') 

// 今日收益统计
SELECT SUM(everyday_interest) AS mon1 FROM `t_repay_log` WHERE `everyday_interest` >0  AND `created` <= '2015-07-20 09:45:08'  AND `recover_time` >= 1437408000  AND `status` IN('wait', 'done')  AND `uid` = '2376'   
 
SELECT SUM(recover_interest) AS mon2 FROM `t_repay_log` WHERE `status` IN('wait', 'done')  AND `recover_time` >= 1437408000 AND `recover_time` < 1437494399  AND `uid` = '2376'  AND `everyday_interest` =0


// 导流水
SELECT id AS '序号',amount_before AS '总金额（前）',balance_before AS '可用（前）', frozen_before AS '冻结（前）' ,await_before AS '代收总额（前）',
money AS '本次操作金额', tob AS '操作类型', amount_after AS '总资金（后）', balance_after AS '可用（后）',frozen_after AS '冻结（后）', await_after AS '代收总额（后）' , created AS '操作时间'
FROM t_account_log_201601 WHERE uid = 6585 ORDER BY created ASC ,id ASC 
```

### 大数据导入示例

```
load data infile "D:/5w.csv" ignore into table am_demand CHARACTER SET utf8 fields terminated by ','  ignore 1 lines (@contact_phone, @name, @sex, @remark) set contact_phone=trim(@contact_phone),name=trim(@name),sex=if(trim(@sex)='男',1,if(trim(@sex)='女',2,0)),remark=trim(@remark),contact_phone_second=trim(@contact_phone),contact_phone_third=trim(@contact_phone);

load data infile "D:/test.csv" ignore into table am_demand CHARACTER SET utf8 fields terminated by ','  ignore 1 lines (@contact_phone, @name, @sex, @remark) set contact_phone=trim(@contact_phone),name=trim(@name),sex=REPLACE(@sex, "男", 1),remark=trim(@remark),contact_phone_second=trim(@contact_phone),contact_phone_third=trim(@contact_phone);
```