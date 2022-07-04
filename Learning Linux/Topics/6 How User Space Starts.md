# How User Space Starts
The user space starts in the following order:
	1. init
	2. Essential low-level services, such as udevd and syslogd.
	3. Network configs.
	4. Mid and high level services(cron, printing, etc.)
	5. Login prompts, GUI, and high level applications such as servers.
## Introduction to init
`init` is located with `/sbin` like other system processes.
There are other versions/names of init called:
+ System V
	Located on prior versions of RHEL 7.0 and Debian 8.
+ Upstart
	Present on versions of Ubuntu before 15.04.
+ `runit`
	Found on Android.
## Identifying Your Init
+ `systemd`
	If you have `/usr/lib/systemd` and `/etc/systemd`, then you have systemd.
+ Upstart
	If you have `/etc/init` with several `.conf` files.
+ System V
	`/etc/inittab` is the indicator for System V.
## systemd
`daemon`
	A daemon is a program that runs in the background that does not interact with the user.
	
Units, otherwise understood as goals for a system, are services it is to start. This could involve starting other units.

There are various types of units, and requirement specifications.
### Units and Unit Types
Each unit in a system is to be activated and is accompanied by a unit configuration file.

`Service Units` Controls service daemons on a UNIX system.
`Target Units` Controls other units by grouping them.
`Socket Units` Represent incoming network connection requests.
`Mount Units` Represent the attachment of file systems to the system.

You can distinguish between these unit files by look at the unit config's file extension.

### Booting and Unit Dependency Graphs
The unit dependency graph can be viewed with `systemd-analyze`. 

There is a default unit such as `default.target` which has grouped together other units to start.

### Finding system configuration
The system unit directory can be found at `/lib/systemd/system`, or `/usr/lib/systemd/system`

The configuration files can be found at `/etc/systemd/system`.

It is preferrable to use `/etc/systemd/system` and have the rest be managed by your system.

You can find the locations for services by using `systemctl -p UnitPath show`.

##### Unit Files
When looking at a unit file, sections names are distinguished with square brackets such as \[Unit\].

You will more than likely find:
\[Unit\] which describes the Unit and its dependencies.
\[Service\] which defines how the service should prep, start and reload.

#### Variables
Things that start with a $ are variables.
These variables are defined in a file which is defined with `EnvironmentFile=` setting.

#### Specifiers
Specifiers are short hand definitions for things and start with a `%`.
`%n` is the current unit name while `%H` is the current hostname.
`@` can be used when making multiple instances of something such as `getty@.service` that makes `getty@tty1` and `getty@tty2` etc.

### systemd Operation
`systemctl list-units` will list all of the active units on your system.
	`--full` will show the full unit name.
	`--all` will show all of the units, not just those that are active.
`systemctl status UNITNAME` will show the status of a particular unit.
	There will also be information regarding the `cgroup` for your unit.
	
#### How Jobs relate to starting, stopping and reloading units.

Unit configurations that you have changed can typically be reloaded with the `systemctl reload *unit*` command.

When a system needs to activate, reactivate, or restart a process, it is considered a *job*.

You can see the list of current jobs for systemd with `systemctl list-jobs`.
	Here you will see the type of job, and it's current state which could be `waiting` or `running`.
	
#### Adding and Stopping Units
This section needs to be filled in later with practice.


#### systemd Process Tracking and Synchronization
As specified earlier, cgroups are meant for the organizations into services that can control their behavior.

There are various behaviors for processes and can be defined as such:
| Type    | Description                                                                                                 |
| ------- | ----------------------------------------------------------------------------------------------------------- |
| simple  | Does not fork and terminate.                                                                                |
| forking | Expect for it to fork and terminate it's original unit. At this point systemd will consider it to be ready. |
| notify  | Sends a notification to systemd when ready to begin certain functions.                                      |
| dbus    | Places it on the dbus when ready.                                                                                                            |


There is also `Type=oneshot` which specifies a process that creates no children and terminates after its execution.
	Systemd will consider this process to `ready` after it terminates.
#### Dependencies
If you want to specify dependencies.
	Since some process are dependent on others to function, they could also not run if the parent process fails to start.
	Therefore, dependency rules can be defined to allow for granular control of services.
| Dependency | Description                                                                                                                              |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Requires   | The unit needs other unit(s) specified which systemd will try to start. If this fails, systemd will terminate both the parent and child. |
| Wants      | Upon activation, systemd will start the wanted units and does nothing if they fail.                                                      |
| Requisite  | Units that need to be activated before this one can start. If not activated, systemd fails activation.                                   |
| Conflicts  | Defines conflicting units, and if active, will kill them to active this one.                                                                                                                                         |

`systemctl show -p type unit` will show the unit's type and dependencies.

#### Ordering
`Before` specifies units to start before others.
`After` specifies units to start after certain units have started.

### SystemD On-Demand and Resource-Parallized Startup
Filles in later after chapter 9