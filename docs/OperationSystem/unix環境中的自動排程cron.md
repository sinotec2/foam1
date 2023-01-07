---
layout: default
title: unix環境中的自動排程cron
parent:   Operation System
grand_parent: Utilities
last_modified_date: 2022-11-11 09:01:53
tags: Linux crontab
---

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

---

# 自動排程程式cron

## cron.d的執行
### cron.d與libc更新
- cron.d與libc及gcc版本有關，如果更新相關程式庫，需reboot以符合版本，否則出現下面錯誤。

```

...
Nov  8 08:35:01 DEVP CROND[53784]: (kuang) CMD (if ! [ -e /home/kuang/mac/do_not_delete ];then /usr/bin/fusermount -u /home/kuang/mac;/usr/bin/sshfs kuang@IMacKuang:/Users ~/mac -o password_stdin < ~/bin/PW;fi)
Nov  8 08:35:01 DEVP CROND[53785]: (kuang) CMD (if ! [ -e /nas3/do_not_delete ];then /usr/bin/fusermount -u /nas3;/usr/bin/sshfs kuang@dev2:/u01 /nas3 -o password_stdin < ~/bin/PW2;fi)
Nov  8 08:36:01 DEVP crond[55611]: (kuang) PAM ERROR (Module is unknown)
Nov  8 08:36:01 DEVP crond[55611]: (kuang) FAILED to authorize user with PAM (Module is unknown)
Nov  8 08:36:01 DEVP crond[55610]: (kuang) PAM ERROR (Module is unknown)
Nov  8 08:36:01 DEVP crond[55610]: (kuang) FAILED to authorize user with PAM (Module is unknown)
Nov  8 08:37:01 DEVP crond[55625]: (kuang) PAM ERROR (Module is unknown)
...
```
- 11/8/8:35 原還可執行crontab的內容，8:36旋即發生錯誤
- [網友](https://www.twblogs.net/a/5c03dc2bbd9eee728c16acb6)建議：

```
root@sasha-lab ~]# vim /etc/pam.d/crond
#
# The PAM configuration file for the cron daemon
#
#
# No PAM authentication called, auth modules not needed
account    required   pam_access.so
account    include    password-auth
#session    required   pam_loginuid.so
session    sufficient   pam_loginuid.so
session    include    password-auth
auth       include    password-auth
說明：session    required   pam_loginuid.so 修改爲：session    sufficient   pam_loginuid.so
```
- 經實證並無效果。reboot之後就好了。

## crontab的設定

- G. T. Wang, **Linux 設定 crontab 例行性工作排程教學與範例**,[G. T. Wang](https://blog.gtwang.org/linux/linux-crontab-cron-job-tutorial-and-examples/), 2019/06/28
[emoji]: <https://www.webfx.com/tools/emoji-cheat-sheet/> "emoji"

## crontab的應用

### master

- act as user
- 執行批之說明次詳見[[master_crontab]](包括未開啟項目)

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

#every 5 min ($min%5==0)
   *  *  *  *  * kuang /home/backup/data/ETC/JiaYiVD/getJiayiVD_cron.cs

# every day from NCEP
0   0  *  *  * kuang /home/backup/data/NOAA/NCEP/fusv2.cs
0  12  *  *  * kuang /home/backup/data/NOAA/NCEP/SST/get_noaa.cs
```

- act as root
- 執行批之說明次詳見[[master_crontabRoot]](包括未開啟項目)

```bash
  0  0  *  *  *  /home/cpuff/UNRESPForecastingSystem/Run.sh -c > 
 15 * * * * cd /home/sespub/power;LC_ALL='zh_TW.BIG5' ./rd_today.py >& rd_today.out
```

### node03

- act as user
- 執行批之說明次詳見[[node03_crontab]](包括未開啟項目)

```bash
#               wget the daily WRF forecast from cwb
10 20  *  *  *   /nas1/Data/cwb/WRF_3Km/get_M-A0064.cs &> /nas1/Data/cwb/WRF_3Km/get_M-A0064.out 2>&1

# earth CWB_WRF
55 2,8,14,20 * * * /nas1/Data/javascripts/D3js/earthCWB/public/data/weather/current/earth_cwbwrf.cs

# earth GFS
0 2,8,14,20 * * * /nas1/Data/javascripts/D3js/earth/public/data/weather/current/earth_gfs.cs
0 * * * * /nas1/Data/javascripts/D3js/earth/public/data/weather/current/lnk_curr.cs
0 * * * * /nas1/Data/javascripts/D3js/earthFcst45/public/data/weather/current/lnk_curr.cs

# CAMS ozone
0 8,20 * * * /nas1/ecmwf/CAMS/CAMS_global_atmospheric_composition_forecasts/2022/get_grb2json.cs
0 0 * * * /nas1/ecmwf/CAMS/CAMS_global_atmospheric_composition_forecasts/2022/get_all.cs

# NCAR WACCM forecast download
10 18 * * * /nas1/WACCM/dl_tdy.cs
```

### devp

- act as user
- 執行批之說明次詳見[[devp_crontab]](包括未開啟項目)

```bash
  0  0  *  *  *  /home/cpuff/UNRESPForecastingSystem/Run.sh -c > /home/cpuff/UNRESPForecastingSystem/Run.out
#*/1  *  *  *  *  /home/kuang/find_run.sh m

#put the results to mac
#*/1 * * * * tail /home/kuang/node*.[hl]*>&/home/kuang/mac/kuang/master_MailBox/nodes.log

#scan for all possible cmd's from mac
#*/1 * * * * if ls /home/kuang/mac/kuang/master_MailBox/*.cmd >& /dev/null;then mv /home/kuang/mac/kuang/master_MailBox/*.cmd /home/kuang;fi

#confirm the IMac is connected
#*/1 * * * * if ! [ -e /home/kuang/mac/do_not_delete ];then fusermount -u /home/kuang/mac;/usr/bin/sshfs kuang@IMacKuang:/Users ~/mac -o password_stdin < ~/bin/PW;fi

#confirm the dev2 is connected
#*/1 * * * * if ! [ -e /nas3/do_not_delete ];then /usr/bin/fusermount -u /nas3;/usr/bin/sshfs kuang@dev2:/u01 /nas3 -o password_stdin < ~/bin/PW2;fi


#import the temp.logs from centos8 and put to gmet
#*/6 * * * * /usr/bin/sshpass -f ~/.ssh/.pw /usr/bin/scp -q centos8:/tmp/cpu.log /tmp  >& /tmp/getCPUtemp.out;/usr/bin/sshpass -f ~/.ssh/.pw /usr/bin/scp -q centos8:/tmp/ambient.log /tmp  >> /tmp/getCPUtemp.out

#export the cmaq LOG file to github every minunte
#*/1 * * * * /nas2/cmaqruns/2019force/GT.cs >& ~/log.out
 15 * * * * cd /home/sespub/power;LC_ALL='zh_TW.BIG5' ./rd_today.py >& rd_today.out
```

### dev2

- act as user
- 執行批之說明次詳見[[dev2_crontab]](包括未開啟項目)

```bash
#confirm the IMac is connected
#*/1 * * * * if ! [ -e /home/kuang/mac/do_not_delete ];then /usr/bin/fusermount -u /home/kuang/mac;/usr/bin/sshfs kuang@IMacKuang:/Users ~/mac -o password_stdin < ~/bin/PW;fi

#WRF forecasting from gfs and CWBWRF results
0 3 * * * /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_dev2.cs >& /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_dev2.out
```

### macOS

- act as user
- 執行批之說明次詳見[[mac_crontab#as User]](包括未開啟項目)

```bash
#WRF forecasting from gfs and CWBWRF results
0 3 * * * /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_dev2.cs >& /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_dev2.out
```

- act as root
- 執行批之說明次詳見[[mac_crontab#as root]](包括未開啟項目)

```bash
#remove the mmif_* 2 days ago
0 0  *  *  * cd /private/tmp;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep mmif_|grep $dd|/opt/local/bin/awkk 9);do rm -fr $i;done
#remove the *csv* 2 days ago
0 0  *  *  * cd /Library/WebServer/Documents/trj_results;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep csv|grep $dd|/opt/local/bin/awkk 9);do echo $i;rm -fr $i;done >> /var/log/apache2/access_log
0 0  *  *  * cd /Library/WebServer/Documents/isc_results;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep _|grep $dd|/opt/local/bin/awkk 9);do echo $i;rm -fr $i;done >> /var/log/apache2/access_log
0 0  *  *  * cd /tmp/isc;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep $dd|/opt/local/bin/awkk 9);do echo $i;rm -fr $i;done >> /var/log/apache2/access_log

##stop and start of apache
0  7 *  *  1,2,3,4,5 /usr/local/opt/httpd/bin/httpd -k start


## trajectories update
0  4 *  *  * /Library/WebServer/Documents/trj_results/daily_traj.cs >& /Library/WebServer/Documents/trj_results/daily_traj.out


#check the acc # >500/hr and block them
0 *  *  *  * /Users/kuang/bin/BlockIP/ana_accHr.py >& /Users/kuang/bin/BlockIP/ana_accHr.out
```