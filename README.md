
<p><strong><u>Introduction</u></strong></p>
<p>Nowadays lots of accidents happen on highways due to increase in traffic and also due to the rash driving of the drivers. And in many situations, the family members of the ambulance and police authority are not informed in time. This result in delaying the help reached to the person who suffered due to an accident. Our project <strong>Vehicle Accident Detection with GPS, GSM and Heartbeat Sensor </strong>is designed to avoid such situations.</p>
<p><strong>Components Required:</strong></p>
<ul>
<li>Arduino Uno (Microcontroller)</li>
<li>GSM Module</li>
<li>GPS Module (Neo 6m)</li>
<li>Heartbeat Sensor</li>
<li>16x2 LCD</li>
<li>Power Supply</li>
<li>Connecting Wires</li>
<li>10 K-POT</li>
<li>Breadboard or PCB</li>
<li>Power supply 12v 1amp</li>
</ul>
<p>Before going into Project, we will discuss about GPS, GSM and Heartbeat Sensor.</p>
<p><strong><u>GPS Module and Its Working:</u></strong></p>
<p><a href="http://circuitdigest.com/article/what-is-gps">GPS stands for Global Positioning System</a>&nbsp;and used to detect the Latitude and Longitude of any location on the <strong>Earth</strong>, with exact UTC time (Universal Time Coordinated). GPS module is used to track the location of accident in our project. This device receives the coordinates from the satellite for each and every second, with time and date. We have previously extracted&nbsp;<strong>$GPGGA</strong>&nbsp;string in&nbsp;<a href="http://circuitdigest.com/microcontroller-projects/vehicle-tracking-system-using-arduino-gps-and-gsm">Vehicle Tracking System</a>&nbsp;to find the Latitude and Longitude Coordinates.</p>
<p><strong>GPS module</strong>&nbsp;sends the data related to tracking position in real time, and it sends so many data in NMEA format (see the screenshot below). NMEA format consist several sentences, in which we only need one sentence. This sentence starts from&nbsp;<strong>$GPGGA</strong>&nbsp;and contains the coordinates, time and other useful information. This&nbsp;<strong>GPGGA</strong>&nbsp;is referred to&nbsp;<strong>Global Positioning System Fix Data</strong>.&nbsp;Know more about&nbsp;<a href="http://circuitdigest.com/microcontroller-projects/reading-gps-data-using-computer-and-arduino">NMEA sentences and reading GPS data here.</a></p>
<p>We can extract coordinate from $GPGGA string by counting the commas in the string. Suppose you find $GPGGA string and stores it in an array, then Latitude can be found after two commas and Longitude can be found after four commas. Now, this latitude and longitude can be put in other arrays.</p>
<p><strong>Serial Monitor Reading</strong></p>
<p>Below is the&nbsp;<strong>$GPGGA</strong>&nbsp;String, along with its description:</p>
<p><strong>$GPGGA,104534.000,7791.0381,N,06727.4434,E,1,08,0.9,510.4,M,43.9,M,,*47</strong></p>
<p>$GPGGA,HHMMSS.SSS,latitude,N,longitude,E,FQ,NOS,HDP,altitude,M,height,M,,checksum data</p>
<table>
<tbody>
<tr>
<td>
<p><strong>Identifier</strong></p>
</td>
<td>
<p><strong>Description</strong></p>
</td>
</tr>
<tr>
<td>
<p>$GPGGA</p>
</td>
<td>
<p>Global Positioning system fix data</p>
</td>
</tr>
<tr>
<td>
<p>HHMMSS.SSS</p>
</td>
<td>
<p>Time in hour minute seconds and milliseconds format.</p>
</td>
</tr>
<tr>
<td>
<p>Latitude</p>
</td>
<td>
<p>Latitude (Coordinate)</p>
</td>
</tr>
<tr>
<td>
<p>N</p>
</td>
<td>
<p>Direction N=North, S=South</p>
</td>
</tr>
<tr>
<td>
<p>Longitude</p>
</td>
<td>
<p>Longitude(Coordinate)</p>
</td>
</tr>
<tr>
<td>
<p>E</p>
</td>
<td>
<p>Direction E= East, W=West</p>
</td>
</tr>
<tr>
<td>
<p>FQ</p>
</td>
<td>
<p>Fix Quality Data</p>
</td>
</tr>
<tr>
<td>
<p>NOS</p>
</td>
<td>
<p>No. of Satellites being Used</p>
</td>
</tr>
<tr>
<td>
<p>HDP</p>
</td>
<td>
<p>Horizontal Dilution of Precision</p>
</td>
</tr>
<tr>
<td>
<p>Altitude</p>
</td>
<td>
<p>Altitude (meters above from sea level)</p>
</td>
</tr>
<tr>
<td>
<p>M</p>
</td>
<td>
<p>Meter</p>
</td>
</tr>
<tr>
<td>
<p>Height</p>
</td>
<td>
<p>Height</p>
</td>
</tr>
<tr>
<td>
<p>Checksum</p>
</td>
<td>
<p>Checksum Data</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><strong><u>GSM Module:</u></strong></p>
<p>The SIM900 is a complete Quad-band GSM/GPRS Module which can be embedded easily used by customer or hobbyist. SIM900 GSM Module provides an industry-standard interface. SIM900 delivers GSM/GPRS 850/900/1800/1900MHz performance for voice, SMS, Data with low power consumption. It is easily available in the market.</p>
<ul>
<li>SIM900 designed by using single-chip processor integrating AMR926EJ-S core</li>
<li>Quad - band GSM/GPRS module in small size.</li>
<li>GPRS Enabled</li>
</ul>
<p><strong>AT Command:</strong></p>
<p>AT&nbsp; means ATTENTION. This command is used to control GSM module. There are some commands for calling and messaging that we have used in many of our previous&nbsp;<a href="https://circuitdigest.com/search/node/gsm%20and%20arduino">GSM projects with Arduino</a>. For testing GSM Module we used AT command. After receiving AT Command GSM Module respond with OK. It means GSM module is working fine. Below is&nbsp;<strong>some AT commands</strong>&nbsp;we used here in this project :</p>
<p>ATE0 For echo off</p>
<p>AT+CNMI=2,2,0,0,0&nbsp; &lt;ENTER&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Auto opened message Receiving.&nbsp; (No need to open message)</p>
<p>ATD&lt;Mobile Number&gt;; &lt;ENTER&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; making a call (ATD+919610126059;\r\n)</p>
<p>AT+CMGF=1 &lt;ENTER&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Selecting Text mode</p>
<p>AT+CMGS=&rdquo;Mobile Number&rdquo; &lt;ENTER&gt;&nbsp; Assigning recipient&rsquo;s mobile number</p>
<p>&gt;&gt;Now we can write our message</p>
<p>&gt;&gt;After writing message</p>
<p>Ctrl+Z&nbsp; send message command (26 in decimal).</p>
<p>ENTER=0x0d in HEX</p>
<p>(To learn more about GSM module, Check our various&nbsp;<a href="https://circuitdigest.com/tags/gsm">GSM projects with various microcontrollers here</a>).</p>
<p><strong><u>Heartbeat Sensor</u></strong><strong>:</strong></p>
<p>The principle behind the working of the Heartbeat Sensor is Photoplethysmograph. According to this principle, the changes in the volume of blood in an organ are measured by the changes in the intensity of the light passing through that organ.</p>
<p>Usually, the source of light in a heartbeat sensor would be an IR LED and the detector would be any Photo Detector like a Photo Diode, an LDR (Light Dependent Resistor) or a Photo Transistor.</p>
<p>With these two i.e. a light source and a detector, we can arrange them in two ways: A Transmissive Sensor and a Reflective Sensor.</p>
<p>In a Transmissive Sensor, the light source and the detector are place facing each other and the finger of the person must be placed in between the transmitter and receiver.</p>
<p>Reflective Sensor, on the other hand, has the light source and the detector adjacent to each other and the finger of the person must be placed in front of the sensor.&nbsp;</p>
<p>&nbsp;</p>
<p><strong><u>Working Explanation</u></strong><strong>:</strong></p>
<p>In this project we are going to use an accident detection unit which will be fitted inside the front of carrier of the car. In this project, Arduino is used for controlling whole the process with a&nbsp;<strong>GPS Receiver, GSM module and Heartbeat Sensor</strong>. GPS Receiver is used for detecting coordinates of the vehicle, GSM module is used for sending the alert SMS with the coordinates and the link to Google Map.&nbsp;<strong>Heartbeat Sensor</strong>&nbsp;is used for detecting accident or sudden change in heartbeat of driver. And an optional 16x2 LCD is also used for displaying status messages or coordinates.&nbsp;<strong>We have used GPS Module Neo 6M 001 and GSM Module SIM900A / SIM800l.</strong></p>
<p><strong>Workflow Diagram</strong></p>
<p>&nbsp;</p>
<p>When we are ready with our hardware after programming, we can install it in our vehicle and power it up. Now whenever there is an accident, the heartbeat of driver sudden change and heartbeat sensor changes his&nbsp; values. These values read by Arduino and checks if any change occurs in heartbeat. If any change occurs then Arduino reads coordinates by extracting $GPGGA String from GPS module data (GPS working explained above) and send SMS to the predefined number to the police or ambulance or family member with the location coordinates of accident place. The message also contains a Google Map link to the accident location, so that location can be easily tracked. When we receive the message then we only need to click the link and we will redirect to the Google map and then we can see the exact location of the vehicle.</p>
<p><strong>Content Of The Text SMS is:</strong></p>
<p>Accident has Ocurred.</p>
<p>Lon= 66133.145,&nbsp;&nbsp; lat= 45641324</p>
<p><a href="http://maps.google.com/maps?&amp;z=15&amp;mrt=yp&amp;t=k&amp;q=">http://maps.google.com/maps?&amp;z=15&amp;mrt=yp&amp;t=k&amp;q=</a></p>
<p><strong>Enhancement / Feature added to this project:</strong></p>
<p>In this project we have added alcohol sensor. Purpose of Alcohol sensor is to detect the consumption of alcohol by driver of vehicle. This will help to prevent the accident caused due to&nbsp;&ldquo;Drink and drive&rdquo;&nbsp;condition. By implementing alcohol sensor project will be&nbsp;&ldquo;Vehicle accident detection and prevention&rdquo;.&nbsp;We are informing owner of the car through SMS that the driver has consumed alcohol. The alcohol sensor will be placed on the steering wheel of the car. Which means sensor will be just near the driver of vehicle. Purpose behind this is that if some other person has consumed the alcohol then it should send SMS. For example the person near the driver or backseat. If person other than driver has consumed alcohol then sensor will not detect the presence of alcohol. This is because range of sensor is low. Sensor detects only the percentage of alcohol in air which is near the steering wheel.</p>
<p><strong><u>Applications and Advantages</u></strong>:</p>
<p>1) School transport vehicle accident detection: &ldquo;Vehicle Accident Detection system&rdquo;can be used in the school bus.</p>
<p>2) This project can be used for cab or car of companies.</p>
<p><strong>Future Development:</strong></p>
<ol>
<li>We can monitor some parameters of vehicle like overheat or LPG gas leakage.</li>
<li>We can dial an emergency call if the vehicle goes out of a certain / pre-decided track.</li>
</ol>
<p><strong><u>Programming Explanation</u></strong><strong>:</strong></p>
<p><em>Note - Some variables and functions may change in final Projection Submission due to experimental changes. Below shown code is only for basic explanation. </em></p>
<p>Basic Program has been given below in Code section; here we are explaining its various functions in brief.</p>
<p>First we have included all the required libraries or headers files and declared various variables for calculations and storing data temporary.</p>
<p>After this, we have created a function&nbsp;<strong><em>void initModule(String cmd, char *res, int t)</em></strong>&nbsp;to initialize the GSM module and checking its response using AT commands.</p>
<p>.</p>
<p>void initModule(String cmd, char *res, int t)</p>
<p>{</p>
<p>&nbsp; while(1)</p>
<p>&nbsp; {</p>
<p>&nbsp;&nbsp;&nbsp; Serial.println(cmd);</p>
<p>&nbsp;&nbsp;&nbsp; Serial1.println(cmd);</p>
<p>&nbsp;&nbsp;&nbsp; delay(100);</p>
<p>&nbsp;&nbsp;&nbsp; while(Serial1.available()&gt;0)</p>
<p>&nbsp;&nbsp;&nbsp; {</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; if(Serial1.find(res))</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Serial.println(res);</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; delay(t);</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; else</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Serial.println("Error");</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }</p>
<p>&nbsp;&nbsp;&nbsp; }</p>
<p>&nbsp;&nbsp;&nbsp; delay(t);</p>
<p>&nbsp; }</p>
<p>}</p>
<p>After this, in&nbsp;<strong><em>void setup()</em></strong>&nbsp;function, we have initialized hardware and software serial communication, LCD, GPS, GSM module and accelerometer.</p>
<p>&nbsp;</p>
<p>void setup()</p>
<p>{</p>
<p>&nbsp; Serial1.begin(9600);</p>
<p>&nbsp; Serial.begin(9600);</p>
<p>&nbsp; lcd.begin(16,2);&nbsp;</p>
<p>&nbsp; lcd.print("Accident Alert&nbsp; ");</p>
<p>&nbsp; lcd.setCursor(0,1);</p>
<p>&nbsp; lcd.print("&nbsp;&nbsp;&nbsp;&nbsp; System&nbsp;&nbsp;&nbsp;&nbsp; ");</p>
<p>&nbsp; delay(2000);</p>
<p>&nbsp; lcd.clear();</p>
<p>&nbsp; .... ......</p>
<p>Here we have also created some other function for various puposes like&nbsp;<strong><em>void gpsEvent()</em></strong>&nbsp;to get GPS coordinates,&nbsp;<strong><em>void coordinate2dec()</em></strong>&nbsp;for extracting coordinates from the GPS string and&nbsp;<a href="https://circuitdigest.com/microcontroller-projects/arduino-vehicle-tracker-on-google-maps-using-esp8266">convert them into Decimal values</a>,&nbsp;<strong><em>void show_coordinate()</em></strong>&nbsp;for displaying values over serial monitor and LCD, and finally the&nbsp;<strong><em>void Send()</em></strong>&nbsp;for sending alert SMS to the predefined number.</p>
