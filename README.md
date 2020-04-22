# TUTORIAL FOR INITIALIZING BLUETOOTH COMMUNICATION BETWEEN ANDROID AND ARDUINO

some pre requirements
- First of all download arduino software from www.arduino.cc

- download software serial library from github.com (type on google).

- download four tier software development system for android app
refer the following link for guidance -

www.niktechs.wordpress.com.

1.
## ARDUINO
```
#include <SoftwareSerial.h>
int bluetoothTx = 2;
int bluetoothRx = 3;
SoftwareSerial bluetooth(bluetoothTx, bluetoothRx);
void setup()
{
 //Setup usb serial connection to computer
 Serial.begin(9600);
 //Setup Bluetooth serial connection to android
 bluetooth.begin(115200);
 bluetooth.print("$$$");
 delay(100);
 bluetooth.println("U,9600,N");
 bluetooth.begin(9600);
}
void loop()
{
 //Read from bluetooth and write to usb serial
 if(bluetooth.available())
 {
 char toSend = (char)bluetooth.read();
 Serial.print(toSend);
 }
 //Read from usb serial to bluetooth
 if(Serial.available())
 {
 char toSend = (char)Serial.read();
 bluetooth.print(toSend);
 }
}


```

_For connection see tutorial on aubtm-20 and arduino interfacing with lcd.
That takes care of the Arduino side of things. The Android bits are little bit tougher._

2.
## The Android project we are going to write is going to have to do a few things:
1. Open a bluetooth connection

2. Send data

3. Listen for incoming data

4. Close the connection 
