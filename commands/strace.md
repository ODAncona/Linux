# strace

## Description

{% embed url="https://blog.packagecloud.io/eng/2015/11/15/strace-cheat-sheet/" %}

Strace is an essential tool for debugging anything on a Linux system. You should use `strace` anytime you want to understand what a process is doing. Reaching for `strace` as the first line of defense when debugging anything is a great way to quickly gather context about a problem

## Syntaxe

### options

| Options                                        | Description                                                                                                                                                     |
| ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><p><code>-f</code> </p>                 | <p></p><p>Follow threads and child processes that are created. Useful option because many programs will spawn additional processes or threads to do work.</p>   |
| `-T`                                           | <p></p><p>Print time spent in system call. This can be useful if you are trying to determine if a particular system call is taking a lot of time to return.</p> |
| `-t`                                           | <p></p><p>Print the time of day at the start of each line.</p>                                                                                                  |
| <p></p><p><code>s[size]</code></p>             | Print \[size] characters per string displayed. This is useful if you are trying to trace what a program is writing to a file descriptor.                        |
| `-c`                                           | <p></p><p>Print a histogram of the number of system calls and the time spent at the termination of strace</p>                                                   |
| <p></p><p><code>-e trace=open,close</code></p> | <p></p><p>Trace only the <code>open</code> and <code>close</code> system calls.</p>                                                                             |

## Utilisation
