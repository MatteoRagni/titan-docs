% TITAN(7) Titan Mount Script Manual
% Matteo Ragni
% September 6, 2016

# Name

titan-mount-script - Utility that creates a mount script for sshfs clients

# Synopsis

titan_mount_script *CLIENT_MOUNT* [*options*]

# Description

The script is a generator for a mount script for sshfs to be run on a client machine.
This will help people to setup their environments. The generated script creates the mount
directory (if does not exists) and then calls **sshfs**.

The output of the generator is a string with the script that can be redirected to a file
or copied manually.

For example:

```
ssh user@sci-titan.unitn.it "titan-mount-script /tmp/titan" > /usr/bin/mount-titan
```

will save the script in the local system, with mountpoint set to /tmp/titan.

# Options

-u *USER*, \--user *USER*
:  Specify the username for sshfs connection. Default to actual user.

-s *SERVER*, \--server *SERVER*
:  Specify the server for sshfs connection. Default to localhost FQDN.

-r *REMOTE_MOUNT*, \--remotemount *REMOTE_MOUNT*
:  Specify the server mountpoint, Default to $HOME.
