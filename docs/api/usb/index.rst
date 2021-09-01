:py:mod:`usb`
=============

.. py:module:: usb

PyUSB - Easy USB access in Python

This package exports the following modules and subpackages:

- :doc:`core/index` - the main USB implementation
- :doc:`legacy/index` - the compatibility layer with 0.x version
- :doc:`backend/index` - the support for backend implementations.
- :doc:`control/index` - USB standard control requests.
- :doc:`libloader/index` - helper module for backend library loading.

Since version 1.0, main PyUSB implementation lives in the 'usb.core'
module. New applications are encouraged to use it.



Subpackages
-----------
.. toctree::
   :titlesonly:
   :maxdepth: 3

   backend/index.rst


Submodules
----------
.. toctree::
   :titlesonly:
   :maxdepth: 1

   _debug/index.rst
   _interop/index.rst
   _lookup/index.rst
   _objfinalizer/index.rst
   control/index.rst
   core/index.rst
   legacy/index.rst
   libloader/index.rst
   util/index.rst


