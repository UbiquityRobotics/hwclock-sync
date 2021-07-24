# hwclock-sync

This is a simple package that attempts to smartly handle syncing the system time to an RTC at bootup.

If a hardware RTC exists, it will read the time off of it and set it as the system time (using `hwclock -s`).
If there is no hardware RTC, the systemd unit will not run.

The systemd unit is set to always run before fake-hwclock, that way the system will always end up with the "newest" time between 
the time at shutdown that fake-hwclock recorded and the time reported by the RTC. This is useful because the RTC can come up with some default
reset time if it does not have a battery installed, in which case the time of shutdown (which should be newer) may be more accurate. 
