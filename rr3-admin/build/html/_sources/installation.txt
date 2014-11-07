Installation process (final)
****************************
In the documentation there predefined:

* website https://yourhost.example.com/rr3 
* Codeigniter framework will be installed in  */opt/codeigniter*
* ResourceRegistry3 source code will stored in */opt/rr3*

Requirements
============
* composer https://getcomposer.org/
 
 .. code:: bash

  curl -sS https://getcomposer.org/installer | php
  cp composer.phar /usr/local/bin/composer

* mysql > 5.1  (it should work with postgres etc but not tested) 
* PHP >= 5.3 with modules: php-apc, php5-cli, php5-curl, php5-mysql, php5-mcrypt, php5-memcached
* Apache >= 2.2 with enabled modules: rewrite, unique_id 
* Shibboleth-SP >= 2.4 - optional needed for federated access 
* Codeigniter framework 3.0 - it's not official release yet from git://github.com/EllisLab/CodeIgniter.git

 .. warning::  Since Oct 2014 Codeigninter has new home and changes licence to MIT. Also location on github has been changed https://github.com/bcit-ci/CodeIgniter

* Doctrine >= 2.4.x http://www.doctrine-project.org

 .. note:: Doctrine it will be installed with composer

* Zend Framework 

  Only Zend-ACL (Acl dir, Acl.php,  Exception.php) part from http://framework.zend.com/download/current/
  into APP_PATH/libraries/Zend

 .. note:: Zend-ACL it will be downloaded within install script

* Memcached server on the same host

* gearman-php, gearnam-job-server - allows to enable additional features in JAGGER 

Download JAGGER and Codeigniter
===============================

In the time writting this document there wasn't official release of Codeigniter version 3.0.
So we are going to use source code from GitHub repository

 .. note:: we will be using develop branch 

.. code:: bash

 git clone git://github.com/bcit-ci/CodeIgniter.git /opt/codeigniter
 cd /opt/codeigniter
 git checkout -b develop origin/develop 
 git pull

ResourceRegistry3 is published on GITHUB https://github.com/Edugate/ResourceRegistry  under MIT License.

.. code:: bash

 git clone https://github.com/Edugate/ResourceRegistry /opt/rr3
 cd /opt/rr3

Install dcotrine with composer tool

.. code:: bash

 composer install

Set *index.php* file 

.. code:: bash

 cp /opt/codeigniter/index.php /opt/rr3/

and modify it. You need to change default path to system folder. Open */opt/rr3/index.php* file and find

.. code:: php
 
  $system_path = 'system';

and change to 

.. code:: php
 
  $system_path = '/opt/codeigniter/system';

You may also want to set production environment. To do it find line

.. code:: php

 define('ENVIRONMENT', isset($_SERVER['CI_ENV']) ? $_SERVER['CI_ENV'] : 'development');

and before that line add

.. code:: php

 $_SERVER['CI_ENV'] = 'production';


Apache/PHP configuration
========================

.. code:: apache 

      Alias /rr3 /opt/rr3
        <Directory /opt/rr3>

              #  you may need to uncomment next line
              #  Require all granted

                RewriteEngine On
                RewriteBase /rr3
                RewriteCond $1 !^(Shibboleth\.sso|index\.php|logos|signedmetadata|flags|images|app|schemas|fonts|styles|images|js|robots\.txt|pub|includes)
                RewriteRule  ^(.*)$ /rr3/index.php?/$1 [L]
        </Directory>
        <Directory /opt/rr3/application>
                Order allow,deny
                Deny from all
        </Directory>




MySQL 
=======================

You need to create database and set permissions for instance:

.. code:: bash

 DBUSER = 'rr3user' 
 DBPASS = 'rr3pass'
 DATABASENAME= 'rr3'
 
Log in to mysql as superuser and run: 

.. code:: bash

   mysql> create database rr3 CHARACTER SET utf8 COLLATE utf8_general_ci;
   mysql> grant all on rr3.* to rr3user@'localhost' identified by 'rr3pass';
   mysql> flush privileges;


install.sh script
=================

Now it's time to run install.sh script. Go to **/opt/rr3/**

.. code:: bash

 ./install.sh


What it does is downloading Doctrine, Zend-ACL, Geshi, XMLseclib and exctract them.
Then you need to set required config files - you can copy templates and customize them.
Stay in  **/opt/rr3/**

.. code:: bash

 cp config-default.php -> config.php
 cp config_rr-default.php -> config_rr.php
 cp database-default.php -> database.php
 cp email-default.php -> email.php
 cp memcached-default.php -> memcached.php

Please follow section :ref:`configfile`

Set permission - writeable by apache user. Ralive path of folders need to be set:

* application/cache
* application/models/Proxies

Database - populate tables
==========================

To populate tables we are going to use doctrine tool. 

Go to **application** folder and you should see **doctrine** file. It should be executable.

.. code:: bash
 
 ./doctrine


You will get many available options, be carefull. To populate tables please run below command. It will parse all entities in application/model

.. code:: bash 

 ./doctrine orm:schema-tool:create

If you going to run application in production mode then you also need to regenerate proxies:

.. code:: bash

 ./doctrine orm:generate-proxies

and verify owner of application/models/Proxies/* - apache user should be owner

In the future after every update you will need to run

.. code:: bash

 ./doctrine orm:schema-tool:update --force
 ./doctrine orm:generate-proxies






.. _final-setup-step:

Final setup step
================

This is the last step in Installation process.
To be able to run it you need to set in **config_rr.php** file:

.. code:: php
 
 $config['rr_setup_allowed'] = TRUE;


.. note:: remember to change it back to FALSE

Open page **https://yourhost.example.com/rr3/setup** and fill the form.

After submit user you entered will be in Administration group.

.. warning:: Again: **please change rr_setup_allowed to FALSE**




