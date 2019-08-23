# Log file archiving

Darwin doesn't include `logrotate` it has `newsyslog`. Like all the services on Darwin they are run by `launchd`. `newsyslog` is configured in `/etc/newsyslog.d/`.

```
# logfilename                   [owner:group]   mode    count   size    when    flags [/pid_file] [sig_num]
/Users/andrew/logs/*.log                        644     5       1024    *       GN
```

The comment shows the optional fields in square brackets.  If specifying the owner:group option the colon is mandatory.

| Field        | Usage |
| :-----       | :----- |
| logfile_name | Pattern for log files to be managed by this configuration. |
| owner:group  | Optional owner and group for archived files.  Colon is mandatory. |
| mode         | File permission mode. |
| count        | Maximum number of archived files.  Does not include active log file. |
| size         | Size at which to archive the log file.  Size is in kb.  * indicates ignore file size. |
| when         | * indicates archive based on file size only.  The man pages describe how to define an interval, specific time, etc. |
| flags        | Optional.  Define special processing.  <ul><li>G indicates logfile name is a pattern so newsyslog will archive all matching files.</li><li>N indicates no process needs to be notified when a file is archived.</li></ul>|
| pid_file     | Optional. Location of pid for process to be notified when a file is archived.|
| sig_num      | Optional.  Number of signal to send to process identified in pid_file.|


See the man pages man `newsyslog` and man `newslog.conf` for details.

The `newsyslog` job is defined as a system `launchd` in `/System/Library/LaunchDaemons/com.apple.newsyslog.plist`