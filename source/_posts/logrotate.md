title: logrotate
date: 2015-09-16 10:10:03
tags:
---

### logrotate 配置
logrotate使用简单，直接在/etc/logrotate.d/ 下添加一个配置文件即可，以apache httpd 为例：
```shell
	/var/log/httpd/*log {
		 missingok
		 notifempty
		 sharedscripts
		 delaycompress
		 postrotate
			  /bin/systemctl reload httpd.service > /dev/null 2>/dev/null || true
		 endscript
	}
```

logrotate的配置很简答，但需注意：

1. logrotate默认是一天执行一次，在/etc/cron.daily/logrotate 有其执行脚本，作为定时任务执行。可以通过执行logrotate /etc/logrotate.conf 来手动执行rotate，注意，-f 是--force的意思，而不是--file的意思，使用-f 会强制执行生成新的rotate.
 *Normally, logrotate is run as a daily cron job. It will not modify a log multiple times in one day unless the criterion for that log is based on the log's size and logrotate is being run multiple times each day, or unless the -f or --force option is used.*

2. 另外，logrotate 本身没有daemon 在运行，其执行必须要等到某个地方调用logrotate才会跑，正常情况下只有手动调用logrotate命令或者到/etc/cron.daily下的定时任务执行的时候才会执行。

### weekly、daily、size、minsize 的关系
 - 若未使用weekly、daily等时间中的任何一个，由于/etc/logrotate.conf中定义了weekly，因此默认会采用weekly，后面的配置会覆盖前面的配置
 -  daily、weekly是通过生成的上个rotate文件的创建时间来确定下一个打包时间的，若当前进行rotate的时间与上一次打包的时间间隔超过了设置的时间间隔(daily)，则会进行rotate，否则不会。
 - size：若采用了size，会优先根据size的大小来进行rotate，只要当前日志文件的size超过了设定的size，则会进行打包，而不管是否达到了daily所设定的时间间隔。
 - minsize： manual手册是这么解释的：
	**minsize size**
	*Log files are rotated when they grow bigger than size bytes, but not before the additionally specified time interval (daily, weekly, monthly, or yearly). The related size option is similar except that it is mutually exclusive with the time interval options, and it causes log files to be rotated without regard for the last rotation time. When minsize is used, both the size and timestamp of a log file are considered.*

    意思是，minsize既考虑日志文件的大小，又考虑时间间隔，必须等两者均满足条件时才会执行。
    与size不同的地方就在于此，size是只要大小超过限制，则只要logrotate被调用便会执行，而minsize必须要大小超过限制且距离上次打包时间超过间隔时间才会打包。
