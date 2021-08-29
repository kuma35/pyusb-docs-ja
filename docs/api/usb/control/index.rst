:py:mod:`usb.control`
=====================

.. py:module:: usb.control

usb.control - USB standard control requests

This module exports:

- get_status - get recipeint status
- clear_feature - clear a recipient feature
- set_feature - set a recipient feature
- get_descriptor - get a device descriptor
- set_descriptor - set a device descriptor
- get_configuration - get a device configuration
- set_configuration - set a device configuration
- get_interface - get a device interface
- set_interface - set a device interface



Module Contents
---------------


Functions
~~~~~~~~~

- usb.control.get_status
- usb.control.clear_feature
- usb.control.set_feature
- usb.control.get_descriptor
- usb.control.set_descriptor
- usb.control.get_configuration
- usb.control.set_configuration
- usb.control.get_interface
- usb.control.set_interface



Attributes
~~~~~~~~~~

- usb.control.ENDPOINT_HALT
- usb.control.FUNCTION_SUSPEND
- usb.control.DEVICE_REMOTE_WAKEUP
- usb.control.U1_ENABLE
- usb.control.U2_ENABLE
- usb.control.LTM_ENABLE


.. py:data:: ENDPOINT_HALT
   :annotation: = 0

   

.. py:data:: FUNCTION_SUSPEND
   :annotation: = 0

   

.. py:data:: DEVICE_REMOTE_WAKEUP
   :annotation: = 1

   

.. py:data:: U1_ENABLE
   :annotation: = 48

   

.. py:data:: U2_ENABLE
   :annotation: = 49

   

.. py:data:: LTM_ENABLE
   :annotation: = 50

   

.. py:function:: get_status(dev, recipient=None)

   Return the status for the specified recipient.

   dev is the Device object to which the request will be
   sent to.

   The recipient can be None (on which the status will be queried
   from the device), an Interface or Endpoint descriptors.

   The status value is returned as an integer with the lower
   word being the two bytes status value.


.. py:function:: clear_feature(dev, feature, recipient=None)

   Clear/disable a specific feature.

   dev is the Device object to which the request will be
   sent to.

   feature is the feature you want to disable.

   The recipient can be None (on which the status will be queried
   from the device), an Interface or Endpoint descriptors.


.. py:function:: set_feature(dev, feature, recipient=None)

   Set/enable a specific feature.

   dev is the Device object to which the request will be
   sent to.

   feature is the feature you want to enable.

   The recipient can be None (on which the status will be queried
   from the device), an Interface or Endpoint descriptors.


.. py:function:: get_descriptor(dev, desc_size, desc_type, desc_index, wIndex=0)

   Return the specified descriptor.

   dev is the Device object to which the request will be
   sent to.

   desc_size is the descriptor size.

   desc_type and desc_index are the descriptor type and index,
   respectively. wIndex index is used for string descriptors
   and represents the Language ID. For other types of descriptors,
   it is zero.


.. py:function:: set_descriptor(dev, desc, desc_type, desc_index, wIndex=None)

   Update an existing descriptor or add a new one.

   dev is the Device object to which the request will be
   sent to.

   The desc parameter is the descriptor to be sent to the device.
   desc_type and desc_index are the descriptor type and index,
   respectively. wIndex index is used for string descriptors
   and represents the Language ID. For other types of descriptors,
   it is zero.


.. py:function:: get_configuration(dev)

   Get the current active configuration of the device.

   dev is the Device object to which the request will be
   sent to.

   This function differs from the Device.get_active_configuration
   method because the later may use cached data, while this
   function always does a device request.


.. py:function:: set_configuration(dev, bConfigurationNumber)

   Set the current device configuration.

   dev is the Device object to which the request will be
   sent to.


.. py:function:: get_interface(dev, bInterfaceNumber)

   Get the current alternate setting of the interface.

   dev is the Device object to which the request will be
   sent to.


.. py:function:: set_interface(dev, bInterfaceNumber, bAlternateSetting)

   Set the alternate setting of the interface.

   dev is the Device object to which the request will be
   sent to.


