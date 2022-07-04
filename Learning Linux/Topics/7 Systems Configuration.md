### syslog severity levels
| Level | Meaning   |     |
| ----- | --------- | --- |
| 0     | emergency |     |
| 1     | alert     |     |
| 2     | crit      |     |
| 3     | err       |     |
| 4     | warning   |     |
| 5     | notice    |     |
| 6     | info      |     |
| 7     | debug          |     |
Syslog was very popular amongst network administrators, because of its networking capability. Therefore Cisco IOS logging uses the same severity levels.

## User Management FIles
### The `/etc/passwd` File

![[Pasted image 20220616135415.png]]

`root` always has an ID and GID of 0.
`daemon` daemon does not have any login privileges. 
#### `/etc/shadow`

### Groups
![[Pasted image 20220616141313.png]]

### `cron` and timer units
![[Pasted image 20220616142109.png]]

### Process Ownership, Effective UID, Real UID, Saved UID

The `euid` is the actor while the the `ruid` is the executioner.

## User Access Topics
### Identification, Authentication and Authorization

| Term             | Meaning                                               |
| ---------------- | ----------------------------------------------------- |
| *identification* | answers who the user is.                              |
| *authentication* | asks the user to prove that they are who they are.    |
| *authorization*  | is to define and limit what the use is allowed to do. |


### PAM
PAM configuration can be found in `/etc/pam.d` or `/etc/pam.conf` in older systems.

Function Types
| Type       | Function                                                      |
| ---------- | ------------------------------------------------------------- |
| `auth`     | Authenticate the user.                                        |
| `account`  | Check user account status/if it's authorized to do something. |
| `session`  | Perform something only for the user's session.                |
| `password` | Change the user's password.                                                              |

Control Arguments






## Acronyms and more
| Acronym | Meaning                          |
| ------- | -------------------------------- |
| PAM     | Pluggable Authentication Modules | 
