zrsync - An rysnc wrapper
=========================

Description
-----------

For simple deployments and updates to a website, rysnc is a wonderful tool. `zrsync` is a simple 
rsync wrapper I wrote because I got tired of typing commands like this:

```sh
rsync -auv -e ssh --delete-after --stats --exclude=.svn --exclude=.git* 
--exclude-from=sync.exclude /Users/chronon/www/chronon.com/public/ 
chronon.com:/home/chronon/www/chronon.com/public
```

Following a few required conventions and using `zrsync`, the above command becomes:

```sh
zrsync
```

A little easier to remember!

Installation
------------

Put the script in your `$PATH`. Obviously SSH access to the remote host is required, preferably
using [key pair authentication](http://library.linode.com/securing-your-server#sph_using-ssh-key-pair-authentication).

Configuration
-------------

**Optional:** Set an environment variable for your most commonly used remote host. In `.bashrc` for
example:

```sh
export ZRSYNC_REMOTE="chronon.com"
```

**Optional:** Set an environment variable to convert Mac OS X directory `/Users` to `/home` when
figuring out the remote path. See the conventions section below for details. In `.bashrc` for
example:

```sh
export ZRSYNC_OSXUSER=1
```

Conventions
-----------

This script is based on (my) conventions, which if followed make using it very simple. 

* Use the **same directory structure** on your local development machine as you do on your server.
  Since OS X puts users in `/Users` and servers rooted in UNIX put users in `/home`, set the above
  mentioned environment variable `ZRSYNC_OSXUSER` to `1`.

* To exlcude files or directories, create a file in the root of your project named `sync.exclude`
  and list stuff there. Example `sync.exclude` contents:

```
Tests/  
tmp/  
webroot/test.php
```

* Both .svn and .git files/directories are automatically excluded. 

Usage
-----

If the above conventions are followed, to perform an rsync deployment or update of a project is as
simple as `cd` to project root, and typing `zrsync`. 

All command line options can be seen by typing `zrsync -h`. A pretend/dry-run mode is available by
using the `-p` option. 

