# Log Analysis

Are you a security practitioner who needs to analyze log files on the job? A student wondering how log analysis is done? A programmer who wants to incorporate logfiles into the development process? Or, are you a security hobbyist looking to get into some forensics research? If so, this guide is for you!

Today, we are going to analyze Linux logs using some of the most common command-line tools!

### A Quick Guide To Linux Logs

Linux logs are an important tool for developers, network admins, and security professionals alike. They document a timeline of events that occur on a Linux system, including operating system events, application activity, and user actions.

These logs are stored in the `/var/log` directory. You can view the contents of this directory by running the command:

```bash
ls /var/log
Bash
```

Here, you’ll see filenames like `syslog`, `messages`, `auth.log`, `secure`, `cron`, `kern.log`, `apache2`, `mysql` and more.

The `syslog` or `messages` file contains general messages that log activities across the entire system. `auth.log` or `secure` stores authentication logs, including all successful and failed login attempts.

`cron` stores cron job-related messages, such as cron initiations and failures. `kern` is for kernel logs and related warning messages.

User applications often store their logs in this directory, as well. Notable examples are Apache and MySQL. They store their application logs in the `apache2` and `mysql` files, respectively. Some applications can write directly into the `syslog` file as well.

#### The Linux Log Format

The format of these logs is customizable. For example, you can log additional information by specifying extra fields in log configuration files. By default, however, log file entries are in a format close to this:

```
Timestamp, Hostname, Application name, Priority, Message
```

While `Hostname` is the server in the system where the message originated, `Application name` refers to the name of the application that generated the event, and `Priority` denotes how urgent or severe an event is. For example, the below entry logs a failed login attempt with the username `root`.

```
May 11 20:04:33 main_server sshd[41458] Failed password for root from 192.168.0.3 port 22 ssh
```

### Command Line Tools for Log Analysis

With log files securely storing all the information, how do we extract security intel from them efficiently?

There are a lot of advanced log analysis tools out there, but today we’re going to talk about the most basic option: using command-line tools. In particular, we are going to talk about using the most common Linux utilities to analyze Linux logs.

#### Grep for Flexible Search

Grep is a search tool that should be in every security professional’s arsenal. You can search inside documents based on plain text or regex patterns.

For log analysis purposes, regex can reduce false positives as it provides a more accurate search. The `-E` option is used to specify a regex pattern to search for. For example, this command searches for lines in the log file that contains IP addresses within the `192.168.25.0/24` subnet.

```bash
grep -E "192\.168\.0\.\d{1,3}" /var/log/syslog
```

You can also utilize the powerful inverse search to rule out certain lines:

```bash
grep -v -E "192\.168\.0\.\d{1,3}" /var/log/syslog
```

This command searches for all lines that **do not** contain IP addresses within the `192.168.25.0/24` subnet. You can probably imagine how functionalities like this can be useful: they allow you to rule out safe IP addresses and application names while filtering for certain criteria like timestamps, IP addresses, and hostnames that indicate suspicious behavior.

Another very useful feature built into grep is "surround search." It allows you to display the lines before and after the matching line. For example, your logs might document an event extensively across multiple lines. In this case, you’d want to read the context beyond the line that contains the IP address.

```bash
grep -B 2 -A 2 -E "192\.168\.0\.\d{1,3}" /var/log/syslog
```

This command will display two lines before and after the line that contains the target IP addresses.

```
grep -E "([0-9]{1,3}[\.]){3}[0-9]{1,3}" auth.log
```

#### Awk’s Powerful Parsing

Awk is a powerful text-processing language wrapped into a command-line utility. You can use it to filter and parse log files efficiently. It's an extremely powerful utility with lots of different options. To see the full list of possibilities, run `man awk` to view the documentation.

For example, take a look at this line. Suppose that this is the format of a log file and you want to extract all the usernames that have had a failed password attempt.

```
May 11 20:04:33 main_server sshd[41458] Failed password for root from 192.168.0.3 port 22 ssh
```

To extract the usernames, you can run:

```
awk "/.*Failed password.*/ { print $8 }" /var/log/auth.log
```

In the above command, `/.*Failed password.*/` finds the lines that contain the string "Failed password", and `{ print $8 }` tells awk to print out the eighth field in the line (default delimiter is whitespace). So it will print out:

```
root
```

#### Sed for Streamlined Editing

Sed stands for "stream editor". It reads the input file and modifies the input as specified by a list of commands. Again, sed is an extremely powerful utility with lots of different options. To see the full list of possibilities, run `man sed` to see the tool manual.

Here’s an example of how to use it. The "s" symbol in sed stands for search and "g" stands for copy and append.

```
sed "s/May 11//g" /var/log/auth.log > newfile.txt
```

This command will search for lines that contain the string "May 11" and append all the contents of those lines into a file called `newfile.txt`. Pretty useful for quickly finding and processing logs from that day!

#### Tail to See the Tail End

The tail command displays the last few lines of a file. Its default behavior is to output the last ten lines of a file to standard output. This is useful if you want to quickly inspect the most recent entries of a particular log file.

```bash
tail /var/log/auth.log
```

Using tail with the `-f` flag instructs it not to stop at the end of the file, and wait for additional data to be appended to the input. This is useful when you want to monitor a particular log file in real-time.

```bash
tail -f /var/log/auth.log
```

#### Cut to Parse Delimited Files

cut is a command-line utility that cuts and parses files according to a delimiter, which is perfect for analyzing delimited log files (the default delimiter is whitespace).

```bash
who | cut -c 1-16
```

The above command parses the output of the `who` command to show the names of the users currently logged into the system.

#### wc to Count Events

The wc utility displays the number of lines, words, and bytes contained in each input file. This can be useful to count the occurrence of events in a log file.

For example, you can pipe the output of some of the above commands into `wc`. (`wc -l` counts the number of lines in a file.) This command counts the times the IP address 192.168.0.3 was logged:

```bash
grep -E "192\.168\.0\.3" /var/log/syslog | wc -l
```

#### Python, Bash, and Other Scripting Languages

If all else fails, you can always fall back to quickly writing a script in your favorite scripting language to perform the log analysis for you!

### Analyzing Honeypot Logs

Armed with some log analysis skills, let’s dig into some logs!

A honeypot is a system placed on a network to lure attackers to connect to it. By analyzing the logs of a honeypot, you can gain insight into who is targeting your system and how they are attacking it.

#### Finding Failed SSH Logins

One very useful piece of information is failed SSH logins in `auth.log`. Here we can see that on May 11th, an attacker located at `172.217.8.196` attempted to log in as root through SSH on port 22.

```
May 11 20:04:33 main_server sshd[41458] Failed password for root from 172.217.8.196 port 22 ssh
```

Using grep, you can list all IPs that have failed login attempts and analyze their geographic location.

```bash
grep "Failed password" /var/log/auth.log | awk ‘{print $11}’ >> ips.txt
```

Is there a pattern? Are the failed login attempts clustering somewhere? You can also classify failed login attempts by applications, ports, and usernames used to gain insight into who your attackers are and where they are located.

#### Recording Sudo Attempts

The sudo command also creates log entries in `auth.log`. Any failed or successful commands executed via sudo are logged.

```
May 11 20:04:33 localhost sudo: user : TTY=pts/3 ; PWD=/home/user ; USER=root ; COMMAND=/bin/bash
```

We can, for example, look at the most commonly executed commands using sudo:

```
grep "sudo" /var/log/auth.log | awk ‘{print $10}’ >> sudo_commands.txt
```

We can also look at which usernames are used for these attempted sudo commands.

This type of analysis can help detect security breaches before they escalate. By analyzing who your attackers are, what they are after, and which methods they are using, you can predict what they will do next.
