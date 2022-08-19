# tmuxssh

`tmuxssh` allows spawning SSH sessions within an existing tmux session, either one SSH session per pane (default), or one SSH session in its own tmux window if `-w` option is used. If the default *one-ssh-per-pane* mode is used, all the panes will be created within a new tmux window. This is usually useful if there's a set of ad-hoc commands that have to be executed on a small-ish number of hosts, although I have tested this in cases where number of hosts is >100, just make sure your terminal is big enough to fit all the panes.

Usage:
```
tmuxssh [OPTION]... [HOSTNAME]...

OPTIONS:
  -h           Display usage information
  -c command   Send command to all panes after connecting
  -r           Connect as root
  -s           Set pane synchronization to on (keys go to all panes)
  -u username  Connect as user <username>
  -w           Open each SSH session in a separate window
```
By far the most common usecase would be:
 ```
$ cat hosts.txt | xargs tmuxssh -rs
```
This would in turn create a new tmux window in the existing/active tmux session, create a new tmux window, and create a new pane in that new window for each SSH session (connected as root). After all sessions have been created, the panes would be tiled, and `tmux synchronize-panes` mode would be turned on, so all the keys pressed would go to all panes.
