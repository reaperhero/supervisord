# supervisord

## Supervisord daemon settings

`/etc/supervisor/supervisord.conf`

```
[inet_http_server]
port = :9001
;username=test1
;password=thepassword

[program-default]
environment=VAR1="value1",VAR2="value2"

[program:web]
directory = /Users/chenqiangjun/gitlab/hello-world
command = npm run serve
autostart = true
```

> 文件说明

- Following parameters configured in "supervisord" section:
```
- **logfile**. Where to put log of supervisord itself.
- **logfile_maxbytes**. Rotate log-file after it exceeds this length.
- **logfile_backups**. Number of rotated log-files to preserve.
- **loglevel**. Logging verbosity, can be trace, debug, info, warning, error, fatal and panic (according to documentation of module used for this feature). Defaults to info.
- **pidfile**. Full path to file containing process id of current supervisord instance.
- **minfds**. Reserve al least this amount of file descriptors on supervisord startup. (Rlimit nofiles).
- **minprocs**. Reserve at least this amount of processes resource on supervisord startup. (Rlimit noproc).
- **identifier**. Identifier of this supervisord instance. Required if there is more than one supervisord run on one machine in same namespace.
```
- Supervised program settings configured in [program:programName] section and include these options:
```
- **command**. Command to supervise. It can be given as full path to executable or can be calculated via PATH variable. Command line parameters also should be supplied in this string.
- **process_name**. the process name
- **numprocs**. number of process
- **numprocs_start**. ??
- **autostart**. Should be supervised command run on supervisord start? Defaults to **true**.
- **startsecs**. The total number of seconds which the program needs to stay running after a startup to consider the start successful (moving the process from the STARTING state to the RUNNING state). Set to 0 to indicate that the program needn’t stay running for any particular amount of time.
- **startretries**. The number of serial failure attempts that supervisord will allow when attempting to start the program before giving up and putting the process into an FATAL state. See Process States for explanation of the FATAL state.
- **autorestart**. Automatically re-run supervised command if it dies.
- **exitcodes**. The list of “expected” exit codes for this program used with autorestart. If the autorestart parameter is set to unexpected, and the process exits in any other way than as a result of a supervisor stop request, supervisord will restart the process if it exits with an exit code that is not defined in this list.
- **stopsignal**. Signal to send to command to gracefully stop it. If more than one stopsignal is configured, when stoping the program, the supervisor will send the signals to the program one by one with interval "stopwaitsecs". If the program does not exit after all the signals sent to the program, supervisord will kill the program.
- **stopwaitsecs**. Amount of time to wait before sending SIGKILL to supervised command to make it stop ungracefully.
- **stdout_logfile**. Where STDOUT of supervised command should be redirected. (Particular values described lower in this file).
- **stdout_logfile_maxbytes**. Log size after exceed which log will be rotated.
- **stdout_logfile_backups**. Number of rotated log-files to preserve.
- **redirect_stderr**. Should STDERR be redirected to STDOUT.
- **stderr_logfile**. Where STDERR of supervised command should be redirected. (Particular values described lower in this file).
- **stderr_logfile_maxbytes**. Log size after exceed which log will be rotated.
- **stderr_logfile_backups**. Number of rotated log-files to preserve.
- **environment**. List of VARIABLE=value to be passed to supervised program.
- **priority**. The relative priority of the program in the start and shutdown ordering
- **user**. Sudo to this USER or USER:GROUP right before exec supervised command.
- **directory**. Jump to this path and exec supervised command there.
- **stopasgroup**. Also stop this program when stopping group of programs where this program is listed.
- **killasgroup**. Also kill this program when stopping group of programs where this program is listed.
- **restartpause**. Wait (at least) this amount of seconds after stpping suprevised program before strt it again.
- **restart_when_binary_changed**. Boolean value (false or true) to control if the supervised command should be restarted when its executable binary changes. Defaults to false.
- **restart_cmd_when_binary_changed**. The command to restart the program if the program binary itself is changed.
- **restart_signal_when_binary_changed**. The signal sent to the program for restarting if the program binary is changed.
- **restart_directory_monitor**. Path to be monitored for restarting purpose.
- **restart_file_pattern**. If a file changes under restart_directory_monitor and filename matches this pattern, the supervised command will be restarted.
- **restart_cmd_when_file_changed**. The command to restart the program if any monitored files under **restart_directory_monitor** with pattern **restart_file_pattern** are changed.
- **restart_signal_when_file_changed**. The signal will be sent to the proram, such as Nginx, for restarting if any monitored files under **restart_directory_monitor** with pattern **restart_file_pattern** are changed.
- **depends_on**. Define supervised command start dependency. If program A depends on program B, C, the program B, C will be started before program A. Example:

```
- 使用帮助

start
```
supervisord -d
```

```shell
$ supervisord ctl status
$ supervisord ctl stop web
$ supervisord ctl stop all
$ supervisord ctl start web
$ supervisord ctl start all
$ supervisord ctl shutdown
$ supervisord ctl reload
```

