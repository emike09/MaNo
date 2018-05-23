Sample init scripts and service configuration for manod
==========================================================

Sample scripts and configuration files for systemd, Upstart and OpenRC
can be found in the contrib/init folder.

    contrib/init/manod.service:    systemd service unit configuration
    contrib/init/manod.openrc:     OpenRC compatible SysV style init script
    contrib/init/manod.openrcconf: OpenRC conf.d file
    contrib/init/manod.conf:       Upstart service configuration file
    contrib/init/manod.init:       CentOS compatible SysV style init script

1. Service User
---------------------------------

All three Linux startup configurations assume the existence of a "manocore" user
and group.  They must be created before attempting to use these scripts.
The OS X configuration assumes manod will be set up for the current user.

2. Configuration
---------------------------------

At a bare minimum, manod requires that the rpcpassword setting be set
when running as a daemon.  If the configuration file does not exist or this
setting is not set, manod will shutdown promptly after startup.

This password does not have to be remembered or typed as it is mostly used
as a fixed token that manod and client programs read from the configuration
file, however it is recommended that a strong and secure password be used
as this password is security critical to securing the wallet should the
wallet be enabled.

If manod is run with the "-server" flag (set by default), and no rpcpassword is set,
it will use a special cookie file for authentication. The cookie is generated with random
content when the daemon starts, and deleted when it exits. Read access to this file
controls who can access it through RPC.

By default the cookie is stored in the data directory, but it's location can be overridden
with the option '-rpccookiefile'.

This allows for running manod without having to do any manual configuration.

`conf`, `pid`, and `wallet` accept relative paths which are interpreted as
relative to the data directory. `wallet` *only* supports relative paths.

For an example configuration file that describes the configuration settings,
see `contrib/debian/examples/mano.conf`.

3. Paths
---------------------------------

3a) Linux

All three configurations assume several paths that might need to be adjusted.

Binary:              `/usr/bin/manod`  
Configuration file:  `/etc/manocore/mano.conf`  
Data directory:      `/var/lib/manod`  
PID file:            `/var/run/manod/manod.pid` (OpenRC and Upstart) or `/var/lib/manod/manod.pid` (systemd)  
Lock file:           `/var/lock/subsys/manod` (CentOS)  

The configuration file, PID directory (if applicable) and data directory
should all be owned by the manocore user and group.  It is advised for security
reasons to make the configuration file and data directory only readable by the
manocore user and group.  Access to mano-cli and other manod rpc clients
can then be controlled by group membership.

3b) Mac OS X

Binary:              `/usr/local/bin/manod`  
Configuration file:  `~/Library/Application Support/ManoCore/mano.conf`  
Data directory:      `~/Library/Application Support/ManoCore`
Lock file:           `~/Library/Application Support/ManoCore/.lock`

4. Installing Service Configuration
-----------------------------------

4a) systemd

Installing this .service file consists of just copying it to
/usr/lib/systemd/system directory, followed by the command
`systemctl daemon-reload` in order to update running systemd configuration.

To test, run `systemctl start manod` and to enable for system startup run
`systemctl enable manod`

4b) OpenRC

Rename manod.openrc to manod and drop it in /etc/init.d.  Double
check ownership and permissions and make it executable.  Test it with
`/etc/init.d/manod start` and configure it to run on startup with
`rc-update add manod`

4c) Upstart (for Debian/Ubuntu based distributions)

Drop manod.conf in /etc/init.  Test by running `service manod start`
it will automatically start on reboot.

NOTE: This script is incompatible with CentOS 5 and Amazon Linux 2014 as they
use old versions of Upstart and do not supply the start-stop-daemon utility.

4d) CentOS

Copy manod.init to /etc/init.d/manod. Test by running `service manod start`.

Using this script, you can adjust the path and flags to the manod program by
setting the MANOD and FLAGS environment variables in the file
/etc/sysconfig/manod. You can also use the DAEMONOPTS environment variable here.

4e) Mac OS X

Copy org.mano.manod.plist into ~/Library/LaunchAgents. Load the launch agent by
running `launchctl load ~/Library/LaunchAgents/org.mano.manod.plist`.

This Launch Agent will cause manod to start whenever the user logs in.

NOTE: This approach is intended for those wanting to run manod as the current user.
You will need to modify org.mano.manod.plist if you intend to use it as a
Launch Daemon with a dedicated manocore user.

5. Auto-respawn
-----------------------------------

Auto respawning is currently only configured for Upstart and systemd.
Reasonable defaults have been chosen but YMMV.
