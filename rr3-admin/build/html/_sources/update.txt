Upgrading
*********
In branch *1.x-stable* trying to keep backward compatibility so there are some deprecated code or columns/tables not used in current version.

 
Generally you can upgrade the JAGGER code by pulling new revision from GitHub.

Before that i would recommend alway make backup code and database. 

Here are steps:

#. update code from gihub

   .. code:: bash

     cd /opt/rr3
     git pull

#. check and update database schema

   .. code:: bash

     cd /opt/rr3/application
     ./doctrine orm:schema-tool:update

   If there is some changes then you get something like this

   .. code:: bash
  
     ATTENTION: This operation should not be executed in a production environment.
                Use the incremental update to detect changes during development and use
                the SQL DDL provided to manually update your database in production.

     The Schema-Tool would execute "1" queries to update the database.
     Please run the operation by passing one of the following options:
        orm:schema-tool:update --force to execute the command
        orm:schema-tool:update --dump-sql to dump the SQL statements to the screen

   That's why you should always make backup. No you can try to force it by executing

   .. code:: bash

     ./doctrine orm:schema-tool:update --force

   and then regenerate proxies

   .. code:: bash

    ./doctrine orm:generate-proxies
    
#. reload apache because as you use apc then some code may be still in cache

#. Open https://yourhost/rr3/update/upgrade to call migration process if needed




