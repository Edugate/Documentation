Federation Metadata Validators
******************************
This document describes metadata validators in JAGGER.

About Validators
================
When an entity, for example a Service Provider (SP), should be joined to a federation, you may use external validators to check metadata of such an entity before asking to join the federation. Using this technique, the person asking to join the SP to the federation can find out if metadata is correct and contains all the required information within.

Adding a Validator
==================
To add (or edit) federation validators go to ``Federations``, choose a desired federation and click on ``Validators`` tab.

1. General

* **Federation validator name:** e.g. eduID.cz
* **Enabled:** check the checkbox to enable the validator
* **Description:** e.g. eduID.cz metadata validator
* **URL of federation validator:** e.g. https://myhost.tld/validator/validator.php?
* **HTTP Method:** e.g. GET
* **Arg name where entity metadata will be assigned to:** e.g. filename
* **Optional args to be sent in POST/GET:** optional field
* **Args separator in URL (GET):** &
* **Expected document type in response:** xml (cannot be changed, only XML at this moment)

2. Response

* **Elements names containing return code:** e.g. returncode
* **Expected value for success:** e.g. 0
* **Expected value for warning:** e.g. 1
* **Expected value for error:** e.g. 2
* **Expected value for critical:** e.g. 3
* **Elements names containing message:** e.g. message info

In case you would like to try (use or tweak and then use) eduID.cz's `SAML-validator`_, read the `SAML-validator Wiki`_ page.

Validation Results
==================
A XML document sent back to JAGGER as a validation result has to be a well-formed XML document, i.e. all the elements (returncode, message and info as mentioned above) have to be inside a root-element, for example:

.. code:: xml

 <?xml version="1.0" encoding="utf-8"?>
 <validation>
    <returncode>0</returncode>
    <message>Lorem ipsum</message>
    <info>Lorem ipsum dolor sit amet...</info>
 </validation>

Metadata Validator Example
==========================
Metadata can be validated in a number of ways. `SAML-validator`_ grabs metadata (either uploaded from a local host or fetched from a URL address), process it and return a well-formed XML document. Of course, you can write your own validator and process metadata using a shell script, for example.

Frequently Asked Questions
==========================
| Q: I have defined more validators, but I can see just the first one and the others are hidden.
| A: Yes, that is right. It will be fixed soon.

.. _SAML-validator: https://github.com/JanOppolzer/saml-validator
.. _SAML-validator Wiki: https://github.com/JanOppolzer/saml-validator/wiki
