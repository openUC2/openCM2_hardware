# openCM2 hardware
This is the hardware part of the openCM2 project, the software part can be found under https://github.com/bjks/openCM2_software. 

## Setup your ESP32
The ESP32 will run the script provided here to control the stepper motors connected to it. Firstly, you need to flash the script onto you ESP32. The instruction here are for the use of the Ardunio IDE, you are of course welcome to use something else.

### Setup your Ardunio IDE
- Download and install the IDE as described [here](https://www.arduino.cc/en/software)
- To setup your IDE, we recommend to follow [this guide](https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/)
- Now we need to install the needed libraries, for that you go to `Tool -> Manage Libraries...` and install the following libraries:
  - PubSubClient
  - AccelStepper

Now you need to set/check the _Board_ and the _Port_ under `Tools`. The _Board_ should be `ESP32 dev Module` and the port should correspond to the usb port you use to connect the ESP32. If you do not know which one to choose, you can unplug the ESP32 and re-connect it to see what changes.
### Prepare the script
In order to communicate to the Raspberry Pi, you need to provide some information to the ESP32. The Raspberry Pi needs to be in the same Wifi as you will give the ESP32. You will also need the ip adress of your Raspberry Pi, that you can find by running `ifconfig wlan0 | grep -w inet`.
After you cloned this repository and open [the script](https://github.com/bjks/openCM2_hardware/tree/main/esp32/ESP32_openCM2). The lines you will need to modify look like this:
```
const char *ssid = "_____________";
const char *password = "_____________";
WiFiClient espClient;
PubSubClient client(espClient);
// ~~~~  MQTT  ~~~~
const char *MQTT_SERVER = "_____________";
```
Where you see the placeholder `_____________` you need to write
- the name of your Wifi (ssid)
- the password of your Wifi (password)
- and the ip adress of your Raspberry Pi (MQTT_SERVER) 

### Flash your ESP32
You can now flash the script onto your ESP32. 
- When your ESP32 is connected to you computer, press the `Upload` button in your IDE (top left). 
- When the console in the bottom is showing that it tries to connect press and hold the `BOOT` of your ESP32. 
- To monitor what is happening on your ESP32, use the `Serial Monitor` (`Tools -> Serial Monitor`) and set the _BAUD-rate_ to 115200.

When the Serial Monitor shows that the ESP32 is connected to the MQTT server, the motor(s) connected to the ESP32 can be controlled by the Raspberry Pi and thus the PS controller! (See the Readme in our software git [here](https://github.com/bjks/openCM2_software/blob/master/README.md) for more information)