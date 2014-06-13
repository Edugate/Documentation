Federation Metadata Validators
******************************
This document describes metadata validators in JAGGER.

About Validators
================
When an entity, for example a Service Provider (SP), should be joined to a federation, you may use external validators to check metadata of such an entity before asking to join the federation. Using this technique, the person asking to join the SP to the federation can find out if metadata are correct or contains all the required information within.

Adding a Validator
==================
To add (or edit) federation validators go to ``Federations``, choose a desired federation and click on ``Validators`` tab.

1. General

* **Federation validator name:** e.g. ext-scope
* **Enabled:** check the checkbox to enable the validator
* **Description:** e.g. External ext-scope (Extensions/Scope) validator 
* **URL of federation validator:** e.g. https://myhost.tld/validator/ext-scope.php?
* **HTTP Method:** e.g. GET
* **Arg name where entity metadata will be assigned to:** e.g. from
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
Metadata can be validated in a number of ways. In the example below, a shell script is executed by a PHP script. Depending on the exit code of the shell script a PHP script generates a XML document as an answer.

.. code:: php

 <?php
 $command = "./ext-scope.sh $_GET[from]";
 exec($command, $output, $returncode);

 if($returncode == 0) {
    echo "<?xml version=\"1.0\" encoding=\"utf-8\"?>\n";
    echo "<validation>\n";
    echo "\t<returncode>0</returncode>\n";
    echo "\t<message>Element 'shibmd:Scope' present.</message>\n";
    echo "</validation>\n";
 } elseif($returncode == 1) {
    echo "<?xml version=\"1.0\" encoding=\"utf-8\"?>\n";
    echo "<validation>\n";
    echo "\t<returncode>1</returncode>\n";
    echo "\t<message>";
    foreach ($output as $output_line)
        echo $output_line;
    echo "</message>\n";
    echo "\t<info>Element 'shibmd:Scope' is missing! For more info, see https://myhost.tld/metadata/ext-scope</info>\n";
    echo "</validation>\n";
 }
 ?>

Frequently Asked Questions
==========================
| Q: I have defined more validators, but I can see just the first one and the others are hidden.
| A: Yes, that is right. It will be fixed soon.

