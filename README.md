# Task 1 
---

## Idea  
Parking Sensor.  
we used LDR as a proximity sensor and took its reading using ESP8266 and published it on a webserver and then we sent the readings to a mobile application `MIT APP INVENTOR` and a desktop application `Python - PYQT5` and they both monitored the readings and gave a warning when the sensor readings indicates a critical proximity level.

## Libraries we used 
`ESP8266WebServer.h` -->  webserver.  
`PYQT5` --> Desktop APP GUI.   
`requests` --> communication between desktop app and webserver (it uses the get/post methods through http protocol).  

## Problems we faced  
**Sending sensor readings from webserver to the desktop application using http**  
our approach was to use the `get` method to retrieve the sensor reading from the webserver but 
the return of the get method was the whole html of the web page we created.
so we went for a dummy solution which is we used `web scraping` to scrap the sensor reading from the html code
and for that we used a python web scraping library called `bs4`

---
---

# Task 2
---

## Idea 
Localizing in a map for our Department.  
we measured the wifi readings strenghths in multiple areas in the department and created a dataset of readings so that we could
train a machine learning classifier to decide where is the person depending on the wifi strengths readings in his position.
A mobile application was created to monitor a person movement in the department. that person needed to hold the microcontroller `ESP8266 NodeMCU` 
which was sending the wifi strengths readings to a database (firebase) and then a machine learning classifier takes those readings and
makes a prediction of where the person should be and sends it also to the firebase. Finally, the mobile application retrive the prediction and draws a point in the department map which indicates where the person is.

## Frameworks
`Flutter` --> It is a cross-platform framework that uses just one code to create apps for different devices. Applications that are programmed in `Dart` language act almost identically on each mobile operating platform (Android & iOS) and they have similar efficiency to their native solutions

## Libraries we used 
`ESP8266WiFi.h` --> measure WIFI strengths.  
`FirebaseArduino.h` -->  connect ESP8266 with firebase to send the wifi strengths readings.  
`firebase_database.dart` --> Dart library to connect the flutter mobile application with firebase database.  
`RandomForest` --> Machine learning classifier.  


## Problems we faced
**the machine learning classifier was a python script which means we needed a running laptop all the time**  
our approach to fix this problem was that we converted the python script into a `C` code and then compiled it on the microcontrller itself and 
for that we used a library called `micromlgen`.

---
---

# Task 3
---

## Idea 
Manual / Autonomous car  
**Manual**  
we created a remote control mobile application that sends commands to the microcontroller `ESP8266 NodeMCU` and then based 
on these commands the controller would send commands to the motors and move the car.

**Autonomous**  
we created a mobile application that would stream the camera images to a server and then the server should process these 
streamed images and perform lane detection algorithms and then send commands to the microcontroller telling it where the car should move.  


## Frameworks  
Flutter --> It is a cross-platform framework that uses just one code to create apps for different devices. Applications that are programmed in `Dart` language act almost identically on each mobile operating platform (Android & iOS) and they have similar efficiency to their native solutions.  

## Libraries we used   
`Flask` --> Create the server which recieves images from the mobile application and process them.  
`opencv` --> image processing.  
`canny` --> used algorithm for lane detection.  
`requests` --> communication between the camera mobile app and flask server (it uses the get/post methods through http protocol).  
`ESP8266WebServer.h` -->  create a webserver for the NodeMCU to recieve moving commands from remote control / Flask server using the http protocol.  
`http.dart` --> remote control communicating with microcontroller NodeMCU.  
`camera.dart` --> obtain a stream of frames from mobile camera.  



## Problems we faced
**Camera frames were in YUV format**  
the camera frames we get from mobile needed to be converted to any standard format before being sent to flask server 
like png or jpg.

**Images are big in size**  
to make the sending process easier we encoded the images before sending them using `base64` format.

**weak internet connection**  
we decreased the number of sent images to the flask server to reduce the processing power as we only sent one frame per second `1 fps`.

