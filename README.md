# TITTLE:
 Smart Irrigation System using IOT Project

## ABSTRACT:
The key objective of this project is to monitor the soil’s moisture content during its dry and wet conditions with the aid of a moisture sensor circuit, calculate the corresponding relative humidity and irrigate it based on its nature using Arduino, Soil moisture sensor, Ultrasonic sensor, GSM and an automatic water inlet setup which can also monitor and record temperature, which is constantly modified and can be controlled in future to optimize these resources so that the plant growth and yield is maximized.

## INTRODUCTION:
Aim is to develop a smart irrigation system to provide irrigation system which is automatic for the plants which help in saving water and money. Fields should neither be over-irrigated nor under-irrigated. The objective of this thesis is to design a simple, easy to install methodology to monitor and indicate the level of soil moisture that is continuously controlled in order to achieve maximum plant growth.

The Arduino UNO can be programmed to analyze some signals from sensors such as moisture, temperature, and rain. A pump is used to pump the fertilizer and water into the irrigation system. The use of easily available components reduces the manufacturing and maintenance costs.
## LITERATURE REVIEW:
In [1], the paper emphasizes about the essentiality of water for human beings, plants and animals. The key aim of the paper is to reduce human intervention to reduce percentage water  wastage  in  agricultural  farms  using  a  water  level controller  with  wireless  technology.  The  paper  has  said about the development of 4 stages of water pumping system. The paper has also compared between the wired and wireless Bluetooth based water level controller. They have used an Ultrasonic sensor, Arduino uno microcontroller, pump, relay and Bluetooth module HC-12. The controller decides unique code for  water level based on  4 stages  of water pumping. Distance  is  calculated  using  formula d=S*(T/2)=0.03435*(T/2), where S is speed of sound, T is duration of transmission and reception of sound wave from an  ultrasonic  sensor.  S=0.003435  cm/microsecond.  
The paper  also displays  drawbacks of  wired controller,  which includes  limited  wire  length,  which  paved  way  for introducing wireless automatic water level controller. In [2], the paper says about the issue due to excessive water usage in the domestic or commercial purposes, which in turn may  lead to  further problems  like problem  with weather patterns.  The paper  has said  about  the development  of a system  comprising  of  a  water  level  sensor,  digital  logic processing  unit  or integrated  circuit(IC),  for input  signal processing,  7  segment  display,  JK  flip  flop  sequential circuit, motor driver controlled by relay. The data from the water  level  sensor  is  encoded  using  a  digital  encoding circuit, where water level is encoded to decimal, indicating the water  level from 0  to 9. 
The  decimal is then  decoded from BCD to 7 segment using BCD to 7 segment decoder (IC7447).  Digital  logic  controller,  responsible  for  the turning on or off of the pump, turns the pump whenever the water level reaches ONE, and turns off when it reaches level NINE. A JK flip flop is used as a driver circuit to turn on or off the motor. Relay is used as a switch, which turns on the International Journal of Engineering Research & Technology (IJERT)ISSN: 2278-0181http://www.ijert.orgIJERTV9IS070458 (This work is licensed under a Creative Commons Attribution 4.0 International License.)Published by :www.ijert.orgVol. 9 Issue 07, July-20201092 motor and also turns it  off whenever the tank reaches full capacity.
## PROPOSED METHODLOGY:
Internet of Things with ESP8266
The Internet of Things has two keywords, internet and
things. Internet, which stands for interconnectionnetworking, is a network of the computer that connect to each
other using TCP/IP (Transmission Control Protocol/ Internet
Protocol).
Things in the Internet of Things are the object that we use
daily where the information of that things retriever from
sensors that read environment around in real time without
human intervention. Such as room temperature, humidity,
and pressure.
So Internet of Things means objects that can generate data
through sensors and the data sent to the server or computer
via the internet connection. The Internet of Things is also very
closely related to the communication Machine to Machine
(M2M) that can communicate without any human
intervention in it [1]. Internet of Things is also the first step
in making Smart World where mixing of data from objects
and smart city [2]. The Internet of Things has 3 crucial
component:
1. A Hardware that consist of sensors, actuators,
microcontroller and communication device.
2. A Middleware that consists of data storage a data
analytic capability.
3. A presentation that consist of easy understand
visualization data from middleware and provide useful
information.
Firstly the Ultra Sonic sensor reads the level of water tank, converts it into scale of 100 and sends the data to Arduino.
Similar for Soil moisture sensor. It reads the water content of soil, converts it into 100 and sends the data to Arduino.
In Arduino it analyses the data received from UltraSonic sensor and Soil moisture sensor.
Arduino operates their respective Motors as per their threshold levels of Water tank level and Soil moisture.
Prints the Output in LCD.
## CIRCUIT DIAGRAM:
![project](https://github.com/Jeganvjk/Simulation-project/assets/132189820/8f51cf41-0f96-442b-af1c-59b8795cddce)

## PROGRAM:
 #include<LiquidCrystal.h></br>
#define echo 9</br>
#define trigger 10</br>
#define tank_pump 4</br>
#define watering_pump 13</br>
#define moisture_sensor A0</br>
long duration;</br>
int distance;</br>
int moisture_value;</br>
int distance_percent;</br>
int moist_percent;</br>
LiquidCrystal lcd(12,11,8,7,6,5);</br>

void setup () {</br>
lcd.begin(20,4);</br>
pinMode(echo,INPUT);</br>
pinMode(moisture_sensor,INPUT);</br>
pinMode(trigger,OUTPUT);</br>
digitalWrite(trigger,LOW);</br>
pinMode(watering_pump,OUTPUT);</br>
pinMode(tank_pump,OUTPUT);</br>
digitalWrite(watering_pump,LOW);</br>
digitalWrite(tank_pump,LOW);</br>
lcd.setCursor(0,1);</br>
lcd.print(" Fully Automated "    );</br>
lcd.setCursor(0,2);</br>
lcd.print("    Water Pumping"    );</br>
lcd.setCursor(0,3);</br>
lcd.print("      System");</br>
delay(500);</br>
lcd.clear(); </br>
}</br>


void loop(){</br>

 // LEVEL SENSOR</br>
 digitalWrite(trigger,LOW);</br>
 delayMicroseconds(2);</br>
 digitalWrite(trigger,HIGH);</br>
 delayMicroseconds(10); </br>
 digitalWrite(trigger,LOW);</br>
 duration=pulseIn(echo,HIGH);</br>
 distance=duration*0.017; </br>
 distance_percent=map( distance,0,1023,0,100);</br>
 moisture_value= analogRead(moisture_sensor);</br>
moist_percent=map(moisture_value,0,1023,0,100);</br>
 condition();</br>
}</br>
void condition(){</br>
if (distance_percent>65 &&moist_percent<85){</br>
LCD_3();</br>
digitalWrite(tank_pump,LOW);</br>
digitalWrite(watering_pump,HIGH);</br>
delay(500);</br>
}</br>
else if (distance_percent<65 &&moist_percent>85)</br>
{</br>
LCD_2();</br>
digitalWrite(tank_pump,HIGH);</br>
digitalWrite(watering_pump,LOW);</br>

delay(500);</br>
}</br>
else if (distance_percent>65 &&moist_percent>85)</br>
{</br>

LCD_4();</br>
digitalWrite(tank_pump,LOW);</br>
digitalWrite(watering_pump,LOW);</br>
delay(500);</br>

}</br>

else if (distance_percent<65 &&moist_percent<85)</br>
{</br>
LCD_1();</br>
digitalWrite(tank_pump,HIGH);</br>
digitalWrite(watering_pump,HIGH);</br>
delay(500);</br>

}</br>
}</br>

  void LCD_1()</br>
  {</br>
  lcd.clear();</br>
  lcd.setCursor(0,0);</br>
  lcd.print("TANK LEVEL=  ");</br>
  lcd.print(distance_percent);</br>
  lcd.print("%");</br>
  lcd.setCursor(0,1);</br>
  lcd.print("MOIST CONTENT= ");</br>
  lcd.print(moist_percent);</br>
  lcd.print("%");</br>
   lcd.setCursor(0,2);</br>
  lcd.print("W-PUMP STATUS  ");</br>
  lcd.print("  ON");</br>
  lcd.setCursor(0,3);</br>
  lcd.print("T-PUMP STATUS  ");</br>
  lcd.print("  ON");</br>
  }</br>

void LCD_2(){</br>
  lcd.clear();</br>
  lcd.setCursor(0,0);</br>
   lcd.print("TANK LEVEL=  ");</br>
  lcd.print(distance_percent);</br>
  lcd.print("%");</br>
  lcd.setCursor(0,1);</br>
  lcd.print("MOIST CONTENT= ");</br>
  lcd.print(moist_percent);</br>
  lcd.print("%");</br>
   lcd.setCursor(0,2);</br>
  lcd.print("W-PUMP STATUS ");</br>
  lcd.print("  OFF");</br>
  lcd.setCursor(0,3);</br>
  lcd.print("T-PUMP STATUS ");</br>
  lcd.print("   ON");</br>
  }</br>
  void LCD_3(){</br>
  lcd.clear();</br>
  lcd.setCursor(0,0);</br>
   lcd.print("TANK LEVEL=  ");</br>
  lcd.print(distance_percent);</br>
  lcd.print("%");</br>
  lcd.setCursor(0,1);</br>
  lcd.print("MOIST CONTENT= ");</br>
  lcd.print(moist_percent);</br>
  lcd.print("%");</br>
   lcd.setCursor(0,2);</br>
  lcd.print("W-PUMP STATUS ");</br>
  lcd.print("  ON");</br>
  lcd.setCursor(0,3);</br>
  lcd.print("T-PUMP STATUS ");</br>
  lcd.print("  OFF");</br>
  }</br>

  void LCD_4(){</br>
  lcd.clear();</br>
  lcd.setCursor(0,0);</br>
   lcd.print("TANK LEVEL=  ");</br>
  lcd.print(distance_percent);</br>
  lcd.print("%");</br>
  lcd.setCursor(0,1);</br>
  lcd.print("MOIST CONTENT= ");</br>
  lcd.print(moist_percent);</br>
  lcd.print("%");</br>
   lcd.setCursor(0,2);</br>
  lcd.print("W-PUMP STATUS");</br>
  lcd.print("  OFF");</br>
  lcd.setCursor(0,3);</br>
  lcd.print("T-PUMP STATUS");</br>
  lcd.print("  OFF");</br>
  }</br>
## RESULTS:
![out](https://github.com/Jeganvjk/Simulation-project/assets/132189820/6c500a57-e009-4f94-8590-f82b6e8b37fe)

## CONCLUSION:
This project presented a new design of water pump
control for the development of smart irrigation system
linked with a mobile application. The developed irrigation
system supports the farmers to save wasted water, time
and effort to increase the productivity of their crops.
In the future work of this project, case studies of
different crops will be used, and also automatic
measuring the level of the water the tank to alert the
farmers.Finally, applying the developed
automatic irrigation system in the farms of india
## REFERENCE:
[1] "Sensor based Automated Irrigation System with IOT", International Journal
of Computer Science and Information Technologies, vol. 6, no. 6, pp. 5331-
5333, 2015.

[2] Major Agricultural Problems of India and their Possible Solutions Article
shared by: Puja Mondal, www.yourarticlelibrary.com

[3] Shiraz Pasha B.R., Dr. B Yogesha, “Microcontroller Based Automated
Irrigation System”, the International Journal of Engineering and Science
(IJES), Volume3, Issue 7, pp 06-09, June 2014.

[4] IoT based smart irrigation system using soil moisture sensor and ESP 8266
Node MCU by Abhiiemanyu Pandit, 15th July – 2015.

[5] N. A. Z. M. Noar, M. M. Kamal, "The development of smart flood
monitoring system using ultrasonic sensor with Blynk applications", 2017

[6] P.Rajalakshmi, Devi Mahalashmi (2016) “IOT based crop-field monitoring
and irrigation automation”10th International Conference on Intelligent
Systems and Control (ISCO).IEEE Press. Year: 2016.

[7] Dr.P.Sukumar.Ph.D.S.Akshaya, D.Chandrika, R.Dhilipkumar, “IOT based
agriculture crop-field monitoring system and irrigation Automation”2018.

[8] Shrinidhi Rajagopal; Vallidevi Krishnamurthy OO design for an IoT based
automated plant watering system, 2017 International Conference on
Computer, Communication and Signal Processing (ICCCSP) Year: 2017.

[9] Liu, C. et al., 2011. The Application of Soil Temperature Measurement by
Temperature Sensors. Proceedings of 2011 International Conference on
Electronic & Mechanical Engineering and Information Technology.

[10] Water Level Detection System Based on Ultrasonic Sensors HC-SR04 and
ESP8266-12 Modules Hanan, Anak Agung Ngurah Gunawan, Made
Sumadiyasa, Department of Physics, University of Udayana at Bali,
Indonesia

