Enable Federated access
**********************

RR3 supports both local authentication and federated access. Right now shibboleth-sp is supported. There will be support for simpleSAMLphp too.

Obviusly you need to have shibboleth-sp configured.

#. Enable federated access in RR3

   Find and set following keywords  in  :ref:`configfile` :

   autoregister_federated, register_defaultrole, Shib_required, Shib_username, Shib_mail, Shibboleth
  
#. Next thing is to protect specific URI in apache with shibboleth. Here is example part from apache config. 
  
   .. note::
     
     remove or replace ALIAS with your base location for RR3

   .. code:: apache

       <Location /ALIAS/auth/fedauth>
         Options -Indexes FollowSymLinks MultiViews
         Order allow,deny
         Allow from all
         AuthType shibboleth
         ShibRequireSession On
         require valid-user
       </Location>
       <Location /ALIAS/index.php/auth/fedauth>
         Options -Indexes FollowSymLinks MultiViews
         Order allow,deny
         Allow from all
         AuthType shibboleth
         ShibRequireSession On
         require valid-user
        </Location>

#. You may also want to enable embeded DiscoveryService. To get this working you need to have DiscoFeed enabled in shibboleth2.xml file:

   .. code:: apache
   
     <Handler type="DiscoveryFeed" Location="/DiscoFeed"/>

   enable and set as default
   

   .. code:: apache

     <SessionInitiator type="Chaining" Location="/DS" id="DS" isDefault="true"  relayState="cookie">
        <SessionInitiator type="SAML2" acsIndex="1" template="bindingTemplate.html"/>
        <SessionInitiator type="Shib1" acsIndex="5"/>
        <SessionInitiator type="SAMLDS" URL="https://yourHOST/ALIAS/eds"/>
     </SessionInitiator>


   .. note:: replace URL="https://yourHOST/ALIAS/eds" with yours

Now you should be able to see both local authentication part and federated access.

.. image:: images/loginform1.png
    :scale: 100%
    :alt: Login Form
