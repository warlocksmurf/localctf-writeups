# Task 1: Water Sensor 
Question: 
```
ZX Company has released their brand new water sensing Arduino-based device. This innovative system is designed to detect the presence or absence of water using various sensors connected to an Arduino microcontroller board. The device typically includes one or more types of water sensors, such as resistive or capacitive sensors, which are capable of detecting changes in conductivity or capacitance when in contact with water. This advanced technology allows for accurate and reliable water detection, making it suitable for various applications ranging from flood detection to irrigation system management.

The Arduino board serves as the central processing unit, receiving input from the water sensors and executing programmed logic to interpret the sensor data and trigger appropriate actions or alerts. This can include activating pumps to remove water, sounding alarms to warn of flooding, or sending notifications to a connected device or network. This water sensor device consists of a memory size of 700MB. Every 1 minutes, it will respectively load a new set of data without clearing the old one. This allows for continuous monitoring and storage of water sensor readings over time. The device may also incorporate additional components such as relays, actuators, and communication modules (e.g., Wi-Fi, GSM) to enable more advanced functionality or remote monitoring capabilities.

Overall, this water sensing Arduino device provides a cost-effective and customizable solution for monitoring and managing water levels in various applications, including flood detection, irrigation systems, and leak detection in buildings.

Can you hack the device physically and look for any bugs according to info given?
```

Flag: RWSC{ILUVU1337}

Reading the question, it seems that we have to perform buffer overflow on the sensor since the memory can only hold 700 MB and it loads a new set of data every minute without clearing the old one. So we placed the water sensor for 7 minutes so that the memory will keep loading until it crashes. After it crashes, the flag can be obtained.

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/6b6599b5-820c-4541-96fd-1241f57cb912)
