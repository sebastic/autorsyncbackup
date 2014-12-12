autorsyncbackup
---------------

autorsyncbackup is a backup solutuon completely written in bash as wrapper around rsync. Currently it's only tested for Debian Wheezy. Please create a issue if you find any problem.

    @author: Teun Ouwehand (teun@nextpertise.nl)
    @company: Nextpertise B.V.

How to use:
-----------

Export by example to: `/usr/local/share/autorsyncbackup`

    $ cd /usr/local/share/
    $ git clone git@github.com:Nextpertise/autorsyncbackup.git
    
Create symlink:

    $ ln -s /usr/local/share/autorsyncbackup/autorsyncbackup-main/autorsyncbackup /usr/local/bin/autorsyncbackup

Create a job directory, this directory will contain .job files with rsync hosts:

    $ mkdir /etc/autorsyncbackup

The job files are written in YAML syntax and will only apply with the `.job` file extension, config example: `/etc/autorsyncbackup/host.domain.tld.job`

    --
    hostname: host.domain.tld
    username: rsyncuser
    password: rsyncpassword
    share: rsyncshare
    backupdir: /var/data/backups_rsync
    speedlimitkb: 1600
    maxcycles: 32
    fileset:
      0: /etc/
      1: /home/

Note: The backupdir will be postfixed with the hostname, by example: `/var/data/backups_rsync/host.domain.tld/`

Create a directory which contain the backups:

    $ mkdir /var/data/backups_rsync

Create a directory for output XML files, these contain information about the executed jobs:

    $ mkdir /var/spool/autorsyncbackup

Finally execute the backup (you can cron this command)

    $ /usr/local/bin/autorsyncbackup -j /etc/autorsyncbackup -l /var/spool/autorsyncbackup/
