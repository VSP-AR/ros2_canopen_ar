Cia402 Driver
========================

The Cia402 Driver implements the CIA402 profile for motion controllers and enables setting
the drive status, operation mode and sending target values to the motion controller.


Services
--------

.. list-table::
  :widths: 30 20 50
  :header-rows: 1
  :align: left

  * - Services
    - Type
    - Description
  * - ~/nmt_reset_node
    - Trigger
    - Resets CANopen Device the Proxy Device Node manages.
  * - ~/sdo_read
    - CORead
    - Reads an SDO object from the specified index, subindex and datatype of the remote device.
  * - ~/sdo_write
    - COWrite
    - Writes data to an SDO object on the specified index, subindex and datatype of the remote device.
  * - ~/init
    - Trigger
    - Initialises motion controller including referencing
  * - ~/recover
    - Trigger
    - Recovers motion controller
  * - ~/halt
    - Trigger
    - Stops motion controller
  * - ~/position_mode
    - Trigger
    - Switches to profiled position mode
  * - ~/velocity_mode
    - Trigger
    - Switches to profiled velocity mode
  * - ~/torque_mode
    - Trigger
    - Switches to profiled torque mode
  * - ~/cyclic_position_mode
    - Trigger
    - Switches to cyclic position mode
  * - ~/cyclic_velocity_mode
    - Trigger
    - Switches to cyclic velocity mode
  * - ~/interpolated_position_mode
    - Trigger
    - Switches to interpolated position mode, only linear mode with fixed time is supported
  * - ~/target
    - CODouble
    - Sets the target value. Only accepted when an operation mode is set.

Publishers
----------
.. list-table::
  :widths: 30 20 50
  :header-rows: 1
  :align: left

  * - Publishers
    - Type
    - Description
  * - ~/joint_states
    - sensor_msgs/msg/JointState
    - Joint states of the drive


Subscribers
-----------

.. list-table::
  :widths: 30 20 50
  :header-rows: 1

  * - Topic
    - Type
    - Description
  * - ~/target
    - COTargetDouble
    - Sets target value.

Bus Configuration Parameters
----------------------------
Additional parameters that can be used in bus.yml for this driver.


.. list-table::
  :widths: 30 20 50
  :header-rows: 1

  * - Parameter
    - Type
    - Description
  * - switching_state
    - see below
    - The state to switch the operation mode in.
  * - scale_pos_to_dev
    - double
    - Scaling factor to convert from SI units to device units for position.
  * - scale_vel_to_dev
    - double
    - Scaling factor to convert from SI units to device units for velocity.
  * - scale_pos_from_dev
    - double
    - Scaling factor to convert from device units to SI units for position.
  * - scale_vel_from_dev
    - double
    - Scaling factor to convert from device units to SI units for velocity.

.. note::

  Selecting poll timer:

  - When following is added to a node in bus.yaml, the driver will use the ros2 timer to poll the drive status. Polling using ros2 timer is default. However, it is not recommended.

    .. code-block:: yaml

      polling: true
      period: 10 # ms

      [or]

      polling: true # default period is 10ms

  - When following is added to a node in bus.yaml, the driver will use the CANopen SYNC message to poll the drive status.

    .. code-block:: yaml

      polling: false

  For more information on bus configuration parameters refer to bus configuration.
