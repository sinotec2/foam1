---
tags: crontab Linux
---

# master_crontab

```bash
$ cat /etc/crontab
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
# every day
  0  8  *  *  * kuang /home/kuang/bin/bash_his.py
  0  8  *  *  * kuang /home/backup/data/pm25.jp_yosoku_parts_casu/pm25.cs
  0  8  *  *  * kuang /home/backup/data/www.jma.go.jp/jma_cron.cs
  0  8  *  *  * kuang /home/backup/data/taqm.epa.gov.tw/dust/taqm.dust_cron.cs
  0 12  *  *  * kuang /home/backup/data/cwb/e-service/get_cwb.sh >& /home/backup/data/cwb/e-service/get_cwb.out
#  0  8  *  *  * kuang /home/sespub/watch_PID.cs
#  0 12  *  *  * kuang /home/sespub/watch_PID.cs
#  0 12  *  *  * openkm rsync -a /home/openkm/tomcat_sino4 /nas1/backup
#every hour
#  0  *  *  *  * kuang rsync -a /home/kuang/bin /autofs/sino4/kuang
#every 5 min ($min%5==0)
#  *  *  *  *  * kuang /home/backup/data/ETC/DirectoreGeneralOfHighways/getTHBvd.cs
#every 5 min ($min%5==0)
   *  *  *  *  * kuang /home/backup/data/ETC/JiaYiVD/getJiayiVD_cron.cs
#   *  *  *  *  * kuang /home/backup/data/ETC/KaoxiongVD/KaoxiongGetVD_cron.cs
#every 5 min ($min%5==0)
#   *  *  *  *  * kuang /home/backup/data/ETC/NewtaipeiVD/NewtpGetVD_cron.cs
#  0  *  *  *  * kuang /home/backup/data/ETC/TaichungVD/getTaichongVD_cron.cs
#   *  *  *  *  * kuang /home/backup/data/ETC/TainanVD/TainanGetVD_cron.cs
#every 5 min ($min%5==0)
#   *  *  *  *  * kuang /home/backup/data/ETC/TaipeiVD/TaipeiGetVD_cron.cs
#every 5 min ($min%5==0)
#   *  *  *  *  * kuang /home/backup/data/ETC/TaoyuanVD/TaoyuanGetVD.cs

# every day from NCEP
0   0  *  *  * kuang /home/backup/data/NOAA/NCEP/fusv2.cs
0  12  *  *  * kuang /home/backup/data/NOAA/NCEP/SST/get_noaa.cs
# backup the okmdb and ascync with master
# 0  0  *  *  * openkm /home/openkm/tomcat/mysql_okmdb/backup_okmdb.bsh
# 0  0  *  *  * openkm /home/openkm/tomcat/reset.sh >& /home/openkm/tomcat/reset.txt
# 5 12  *  *  * openkm /home/openkm/tomcat/reset.sh >& /home/openkm/tomcat/reset.txt
#  0  1  *  *  * openkm rsync -a /home/openkm/tomcat_sino4/* /autofs/sino4/openkm/tomcat
# daily du filesystem
#10  1  *  *  * openkm /home/openkm/tomcat/scripts/rd_openkm.log/rd_log.py >& /home/openkm/tomcat/scripts/rd_openkm.log/rd_log.rst
# read the okmdb content, analysis and report, which is read by pyforms
# 0  *  *  *  * openkm /home/openkm/tomcat/scripts/rd_okmdb/rd_okmdb.bsh>& /home/openkm/tomcat/scripts/rd_okmdb/rd_okmdb.rst
```

- 引用：[[unix環境中的自動排程cron]]
