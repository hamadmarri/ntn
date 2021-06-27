# Not Too Nice (NTN)
Is a tool that adds alias file for other commands to make them run in very low priority by default.
It adds this prefix: `chrt -i 0 ionice -c 3` to the command, which means that a the command will
run on IDLE scheduler policy and on IDLE IO priority. The idle here doesn't mean that the command
is idle (not running), it means that the task will be scheduled in IDLE policy which is in the least
priority among others.

## Adding Example
sudo ntn -a balooctl

This will add `/usr/local/bin/balooctl` file with the following content:
```
#!/usr/bin/env bash
chrt -i 0 ionice -c 3 /usr/bin/balooctl $@
```

If you, or the system runs balooctl. Then it will be run with IDLE sched/io policies.


## Remove Example
sudo ntn -r balooctl

## Watch tasks policies
ntn -w

TS: means normal policy (i.e. CFS)
You will see IDLE instead if the task you're watching is added via ntn


## TODO
Make a default list of commands that are heavy on io like make, gcc, cmake, ...
Those commands can be auto added with for example
ntn -u <- i.e. update

Thanks
