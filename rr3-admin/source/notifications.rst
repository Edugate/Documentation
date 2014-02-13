Notification system
***********************

Jagger doesn't send mail notification during operational processes as it could slow down the system.
Instead it creates notifications in mailqueue table with its status.

So you need a tool to monitor the mailqueue and preocess notificatations if needed.

Setup JaggerMailer
====================
This is simple process in demon mode wchich allow to monitor the mailqueue and send messages.
The only thing you need to run is:

   .. code:: bash
     
      php /JAGGER_PATH/index.php gworkers mailqueuesender

The process will be checking mailqueue for new mails to be sent every 60secs


 
