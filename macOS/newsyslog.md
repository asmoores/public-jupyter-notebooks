# Log files

Darwin doesn't include `logrotate` it has `newsyslog`. Like all the services on Darwin they are run by `launchd`. `newsyslog` is configured in `/etc/newsyslog.d/`.

```
# logfilename                   [owner:group]   mode    count   size    when    flags [/pid_file] [sig_num]
/Users/andrew/logs/*.log                        644     5       1024    *       G
```

See the man pages man `newsyslog` and man `newslog.conf` for details.

The `newsyslog` job is defined as a system `launchd` in `/System/Library/LaunchDaemons/com.apple.newsyslog.plist`