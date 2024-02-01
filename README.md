# Submersion-Module-Test-Plan
# System Power

1. Test Case 1: 3V3 Rail with USB:
	* *Description*:  Verify that 3V3 rail is functional when powered from USB
	* Setup: Attach Micro-USB cable. 
	* Steps: Probe 3V3 rail, 
	* Expected Result: Voltage between 2.9-3.4 
2. Test Case 2: 3V3 Rail with LiPO Battery:
	* Description: Verify that 3V3 rail is functional when powered from battery
	   * Setup: Attach LiPO battery to microJST header
	   * Probe 3V3 rail 
	   * Expected Result: Voltage between 2.9-3.4
3. Test Case 3: V_GPS Rail enabling
	* *Description*: Assert PICO-D4 can enable VGPS rail
	* Setup: Power on System (USB or Battery), 
		* Inject test script that turns on GPS_Control Pin
		* Pause execution
		* Probe VGPS rail 
	* Expected Result: Between 2.4 -3.2 Voltage on VGPS

# Unit (USB-Interface)

1. Test  Case 1:  USB Device
	* *Description:* Check that USB interface is operating correctly and Host can detect device with CP2102 Driver
	* Setup:  Insert Micro-USB cable from Host PC to Submersion Module 
	* Expected Result: Windows/Linux (CP2102 Serial Port is visiable with driver available)
* Test Case 2: USB-Serial Reset/Flash
	* *Description*: Check that Host can issue soft reset of target (ESP32-PicoD4) via CP2102 and can flash basic program
	* Setup: Insert Micro-USB cable from Host PC to submerison module
		 ```idf.py build flash monitor```

	* Expected Result: esp-idf automatically resets and loads application
# Unit (Submersion Sensor)

* Test Case 1: Verify Submersion Module Toggle 
	* *Description*: Verify Submersion module toggles wake. 
	* Setup: Power on from either battery or USB
	* Load submersion-module application
	* Force Submersion module switch (move switch)
	* Expected Result:  wake state is visible on serial output

# Unit (ESP-NOW Interface)
* Test Case 1: ESP-NOW Functionality
	* *Description*: Verify ESP-NOW RF system is functional
	* Setup: Power on system from either battery or USB
	* Load esp-now example to submersion module and peer link partner
	* Expected Result: Packets RX and TX


# Unit (GPS Interface)

* Test Case 1: GPS RF Functionality
	* *Description*: Verify NEO-7M Module is alive and able to lock on satellite
	* Setup: Power on system from either battery or USB
	* Ensure system is outside with direct LoS to sky
	* Enable VPGS Rail
	* Wait for 30 seconds
	* Expected Result: GPS LED indicator is on
	
*  Test Case 2: GPS UART RX Functionality
	* *Description*: Verify NEO-7M Module is alive and able to transmit GPS information to ESP32-PIco
	* Setup: Power on system from either battery or USB
	* Ensure system is outside with direct LoS to sky
	* Enable VPGS Rail
	* Start NMEA event handler on PICO-D4
	* Wait for 30 seconds
	* Expected Result: GPS LED indicator is on, UART event with NMEA packets. GPS coordinates corresponding to verified location

## Benchmarking
* Battery Life 
	* LiPO Battery
		* During Sleep
		* During Wake
	   * CR2032 Battery
		   * During Sleep
		   * During Wake
* GPS 
	* Link up time
	* Power consumption
	* Range
* ESP-NOW
	* Range 

