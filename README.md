# BirdAttractor

## Requirements
- 5V Power input from in USB-B female form
- Two 5V Power output in USB-A female form
- Relay to control flow of at least 2A. Possibly more current support for better generalization. Most usb battery chargers are 2A, but some do 3A or 4A.
- Transistors to ensure relay coils trigger from MCU pins. ESP8266 can only drive 12mA on GPIO pins. Relays need >20mA.
 
- Ability to put microcontroller into deep sleep, waking up every 15 seconds to check for updates.
- Infinite alarms for super customization. Not interrupt based, only 15 second accuracy, due to deep sleep wakeup cycle.
- Ability to set the wakeup cycle from 1 second to 5 minutes. ESP8266 GPIO16 pulls CH-DP low during deep sleep. Anything that pulls 
 
- Microcontroller Interrupts for wakeup from deep sleep. ESP8266 can do this from the RTC on GPIO16 connected to reset.
- Two daily alarms for on and off settings. Interrupt based. The alarm interrupt on DS3231 only pulls down to 3mA, so it might need a transistor to boost the current capability to overcome the GPIO16 high signal when in deep_sleep.
 
- FTDI header pins with TX,RX,GND,5V for programming (could be removed if we can program using pogo pins and the firmware is completely debugged).
- Button to control Reset for programming. Button should ideally be hardware debounced, but could probably work without it. ESP8266 needs to pull Reset low, and then GPIO0 low to enter programming mode.
 
- Button to activate Wi-Fi for configuration.
- LED to notify users that the Wi-Fi is on. Should draw less than 12mA.
- LED to show that power is coming in. Should draw less than 12mA.
- LED to show that output power is switched on. Should draw less than 12mA.
 
- Voltage regulator to bring down 5V input to 3.3V for electronics. Should have decoupling capacitors to smooth the supply.
 
- Photoresistor to detect the amount of light for use as a trigger.
- Ability to configure light based alarm. Five minute response time is sufficient.
 
- Real Time Clock with a temperature compensated crystal oscillator (TCXO).
- Real Time Clock with sub 0C and very high temperature range with high accuracy.
- Ability to set the timezone on the RTC.
- Ability to push time from Wi-Fi connected device onto the MCU to update the RTC.
 
---------------
## LED
- Blue LED
- 150080BS75000
- Package:0805
- Forward Voltage: 3.2V
- Max Current: 20mA
- Current Limiting Resistor at 12mA: 16.6 ohms (E12=18 ohms or 22 ohms)
- $0.29@1, digi-key
- $0.23@100, digi-key

---------------
## RTC

### DS1305
- Arduino Library: https://github.com/cjbearman/ds1305-arduino
- Alarms:2
- has two alarms, each alarm must be reset by a read or write to the Alarm interrupt register. Must use an MCU to do this.
- The INT0 and INT1 interrupt output pins are pulled low, so when the alarm asserts, we have to have a pull-up resistor to bring the value up.
- It is likely the INT0 and INT1 pins may not be able to sink enough current to have a small pull up resistor. So with a larger value pull up resistor, the provided current on alarm assertion will be small as well. To magnify this current, a MOSFET may be needed.

### DS1307
- Arduino Library: DS1307RTC, Rtc by Makuna, RTCx 
- TXCO:No, not accurate enough

### DS3231
-Arduino Library: Rtc by Makuna, Sodaq_DS3231
#### DS3231SN
- has temperature compensated crystal oscillator (may need this for cold temps)
- TCXO:Yes
- Alamrs:2
- $9.97@1, digi-key
- $6.59@100, digi-key
- $2.50@10, aliexpress
#### DS3231M
- TCXO: unclear
- $6.46@1, digi-key
- $4.801@50, digi-key

### PCF2129
- TCXO:yes
- Arduino Library: FaBo 215 RTC PCF2129
#### PCF2129T
- Package:16-SOIC
- Temp:-30C to +80C
- $3.36@1, digi-key
- $2.47@100, digi-key
#### PCF2129AT
- Package:20-SOIC, similar as 16-SOIC but with 4 NC pins
- Temp:-15C to +60C
- $2.92@1, digi-key
- $2.15@100, digi-key

### PCF2127
- TXCO:Yes
- Arduino Library: I2C-Sensor-Lib iLib
- includes 512 bytes of general-purpose static RAM
#### PCF2127T
- Package:16-SOIC
- Temp:-30C to +80C
- $4.01@1, digi-key
- $2.95@100, digi-key
#### PCF2127AT
- Package:20-SOIC
- Temp:-15C to +60C
- $3.60@1, digi-key
- $2.65@100, digi-key
 
### PCA2129
- Arduino Library: None Found
- TXCO:Yes
#### PCA2129T
- Package:16-SOIC
- Temp:-30C to +80C
- $4.70@1, digi-key
- $3.46@100, digi-key

### MCP79400
- TXCO:No
- Arduino Library: RTCx (includes MCP7941x)
- accuracy potentially better than ds1307 and pcf8563, but not ds3231
- $0.82@1, digi-key
- $0.72@100, digi-key


---------------
## Relay
- latching, dual coil, bistable
- contact current: 2,3-10 Amps (2A seems an industry threshold)
- coil voltage: 3.3V,5V
- coil current: <100mA
- switching voltage: >5VDC

### V23079
- Current:2A
#### V23079-E1201-B301
- Signal Volage:3.75V-5V
- Signal Current:28mA
- Latching:Yes
- Bistable:Yes
- $3.69@1, digi-key
- $2.77@100, digi-key
#### V23079-A1001-B301
- $5.17@10, aliexpress
- Monstable:Yes
- Bistable:No
- standard coil, coil 001
- standard version, 2 form C contacts

### TX2SA
#### TX2SA-LT-5V-TH-Z
- Signal Volage:5V
- Signal Current:28.1mA
- Current:2A
- $5.83@1, digi-key
- $4.38@100, digi-key

### G6BK (5A, twice as expensive as 2A)
#### G6BK-1114P-US-DC5
- Signal Voltage:5V
- Signal Current:56mA
- Current:5A
- $7.61@1, digi-key
- $5.71@100, digi-key

### AQV25
- Type:solid state
### AQV251G
- Package:6-DIP
- Current:3.5A
- Voltage:0-30V
- $7.75@1, digi-key
- $5.85@100, digi-key
### AQV252G
- Package:6-SOIC
- Current:2.5A
- Voltage:0-60V
#### AQV252GAX
- Tape and Reel packaging on 123 pin side
- $5.39@1, digi-key
- $4.04@100, digi-key
#### AQV252GAZ
- Tape and Reel packaging on 456 pin side
#### AQV252GA
- Tube packing style


---------------
## Coin Cell Retainer/Holder
- Battery:CR2032
- Battery Diameter:20mm
### BU2032
#### BU2032-1-HD-G
- Type:through hole holder
- $0.83@1, digi-key
- $0.69@100, digi-key
#### BU2032SM-HD-G
- Type:surface mount holder
- $0.87@1, digi-key
- $0.76@100, digi-key
### BK
#### BK-913
- Type:through hole retainer
- Notes:easy replacement
- $0.35@1, digi-key
- $0.30@100, digi-key
#### BK-888
- Type:through hole retainer
- blocks inner side
- easy replacement
- $0.39@1, digi-key
- $0.33@100, digi-key

---------------
## LDO
- needed for running the esp8266 microprocessor
### AMS1117-3.3
- Package:SOT-223
- $1.58@50, aliexpress

---------------
## MCU
### ESP8266
- Wi-Fi:Yes
- Allows us to have a Wi-Fi interface for setting the time and other settings.
- VCC:3.3V
- Runs on 3.3V, so should have an LDO or similar to bring down the 5V supply.
- Should only be turned in two instances. First is to creating the Wi-Fi interface. Second is at an alarm, to turn off the alarm, and then shut itself down. If we use deep sleep, then we could check every 5 minutes (or less) to see if the alarm pin is pulled high.
- It might be possible to use the reset pin on the ESP8266 to wake it up with the alarm. This would be more power efficient and have better reaction time (within milliseconds) to the alarm assertion, but the solution is more complex and takes longer to develop. https://github.com/esp8266/Arduino/issues/1488
- pin mapping: http://www.esp8266.com/wiki/doku.php?id=esp8266_gpio_pin_allocations


