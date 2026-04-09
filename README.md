# SendIt Firmware

This is the firmware that runs on a [SendIt](https://github.com/hoeken/sendit) compatible board.  

## First Time Connection

1. Open the [Firmware Helper](https://hoeken.github.io/sendit-firmware/) page
1. Select your board version, firmware version and upload
1. Enter your wifi credentials using serial or Bluetooth
1. Open browser to http://sendit.local
1. Update your board settings, such as login info, name, etc.
1. Install SignalK + signalk-yarrboard-plugin and configure
1. Setup any Node-RED flows and custom logic you want.

## Firmware Update Methods

* Update the firmware using OTA from the web interface
* Use the Firmware Helper linked above to choose a specific version
* Compile from source using instructions below

## Developer Installation

1. Clone this repository
1. Run ```npm install``` in the repository to get some dev tools
1. Plug your computer into the board
1. Open the repository in VSCode
1. Install the Platformio plugin if needed
1. At the bottom, select your board from the build environments
1. Build and/or upload firmware with the arrow in the upper right.

### ArduinoOTA

This allows you to upload new firmware over wifi from VSCode.

1. Enable Arduino OTA in Settings -> Miscellaneous on the board
1. Edit platformio.ini and add this to the bottom of your desired board [env:] section

```
; OTA Upload Config, auth password is your admin password
upload_protocol = espota
upload_port = sendit.local
upload_flags = 
 	--auth=admin
 	--port=3232
```

## Protocol

The protocol for communicating with Yarrboard is entirely based on JSON messages. Each request to the server should be a single JSON object, and the server will respond with a JSON object.

The protocol works over the following transport layers:

* HTTP API
* Websockets
* USB Serial
* MQTT

Here are some example commands you could send:

Get an update from the board
```
{
  "cmd": "get_update",
}
```

For detailed information on the SendIt specific protocol, see ```src/controllers/ADCController.cpp```

Visit the [YarrboardFramework documentation](https://github.com/hoeken/YarrboardFramework#protocol) page for more details on the underlying protocol.