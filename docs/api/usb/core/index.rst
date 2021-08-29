:py:mod:`usb.core`
==================

.. py:module:: usb.core

usb.core - Core USB features.

This module exports:

- Device - a class representing a USB device.
- Configuration - a class representing a configuration descriptor.
- Interface - a class representing an interface descriptor.
- Endpoint - a class representing an endpoint descriptor.
- find() - a function to find USB devices.
- show_devices() - a function to show the devices present.



Module Contents
---------------

Classes
~~~~~~~

- usb.core.Endpoint
- usb.core.Interface
- usb.core.Configuration
- usb.core.Device



Functions
~~~~~~~~~

- usb.core.find
- usb.core.show_devices

.. py:exception:: USBError(strerror, error_code=None, errno=None)

   Bases: :py:obj:`OSError`

   Exception class for USB errors.

   Backends must raise this exception when USB related errors occur.  The
   backend specific error code is available through the 'backend_error_code'
   member variable.


.. py:exception:: USBTimeoutError(strerror, error_code=None, errno=None)

   Bases: :py:obj:`USBError`

   Exception class for connection timeout errors.

   Backends must raise this exception when a call on a USB connection returns
   a timeout error code.


.. py:exception:: NoBackendError

   Bases: :py:obj:`ValueError`

   Exception class when a valid backend is not found.


.. py:class:: Endpoint(device, endpoint, interface=0, alternate_setting=0, configuration=0)

   Bases: :py:obj:`object`

   Represent an endpoint object.

   This class contains all fields of the Endpoint Descriptor according to the
   USB Specification. You can access them as class properties. For example, to
   access the field bEndpointAddress of the endpoint descriptor, you can do so:

   >>> import usb.core
   >>> dev = usb.core.find()
   >>> for cfg in dev:
   >>>     for i in cfg:
   >>>         for e in i:
   >>>             print e.bEndpointAddress

   .. py:method:: __repr__(self)

      Return repr(self).


   .. py:method:: __str__(self)

      Return str(self).


   .. py:method:: write(self, data, timeout=None)

      Write data to the endpoint.

      The parameter data contains the data to be sent to the endpoint and
      timeout is the time limit of the operation. The transfer type and
      endpoint address are automatically inferred.

      The method returns the number of bytes written.

      For details, see the Device.write() method.


   .. py:method:: read(self, size_or_buffer, timeout=None)

      Read data from the endpoint.

      The parameter size_or_buffer is either the number of bytes to
      read or an array object where the data will be put in and timeout is the
      time limit of the operation. The transfer type and endpoint address
      are automatically inferred.

      The method returns either an array object or the number of bytes
      actually read.

      For details, see the Device.read() method.


   .. py:method:: clear_halt(self)

      Clear the halt/status condition of the endpoint.


   .. py:method:: _str(self)



.. py:class:: Interface(device, interface=0, alternate_setting=0, configuration=0)

   Bases: :py:obj:`object`

   Represent an interface object.

   This class contains all fields of the Interface Descriptor
   according to the USB Specification. You may access them as class
   properties. For example, to access the field bInterfaceNumber
   of the interface descriptor, you can do so:

   >>> import usb.core
   >>> dev = usb.core.find()
   >>> for cfg in dev:
   >>>     for i in cfg:
   >>>         print i.bInterfaceNumber

   .. py:method:: __repr__(self)

      Return repr(self).


   .. py:method:: __str__(self)

      Show all information for the interface.


   .. py:method:: endpoints(self)

      Return a tuple of the interface endpoints.


   .. py:method:: set_altsetting(self)

      Set the interface alternate setting.


   .. py:method:: __iter__(self)

      Iterate over all endpoints of the interface.


   .. py:method:: __getitem__(self, index)

      Return the Endpoint object in the given position.


   .. py:method:: _str(self)


   .. py:method:: _get_full_descriptor_str(self)



.. py:class:: Configuration(device, configuration=0)

   Bases: :py:obj:`object`

   Represent a configuration object.

   This class contains all fields of the Configuration Descriptor according to
   the USB Specification. You may access them as class properties.  For
   example, to access the field bConfigurationValue of the configuration
   descriptor, you can do so:

   >>> import usb.core
   >>> dev = usb.core.find()
   >>> for cfg in dev:
   >>>     print cfg.bConfigurationValue

   .. py:method:: __repr__(self)

      Return repr(self).


   .. py:method:: __str__(self)

      Return str(self).


   .. py:method:: interfaces(self)

      Return a tuple of the configuration interfaces.


   .. py:method:: set(self)

      Set this configuration as the active one.


   .. py:method:: __iter__(self)

      Iterate over all interfaces of the configuration.


   .. py:method:: __getitem__(self, index)

      Return the Interface object in the given position.

      index is a tuple of two values with interface index and
      alternate setting index, respectivally. Example:

      >>> interface = config[(0, 0)]


   .. py:method:: _str(self)


   .. py:method:: _get_full_descriptor_str(self)



.. py:class:: Device(dev, backend)

   Bases: :py:obj:`usb._objfinalizer.AutoFinalizedObject`

   Device object.

   This class contains all fields of the Device Descriptor according to the
   USB Specification. You may access them as class properties.  For example,
   to access the field bDescriptorType of the device descriptor, you can
   do so:

   >>> import usb.core
   >>> dev = usb.core.find()
   >>> dev.bDescriptorType

   Additionally, the class provides methods to communicate with the hardware.
   Typically, an application will first call the set_configuration() method to
   put the device in a known configured state, optionally call the
   set_interface_altsetting() to select the alternate setting (if there is
   more than one) of the interface used, and call the write() and read()
   methods to send and receive data, respectively.

   When working in a new hardware, the first try could be like this:

   >>> import usb.core
   >>> dev = usb.core.find(idVendor=myVendorId, idProduct=myProductId)
   >>> dev.set_configuration()
   >>> dev.write(1, 'test')

   This sample finds the device of interest (myVendorId and myProductId should
   be replaced by the corresponding values of your device), then configures
   the device (by default, the configuration value is 1, which is a typical
   value for most devices) and then writes some data to the endpoint 0x01.

   Timeout values for the write, read and ctrl_transfer methods are specified
   in miliseconds. If the parameter is omitted, Device.default_timeout value
   will be used instead. This property can be set by the user at anytime.

   .. py:attribute:: default_timeout
      

      

   .. py:method:: __repr__(self)


   .. py:method:: __str__(self)


   .. py:method:: configurations(self)

      Return a tuple of the device configurations.


   .. py:method:: langids(self)
      :property:

      Return the USB device's supported language ID codes.

      These are 16-bit codes familiar to Windows developers, where for
      example instead of en-US you say 0x0409. USB_LANGIDS.pdf on the usb.org
      developer site for more info. String requests using a LANGID not
      in this array should not be sent to the device.

      This property will cause some USB traffic the first time it is accessed
      and cache the resulting value for future use.


   .. py:method:: serial_number(self)
      :property:

      Return the USB device's serial number string descriptor.

      This property will cause some USB traffic the first time it is accessed
      and cache the resulting value for future use.


   .. py:method:: product(self)
      :property:

      Return the USB device's product string descriptor.

      This property will cause some USB traffic the first time it is accessed
      and cache the resulting value for future use.


   .. py:method:: parent(self)
      :property:

      Return the parent device. 


   .. py:method:: manufacturer(self)
      :property:

      Return the USB device's manufacturer string descriptor.

      This property will cause some USB traffic the first time it is accessed
      and cache the resulting value for future use.


   .. py:method:: backend(self)
      :property:

      Return the backend being used by the device.


   .. py:method:: set_configuration(self, configuration=None)

      Set the active configuration.

      The configuration parameter is the bConfigurationValue field of the
      configuration you want to set as active. If you call this method
      without parameter, it will use the first configuration found.  As a
      device hardly ever has more than one configuration, calling the method
      without arguments is enough to get the device ready.


   .. py:method:: get_active_configuration(self)

      Return a Configuration object representing the current
      configuration set.


   .. py:method:: set_interface_altsetting(self, interface=None, alternate_setting=None)

      Set the alternate setting for an interface.

      When you want to use an interface and it has more than one alternate
      setting, you should call this method to select the appropriate
      alternate setting. If you call the method without one or the two
      parameters, it will be selected the first one found in the Device in
      the same way of the set_configuration method.

      Commonly, an interface has only one alternate setting and this call is
      not necessary. For most devices, either it has more than one
      alternate setting or not, it is not harmful to make a call to this
      method with no arguments, as devices will silently ignore the request
      when there is only one alternate setting, though the USB Spec allows
      devices with no additional alternate setting return an error to the
      Host in response to a SET_INTERFACE request.

      If you are in doubt, you may want to call it with no arguments wrapped
      by a try/except clause:

      >>> try:
      >>>     dev.set_interface_altsetting()
      >>> except usb.core.USBError:
      >>>     pass


   .. py:method:: clear_halt(self, ep)

      Clear the halt/stall condition for the endpoint ep.


   .. py:method:: reset(self)

      Reset the device.


   .. py:method:: write(self, endpoint, data, timeout=None)

      Write data to the endpoint.

      This method is used to send data to the device. The endpoint parameter
      corresponds to the bEndpointAddress member whose endpoint you want to
      communicate with.

      The data parameter should be a sequence like type convertible to
      the array type (see array module).

      The timeout is specified in miliseconds.

      The method returns the number of bytes written.


   .. py:method:: read(self, endpoint, size_or_buffer, timeout=None)

      Read data from the endpoint.

      This method is used to receive data from the device. The endpoint
      parameter corresponds to the bEndpointAddress member whose endpoint
      you want to communicate with. The size_or_buffer parameter either
      tells how many bytes you want to read or supplies the buffer to
      receive the data (it *must* be an object of the type array).

      The timeout is specified in miliseconds.

      If the size_or_buffer parameter is the number of bytes to read, the
      method returns an array object with the data read. If the
      size_or_buffer parameter is an array object, it returns the number
      of bytes actually read.


   .. py:method:: ctrl_transfer(self, bmRequestType, bRequest, wValue=0, wIndex=0, data_or_wLength=None, timeout=None)

      Do a control transfer on the endpoint 0.

      This method is used to issue a control transfer over the endpoint 0
      (endpoint 0 is required to always be a control endpoint).

      The parameters bmRequestType, bRequest, wValue and wIndex are the same
      of the USB Standard Control Request format.

      Control requests may or may not have a data payload to write/read.
      In cases which it has, the direction bit of the bmRequestType
      field is used to infer the desired request direction. For
      host to device requests (OUT), data_or_wLength parameter is
      the data payload to send, and it must be a sequence type convertible
      to an array object. In this case, the return value is the number
      of bytes written in the data payload. For device to host requests
      (IN), data_or_wLength is either the wLength parameter of the control
      request specifying the number of bytes to read in data payload, and
      the return value is an array object with data read, or an array
      object which the data will be read to, and the return value is the
      number of bytes read.


   .. py:method:: is_kernel_driver_active(self, interface)

      Determine if there is kernel driver associated with the interface.

      If a kernel driver is active, the object will be unable to perform
      I/O.

      The interface parameter is the device interface number to check.


   .. py:method:: detach_kernel_driver(self, interface)

      Detach a kernel driver.

      If successful, you will then be able to perform I/O.

      The interface parameter is the device interface number to detach the
      driver from.


   .. py:method:: attach_kernel_driver(self, interface)

      Re-attach an interface's kernel driver, which was previously
      detached using detach_kernel_driver().

      The interface parameter is the device interface number to attach the
      driver to.


   .. py:method:: __iter__(self)

      Iterate over all configurations of the device.


   .. py:method:: __getitem__(self, index)

      Return the Configuration object in the given position.


   .. py:method:: _finalize_object(self)


   .. py:method:: __get_timeout(self, timeout)


   .. py:method:: __set_def_tmo(self, tmo)


   .. py:method:: __get_def_tmo(self)


   .. py:method:: _str(self)


   .. py:method:: _get_full_descriptor_str(self)



.. py:function:: find(find_all=False, backend=None, custom_match=None, **args)

   Find an USB device and return it.

   find() is the function used to discover USB devices.  You can pass as
   arguments any combination of the USB Device Descriptor fields to match a
   device. For example:

   .. code-block:: python
   
      find(idVendor=0x3f4, idProduct=0x2009)

   will return the Device object for the device with idVendor field equals
   to 0x3f4 and idProduct equals to 0x2009.

   If there is more than one device which matchs the criteria, the first one
   found will be returned. If a matching device cannot be found the function
   returns None. If you want to get all devices, you can set the parameter
   find_all to True, then find will return an iterator with all matched devices.
   If no matching device is found, it will return an empty iterator. Example:

   .. code-block:: python

      for printer in find(find_all=True, bDeviceClass=7):
          print (printer)

   This call will get all the USB printers connected to the system.  (actually
   may be not, because some devices put their class information in the
   Interface Descriptor).

   You can also use a customized match criteria:

   .. code-block:: python

      dev = find(custom_match = lambda d: d.idProduct=0x3f4 and d.idvendor=0x2009)

   A more accurate printer finder using a customized match would be like
   so:

   .. code-block:: python

      def is_printer(dev):
          import usb.util
          if dev.bDeviceClass == 7:
              return True
          for cfg in dev:
              if usb.util.find_descriptor(cfg, bInterfaceClass=7) is not None:
                  return True

      for printer in find(find_all=True, custom_match = is_printer):
          print (printer)


   Now even if the device class code is in the interface descriptor the
   printer will be found.

   You can combine a customized match with device descriptor fields. In this
   case, the fields must match and the custom_match must return True. In the
   our previous example, if we would like to get all printers belonging to the
   manufacturer 0x3f4, the code would be like so:

   .. code-block:: python

      printers = list(find(find_all=True, idVendor=0x3f4, custom_match=is_printer))

   If you want to use find as a 'list all devices' function, just call
   it with find_all = True:

   devices = list(find(find_all=True))

   Finally, you can pass a custom backend to the find function:

   find(backend = MyBackend())

   PyUSB has builtin backends for libusb 0.1, libusb 1.0 and OpenUSB.  If you
   do not supply a backend explicitly, find() function will select one of the
   predefineds backends according to system availability.

   Backends are explained in the usb.backend module.


.. py:function:: show_devices(verbose=False, **kwargs)

   Show information about connected devices.

   The verbose flag sets to verbose or not.
   \*\*kwargs are passed directly to the find() function.


