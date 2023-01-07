---
tags: crontab Linux
---

# dev2_crontab

```bash
#confirm the IMac is connected
#*/1 * * * * if ! [ -e /home/kuang/mac/do_not_delete ];then /usr/bin/fusermount -u /home/kuang/mac;/usr/bin/sshfs kuang@IMacKuang:/Users ~/mac -o password_stdin < ~/bin/PW;fi

#WRF forecasting from gfs and CWBWRF results
0 3 * * * /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_dev2.cs >& /nas1/backup/data/NOAA/NCEP/GFS/YYYY/fcst_dev2.out
```

- 引用：[[unix環境中的自動排程cron]]