---
tags: Linux crontab
---

# master_crontabRoot

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
# 執行之說明列表

行數|路徑腳本(主要動作)|頻率|active|說明|參見
:-:|:-:|:-:|:-|-|-
1|/home/cpuff/UNRESPForecastingSystem/Run.sh|每天執行|yes|cpuff預報|[本土化CALPUFF濃度預報系統之實現][1]
2|/home/kuang/find_run.sh|每分鐘執行|no|~上之指令在master上執行|-
5|(tail)|每分鐘執行|no|將執行結果(.his/.log)檔之檔末文字傳回mac|
8|(mv)|每分鐘執行|no|尋找mac提供指令移到~|
11|(sshfs)|每分鐘執行|no|將mac目錄建為網路磁碟機|
14|(sshfs)|每分鐘執行|no|將nas3目錄建為網路磁碟機|
18|(sshpass)|每6分鐘執行|no|將centos8的CPU溫度數據取回|
21|/nas2/cmaqruns/2019force/GT.cs|每分鐘執行|no|將CMAQ執行結果po到github|-
22|(rd_today.py)|每天執行|yes|執行前一天電場運轉數據之綜整|[本土化CALPUFF濃度預報系統之實現][1]

- 引用[[unix環境中的自動排程cron]]

[1]: <https://sinotec2.github.io/Focus-on-Air-Quality/TrajModels/CALPUFF/Forecast/> "本土化CALPUFF濃度預報系統之實現"