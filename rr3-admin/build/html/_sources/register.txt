Registration process
*****************************

You can register two type of services: Identity Providers and Service Providers.
As registration form is filled and posted the request is sent for approval.
Only users with admin rights may approve the request. 

Identity Provider registration form
===================================

Definition for :term:`Identity Provider`

.. image:: images/idpregister.png
    :scale: 60%
    :alt: IdP Register Form

The form is available on https://youhost/alias/providers/idp_registration

Home Organization
    The name of your organization 

:term:`Federation`
    Federation you want to join. If you want to apply later please select ">> None <<"

:term:`Metadata` location
    You can add location of your provider's metadata as additional information for FMP administrator

:term:`EntityID`
    This is unique ID of a provider. About the naming please follow https://wiki.shibboleth.net/confluence/display/SHIB2/EntityNaming

PrivacyStatement URL
    Optional but strongly recommended URL to your Organization's Privacy Statement

:term:`Scope`
    Domain of your Organization

Binding Type of Single-Sign-On Handler
    Binding Type of Single-Sign-On Handler

:term:`IdP` Signing Certificate
    Certificate used for signing/encrypting SAML requests/responses
    This certificate is recommened to be selfsigned as some Service Providers might not work with your IdP in the future

Primary contact
    Fill information about yourself


 



Service Provider registration form
===================================

.. image:: images/spregister.png
    :scale: 60%
    :alt: SP Register Form

The form is available on https://youhost/alias/providers/sp_registration


IdP/SP Approval Process
=======================

When Identity or Service Provider is registered then it will appear in queue list in the system. Only users with admin right may approve it.

See snapshot 

.. image:: images/queuelist.png
    :scale: 60%
    :alt: Queue list

Details of the request

.. image:: images/queuedetails.png
    :scale: 60%
    :alt: details

As you review the request you can reject or approve it. As soon as it's been approved administrator may need to delegate "sufficient rights" to the requester.

Federation registration form
============================

.. image:: images/fedregister.png
   :scale: 60%
   :alt: federation register

The form is available on https://youhost/alias/federations/federation_registration

Federation approval process
===========================


