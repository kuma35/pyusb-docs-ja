:py:mod:`usb.legacy`
====================

.. py:module:: usb.legacy


Module Contents
---------------

Classes
~~~~~~~

- usb.legacy.Endpoint
- usb.legacy.Interface
- usb.legacy.Configuration
- usb.legacy.DeviceHandle
- usb.legacy.Device
- usb.legacy.Bus


Functions
~~~~~~~~~

- usb.legacy.busses


Attributes
~~~~~~~~~~

.. py:data:: __author__
   :annotation: = Wander Lairson Costa

   

.. py:data:: USBError
   

   

.. py:data:: CLASS_AUDIO
   :annotation: = 1

   

.. py:data:: CLASS_COMM
   :annotation: = 2

   

.. py:data:: CLASS_DATA
   :annotation: = 10

   

.. py:data:: CLASS_HID
   :annotation: = 3

   

.. py:data:: CLASS_HUB
   :annotation: = 9

   

.. py:data:: CLASS_MASS_STORAGE
   :annotation: = 8

   

.. py:data:: CLASS_PER_INTERFACE
   :annotation: = 0

   

.. py:data:: CLASS_PRINTER
   :annotation: = 7

   

.. py:data:: CLASS_VENDOR_SPEC
   :annotation: = 255

   

.. py:data:: DT_CONFIG
   :annotation: = 2

   

.. py:data:: DT_CONFIG_SIZE
   :annotation: = 9

   

.. py:data:: DT_DEVICE
   :annotation: = 1

   

.. py:data:: DT_DEVICE_SIZE
   :annotation: = 18

   

.. py:data:: DT_ENDPOINT
   :annotation: = 5

   

.. py:data:: DT_ENDPOINT_AUDIO_SIZE
   :annotation: = 9

   

.. py:data:: DT_ENDPOINT_SIZE
   :annotation: = 7

   

.. py:data:: DT_HID
   :annotation: = 33

   

.. py:data:: DT_HUB
   :annotation: = 41

   

.. py:data:: DT_HUB_NONVAR_SIZE
   :annotation: = 7

   

.. py:data:: DT_INTERFACE
   :annotation: = 4

   

.. py:data:: DT_INTERFACE_SIZE
   :annotation: = 9

   

.. py:data:: DT_PHYSICAL
   :annotation: = 35

   

.. py:data:: DT_REPORT
   :annotation: = 34

   

.. py:data:: DT_STRING
   :annotation: = 3

   

.. py:data:: ENDPOINT_ADDRESS_MASK
   :annotation: = 15

   

.. py:data:: ENDPOINT_DIR_MASK
   :annotation: = 128

   

.. py:data:: ENDPOINT_IN
   :annotation: = 128

   

.. py:data:: ENDPOINT_OUT
   :annotation: = 0

   

.. py:data:: ENDPOINT_TYPE_BULK
   :annotation: = 2

   

.. py:data:: ENDPOINT_TYPE_CONTROL
   :annotation: = 0

   

.. py:data:: ENDPOINT_TYPE_INTERRUPT
   :annotation: = 3

   

.. py:data:: ENDPOINT_TYPE_ISOCHRONOUS
   :annotation: = 1

   

.. py:data:: ENDPOINT_TYPE_MASK
   :annotation: = 3

   

.. py:data:: ERROR_BEGIN
   :annotation: = 500000

   

.. py:data:: MAXALTSETTING
   :annotation: = 128

   

.. py:data:: MAXCONFIG
   :annotation: = 8

   

.. py:data:: MAXENDPOINTS
   :annotation: = 32

   

.. py:data:: MAXINTERFACES
   :annotation: = 32

   

.. py:data:: RECIP_DEVICE
   :annotation: = 0

   

.. py:data:: RECIP_ENDPOINT
   :annotation: = 2

   

.. py:data:: RECIP_INTERFACE
   :annotation: = 1

   

.. py:data:: RECIP_OTHER
   :annotation: = 3

   

.. py:data:: REQ_CLEAR_FEATURE
   :annotation: = 1

   

.. py:data:: REQ_GET_CONFIGURATION
   :annotation: = 8

   

.. py:data:: REQ_GET_DESCRIPTOR
   :annotation: = 6

   

.. py:data:: REQ_GET_INTERFACE
   :annotation: = 10

   

.. py:data:: REQ_GET_STATUS
   :annotation: = 0

   

.. py:data:: REQ_SET_ADDRESS
   :annotation: = 5

   

.. py:data:: REQ_SET_CONFIGURATION
   :annotation: = 9

   

.. py:data:: REQ_SET_DESCRIPTOR
   :annotation: = 7

   

.. py:data:: REQ_SET_FEATURE
   :annotation: = 3

   

.. py:data:: REQ_SET_INTERFACE
   :annotation: = 11

   

.. py:data:: REQ_SYNCH_FRAME
   :annotation: = 12

   

.. py:data:: TYPE_CLASS
   :annotation: = 32

   

.. py:data:: TYPE_RESERVED
   :annotation: = 96

   

.. py:data:: TYPE_STANDARD
   :annotation: = 0

   

.. py:data:: TYPE_VENDOR
   :annotation: = 64

   

.. py:class:: Endpoint(ep)

   Bases: :py:obj:`object`

   Endpoint descriptor object.


.. py:class:: Interface(intf)

   Bases: :py:obj:`object`

   Interface descriptor object.


.. py:class:: Configuration(cfg)

   Bases: :py:obj:`object`

   Configuration descriptor object.


.. py:class:: DeviceHandle(dev)

   Bases: :py:obj:`usb._objfinalizer.AutoFinalizedObject`

   .. py:method:: _finalize_object(self)


   .. py:method:: bulkWrite(self, endpoint, buffer, timeout=100)

      Perform a bulk write request to the endpoint specified.

      :param endpont: endpoint number.
      :param buffer: sequence data buffer to write. 
                     This parameter can be any sequence type.
      :param timeout: operation timeout in milliseconds.
		      (default: 100)
      :return: the number of bytes written.


   .. py:method:: bulkRead(self, endpoint, size, timeout=100)

      Performs a bulk read request to the endpoint specified.

      :param endpoint: endpoint number.
      :param size: number of bytes to read.
      :param timeout: operation timeout in milliseconds.
		      (default: 100)
      :return: a tuple with the data read.


   .. py:method:: interruptWrite(self, endpoint, buffer, timeout=100)

      Perform a interrupt write request to the endpoint specified.

      :param endpoint: endpoint number.
      :param buffer: sequence data buffer to write.
                     This parameter can be any sequence type.
      :param timeout: operation timeout in milliseconds.
		      (default: 100)
      :return: the number of bytes written.


   .. py:method:: interruptRead(self, endpoint, size, timeout=100)

      Performs a interrupt read request to the endpoint specified.

      :param endpoint: endpoint number.
      :param size: number of bytes to read.
      :param timeout: operation timeout in milliseconds.
		      (default: 100)
      :return: a tuple with the data read.


   .. py:method:: controlMsg(self, requestType, request, buffer, value=0, index=0, timeout=100)

      Perform a control request to the default control pipe on a device.

      :param requestType: specifies the direction of data flow,
			  the type of request, and the recipient.
      :param request: specifies the request.
      :param buffer: if the transfer is a write transfer,
		     buffer is a sequence with the transfer data,
		     otherwise, buffer is the number of bytes to read.
      :param value: specific information to pass to the device. (default: 0)
      :param index: specific information to pass to the device. (default: 0)
      :param timeout: operation timeout in milliseconds. (default: 100)
      :return: the number of bytes written.


   .. py:method:: clearHalt(self, endpoint)

      Clears any halt status on the specified endpoint.

      :param endpoint: endpoint number.


   .. py:method:: claimInterface(self, interface)

      Claims the interface with the Operating System.

      :param interface: interface number or an Interface object.


   .. py:method:: releaseInterface(self)

      Release an interface previously claimed with claimInterface.


   .. py:method:: reset(self)

      Reset the specified device by sending a RESET
      down the port it is connected to.


   .. py:method:: resetEndpoint(self, endpoint)

      Reset all states for the specified endpoint.

      :param endpoint: endpoint number.


   .. py:method:: setConfiguration(self, configuration)

      Set the active configuration of a device.

      :param configuration: a configuration value or a Configuration object.


   .. py:method:: setAltInterface(self, alternate)

      Sets the active alternate setting of the current interface.

      :param alternate: an alternate setting number or an Interface object.


   .. py:method:: getString(self, index, length, langid=None)

      Retrieve the string descriptor specified by index
          and langid from a device.

      :param index: index of descriptor in the device.
      :param length: number of bytes of the string (ignored)
      :param langid: Language ID. If it is omitted,
		     the first language will be used.


   .. py:method:: getDescriptor(self, desc_type, desc_index, length, endpoint=-1)

      Retrieves a descriptor from the device identified by the type
      and index of the descriptor.

      :param desc_type: descriptor type.
      :param desc_index: index of the descriptor.
      :param len: descriptor length.
      :param endpoint: ignored.


   .. py:method:: detachKernelDriver(self, interface)

      Detach a kernel driver from the interface (if one is attached,
          we have permission and the operation is supported by the OS)

      :param interface: interface number or an Interface object.



.. py:class:: Device(dev)

   Bases: :py:obj:`object`

   Device descriptor object

   .. py:method:: open(self)

      Open the device for use.

      :return: a DeviceHandle object



.. py:class:: Bus(devices)

   Bases: :py:obj:`object`

   Bus object.


.. py:function:: busses()

   :return: a tuple with the usb busses.


