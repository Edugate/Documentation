Important changes
****************

* 2015/12/17

  Please, don't use CodeIgniter's develop branch anymore and preferably switch to "3.0-stable" branch instead. Recent develop branch (as of 17 December 2015) breaks local authentication. If you're using develop branch, switching to 3.0-stable may be achieved by the following code if you installed CodeIgniter into :code:`/opt/codeigniter` directory:

  .. code:: bash

    cd /opt/codeigniter
    git checkout -b 3.0-stable origin/3.0-stable
    git pull

* 2015/02/25
  Since now Doctrine, Zend-ACL is loaded via autoloader. 

  Steps for updates:

  * composer.json has been moved from APP_ROOT into application folder -> you need to run in that folder:

    .. code:: php

       composer install

  * edit index.php file and make sure the below line is removed if exists

    .. code:: php
      
       require_once('vendor/autoload.php');
  
  * edit application/config/config.php and add line:

    .. code:: php
      
       $config['composer_autoload'] = true;

  * in aplpication folder run:

    .. code:: php
      
       ./doctrine orm:schema-tool:update --force
       ./octrine orm:generate:proxies

    set proper ownership (apache user) for application/models/Proxies

  * finaly you can delete following folders as they will be loaded from application/vendor:

    .. code:: php
      
       application/libraries/Doctrine
       application/libraries/Zend


* 2015/02/20

  The recent changes in Codeigniter Core , please make sure have changed 

  from 

  .. code:: php

     $config['sess_driver'] = 'native'; 

  to

  .. code:: php

     $config['sess_driver'] = 'files';
