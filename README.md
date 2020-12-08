# IOT-Project-Major
 Major Project (Vehicle Accident Detection Syatem)
Introduction
Nowadays lots of accidents happen on highways due to increase in traffic and also due to the rash driving of the drivers. And in many situations, the family members of the ambulance and police authority are not informed in time. This result in delaying the help reached to the person who suffered due to an accident. Our project Vehicle Accident Detection with GPS, GSM and Heartbeat Sensor is designed to avoid such situations.
Components Required:
	Arduino Uno (Microcontroller)
	GSM Module 
	GPS Module (Neo 6m)
	Heartbeat Sensor
	16x2 LCD
	Power Supply
	Connecting Wires
	10 K-POT
	Breadboard or PCB
	Power supply 12v 1amp
Before going into Project, we will discuss about GPS, GSM and Heartbeat Sensor.
GPS Module and Its Working:
GPS stands for Global Positioning System and used to detect the Latitude and Longitude of any location on the Earth, with exact UTC time (Universal Time Coordinated). GPS module is used to track the location of accident in our project. This device receives the coordinates from the satellite for each and every second, with time and date. We have previously extracted $GPGGA string in Vehicle Tracking System to find the Latitude and Longitude Coordinates.
GPS module sends the data related to tracking position in real time, and it sends so many data in NMEA format (see the screenshot below). NMEA format consist several sentences, in which we only need one sentence. This sentence starts from $GPGGA and contains the coordinates, time and other useful information. This GPGGA is referred to Global Positioning System Fix Data. Know more about NMEA sentences and reading GPS data here.
We can extract coordinate from $GPGGA string by counting the commas in the string. Suppose you find $GPGGA string and stores it in an array, then Latitude can be found after two commas and Longitude can be found after four commas. Now, this latitude and longitude can be put in other arrays.
 
Serial Monitor Reading
Below is the $GPGGA String, along with its description:
$GPGGA,104534.000,7791.0381,N,06727.4434,E,1,08,0.9,510.4,M,43.9,M,,*47
$GPGGA,HHMMSS.SSS,latitude,N,longitude,E,FQ,NOS,HDP,altitude,M,height,M,,checksum data
Identifier	Description
$GPGGA	Global Positioning system fix data
HHMMSS.SSS	Time in hour minute seconds and milliseconds format.
Latitude	Latitude (Coordinate)
N	Direction N=North, S=South
Longitude	Longitude(Coordinate)
E	Direction E= East, W=West
FQ	Fix Quality Data
NOS	No. of Satellites being Used
HDP	Horizontal Dilution of Precision
Altitude	Altitude (meters above from sea level)
M	Meter
Height	Height
Checksum	Checksum Data

GSM Module:
The SIM900 is a complete Quad-band GSM/GPRS Module which can be embedded easily used by customer or hobbyist. SIM900 GSM Module provides an industry-standard interface. SIM900 delivers GSM/GPRS 850/900/1800/1900MHz performance for voice, SMS, Data with low power consumption. It is easily available in the market.
	SIM900 designed by using single-chip processor integrating AMR926EJ-S core
	Quad - band GSM/GPRS module in small size.
	GPRS Enabled
 
AT Command:
AT  means ATTENTION. This command is used to control GSM module. There are some commands for calling and messaging that we have used in many of our previous GSM projects with Arduino. For testing GSM Module we used AT command. After receiving AT Command GSM Module respond with OK. It means GSM module is working fine. Below is some AT commands we used here in this project :
ATE0 For echo off
AT+CNMI=2,2,0,0,0  <ENTER>       Auto opened message Receiving.  (No need to open message)
ATD<Mobile Number>; <ENTER>      making a call (ATD+919610126059;\r\n)
AT+CMGF=1 <ENTER>                Selecting Text mode
AT+CMGS=”Mobile Number” <ENTER>  Assigning recipient’s mobile number
>>Now we can write our message
>>After writing message
Ctrl+Z  send message command (26 in decimal).
ENTER=0x0d in HEX
(To learn more about GSM module, Check our various GSM projects with various microcontrollers here).
Heartbeat Sensor:
The principle behind the working of the Heartbeat Sensor is Photoplethysmograph. According to this principle, the changes in the volume of blood in an organ are measured by the changes in the intensity of the light passing through that organ.
 
Usually, the source of light in a heartbeat sensor would be an IR LED and the detector would be any Photo Detector like a Photo Diode, an LDR (Light Dependent Resistor) or a Photo Transistor.
With these two i.e. a light source and a detector, we can arrange them in two ways: A Transmissive Sensor and a Reflective Sensor.
In a Transmissive Sensor, the light source and the detector are place facing each other and the finger of the person must be placed in between the transmitter and receiver.
Reflective Sensor, on the other hand, has the light source and the detector adjacent to each other and the finger of the person must be placed in front of the sensor. 

Working Explanation:
In this project we are going to use an accident detection unit which will be fitted inside the front of carrier of the car. In this project, Arduino is used for controlling whole the process with a GPS Receiver, GSM module and Heartbeat Sensor. GPS Receiver is used for detecting coordinates of the vehicle, GSM module is used for sending the alert SMS with the coordinates and the link to Google Map. Heartbeat Sensor is used for detecting accident or sudden change in heartbeat of driver. And an optional 16x2 LCD is also used for displaying status messages or coordinates. We have used GPS Module Neo 6M 001 and GSM Module SIM900A / SIM800l.
 
Workflow Diagram

When we are ready with our hardware after programming, we can install it in our vehicle and power it up. Now whenever there is an accident, the heartbeat of driver sudden change and heartbeat sensor changes his  values. These values read by Arduino and checks if any change occurs in heartbeat. If any change occurs then Arduino reads coordinates by extracting $GPGGA String from GPS module data (GPS working explained above) and send SMS to the predefined number to the police or ambulance or family member with the location coordinates of accident place. The message also contains a Google Map link to the accident location, so that location can be easily tracked. When we receive the message then we only need to click the link and we will redirect to the Google map and then we can see the exact location of the vehicle.
Content Of The Text SMS is:
Accident has Ocurred.
Lon= 66133.145,   lat= 45641324
http://maps.google.com/maps?&z=15&mrt=yp&t=k&q=
Enhancement / Feature added to this project:
In this project we have added alcohol sensor. Purpose of Alcohol sensor is to detect the consumption of alcohol by driver of vehicle. This will help to prevent the accident caused due to “Drink and drive” condition. By implementing alcohol sensor project will be “Vehicle accident detection and prevention”. We are informing owner of the car through SMS that the driver has consumed alcohol. The alcohol sensor will be placed on the steering wheel of the car. Which means sensor will be just near the driver of vehicle. Purpose behind this is that if some other person has consumed the alcohol then it should send SMS. For example the person near the driver or backseat. If person other than driver has consumed alcohol then sensor will not detect the presence of alcohol. This is because range of sensor is low. Sensor detects only the percentage of alcohol in air which is near the steering wheel.
Applications and Advantages:
1) School transport vehicle accident detection: “Vehicle Accident Detection system”can be used in the school bus.
2) This project can be used for cab or car of companies.
Future Development:
1. We can monitor some parameters of vehicle like overheat or LPG gas leakage.
2. We can dial an emergency call if the vehicle goes out of a certain / pre-decided track.
Programming Explanation:
Note - Some variables and functions may change in final Projection Submission due to experimental changes. Below shown code is only for basic explanation. 
Basic Program has been given below in Code section; here we are explaining its various functions in brief. 
First we have included all the required libraries or headers files and declared various variables for calculations and storing data temporary.
After this, we have created a function void initModule(String cmd, char *res, int t) to initialize the GSM module and checking its response using AT commands.
.
void initModule(String cmd, char *res, int t)
{
  while(1)
  {
    Serial.println(cmd);
    Serial1.println(cmd);
    delay(100);
    while(Serial1.available()>0)
    {
       if(Serial1.find(res))
       {
        Serial.println(res);
        delay(t);
        return;
       }
       else
       {
        Serial.println("Error");
       }
    }
    delay(t);
  }
}
After this, in void setup() function, we have initialized hardware and software serial communication, LCD, GPS, GSM module and accelerometer.

void setup() 
{
  Serial1.begin(9600);
  Serial.begin(9600);
  lcd.begin(16,2);  
  lcd.print("Accident Alert  ");
  lcd.setCursor(0,1);
  lcd.print("     System     ");
  delay(2000);
  lcd.clear();
  .... ......
Here we have also created some other function for various puposes like void gpsEvent() to get GPS coordinates, void coordinate2dec() for extracting coordinates from the GPS string and convert them into Decimal values, void show_coordinate() for displaying values over serial monitor and LCD, and finally the void Send() for sending alert SMS to the predefined number.
