---
tags: crontab Linux
---

# devp_crontab

```bash
#find and run jobs from mac (node3.cmd)
#*/1 * * * * /home/kuang/find_run.sh d

#scan for all possible cmd's from mac
#*/1 * * * * if ls /home/kuang/mac/kuang/master_MailBox/noded.cmd >& /dev/null;then mv /home/kuang/mac/kuang/master_MailBox/noded.cmd /home/kuang;fi

#confirm the IMac is connected
*/1 * * * * if ! [ -e /home/kuang/mac/do_not_delete ];then /usr/bin/fusermount -u /home/kuang/mac;/usr/bin/sshfs kuang@IMacKuang:/Users ~/mac -o password_stdin < ~/bin/PW;fi

#confirm the dev2 is connected
*/1 * * * * if ! [ -e /nas3/do_not_delete ];then /usr/bin/fusermount -u /nas3;/usr/bin/sshfs kuang@dev2:/u01 /nas3 -o password_stdin < ~/bin/PW2;fi



#export the cmaq LOG file to github every minunte
#*/1 * * * * /nas2/cmaqruns/GT.cs >& ~/log.out

#get the PMf.gif
0  8  *  *  * ~/GitHubRepos/sinotec2.github.io/Run.sh_DEVP  >& /nas1/cpuff/Run.out 2>&1

#WRF forecasting from gfs and CWBWRF results
10 0 * * * /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst.cs >& /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst.out
#38 18 * * * /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_cmaq.cs >& /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_cmaq.out
```

- 引用：[[unix環境中的自動排程cron]]