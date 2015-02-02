.. JAGGER - Guide documentation master file, created by
   sphinx-quickstart on Sat Aug 15 22:25:12 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Jagger - Administration guide! (Draft) - updated: 2015/02/02
=====================================

.. note::
 
 The documentation is not final version yet.

 It means there is still missing content.

 If section title has **(final)** means it's complete - if any mistake fill the bug


.. note:: updating in progress

.. warning:: 
 if you updated Codeigniter code and Jagger, please make sure have changed 

 from $config['sess_driver'] = 'native'; 

 to   $config['sess_driver'] = 'files';


Contents:


Installation, configuration ...
################################

.. toctree::
   :maxdepth: 3

   installation.rst
   configfile.rst
   langs.rst
   authentication.rst
   update.rst
   metadata.rst
   metadatasigner.rst
   gearman.rst
   notifications.rst

Userguide
#########

.. toctree::
   :maxdepth: 2

   register.rst
   entitydetails.rst
   validators.rst
   

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

