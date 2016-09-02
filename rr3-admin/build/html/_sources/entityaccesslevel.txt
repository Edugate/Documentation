Entity and access level
**********************

Default access level

* Administrator role has access to everything.

* Member role has view access to entity excluding Logs/Stats 

* Guest role has no access to vie entitie's details

Obviosly you can still set access level per user.
There are three levels: read, write, manage

* read

  * access to view details about entity excluding Logs
  * no access to edit, manage

* write include read

  * can edit entity

    * most changes are not sent for approval except:

      * changing IDPSSODescriptor/AADescriptor - scope
      * assigning EntityAttribute (EntityCategory etc) 
      * assigning RegistrationPolicy 

  * can apply to join federation
  * can leave federation
  * view/edit stats (if feature is enabled)
  * view logs
  * manage attribute policy (if feature is enabled)


* manage includes read and write

  * all above
  * manage access level for entity
  * change status (disabled, locked)
  * change status of membership (temporary disable membership)
  * remove entity from the system


Administrator role has additional access to change registrationAuthority and registrationDate





