# Not Too Nice (NTN)
Is a linux tool that adds alias files for other commands to make them run in very low priority by default.
It adds this prefix: `chrt -i 0 ionice -c 3` to the command, which means that the command will
run on IDLE scheduler policy and on IDLE IO priority. The idle here doesn't mean that the command
is idle (not running), it means that the task will be scheduled in IDLE policy which is in the least
priority among others.

# Why
Because this solution adds 0 overhead to auto down-prioritize tasks while keeping the
arguments call the same plus without changing/touching any of the others files.

## Adding Example
`sudo ntn -a balooctl`

This will add `/usr/local/bin/balooctl` file with the following content:
```
#!/usr/bin/env bash
chrt -i 0 ionice -c 3 /usr/bin/balooctl "$@"
```

If you, or the system runs balooctl. Then it will be run with IDLE sched/io policies.

-a will also try to update the currently running task by its pid automatically.

## Remove Example
`sudo ntn -r balooctl`

## Watch tasks policies
`ntn -w`

TS: means normal policy (i.e. CFS)
You will see IDLE instead if the task you're watching is added via ntn


## List Added Tasks
`ntn -l`

## Auto Add preconfigured commands
`sudo ntn -u`

This is like an update, it will go through this [list](https://github.com/hamadmarri/ntn/blob/04c212a7a8a953e2ad81c9805f829363a19d3c6c/ntn#L4) and it adds the
command if the command exists.

Thanks
