Helper functions
*****************

.. _base64url_encode:

base64url_encode
----------------

Helper function in file *${RR3}/application/helpers/url_encoder_helper.php*
This modified base64_encode to get working with codeigniter.

.. code:: php

 function base64url_encode($plainText)
 {
    $base64 = base64_encode($plainText);
    $base64url = strtr($base64, '+/=', '-_~');
    return $base64url;
 }


.. _base64url_decode:

base64url_decode
----------------

Helper function in file *${RR3}/application/helpers/url_encoder_helper.php*
Oposite to base64url_encode

.. code:: php

 function base64url_decode($encoded)
 {
    $base64 = strtr($encoded,'-_~','+/=');
    $plainText = base64_decode($base64);
    return $plainText;
 }

