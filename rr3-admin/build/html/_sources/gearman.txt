Gearman
*******

JAGGER has ablity to interconnect with gearman. 

What is Gearman you can find on http://gearman.org/

Here is example instruction how to install gearman  from source and add support into php.

libgearm
========

Go to https://launchpad.net/gearmand and download lates version of gearmand
for example https://launchpad.net/gearmand/1.2/1.1.9/+download/gearmand-1.1.9.tar.gz released on 2013-08-02 
and install it

php-gearman
===========

We're going to use pecl  so before please make sure have installed php-pear.

.. code:: bash

 pecl search  gearman 


you should get listed gearman 1.1.1 (stable)  1.1.1 PHP wrapper to libgearman 

.. code:: bash

 pecl install  gearman 


then enable gearman in one of php ini files (depends on distribution) 

.. code:: bash

  extension=gearman.so

.. note:: some distribution have seperated config for php (apache) and php (cli)


restart apache  and  check

.. code:: php

 <?php 
   phpinfo(); 
 ?> 

and/or

.. code:: bash

 php -i|grep -i gearm


gearman-job-server
==================

You need gearman-job-server server running to handle jobs. As gearman-job-server has no security profile please configure the service to listen on local interface.

example:

**/etc/default/gearman-job-server**

.. code:: bash
 
 PARAMS="--listen=127.0.0.1"

**/etc/init.d/gearman-job-server**

.. code:: bash

 #!/bin/sh

 # Gearman server and library
 # Copyright (C) 2008 Brian Aker, Eric Day
 # All rights reserved.
 #
 # Use and distribution licensed under the BSD license.  See
 # the COPYING file in this directory for full text.

 ### BEGIN INIT INFO
 # Provides:          gearman-job-server
 # Required-Start:    $network $remote_fs $syslog
 # Required-Stop:     $network $remote_fs $syslog
 # Default-Start:     2 3 4 5
 # Default-Stop:      0 1 6
 # Short-Description: Start daemon at boot time
 # Description:       Enable gearman job server
 ### END INIT INFO

 prefix=/usr/local
 exec_prefix=${prefix}
 NAME=gearmand
 DAEMON=${exec_prefix}/sbin/gearmand
 PIDDIR=/var/run/gearman
 PIDFILE=${PIDDIR}/gearmand.pid
 GEARMANUSER="gearman"
 PARAMS=""


 test -x ${DAEMON} || exit 0

 . /lib/lsb/init-functions

 test -f /etc/default/gearman-job-server && . /etc/default/gearman-job-server

 start()
 {
   log_daemon_msg "Starting Gearman Server" "gearmand"
   if ! test -d ${PIDDIR}
   then
     mkdir ${PIDDIR}
     chown ${GEARMANUSER} ${PIDDIR}
   fi
   if start-stop-daemon \
     --start \
     --exec $DAEMON \
     -- --pid-file=$PIDFILE \
        --user=$GEARMANUSER \
        --daemon \
        --log-file=/var/log/gearman-job-server/gearman.log \
        $PARAMS 
   then
     log_end_msg 0
   else
     log_end_msg 1
     log_warning_msg "Please take a look at the syslog"
     exit 1
   fi
 }


 stop()
 { 
   log_daemon_msg "Stopping Gearman Server" "gearmand"
   if start-stop-daemon \
     --stop \
     --oknodo \
     --exec $DAEMON \
     --pidfile $PIDFILE
   then
     log_end_msg 0
   else
     log_end_msg 1
     exit 1
   fi
 }

 status()
 {
     status_of_proc -p $PIDFILE $DAEMON $NAME && exit 0 || exit $?
 }

 case "$1" in

   start)
     start
   ;;

   stop)
     stop
   ;;

   status)
     status
   ;;

   restart|force-reload)
     stop
     start
   ;;


   *)
     echo "Usage: $0 {start|stop|restart|force-reload|status}"
   ;;

 esac









