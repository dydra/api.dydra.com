.. index:: configuration; SFTP

SFTP Configuration
==================

The basic configuration to access Dydra's SFTP service is as follows:

* **Protocol**: SFTP
* **Hostname**: dydra.com
* **Port**: 2200
* **Username**: *<your Dydra account name>*
* **Password**: *<your SFTP password>*

The SFTP username is your `dydra.com <https://dydra.com/>`__ user account
name; in the configuration examples that follow, this is indicated as
`jhacker <https://dydra.com/jhacker>`__, a demo account.

The SFTP password is a unique, long random character string :doc:`issued
<auth>` when SFTP access was granted for your account.

Configuring Cyberduck
---------------------

`Cyberduck <https://cyberduck.io/?l=en>`__ is a free cross-platform SFTP
browser for Mac OS X and for Windows. To connect using Cyberduck, use the
:menuselection:`File --> Open Connection` function to create a connection
with the following settings:

* **Protocol**: SFTP (SSH File Transfer Protocol)
* **Server**: dydra.com
* **Port**: 2200
* **Username**: *<your Dydra account name>*
* **Password**: *<your SFTP password>*

Configuring OpenSSH
-------------------

To connect using the `OpenSSH <http://www.openssh.com/>`__ client software,
which is bundled with Mac OS X as well as most Linux distributions, use the
:program:`sftp` program as follows::

   $ sftp -P 2200 jhacker@dydra.com

To simplify usage, append the following block to the SSH client
configuration file (typically, :file:`~/.ssh/config` on Unix systems)::

   Host dydra dydra.com
     HostName dydra.com
     Port 2200
     User jhacker

After amending the local SSH client configuration as per the above, you can
now connect as follows::

   $ sftp dydra.com
