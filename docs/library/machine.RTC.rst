.. currentmodule:: machine
.. _machine.RTC:

class RTC -- real time clock
============================

The RTC is and independent clock that keeps track of the date
and time.

Example usage::

    rtc = machine.RTC()
    rtc.init((2014, 5, 1, 4, 13, 0, 0, 0))
    print(rtc.now())


Constructors
------------

.. class:: RTC(id=0, ...)

   Create an RTC object. See init for parameters of initialization.

Methods
-------

.. method:: RTC.init(datetime)

   Initialise the RTC. Datetime is a tuple of the form:

      ``(year, month, day[, hour[, minute[, second[, microsecond[, tzinfo]]]]])``

.. method:: RTC.now()

   Get get the current datetime tuple.

.. method:: RTC.deinit()

   Resets the RTC to the time of January 1, 2015 and starts running it again.

.. method:: RTC.alarm(id, time, *, repeat=False)

   Set the RTC alarm. Time might be either a millisecond value to program the alarm to
   current time + time_in_ms in the future, or a datetimetuple. If the time passed is in
   milliseconds, repeat can be set to ``True`` to make the alarm periodic.

.. method:: RTC.alarm_left(alarm_id=0)

   Get the number of milliseconds left before the alarm expires.

.. method:: RTC.cancel(alarm_id=0)

   Cancel a running alarm.

.. method:: RTC.irq(*, trigger, handler=None, wake=machine.IDLE)

   Create an irq object triggered by a real time clock alarm.

      - ``trigger`` must be ``RTC.ALARM0``
      - ``handler`` is the function to be called when the callback is triggered.
      - ``wake`` specifies the sleep mode from where this interrupt can wake
        up the system.

.. method:: RTC.memory([data])

   Stores ``data`` (byte literal) into RTC memory, which is kept stored in deep sleep mode of the ESP8266 or ESP32.
   The data is stored together with a magic word to detect that the RTC memory is valid.
   An uninitialized or cleared RTC memory has no magic word and will deliver ``b''``.
   Without ``data`` the method delivers the RTC memory content.
   In the ESP8266 are max. 492 bytes and in the ESP32 are max. 2048 Bytes storeable by this method. 
   
   Example::

      import machine
      rtc = machine.RTC()
      writedata = b'test'
      rtc.memory(writedata) # this command writes writedata into the RTC memory
      readdata = rtc.memory() # this command puts the RTC memory into readdata
      print(readdata)

   Availability: ESP8266, ESP32

Constants
---------

.. data:: RTC.ALARM0

    irq trigger source
