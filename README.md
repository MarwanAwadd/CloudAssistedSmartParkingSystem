# System Description

This project aims to facilitate the parking system for car drivers. This is done through displaying the
number of available slots before the car enters a parking lot. If there is no available slot, the car will not
be allowed to enter the parking lot. On the other hand, if there is an available one, the entry barrier to
the parking lot will open allowing the car to park. A light source is fixed beside each slot that is turned on
only if there is an available slot.

# Team Members
* Mohamed Elshabshiri
* Noha Abdelkader
* Salma Ahmed
* Marawan Awad
* Hoda Ahmed

# Hardware Components
* LCD I2C 16*2
* IR proximity sensors
* 5 LEDS
* STM32 nucleoboard
* Breadboard
* Jumper wires
* Esp32 board



![image](https://user-images.githubusercontent.com/51237986/164992148-370630ce-c941-4758-9457-1ebb62e6f7e0.png)
![image](https://user-images.githubusercontent.com/51237986/164992162-5d9e2a68-9f01-4e9e-a22f-64ab2b9bd19f.png)
![image](https://user-images.githubusercontent.com/51237986/164992182-185e2260-49f0-4253-bf3a-0b9615068f3b.png)
![image](https://user-images.githubusercontent.com/51237986/164992210-31e982f4-d5d3-48be-8f0f-bc58e49a3422.png)
![image](https://user-images.githubusercontent.com/51237986/164992218-e6c1d9ec-3aa2-426f-9fa8-ce12fd9790e4.png)
![image](https://user-images.githubusercontent.com/51237986/164992226-44ebd129-47d0-40c8-8099-af63b0a3d64b.png)
![image](https://user-images.githubusercontent.com/73145648/169067146-3869b607-a58f-4d78-bbaf-e9c291ee9236.png)


# Software Components
* STM32 CubeMX
* Keil uVision
* Arduino
* ESP32 Dev Kit


# System Design
<img width="610" alt="image" src="https://user-images.githubusercontent.com/73145648/169063067-25bb8e79-8fc0-4199-bdcb-f112339aedb0.png">


# Prototype 1 Update
We were able to hook up all IR sensors needed with a corresponding led output to each that's used as a parking space

# Prototype 2 Updates
We attached an LCD monitor module in order to show drivers when entering to park how many spaces are available for parking.

Used LCD:
LCD 1602A

![image](https://user-images.githubusercontent.com/73145648/169066475-68c5988e-4c35-4e3f-9e1a-726fcbe5c822.png)

Pin 1: connected to GND
Pin 2: connected to 5V
Pin3: connected to a 10k potentiometer to control the contrast
4 pins were used for data transmitting
The module has 2 modes of operation: 4 bit mode and 8 bit mode. For this project we used the 4 bit mode due to the limitation in number of pins.

# Final Demo
We added the last part of our project, a flutter based application that connects to a firebase firestore database that is mapped to our 3 parking spaces. When a parking space is available, the application shows a green spot for that space and red if the spot is taken.

Our Application UI:

![image](https://user-images.githubusercontent.com/73145648/169067718-6205490d-e661-42df-9501-badfe5e8007a.png)

What the firestore cloud database looks like:

<img width="944" alt="image" src="https://user-images.githubusercontent.com/73145648/169067611-a66262e1-d434-4855-a270-cc527c0f6ba9.png">

We then use an ESP32 that comes with a built in wifi module and a library to support it that allows us to send, receive and patch data from firebase firestore. We only need to specify which field is getting patched (which for our case is the Available field). Since the IR sensors are active low, when an obstacle is detected the input coming to the esp32 pin is set to low but when there is no collision with the IR sensor then the input is set to high. After we get the data from the IR sensor, we send it to firestore and only have to scroll down to refresh the application so that the positions would update.

# Challenges
The contrast of the LCD display module was too high so we used a potentiometer to solve this.

# Results
The set-up:
![image](https://user-images.githubusercontent.com/73145648/169069419-7fa703d3-94a2-40b8-8699-64c8bfd65197.png)
![image](https://user-images.githubusercontent.com/73145648/169069705-63b8ba84-709e-4d17-9488-f2b6231eed99.png)

----- Upload Video of test Here -----

# Future Work

* Add more parking spaces
* The app should be more dynamic and show number of free spaces as well as more than 3 spaces depending on parking slot
* Add a servo motor for gate (similar to gates at AUC that go up when someone enters)
