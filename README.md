# checkrestart

```
Usage: checkrestart [--quiet | --silent] [--restart]
```

When the binaries or libraries present on a UNIX system are replaced or
upgraded, any in-memory images of the original binary continue to run
unaffected, and will not gain the benefits of the change until restarted.

Unfortunately, there is no standardised method of detecting this situation and
taking action.

`checkrestart` uses only GNU `findutils` and the contents of the `proc`
filesystem in order to identify obsolete in-memory images and reports the
services which are in need of being restarted (without `--restart`) or restarts
those services which can be safely restarted (with `--restart`).

This script has been written with Gentoo Linux running OpenRC in mind, but
should work on any system with OpenRC or SysV init.  Patches for enhanced
compatibility with other systems are welcomed - currently the checking of which
services are currently running (using `rc-config` if available) is
OpenRC-specific.  Other systems may only be able to derive this information by
attempting to associate files in `/var/lock/subsys` with specific init scripts,
or by interrogating each init script in turn and relying on consistent output.
In addition, the determination of which init scripts are safe or unsafe to
restart is based on Gentoo, and may not be exhaustive.  To be certain, please
always run `checkrestart` without the `--restart` option prior to running with
it.
