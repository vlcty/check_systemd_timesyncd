# check_systemd_timesyncd

## Overview

This Icinga Plugin calls `timedatectl status` and parses two responses wich have to be `yes`:

* System clock synchronized
* systemd-timesyncd.service active

If `System clock synchronized` is `no`, then the plugin exists in CRITICAL state.   
If `systemd-timesyncd.service active` is `no`, then the plugin exits in WARNING state.

This script has to run with root privileges.

## Check command

Here is a CheckCommand you can use in Icinga2:

```
object CheckCommand "systemd_timesyncd" {
    import "import "plugin-check-command"

    command = [ "/usr/bin/sudo", PluginDir + "/check_systemd_timesyncd" ]
}
```

## Further notes

Please check the system clock with a second check! This script only asks systemd if the clock is in sync but does not perform a real test against an NTP server.
