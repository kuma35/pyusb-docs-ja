:py:mod:`usb.util`
==================

.. py:module:: usb.util

usb.util - Utility functions.

This module exports:

- endpoint_address - return the endpoint absolute address.
- endpoint_direction - return the endpoint transfer direction.
- endpoint_type - return the endpoint type
- ctrl_direction - return the direction of a control transfer
- build_request_type - build a bmRequestType field of a control transfer.
- find_descriptor - find an inner descriptor.
- claim_interface - explicitly claim an interface.
- release_interface - explicitly release an interface.
- dispose_resources - release internal resources allocated by the object.
- get_langids - retrieve the list of supported string languages from the device.
- get_string - retrieve a string descriptor from the device.



Module Contents
---------------


Functions
~~~~~~~~~

- usb.util.endpoint_address
- usb.util.endpoint_direction
- usb.util.endpoint_type
- usb.util.ctrl_direction
- usb.util.build_request_type
- usb.util.create_buffer
- usb.util.find_descriptor
- usb.util.claim_interface
- usb.util.release_interface
- usb.util.dispose_resources
- usb.util.get_langids
- usb.util.get_string



Attributes
~~~~~~~~~~

.. py:data:: __author__
   :annotation: = Wander Lairson Costa

   

.. py:data:: DESC_TYPE_DEVICE
   :annotation: = 1

   

.. py:data:: DESC_TYPE_CONFIG
   :annotation: = 2

   

.. py:data:: DESC_TYPE_STRING
   :annotation: = 3

   

.. py:data:: DESC_TYPE_INTERFACE
   :annotation: = 4

   

.. py:data:: DESC_TYPE_ENDPOINT
   :annotation: = 5

   

.. py:data:: ENDPOINT_IN
   :annotation: = 128

   

.. py:data:: ENDPOINT_OUT
   :annotation: = 0

   

.. py:data:: ENDPOINT_TYPE_CTRL
   :annotation: = 0

   

.. py:data:: ENDPOINT_TYPE_ISO
   :annotation: = 1

   

.. py:data:: ENDPOINT_TYPE_BULK
   :annotation: = 2

   

.. py:data:: ENDPOINT_TYPE_INTR
   :annotation: = 3

   

.. py:data:: CTRL_TYPE_STANDARD
   

   

.. py:data:: CTRL_TYPE_CLASS
   

   

.. py:data:: CTRL_TYPE_VENDOR
   

   

.. py:data:: CTRL_TYPE_RESERVED
   

   

.. py:data:: CTRL_RECIPIENT_DEVICE
   :annotation: = 0

   

.. py:data:: CTRL_RECIPIENT_INTERFACE
   :annotation: = 1

   

.. py:data:: CTRL_RECIPIENT_ENDPOINT
   :annotation: = 2

   

.. py:data:: CTRL_RECIPIENT_OTHER
   :annotation: = 3

   

.. py:data:: CTRL_OUT
   :annotation: = 0

   

.. py:data:: CTRL_IN
   :annotation: = 128

   

.. py:data:: _ENDPOINT_ADDR_MASK
   :annotation: = 15

   

.. py:data:: _ENDPOINT_DIR_MASK
   :annotation: = 128

   

.. py:data:: _ENDPOINT_TRANSFER_TYPE_MASK
   :annotation: = 3

   

.. py:data:: _CTRL_DIR_MASK
   :annotation: = 128

   

.. py:data:: _dummy_s
   

   

.. py:data:: SPEED_LOW
   :annotation: = 1

   

.. py:data:: SPEED_FULL
   :annotation: = 2

   

.. py:data:: SPEED_HIGH
   :annotation: = 3

   

.. py:data:: SPEED_SUPER
   :annotation: = 4

   

.. py:data:: SPEED_UNKNOWN
   :annotation: = 0

   

.. py:function:: endpoint_address(address)

   Return the endpoint absolute address.

   The address parameter is the bEndpointAddress field
   of the endpoint descriptor.


.. py:function:: endpoint_direction(address)

   Return the endpoint direction.

   The address parameter is the bEndpointAddress field
   of the endpoint descriptor.
   The possible return values are ENDPOINT_OUT or ENDPOINT_IN.


.. py:function:: endpoint_type(bmAttributes)

   Return the transfer type of the endpoint.

   The bmAttributes parameter is the bmAttributes field
   of the endpoint descriptor.
   The possible return values are: ENDPOINT_TYPE_CTRL,
   ENDPOINT_TYPE_ISO, ENDPOINT_TYPE_BULK or ENDPOINT_TYPE_INTR.


.. py:function:: ctrl_direction(bmRequestType)

   Return the direction of a control request.

   The bmRequestType parameter is the value of the
   bmRequestType field of a control transfer.
   The possible return values are CTRL_OUT or CTRL_IN.


.. py:function:: build_request_type(direction, type, recipient)

   Build a bmRequestType field for control requests.

   These is a conventional function to build a bmRequestType
   for a control request.

   The direction parameter can be CTRL_OUT or CTRL_IN.
   The type parameter can be CTRL_TYPE_STANDARD, CTRL_TYPE_CLASS,
   CTRL_TYPE_VENDOR or CTRL_TYPE_RESERVED values.
   The recipient can be CTRL_RECIPIENT_DEVICE, CTRL_RECIPIENT_INTERFACE,
   CTRL_RECIPIENT_ENDPOINT or CTRL_RECIPIENT_OTHER.

   Return the bmRequestType value.


.. py:function:: create_buffer(length)

   Create a buffer to be passed to a read function.

   A read function may receive an out buffer so the data
   is read inplace and the object can be reused, avoiding
   the overhead of creating a new object at each new read
   call. This function creates a compatible sequence buffer
   of the given length.


.. py:function:: find_descriptor(desc, find_all=False, custom_match=None, **args)

   Find an inner descriptor.

   find_descriptor works in the same way as the core.find() function does,
   but it acts on general descriptor objects. For example, suppose you
   have a Device object called dev and want a Configuration of this
   object with its bConfigurationValue equals to 1, the code would
   be like so:

   >>> cfg = util.find_descriptor(dev, bConfigurationValue=1)

   You can use any field of the Descriptor as a match criteria, and you
   can supply a customized match just like core.find() does. The
   find_descriptor function also accepts the find_all parameter to get
   an iterator instead of just one descriptor.


.. py:function:: claim_interface(device, interface)

   Explicitly claim an interface.

   PyUSB users normally do not have to worry about interface claiming,
   as the library takes care of it automatically. But there are situations
   where you need deterministic interface claiming. For these uncommon
   cases, you can use claim_interface.

   If the interface is already claimed, either through a previously call
   to claim_interface or internally by the device object, nothing happens.


.. py:function:: release_interface(device, interface)

   Explicitly release an interface.

   This function is used to release an interface previously claimed,
   either through a call to claim_interface or internally by the
   device object.

   Normally, you do not need to worry about claiming policies, as
   the device object takes care of it automatically.


.. py:function:: dispose_resources(device)

   Release internal resources allocated by the object.

   Sometimes you need to provide deterministic resources
   freeing, for example to allow another application to
   talk to the device. As Python does not provide deterministic
   destruction, this function releases all internal resources
   allocated by the device, like device handle and interface
   policy.

   After calling this function, you can continue using the device
   object normally. If the resources will be necessary again, it
   will be allocated automatically.


.. py:function:: get_langids(dev)

   Retrieve the list of supported Language IDs from the device.

   Most client code should not call this function directly, but instead use
   the langids property on the Device object, which will call this function as
   needed and cache the result.

   USB LANGIDs are 16-bit integers familiar to Windows developers, where
   for example instead of en-US you say 0x0409. See the file USB_LANGIDS.pdf
   somewhere on the usb.org site for a list, which does not claim to be
   complete. It requires "system software must allow the enumeration and
   selection of LANGIDs that are not currently on this list." It also requires
   "system software should never request a LANGID not defined in the LANGID
   code array (string index = 0) presented by a device." Client code can
   check this tuple before issuing string requests for a specific language ID.

   dev is the Device object whose supported language IDs will be retrieved.

   The return value is a tuple of integer LANGIDs, possibly empty if the
   device does not support strings at all (which USB 3.1 r1.0 section
   9.6.9 allows). In that case client code should not request strings at all.

   A USBError may be raised from this function for some devices that have no
   string support, instead of returning an empty tuple. The accessor for the
   langids property on Device catches that case and supplies an empty tuple,
   so client code can ignore this detail by using the langids property instead
   of directly calling this function.


.. py:function:: get_string(dev, index, langid=None)

   Retrieve a string descriptor from the device.

   dev is the Device object which the string will be read from.

   index is the string descriptor index and langid is the Language
   ID of the descriptor. If langid is omitted, the string descriptor
   of the first Language ID will be returned.

   Zero is never the index of a real string. The USB spec allows a device to
   use zero in a string index field to indicate that no string is provided.
   So the caller does not have to treat that case specially, this function
   returns None if passed an index of zero, and generates no traffic
   to the device.

   The return value is the unicode string present in the descriptor, or None
   if the requested index was zero.


