# BirdAttractor

## RTC
### DS1305
has two alarms, each alarm must be reset by a read or write to the Alarm interrupt register. Must use an MCU to do this.
The INT0 and INT1 interrupt output pins are pulled low, so when the alarm asserts, we have to have a pull-up resistor to bring the value up.
It is likely the INT0 and INT1 pins may not be able to sink enough current to have a small pull up resistor. So with a larger value pull up resistor, the provided current on alarm assertion will be small as well. To magnify this current, a MOSFET may be needed.

### DS3231
has two alarms


## Relay
### V23079
latching, bistable, relay


## MCU
### ESP8266
Allows us to have a Wi-Fi interface for setting the time and other settings.
Runs on 3.3V, so should have an LDO or similar to bring down the 5V supply.
Should only be turned in two instances. First is to creating the Wi-Fi interface. Second is at an alarm, to turn off the alarm, and then shut itself down. If we use deep sleep, then we could check every 5 minutes (or less) to see if the alarm pin is pulled high.
It might be possible to use the reset pin on the ESP8266 to wake it up with the alarm. This would be more power efficient and have better reaction time (within milliseconds) to the alarm assertion, but the solution is more complex and takes longer to develop.


