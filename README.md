# aspects_timesyncd
Configure systemd-timesyncd.

This is an ultra simple role. It just templates `/etc/systemd/timesyncd.conf.d/99-aspects_timesyncd.conf` with the values you set in the 7 available variables. 

See the [official docs](https://www.freedesktop.org/software/systemd/man/timesyncd.conf.html) for details on valid values.


## Role Variables
### aspects_timesyncd_enabled
Default: `False`. Set to `True` to run the roles tasks.

Whether or not to include the tasks from this role.

### aspects_timesyncd_NTP
Default: Undefined. 

Set the value of the `NTP` parameter.

### aspects_timesyncd_FallbackNTP
Default: Undefined. 

Set the value of the `FallbackNTP` parameter.

### aspects_timesyncd_RootDistanceMaxSec
Default: Undefined. 

Set the value of the `RootDistanceMaxSec` parameter.

### aspects_timesyncd_PollIntervalMinSec
Default: Undefined. 

Set the value of the `PollIntervalMinSec` parameter.

### aspects_timesyncd_PollIntervalMaxSec
Default: Undefined. 

Set the value of the `PollIntervalMaxSec` parameter.

### aspects_timesyncd_ConnectionRetrySec
Default: Undefined. 

Set the value of the `ConnectionRetrySec` parameter.

### aspects_timesyncd_SaveIntervalSec
Default: Undefined. 

Set the value of the `SaveIntervalSec` parameter.

### aspects_packages_packages
When `aspects_packages_enabled`, install `systemd-timesyncd` and make sure `chrony` is not installed.

Default:
```yaml
aspects_packages_packages:
  systemd-timesyncd:
    state: "present"
    Ubuntu:
      2004: "systemd-timesyncd"
      2204: "systemd-timesyncd"
    Debian:
      11: "systemd-timesyncd"
    OracleLinux:
      8: "systemd-timesyncd"
  chrony:
    state: "absent"
    Ubuntu:
      2004: "chrony"
      2204: "chrony"
    Debian:
      11: "chrony"
    OracleLinux:
      8: "chrony"
```

## Example Playbook

```yaml
---
- hosts:
  - test
  vars:
    aspects_packages_enabled: True
    aspects_timesyncd_enabled: True
    aspects_timesyncd_NTP: "ntp.ubuntu.com 0.debian.pool.ntp.org"
    aspects_timesyncd_FallbackNTP: "1.debian.pool.ntp.org ntp.ubuntu.com"
    aspects_timesyncd_RootDistanceMaxSec: "100s"
    aspects_timesyncd_PollIntervalMinSec: "24s"
    aspects_timesyncd_PollIntervalMaxSec: "45m"
    aspects_timesyncd_ConnectionRetrySec: "45s"
    aspects_timesyncd_SaveIntervalSec: "45s"
  roles:
    - aspects_timesyncd
```