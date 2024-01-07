Realiza los siguientes ejercicios de localización de datos en Linux: 

a) Analiza y haz un resumen de cómo se están guardando los logs en tu sistema e indica de dónde saca dicha configuración. 

By default the logs are stored  at the /var/log directory, which is specified in the /etc/rsyslog.d/\*.conf . In the config file you can specify for each event (consisting of installation/facility and priority) which you want to log, under which directory it should be stored. Furthermore you can choose which installation or facility, you want to look under an according priority, therefore a standarized language is offered by Linux.
```
auth,authpriv.*			/var/log/auth.log
```

To find the directory including the config files, it needs to be included under /etc/rsyslog.conf, like in the following example:
```
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:/etc$ cat /etc/rsyslog.conf 
# Include all config files in /etc/rsyslog.d/
#
$IncludeConfig /etc/rsyslog.d/*.conf
```

b) Indica cual es la forma de rotado que esta programada paracada uno ellos y cada cuanto se hace
To indicate the form of rotation of our config files, we need to take a look at the /etc/logrotate.d/rsyslog file, which specifies the according configuration of rotation for our rsyslog logs.
```
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:/etc$ cat /etc/logrotate.d/rsyslog 
/var/log/syslog
/var/log/mail.info
/var/log/mail.warn
/var/log/mail.err
/var/log/mail.log
/var/log/daemon.log
/var/log/kern.log
/var/log/auth.log
/var/log/user.log
/var/log/lpr.log
/var/log/cron.log
/var/log/debug
/var/log/messages
{
	rotate 4
	weekly
	missingok
	notifempty
	compress
	delaycompress
	sharedscripts
	postrotate
		/usr/lib/rsyslog/rsyslog-rotate
	endscript
}
```
c) Configura un fichero de log nuevo donde se registren solo los registros de prioridad entre notice y err de cron y de auth
```
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:/etc/rsyslog.d$ cat log_cron_auth.conf 
auth.notice;auth.!crit                  /var/log/learninglogs/auth.log
cron.notice;cron.!crit                  /var/log/learninglogs/cron.log
```
d) Obtén por pantalla las fechas y horas de los últimos 5 reinicios de la máquina. Intenta mostrar sólo por pantalla la fecha y hora. 
```
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:~$ journalctl --list-boots | tail -n 5 | grep -E -o '[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2} CEST—'
2023-10-02 13:22:49 CEST—
2023-10-02 15:00:31 CEST—
2023-10-03 15:39:45 CEST—
2023-10-03 17:12:27 CEST—
2023-10-04 09:06:11 CEST—
```
e) Muestra por pantalla los registros del diario de hace 30 días que corresponden con el cron. 
```
journalctl --since "30 days ago" | grep cron
```

f) Obtén por pantalla en formato JSON los registros de hoy entre las 8 y las 12 de la mañana del servidor mysql junto con los registros del kernel y que correspondan con una prioridad de tipo “info”

```
jmxnzo@jmxnzo-ThinkPad-T470-W10DG:/etc/cron.d$ journalctl --since "$(date '+%Y-%m-%d 08:00:00')" --until "$(date '+%Y-%m-%d 12:00:00')" -o json -p info | grep mysql
```