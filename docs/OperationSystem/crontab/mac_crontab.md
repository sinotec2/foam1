---
tags: crontab Linux 
---

# mac_crontab

## as User

```bash
# get NCEP daily data
0 21  *  *  * /Users/WRF4.1/NCEP/fus.cs &> /Users/WRF4.1/NCEP/crontab_log.txt 2>&1
0 16  *  *  * /Users/WRF4.1/NCEP/SST/get_noaa.cs &> /Users/WRF4.1/NCEP/SST/get_noaa.log 2>&1

# get CWB daily data
0 0,6,12,18 * * * /Users/Data/cwb/WeatherMap/cwb.cs &> /dev/null 2>&1
#0 12  *  *  * /Users/Data/cwb/e-service/get_cwb.sh &> /Users/Data/cwb/e-service/get_cwb.out 2>&1

#get CWBWRF files
30 0  *  *  *  /Users/Data/cwb/WRF_3Km/get_M-A0064.cs &> /Users/Data/cwb/WRF_3Km/get_M-A0064.out 2>&1

#upload the cpuff results PMf.gif
#0  8  *  *  * /Users/cpuff/Run.sh  >& /Users/cpuff/Run.out 2>&1
0  20  1 */3 * /Users/kuang/GitHub/clean_his.cs >& /Users/kuang/GitHub/clean_his.out

#0  *  *  *  * if ! [ -e /miniUsers/kuang ];then /usr/local/bin/sshfs /miniUsers macmini:/Users;fi;ls /miniUsers  &>/dev/null 2>&1

# earth CWB_WRF
55 2,8,14,20 * * * /Users/Data/javascripts/D3js/earthCWB/public/data/weather/current/earth_cwbwrf.cs
0 * * * * /Users/Data/javascripts/D3js/earthCWB/public/data/weather/current/lnk_curr.cs
0 * * * * /Users/Data/javascripts/D3js/earth/public/data/weather/current/lnk_curr.cs
0 * * * * /Users/Data/javascripts/D3js/earthFcst45/public/data/weather/current/lnk_curr.cs

#Wiki.js server
0 6 * * * ~/MyPrograms/Wiki.js/node_server.cs
```

## as root

```bash
#remove the mmif_* 2 days ago
0 0  *  *  * cd /private/tmp;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep mmif_|grep $dd|/opt/local/bin/awkk 9);do rm -fr $i;done
#remove the *csv* 2 days ago
0 0  *  *  * cd /Library/WebServer/Documents/trj_results;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep csv|grep $dd|/opt/local/bin/awkk 9);do echo $i;rm -fr $i;done >> /var/log/apache2/access_log
0 0  *  *  * cd /Library/WebServer/Documents/isc_results;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep _|grep $dd|/opt/local/bin/awkk 9);do echo $i;rm -fr $i;done >> /var/log/apache2/access_log
0 0  *  *  * cd /tmp/isc;dd=$(/bin/date -j -v-2d +"%Y-%m-%d");for i in $(/usr/local/bin/gls -l --time-style=full-iso|grep $dd|/opt/local/bin/awkk 9);do echo $i;rm -fr $i;done >> /var/log/apache2/access_log

##stop and start of apache
#0 19 *  *  * /usr/local/opt/httpd/bin/httpd -k stop
0  7 *  *  1,2,3,4,5 /usr/local/opt/httpd/bin/httpd -k start
## old version
#0 19 *  *  1,2,3,4,5 /usr/sbin/apachectl stop
#0  7 *  *  1,2,3,4,5 /usr/sbin/apachectl start

#0 *  *  *  * cd /Library/WebServer/Documents/wrose_png;lastpng=echo $(ls -rth *png);mv $lastpng example.png

## trajectories update
0  4 *  *  * /Library/WebServer/Documents/trj_results/daily_traj.cs >& /Library/WebServer/Documents/trj_results/daily_traj.out
#0  4 *  *  * cp -r /Users/kuang/GitHub/sinotec2.github.io/traj/trj_results/?? /Library/WebServer/Documents/trj_results

#*/5 * * * * cat /Users/kuang/master_MailBox/noded.log /Users/kuang/master_MailBox/centos8.log > /Library/WebServer/Documents/noded.log

#check the acc # >500/hr and block them
0 *  *  *  * /Users/kuang/bin/BlockIP/ana_accHr.py >& /Users/kuang/bin/BlockIP/ana_accHr.out

#status of remote modeling system
#*/1 * * * * /Library/WebServer/Documents/status.cs
```

- 引用：[[unix環境中的自動排程cron]]