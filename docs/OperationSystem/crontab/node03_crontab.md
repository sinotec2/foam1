---
tags: crontab Linux
---

# node03_crontab

```bash
#find and run jobs from mac (node3.cmd)
#*/1 * * * * /home/kuang/find_run.sh 3

#scan for all possible cmd's from mac
#*/1 * * * * if ls /home/kuang/mac/kuang/master_MailBox/*.cmd >& /dev/null;then mv /home/kuang/mac/kuang/master_MailBox/*.cmd /home/kuang;fi

#put the results to mac
#*/1 * * * * tail /home/kuang/node*.[hl]*>&/home/kuang/mac/kuang/master_MailBox/nodes.log

#confirm the IMac is connected
#*/5 * * * * if ! [ -e /home/kuang/mac/do_not_delete ];then /usr/bin/fusermount -u /home/kuang/mac;/usr/bin/sshfs kuang@IMacKuang:/Users ~/mac -o nonempty -o password_stdin < ~/bin/PW >& /dev/null 2>&1;fi

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
#10 8 * * * for r in 45 09 03;do cd /nas1/Data/javascripts/D3js/earthFcst$r/public/data/weather/current;./cmaq_json.py;done

# NCAR WACCM forecast download
10 18 * * * /nas1/WACCM/dl_tdy.cs
```

# 執行之說明列表

行數|路徑腳本(主要動作)|頻率|active|說明|參見
:-:|:-:|:-:|:-|-|-
2|/home/kuang/find_run.sh|每分鐘執行|no|~上之指令在node03上執行|-
5|(mv)|每分鐘執行|no|尋找mac提供指令移到~|
8|(tail)|每分鐘執行|no|將執行結果(.his/.log)檔之檔末文字傳回mac|
11|(sshfs)|每5分鐘執行|no|將mac目錄建為網路磁碟機|
14|/nas1/Data/cwb/WRF_3Km/get_M-A0064.cs|每天執行|yes|下載CWBWRF數據並進行分析|
17|/nas1/Data/javascripts/D3js/earthCWB<br>/public/data/weather/current/earth_cwbwrf.cs|每6小時執行|yes|下載CWBWRF數據並處理成earthMap型態|
21|/nas2/cmaqruns/2019force/GT.cs|每分鐘執行|no|將CMAQ執行結果po到github|-
22|(rd_today.py)|每天執行|yes|執行前一天電場運轉數據之綜整|[本土化CALPUFF濃度預報系統之實現][1]

- 引用：[[unix環境中的自動排程cron]]

[1]: <https://sinotec2.github.io/Focus-on-Air-Quality/TrajModels/CALPUFF/Forecast/> "本土化CALPUFF濃度預報系統之實現"