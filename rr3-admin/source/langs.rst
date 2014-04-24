Language
*********
JAGGER supports multilanguage. Loading language is defined in **/opt/rr3/application/core/MY_Controller.php**
Firstly english language is loaded and then cookie called **rrlang** is checked. If its value is in range allowed languages then
selected language is selected otherwise english is used.
Files if langs definitions are located in **/opt/rr3/application/language/**. Every lang has own folder and all of them except english are based to letter lang code.

Supported languages
===================

You can select only one of below supported languages

* English (EN) - default

* Czech (CS)

* French-Canadian (FR-CA)

* Italian (IT)

* Lithuanian (LT)

* Polish (PL)

* Portuguese (PT)

* Spanish (ES)




Translation 
===========

To modify existing translation open **https://yourhost.example.com/rr3/manage/translator/tolanguage/${langCode}** where **${langCode}** is two-letter lang code like es, pt, pl etc  can be any of allowed langs. Example URL for polish translation: **https://yourhost.example.com/rr3/manage/translator/tolanguage/pl**.

Next thing is to define permission who can translate and into what language. You need to set it in **config_rr.php** file. For example to give polish translation permission to user with username **joebloggs** add below line into **config_rr.php**

.. code:: php

 $config['translator_access']['pl'] = 'joebloggs';

Also make sure that lang file(s) in **/opt/rr3/application/language/pl** are writable by apache owner

Please contribute your changes to main code on github


Add new language
================

If you want to add language which is not supported nor allowed yet you need to make some temporary changes.

#. the best option is firstly to send request on Github to add lang to allowed group. Then pull new revision and you can start translating and after even partial translation please contribute your code.

#. If you want to do it on your own. then you need to create and modify few files. For instance we want you create German translation:

#. create folder **de** in /opt/rr3/application/language and copy all files from /opt/rr3/application/language/english 

    .. code:: bash

     mkdir /opt/rr3/application/language/de
     cp /opt/rr3/application/language/english/* /opt/rr3/application/language/de/
    
    and set proper owner/permissions

 #. open /opt/rr3/application/controllers/manage/Translator.php
    
    find **$allowedlangs** in 

    .. code:: php
     
     public function tolanguage($l)
     {

     }

    and add new language code. Then you need to add below line into **config_rr.php** file
   
    .. code:: php

     $config['translator_access']['de'] = 'your username';
    
 #. This part adds your language to selection form (top-right corner of the website)

    open /opt/rr3/application/view/page.php
    
    find part 

    .. code:: php
      
       $langs = array(
                    'en' => array('path'=>'english','val'=>'english'),
                    'it' => array('path'=>'it','val'=>'italiano'),
                    'lt' => array('path'=>'lt','val'=>'lietuvos'),
                    'pl' => array('path'=>'pl','val'=>'polski'),
                    'pt' => array('path'=>'pt','val'=>'português'),
                    'es' => array('path'=>'es','val'=>'española'),
                   );
     
    and add definition for German language, it should look like 

    .. code:: php
      
       $langs = array(
                    'de' => array('path'=>'de','val'=>'deutsch'),
                    'en' => array('path'=>'english','val'=>'english'),
                    'it' => array('path'=>'it','val'=>'italiano'),
                    'lt' => array('path'=>'lt','val'=>'lietuvos'),
                    'pl' => array('path'=>'pl','val'=>'polski'),
                    'pt' => array('path'=>'pt','val'=>'português'),
                    'es' => array('path'=>'es','val'=>'española'),
                   );
 

 #. modify ajax
  
    open **/opt/rr3/application/controllers/Ajax.php** 

    and find function

    .. code:: php

     public function changelanguage($language)
     {
        if ($this->input->is_ajax_request())
        {
            log_message('debug', 'ajax');
            $language = substr($language, 0, 2);
            if ($language === 'pl')
            {
                $cookie_value = 'pl';
            }
            elseif ($language === 'pt')
            {
                $cookie_value = 'pt';
            }
        
    
    And again add definition for your language 

    
 #. This last part that allows to switch into your new language 

    open **/opt/rr3/application/core/MY_Controller.php**

    find 

    .. code:: php 
     
     $langs = array('pl','pt','it','lt','es');

    and add you language.    









