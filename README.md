# BirdAttractor

## RTC

### DS1305
Arduino Library: https://github.com/cjbearman/ds1305-arduino
has two alarms, each alarm must be reset by a read or write to the Alarm interrupt register. Must use an MCU to do this.
The INT0 and INT1 interrupt output pins are pulled low, so when the alarm asserts, we have to have a pull-up resistor to bring the value up.
It is likely the INT0 and INT1 pins may not be able to sink enough current to have a small pull up resistor. So with a larger value pull up resistor, the provided current on alarm assertion will be small as well. To magnify this current, a MOSFET may be needed.

### DS1307
Arduino Library: DS1307RTC, Rtc by Makuna, RTCx 
not accurate enough

### DS3231
Arduino Library: Rtc by Makuna, Sodaq_DS3231
#### DS3231SN
has temperature compensated crystal oscillator (may need this for cold temps)
 TCXO/Crystal	
has two alarms
$9.97@1, digi-key
$6.59@100, digi-key
#### DS3231
unclear if it has TCXO
$6.46@1, digi-key
$4.801@50, digi-key


### PCF2129*
TCXO
Arduino Library: FaBo 215 RTC PCF2129
#### PCF2129AT
20-SOIC, same as 16-SOIC but with 4 NC pins
$2.92@1, digi-key
$2.15@100, digi-key
#### PCF2129T
16-SOIC
$3.36@1, digi-key
$2.47@100, digi-key

### PCF2127
TXCO
Arduino Library: I2C-Sensor-Lib iLib
includes 512 bytes of general-purpose static RAM
#### PCF2127AT
20-SOIC
$3.60@1, digi-key
$2.65@100, digi-key
#### PCF2127T
16-SOIC
$4.01@1, digi-key
$2.95@100, digi-key

### PCA2129
Arduino Library: None Found
#### PCA2129T
16-SOIC
$4.70@1, digi-key
$3.46@100, digi-key

### MCP79400
Arduino Library: RTCx (includes MCP7941x)
accuracy potentially better than ds1307 and pcf8563
$0.82@1, digi-key
$0.72@100, digi-key



## Relay
latching, dual coil, bistable
contact current: 2,3-10 Amps (2A seems an industry threshold)
coil voltage: 3.3V,5V
coil current: <100mA
switching voltage: >5VDC


### V23079
2A
#### V23079-E1201-B301
5V,28mA
latching
bistable
$3.69@1, digi-key
$2.77@100, digi-key
#### V23079-A1001-B301
$5.17@10, aliexpress
monostable, standard coil, coil 001
standard version, 2 form C contacts

### TX2SA
#### TX2SA-LT-5V-TH-Z
5V, 28.1mA
2A
$5.83@1, digi-key
$4.38@100, digi-key

### G6BK (5A, twice as expensive as 2A)
#### G6BK-1114P-US-DC5
5V, 56mA
5A
$7.61@1, digi-key
$5.71@100, digi-key

### AQV25
solid state
### AQV251G
6-DIP
3.5A
0-30V
$7.75@1, digi-key
$5.85@100, digi-key
### AQV252G
6-SOIC
2.5A
0-60V
#### AQV252GAX
Tape and Reel packaging on 123 pin side
$5.39@1, digi-key
$4.04@100, digi-key
#### AQV252GAZ
Tape and Reel packaging on 456 pin side
#### AQV252GA
Tube packing style



## Coin Cell Retainer/Holder
CR2032
20mm diameter
### BU2032
#### BU2032-1-HD-G
through hole holder
$0.83@1, digi-key
$0.69@100, digi-key
#### BU2032SM-HD-G
surface mount holder
$0.87@1, digi-key
$0.76@100, digi-key
### BK
#### BK-913
through hole retainer
easy replacement
$0.35@1, digi-key
$0.30@100, digi-key
#### BK-888
through hole retainer
blocks inner side
easy replacement
$0.39@1, digi-key
$0.33@100, digi-key


## LDO
needed for running the esp8266 microprocessor
### AMS1117-3.3
SOT-223
$1.58@50, aliexpress

## MCU
### ESP8266
Allows us to have a Wi-Fi interface for setting the time and other settings.
Runs on 3.3V, so should have an LDO or similar to bring down the 5V supply.
Should only be turned in two instances. First is to creating the Wi-Fi interface. Second is at an alarm, to turn off the alarm, and then shut itself down. If we use deep sleep, then we could check every 5 minutes (or less) to see if the alarm pin is pulled high.
It might be possible to use the reset pin on the ESP8266 to wake it up with the alarm. This would be more power efficient and have better reaction time (within milliseconds) to the alarm assertion, but the solution is more complex and takes longer to develop.


