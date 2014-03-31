.. _metadata:

Metadata  
*********

http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf

JAGGER generates three types of unsigned metadata.


#. metadata for federation

   Generates metadata containing all entities (Identity Providers and Relying Parties) not matter if they are managed localy or imported as external entities.
  
   The URL of unsigned metadata is like https://yourhost.example.com/rr3/metadata/federation/ENCODED_FEDNAME/metadata.xml
   where **ENCODED_FEDNAME** is genereated by taking **Federation name** and encoding it with helper function :ref:`base64url_encode`  
   
   So it's imported to not change the name of federation created in JAGGER 

#. metadata for federation exported for interfederation purpose

   Generates metadata containing only  localy managed Identity Providers and Relying Parties 

   The URL of unsigned metadata is like https://yourhost.example.com/rr3/metadata/federationexport/ENCODED_FEDNAME/metadata.xml
   where **ENCODED_FEDNAME** is genereated by taking **Federation name** and encoding it with helper function :ref:`base64url_encode`  


#. metadata for single entity

   Generated metadata containing single entity. General purpose is to review how information about entity are presented in Metadata.

   The URL of unsigned metadata is like https://yourhost.example.com/rr3/metadata/service/ENCODED_ENTITYID/metadata.xml
   where **ENCODED_ENTITYID** is genereated by taking **entityID of IdP/SP** and encoding it with helper function :ref:`base64url_encode`  

#. metadata - circle of trust - per entity

   Generated metadata contains all trusted entities. If metadata is generated for Sevice Provider then it contains trusted IdPs.
   If metadata is generated for Identity Provider then it will contain only trusted Service Providers.

   The URL of unsigned metadata is like https://yourhost.example.com/rr3/metadata/circle/ENCODED_ENTITYID/metadata.xml
   where **ENCODED_ENTITYID** is genereated by taking **entityID of IdP/SP** and encoding it with helper function :ref:`base64url_encode`  
   






:ref:`metadatasigning`

