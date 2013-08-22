.. _configfile:

Configuration files
*******************
There are a few config files used by RR3 and they're stored in **/opt/rr3/application/config/** folder. 

config.php
==========
This is standard config file for codeigniter based application. It can be copied from **/opt/codeigniter/application/config/config.php** file. Please follow Codeigniter documentation. In most cases it will be default with some below exceptions:

Please follow Codeigniter documentation. In most cases it will be default with some below exceptions:


* base_url

  .. code:: php
   
     $config['base_url']     = 'https://yourhost.example.com/rr3/';

* index_page

  .. code:: php

     $config['index_page'] = ''; 

* log_threshold - you decide what log level

* log_path - set location for example:

  .. code:: php

     $config['log_path'] = '/var/log/rr3/'; 

* encryption_key - you need to set encryption key. you can generate with

 .. code:: bash 
    
    tr -c -d '0123456789abcdefghijklmnopqrstuvwxyz' </dev/urandom | dd bs=32 count=1 2>/dev/null;echo

* sess_driver - please uset native  drive, example:

 .. code:: php

   $config['sess_driver']                  = 'native';
   $config['sess_valid_drivers']   = array();
   $config['sess_cookie_name']             = 'ci_session';
   $config['sess_expiration']              = 7200;
   $config['sess_expire_on_close'] = FALSE;
   $config['sess_encrypt_cookie']  = FALSE;
   $config['sess_use_database']    = FALSE;
   $config['sess_table_name']              = 'ci_sessions';
   $config['sess_match_ip']                = FALSE;
   $config['sess_match_useragent'] = TRUE;
   $config['sess_time_to_update']  = 300;
 
* csrf_protection - set to TRUE, however as csrf_regenerate set to FALSE as there is a problem with ajax forms

 .. code:: php

   $config['csrf_protection'] = TRUE;
   $config['csrf_token_name'] = 'csrf_test_name';
   $config['csrf_cookie_name'] = 'csrf_cookie_name';
   $config['csrf_expire'] = 7200;
   $config['csrf_regenerate'] = FALSE;
   $config['csrf_exclude_uris'] = array();


config_rr.php
=============

As template please use **config_rr-default.php** 

* pageTitlePref - if set then is included into every page's title as prefix, example:

  .. code:: php
 
    $config['pageTitlePref'] = 'RR3:: ';

* rr_setup_allowed - it should be always be set to FALSE. TRUE only when setup is initialized 
 
  .. code:: php
     
    $config['rr_setup_allowed'] = FALSE;

* site_logo - set filename to be used as main logo in top-left corner. File should be stored in **/opt/rr3/images/** folder. 

  .. code:: php
     
    $config['site_logo'] = 'logo-default.png';

* syncpass - please generate strong key. It's used by synchronization - interfederation tool 

 .. code:: bash 
    
    tr -c -d '0123456789abcdefghijklmnopqrstuvwxyz' </dev/urandom | dd bs=32 count=1 2>/dev/null;echo
 
 then assign generated value to attr like:

 .. code:: php
     
    $config['syncpass'] = 'qp7zwgm6vqzptb87uoe7zzfiq1gx1oa6';

* support_mailto - set support email. For example this email is displayed as contact mail.

* rr_rm_member_from_fed - right now it must be set to TRUE

 .. code:: php

    $config['rr_rm_member_from_fed'] = TRUE;

* rr_logobaseurl - if NULL then **base_url** is set. It's used for generating Metadata logo paths if RR3 is a source of logo.  

 .. code:: php
 
   $config['rr_logobaseurl'] = NULL;

* rr_logouriprefix - used together with **rr_logobaseurl** . By default **logos** directory is used.

 .. code:: php
   
  $config['rr_logouriprefix'] = 'logos/';  

 The url generated will look like: *https://yourhost.example.com/rr3/logos/example-logo.png*

 .. note:: 
  If you decide to use different location but under **/opt/rr3** then remember to exclude the folder in apache rewtite rules

* rr_logoupload - it decides wether user may upload logos to the system. By default set to FALSE

 .. code:: php

  $config['rr_logoupload'] = FALSE;

* rr_logoupload_relpath -  if **rr_logoupload** is TRUE then you can decide the defaul location for uploaded logos by users. Bu default you can set **logos/** . You may decide to review every uploaded image the please create another folder under **/opt/rr3** and set its name. The you will need to copy manually reviewed logos from this location into "logos" folder.

 .. code:: php

  $config['rr_logoupload'] = 'logos/';

* rr_logo_maxwidth, rr_logo_maxheight - if **rr_logoupload** is TRUE then  you can decide maximum allowed dimesions in px.

 .. code:: php

   $config['rr_logo_maxwidth'] = 300;
   $config['rr_logo_maxheight'] = 300;

* rr_logo_types -  applied when **rr_logoupload** is TRUE. What type of logos is allowed to be uploaded. Recommended : png

 .. code:: php

   $config['rr_logo_types'] = 'png|jpg';

* rr_logo_maxsize - applied when **rr_logoupload** is TRUE. Maximum allowed size upladed image in KB

 .. code:: php

   $config['rr_logo_maxsize'] = 2000;  

* autoregister_federated - if federated access to RR3 is enabled you can decide wether user who used federated access but doesn't exist in RR3 should be autoprovisioned or not. Strongly recommend to not allow it. If it's set to FALSE then new (not registered) user will get error page with contact support email address.

 .. code:: php
  
  $config['autoregister_federated'] = FALSE;

* register_defaultrole - if you decide to enable **autoregister_federated** then please set default role with lowest permissions. In this case please set "Guest"

 .. code:: php
  
  $config['register_defaultrole'] = 'Guest';

* Shib_required - define required attributes needed to be provided by IdP. By default please require Shib_username and Shib_mail which their mapping are defined next 

 .. code:: php

  $config['Shib_required'] = array('Shib_mail','Shib_username');

* Shib_username - id of attribute from Shibboleth (attribute-map.xml) which will be mapped as username in RR3. Strongly recommend eppn or othe unique scoped attr

 .. code:: php
  
  $config['Shib_username'] = 'eppn';

* Shib_mail - id of attribute from Shibboleth (attribute-map.xml) which will be mapped as user's email address in RR3. By default mail

 .. code:: php

  $config['Shib_mail'] = 'mail';

* Shibboleth - is array containing information wether shibboleth based federated access should be enabled, uri which resolves shibboleth assertion and logout uri which is called in iframe during RR3 logout process - it allows to destroy both RR3 and shibboleth session

 .. code:: php

  $config['Shibboleth']['loginapp_uri'] = 'auth/fedauth';
  $config['Shibboleth']['logout_uri'] = '/Shibboleth.sso/Logout';
  $config['Shibboleth']['enabled'] = TRUE;
  
 .. note:: 

  If you enable federated access then you need to protect **auth/fedauth** by shibboleth in apache configuration
  
  Also when **$config['Shibboleth']['enabled'] = TRUE** you will see "Federate login" button on login page.

* nameids - array of allowed NameID in RR3

 .. code:: php

   $config['nameids'] = array(
        'urn:mace:shibboleth:1.0:nameIdentifier' => 'urn:mace:shibboleth:1.0:nameIdentifier',
        'urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress' => 'urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress',
        'urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified'=>'urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified',
        'urn:oasis:names:tc:SAML:2.0:nameid-format:transient' => 'urn:oasis:names:tc:SAML:2.0:nameid-format:transient',
        'urn:oasis:names:tc:SAML:2.0:nameid-format:persistent' => 'urn:oasis:names:tc:SAML:2.0:nameid-format:persistent',
                );

* metadata_validuntil_days - the value in days give how long generated metadata is valid - in metadata **validUntil** is generated datetime from now + number of days

 .. code:: php
 
   $config['metadata_validuntil_days'] = '7';

* policy_dropdown - dropdown element for attribute policy - this config will be removed in future release, but right now is mandatory.

 .. code:: php

  $config['policy_dropdown'] = array('0' => 'never', '1' => 'permit only if required', '2' => 'permit if required or desired');


* authorities

* includeRegistrationAuth

* registrationAutority

* load_registrationAutority 

* fedloginbtn - optional value used to replace default text for federated button in login form. Example can be like this:

 .. code:: php

  $config['fedloginbtn'] = 'Login via Edugate or Social Media';


* arp_cache_time - set time in seconds how long generated array for AttributeReleasePolicy XML file (shibboleth format) should be in cache.

 .. code:: php

  $config['arp_cache_time'] = 1200;


 metadata_cache_time

* geocenterpoint - this option allows you to define default lang/lat for loaded map when no geo points are set. If not set then (-6.247856140071235,53.34961629053703). Example: 

 .. code:: php
  
  $config['geocenterpoint'] = array('-9.126273968749956','38.684286647936936');

* memcached - it's optional but please use memcached.php config file instead 

 .. code:: php

  $config['memcached'] = array(
                 'optional'=>array(
                        'hostname'  => 'localhost',
                        'port'      => '11211',
                        'weight'    => '1'
                        )
                 );


* cacheprefix - add prefix to each key cached object

 .. code:: php
 
  $config['cacheprefix'] = 'rr3_';


* translator_access - (optional) allows permitted user to modify existing translation. You can set only one person per language.

 .. code:: php
  
  $config['translator_access']['pl'] = 'user444@example';

* gearman - (optional) boolean value - whether to enable gearman. There some benefits using gearman.

 .. code:: php

  $config['gearman'] = TRUE;

* gearmanconf - used if  **$config['gearman']**  is set TRUE. Details about gearman-job-server 

 .. code:: php
  
  $config['gearmanconf']['jobserver'] = array(array('ip'=>'127.0.0.1','port'=>'4730'));


* disable_extcirclemeta - (optional) but in most cases should be set to TRUE. It defines whether should or shouldnt generate circle metadata for providers which are set external.

 .. code:: php

  $config['disable_extcirclemeta'] = TRUE;


email.php
=========

You can use **email-default.php** as a template. Ther are two parts:

#. connection details

   .. code:: php

     $config['protocol'] = 'smtp';
     $config['smtp_host'] = "SMTP_HOST";
     $config['smtp_port'] = 25;
     $config['charset'] = 'utf-8';
     $config['crlf'] = "\r\n";
     $config['newline'] = "\r\n";
     $config['wordwrap'] = TRUE;
     $config['useragent']='ResourceRegistr3';
     $config['smtp_user'] = 'USER';
     $config['smtp_pass'] = 'PASS';
     $config['smtp_crypto'] = 'tls';

#. usage in RR3

 * mail_sending_active - boolean FALSE/TRUE - if FALSE then not mails are sent at all. It takes presedence..

   .. code:: php

     $config['mail_sending_active'] = TRUE;


 * notify_if_provider_rm_from_fed - boolean  - if TRUE then notification will be sent when IdP or SP has been removed from federation. The recipients are: all contacts for IdP/SP and members of Administators group in RR3

   .. code:: php

     $config['notify_if_provider_rm_from_fed'] = TRUE;

 * notify_if_queue_rejected - boolean - if TRUE then requestere will be notified by email if his request is rejected.

   .. code:: php

     $config['notify_if_queue_rejected'] = TRUE;


 * notify_admins_if_queue_accepted

 * notify_requester_if_queue_accepted
 
 * mail_from

 * fake_mail_from

 * reply_to

 * mail_subject_suffix

 * mail_header

 * mail_footer 

 






database.php
============

this file contains information about connection to dabase.
As template **database-default.php** can be used. Some of options are ignored by doctrine. So please focus and change username, password, database

.. code:: php

 $active_group = 'default';
 $active_record = TRUE;

 $db['default']['hostname'] = 'localhost';
 $db['default']['username'] = 'CHANGEME';
 $db['default']['password'] = 'CHANGEME';
 $db['default']['database'] = 'CHANGEME';
 $db['default']['dbdriver'] = 'mysql';
 $db['default']['dbprefix'] = '';
 $db['default']['pconnect'] = TRUE;
 $db['default']['db_debug'] = TRUE;
 $db['default']['cache_on'] = FALSE;
 $db['default']['cachedir'] = '';
 $db['default']['char_set'] = 'utf8';
 $db['default']['dbcollat'] = 'utf8_general_ci';
 $db['default']['swap_pre'] = '';
 $db['default']['autoinit'] = TRUE;
 $db['default']['stricton'] = FALSE;

 
memcached.php
=============

file contains information about available memcached servers
As template **memcached-default.php** can be used - default 

.. code:: php

 $config = array(
        'default' => array(
                'hostname' => '127.0.0.1',
                'port'     => '11211',
                'weight'   => '1',
        ),
 );


.. note::

 If you don't set this file you may get Notice/Error on some pages.

   
