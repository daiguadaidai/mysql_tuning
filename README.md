# mysql_tuning
输出MySQL调优的一些信息

#### 创建参数文件

参数文件主要用于连接 MySQL, 和确认需要显示的调优信息(mysql_tuning.cnf)

```
[database]
server_ip   = 127.0.0.1
db_user     = testuser
db_pwd      = testpwd
db_name     = test
db_port     = 3306

[option]
# 是否显示系统参数
sys_parm    = ON
# 是否显示执行计划
sql_plan    = ON
# 是否显示相关对象(表、索引)统计信息
obj_stat    = ON
# 是否显示运行前后状态信息(激活后会真实执行SQL)
ses_status  = ON
# 是否显示PROFILE跟踪信息(激活后会真实执行SQL)
sql_profile = ON
```

#### 基本使用 和 输出

```
python mysql_tuning.py -p /etc/mysql_tuning.cnf -s 'select * from opt_member'

****************************************************************************************************
*                             MySQL SQL Tuning Tools v1.0 (by hanfeng)                             *
****************************************************************************************************

===== BASIC INFORMATION =====
+----------------------+------------+------------+------------+------------+
|      server_ip       | user_name  |  db_name   |    port    | db_version |
+----------------------+------------+------------+------------+------------+
|      127.0.0.1       | testuser   |  testpwd   |    3306    | 5.6.29-log |
+----------------------+------------+------------+------------+------------+

===== ORIGINAL SQL TEXT =====
SELECT *
FROM opt_member

===== SYSTEM PARAMETER =====
+--------------------------------+------------------------------------------------------------+
|         parameter_name         |                           value                            |
+--------------------------------+------------------------------------------------------------+
| binlog_cache_size              |                                                     32.0 K |
| bulk_insert_buffer_size        |                                                      8.0 M |
| have_query_cache               |                                                        YES |
| interactive_timeout            |                                                      28800 |
| join_buffer_size               |                                                    256.0 K |
| key_buffer_size                |                                                     16.0 M |
| key_cache_age_threshold        |                                                        300 |
| key_cache_block_size           |                                                      1.0 K |
| key_cache_division_limit       |                                                        100 |
| large_pages                    |                                                        OFF |
| locked_in_memory               |                                                        OFF |
| long_query_time                |                                                  10.000000 |
| max_allowed_packet             |                                                    1048576 |
| max_binlog_cache_size          |                                            17179869183.0 G |
| max_binlog_size                |                                                      1.0 G |
| max_connections                |                                                       1000 |
| max_connect_errors             |                                                        100 |
| max_join_size                  |                                            17179869183.0 G |
| max_length_for_sort_data       |                                                       1024 |
| max_seeks_for_key              |                                       18446744073709551615 |
| max_sort_length                |                                                       1024 |
| max_tmp_tables                 |                                                         32 |
| max_user_connections           |                                                          0 |
| optimizer_prune_level          |                                                          1 |
| optimizer_search_depth         |                                                         62 |
| query_cache_size               |                                                      1.0 M |
| query_cache_type               |                                                        OFF |
| query_prealloc_size            |                                                      8.0 K |
| range_alloc_block_size         |                                                      4.0 K |
| read_buffer_size               |                                                    256.0 K |
| read_rnd_buffer_size           |                                                    512.0 K |
| sort_buffer_size               |                                                    512.0 K |
| sql_mode                       |                                     NO_ENGINE_SUBSTITUTION |
| thread_cache_size              |                                                       18 B |
| tmp_table_size                 |                                                     16.0 M |
| wait_timeout                   |                                                      28800 |
+--------------------------------+------------------------------------------------------------+

===== OPTIMIZER SWITCH =====
+------------------------------------------+------------+
|               switch_name                |   value    |
+------------------------------------------+------------+
| index_merge                              |         on |
| index_merge_union                        |         on |
| index_merge_sort_union                   |         on |
| index_merge_intersection                 |         on |
| engine_condition_pushdown                |         on |
| index_condition_pushdown                 |         on |
| mrr                                      |         on |
| mrr_cost_based                           |         on |
| block_nested_loop                        |         on |
| batched_key_access                       |        off |
| materialization                          |         on |
| semijoin                                 |         on |
| loosescan                                |         on |
| firstmatch                               |         on |
| subquery_materialization_cost_based      |         on |
| use_index_extensions                     |         on |
+------------------------------------------+------------+

===== SQL PLAN =====
+--------+------------------+------------+------------+----------------------+------------+------------+------------+------------+------------+------------+
|   id   |   select_type    |   table    |    type    |    possible_keys     |    key     |  key_len   |    ref     |    rows    |  filtered  |   Extra    |
+--------+------------------+------------+------------+----------------------+------------+------------+------------+------------+------------+------------+
|      1 | SIMPLE           | opt_member | ALL        | NULL                 | NULL       | NULL       | NULL       |    1730778 |      100.0 | NULL       |
+--------+------------------+------------+------------+----------------------+------------+------------+------------+------------+------------+------------+

===== OPTIMIZER REWRITE SQL =====
SELECT `nbuy52db`.`opt_member`.`MEMBER_ID` AS `MEMBER_ID`,
       `nbuy52db`.`opt_member`.`UNAME` AS `UNAME`,
       `nbuy52db`.`opt_member`.`PASSWORD` AS `PASSWORD`,
       `nbuy52db`.`opt_member`.`NICK_NAME` AS `NICK_NAME`,
       `nbuy52db`.`opt_member`.`TRUE_NAME` AS `TRUE_NAME`,
       `nbuy52db`.`opt_member`.`OPEN_ID` AS `OPEN_ID`,
       `nbuy52db`.`opt_member`.`AUTH_OPEN_ID` AS `AUTH_OPEN_ID`,
       `nbuy52db`.`opt_member`.`SEX` AS `SEX`,
       `nbuy52db`.`opt_member`.`QQ` AS `QQ`,
       `nbuy52db`.`opt_member`.`EMAIL` AS `EMAIL`,
       `nbuy52db`.`opt_member`.`MOBILE` AS `MOBILE`,
       `nbuy52db`.`opt_member`.`TELPHONE` AS `TELPHONE`,
       `nbuy52db`.`opt_member`.`LASTLOGIN` AS `LASTLOGIN`,
       `nbuy52db`.`opt_member`.`REGTIME` AS `REGTIME`,
       `nbuy52db`.`opt_member`.`BIRTHDAY` AS `BIRTHDAY`,
       `nbuy52db`.`opt_member`.`STATE` AS `STATE`,
       `nbuy52db`.`opt_member`.`REMARK` AS `REMARK`,
       `nbuy52db`.`opt_member`.`PROVINCE_ID` AS `PROVINCE_ID`,
       `nbuy52db`.`opt_member`.`PROVINCE_NAME` AS `PROVINCE_NAME`,
       `nbuy52db`.`opt_member`.`CITY_ID` AS `CITY_ID`,
       `nbuy52db`.`opt_member`.`CITY_NAME` AS `CITY_NAME`,
       `nbuy52db`.`opt_member`.`DISTRICT_ID` AS `DISTRICT_ID`,
       `nbuy52db`.`opt_member`.`DISTRICT_NAME` AS `DISTRICT_NAME`,
       `nbuy52db`.`opt_member`.`PIC_FACE_ID` AS `PIC_FACE_ID`,
       `nbuy52db`.`opt_member`.`PIC_FACE_PATH` AS `PIC_FACE_PATH`,
       `nbuy52db`.`opt_member`.`LIFE_PROVINCE_ID` AS `LIFE_PROVINCE_ID`,
       `nbuy52db`.`opt_member`.`LIFE_PROVINCE_NAME` AS `LIFE_PROVINCE_NAME`,
       `nbuy52db`.`opt_member`.`LIFE_DISTRICT_ID` AS `LIFE_DISTRICT_ID`,
       `nbuy52db`.`opt_member`.`LIFE_DISTRICT_NAME` AS `LIFE_DISTRICT_NAME`,
       `nbuy52db`.`opt_member`.`LIFE_CITY_ID` AS `LIFE_CITY_ID`,
       `nbuy52db`.`opt_member`.`LIFE_CITY_NAME` AS `LIFE_CITY_NAME`,
       `nbuy52db`.`opt_member`.`ADDRESS_DETAIL` AS `ADDRESS_DETAIL`,
       `nbuy52db`.`opt_member`.`RECOMMEND_TERMINAL` AS `RECOMMEND_TERMINAL`,
       `nbuy52db`.`opt_member`.`RECOMMEND_MEMBER_ID` AS `RECOMMEND_MEMBER_ID`,
       `nbuy52db`.`opt_member`.`IS_PARTNER` AS `IS_PARTNER`,
       `nbuy52db`.`opt_member`.`MY_TERMINAL_CODE` AS `MY_TERMINAL_CODE`,
       `nbuy52db`.`opt_member`.`PARTNER_TYPE` AS `PARTNER_TYPE`,
       `nbuy52db`.`opt_member`.`PARTNER_NAME` AS `PARTNER_NAME`,
       `nbuy52db`.`opt_member`.`ASSOCIATOR_ID` AS `ASSOCIATOR_ID`,
       `nbuy52db`.`opt_member`.`FULL_MEMBER` AS `FULL_MEMBER`,
       `nbuy52db`.`opt_member`.`FULL_MEMBER_TIME` AS `FULL_MEMBER_TIME`,
       `nbuy52db`.`opt_member`.`RD` AS `RD`,
       `nbuy52db`.`opt_member`.`TYPE` AS `TYPE`,
       `nbuy52db`.`opt_member`.`IS_AUTH` AS `IS_AUTH`,
       `nbuy52db`.`opt_member`.`ACCOUNT_ID` AS `ACCOUNT_ID`,
       `nbuy52db`.`opt_member`.`CREATED_BY` AS `CREATED_BY`,
       `nbuy52db`.`opt_member`.`CREATION_METHOD` AS `CREATION_METHOD`,
       `nbuy52db`.`opt_member`.`CREATION_TIME` AS `CREATION_TIME`,
       `nbuy52db`.`opt_member`.`UPDATED_BY` AS `UPDATED_BY`,
       `nbuy52db`.`opt_member`.`UPDATE_METHOD` AS `UPDATE_METHOD`,
       `nbuy52db`.`opt_member`.`UPDATE_TIME` AS `UPDATE_TIME`,
       `nbuy52db`.`opt_member`.`DELETE_FLAG` AS `DELETE_FLAG`,
       `nbuy52db`.`opt_member`.`OLD_LV` AS `OLD_LV`,
       `nbuy52db`.`opt_member`.`OLD_YUNNIU` AS `OLD_YUNNIU`,
       `nbuy52db`.`opt_member`.`OLD_JINNIU` AS `OLD_JINNIU`,
       `nbuy52db`.`opt_member`.`OLD_FID` AS `OLD_FID`,
       `nbuy52db`.`opt_member`.`OLD_ID` AS `OLD_ID`,
       `nbuy52db`.`opt_member`.`OLD_LOGIN_NAME` AS `OLD_LOGIN_NAME`,
       `nbuy52db`.`opt_member`.`OLD_LOGIN_PWD` AS `OLD_LOGIN_PWD`,
       `nbuy52db`.`opt_member`.`OLD_CRT_TIME` AS `OLD_CRT_TIME`,
       `nbuy52db`.`opt_member`.`BELONG_COOPERATOR_ID` AS `BELONG_COOPERATOR_ID`
FROM `nbuy52db`.`opt_member`

===== OBJECT STATISTICS =====
+-----------------+------------+------------+------------+------------+------------+------------+------------+
|    table_name   |   engine   |   format   | table_rows |  avg_row   |  total_mb  |  data_mb   |  index_mb  |
+-----------------+------------+------------+------------+------------+------------+------------+------------+
| opt_member      | InnoDB     | Compact    |    1730778 |        391 |    1208.38 |     646.00 |     562.38 |
+-----------------+------------+------------+------------+------------+------------+------------+------------+
+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+
|    index_name   |    non_unique   |   seq_in_index  |   column_name   |    collation    |   cardinality   |     nullable    |    index_type   |
+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+
| IDX_ACCOUNT_ID  |               1 |               1 |      ACCOUNT_ID |               A |               2 |             YES |           BTREE |
| IDX_ASSOCIATOR_ID |               1 |               1 |   ASSOCIATOR_ID |               A |               2 |             YES |           BTREE |
| IDX_AUTH_OPEN_ID |               1 |               1 |    AUTH_OPEN_ID |               A |          865389 |             YES |           BTREE |
| IDX_CITY_ID     |               1 |               1 |         CITY_ID |               A |             684 |             YES |           BTREE |
| IDX_DELETE_FLAG |               1 |               1 |     DELETE_FLAG |               A |               2 |             YES |           BTREE |
| IDX_DISTRICT_ID |               1 |               1 |     DISTRICT_ID |               A |            5637 |             YES |           BTREE |
| IDX_LIFE_CITY_ID |               1 |               1 |    LIFE_CITY_ID |               A |             532 |             YES |           BTREE |
| IDX_LIFE_DISTRICT_ID |               1 |               1 | LIFE_DISTRICT_ID |               A |            5477 |             YES |           BTREE |
| IDX_LIFE_PROVINCE_ID |               1 |               1 | LIFE_PROVINCE_ID |               A |              80 |             YES |           BTREE |
| IDX_MOBILE      |               1 |               1 |          MOBILE |               A |         1730778 |             YES |           BTREE |
| IDX_OPEN_ID     |               1 |               1 |         OPEN_ID |               A |            5807 |             YES |           BTREE |
| IDX_PROVINCE_ID |               1 |               1 |     PROVINCE_ID |               A |              88 |             YES |           BTREE |
| IDX_RECOMMEND_TERMINAL |               1 |               1 | RECOMMEND_TERMINAL |               A |           86538 |             YES |           BTREE |
| IDX_SEX         |               1 |               1 |             SEX |               A |               4 |             YES |           BTREE |
| IDX_UNAME       |               1 |               1 |           UNAME |               A |         1730778 |                 |           BTREE |
| index_regtime   |               1 |               1 |         REGTIME |               A |         1730778 |             YES |           BTREE |
| PRIMARY         |               0 |               1 |       MEMBER_ID |               A |         1730778 |                 |           BTREE |
+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+-----------------+

===== SESSION STATUS (DIFFERENT) =====
+-------------------------------------+-----------------+-----------------+-----------------+
|             status_name             |      before     |      after      |       diff      |
+-------------------------------------+-----------------+-----------------+-----------------+
| Bytes_received                      |             505 |             726 |             221 |
| Bytes_sent                          |             396 |       634821701 |       634821305 |
| Com_select                          |               2 |               4 |               2 |
| Connections                         |           12932 |           12992 |              60 |
| Created_tmp_tables                  |               2 |               3 |               1 |
| Handler_commit                      |               0 |               1 |               1 |
| Handler_external_lock               |               0 |               2 |               2 |
| Handler_read_first                  |               0 |               1 |               1 |
| Handler_read_key                    |               0 |               1 |               1 |
| Handler_read_rnd                    |               0 |             356 |             356 |
| Handler_read_rnd_next               |               6 |         1763843 |         1763837 |
| Handler_write                       |             186 |             542 |             356 |
| Innodb_buffer_pool_read_requests    |         8474525 |        10279407 |         1804882 |
| Innodb_rows_read                    |         2132794 |         3896273 |         1763479 |
| Qcache_not_cached                   |           53846 |           54127 |             281 |
| Queries                             |          148358 |          149060 |             702 |
| Questions                           |               5 |               7 |               2 |
| Select_scan                         |               2 |               4 |               2 |
| Slow_queries                        |               0 |               1 |               1 |
| Sort_rows                           |               0 |             356 |             356 |
| Sort_scan                           |               0 |               1 |               1 |
| Table_locks_immediate               |           17240 |           17341 |             101 |
| Table_open_cache_hits               |               0 |               1 |               1 |
| Threads_created                     |            1266 |            1272 |               6 |
| Uptime                              |           15644 |           15719 |              75 |
| Uptime_since_flush_status           |           15644 |           15719 |              75 |
+-------------------------------------+-----------------+-----------------+-----------------+

===== SQL PROFILING(DETAIL)=====
+--------------------------------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+
|             state              | duration | cpu_user | cpu_sys  |  bk_in   |  bk_out  |  msg_s   |  msg_r   |  p_f_ma  |  p_f_mi  |  swaps   |
+--------------------------------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+
| starting                       | 0.000050 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| checking permissions           | 0.000006 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| Opening tables                 | 0.000019 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| init                           | 0.000018 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| System lock                    | 0.000005 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| optimizing                     | 0.000004 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| statistics                     | 0.000007 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| preparing                      | 0.000008 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| Sorting result                 | 0.000004 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| executing                      | 0.001041 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |      286 |        0 |
| Sending data                   | 0.000018 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| Creating sort index            | 0.000935 | 0.000000 | 0.001000 |        0 |        0 |        0 |        0 |        0 |       18 |        0 |
| end                            | 0.000008 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| query end                      | 0.000004 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| closing tables                 | 0.000003 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| removing tmp table             | 0.000092 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| closing tables                 | 0.000008 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| freeing items                  | 0.000026 | 0.000000 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
| cleaning up                    | 0.000027 | 0.000999 | 0.000000 |        0 |        0 |        0 |        0 |        0 |        0 |        0 |
+--------------------------------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+
bk_in:   block_ops_in
bk_out:  block_ops_out
msg_s:   message sent
msg_r:   message received
p_f_ma:  page_faults_major
p_f_mi:  page_faults_minor

===== SQL PROFILING(SUMMARY)=====
+-------------------------------------+-----------------+------------+-------+-----------------+
|                state                |     total_r     |   pct_r    | calls |      r/call     |
+-------------------------------------+-----------------+------------+-------+-----------------+
| executing                           |        0.001041 |      45.60 |     1 |    0.0010410000 |
| Creating sort index                 |        0.000935 |      40.95 |     1 |    0.0009350000 |
| removing tmp table                  |        0.000092 |       4.03 |     1 |    0.0000920000 |
| starting                            |        0.000050 |       2.19 |     1 |    0.0000500000 |
| cleaning up                         |        0.000027 |       1.18 |     1 |    0.0000270000 |
| freeing items                       |        0.000026 |       1.14 |     1 |    0.0000260000 |
| Opening tables                      |        0.000019 |       0.83 |     1 |    0.0000190000 |
| init                                |        0.000018 |       0.79 |     1 |    0.0000180000 |
| Sending data                        |        0.000018 |       0.79 |     1 |    0.0000180000 |
| closing tables                      |        0.000011 |       0.48 |     2 |    0.0000055000 |
| end                                 |        0.000008 |       0.35 |     1 |    0.0000080000 |
| preparing                           |        0.000008 |       0.35 |     1 |    0.0000080000 |
| statistics                          |        0.000007 |       0.31 |     1 |    0.0000070000 |
| checking permissions                |        0.000006 |       0.26 |     1 |    0.0000060000 |
| System lock                         |        0.000005 |       0.22 |     1 |    0.0000050000 |
| Sorting result                      |        0.000004 |       0.18 |     1 |    0.0000040000 |
| optimizing                          |        0.000004 |       0.18 |     1 |    0.0000040000 |
| query end                           |        0.000004 |       0.18 |     1 |    0.0000040000 |
+-------------------------------------+-----------------+------------+-------+-----------------+

===== EXECUTE TIME =====
0 day 0 hour 1 minute 17 second 801 microsecond 
```
