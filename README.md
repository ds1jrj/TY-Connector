# Tuya Connector

Connector for Tuya devices with [SmartThings](https://www.smartthings.com/getting-started)

Simplifies the setup of Tuya devices with SmartThings.<br/>

If Tuya Connector is installed, virtual devices are registered automatically by the Tuya Connector SmartApp.<br/>

You don't have to do anything to add Tuya devices in SmartThings IDE.

## Docker
fison67/ty-connector:0.0.3</br>
fison67/ty-connector-rasp:0.0.3</br>

## Support Type
Smart Power Strip<br/>
Smart Plug<br/>
Smart Wall Switch<br/><br/>

## Prerequisites
* SmartThings account, Tuya account
* Local server (Synology NAS, Raspberry Pi, Linux Server) with Docker installed
* Tuya Device id, key ( Take it from packet on Android )
<br/><br/>

## Donation
If this project helps you, you can give me a cup of coffee<br/>

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://paypal.me/fison67)
<br/><br/>

## Install

### Take a localkey, devid, local ip address
```
Install a Packet Capture app on Android
https://play.google.com/store/apps/details?id=app.greyshirts.sslcapture&hl=ko
If you capture a packet, you can get these information. [ devid, localkey ]
You have to get a local ip address from router.
```
![total](./imgs/tuya-packet-capture.jpg)
<br/>
#### How to use app
https://www.lynda.com/Android-tutorials/Capturing-packets-your-mobile-app/614303/635544-4.html
<br/><br/>

### Docker

#### Synology NAS
> Docker must be installed and running before continuing the installation. <br/>

```
1. Open Docker app in Synology Web GUI
2. Select the Registry tab in the left menu
3. Search for "fison67"
4. Select and download the "fison67/ty-connector" image 
5. Select the Image tab in the left menu and wait for the image to fully download
6. Select the downloaded image and click on the Launch button
7. Give the Container a sensible name (e.g. "ty-connector")
8. Click on Advanced Settings
9. Check the "auto-restart" checkbox in the Advanced Settings tab
10. Click on Add Folder in the Volume tab and create a new folder (e.g. /docker/ty-connector) for the configuration files. Fill in "/config" in the Mount path field.
11.  Check the "Use the same network as Docker Host" checkbox in the Network tab
12. Click on Apply => Next => Apply
```

#### Raspberry Pi
> Docker must be installed and running before continuing the installation.

```
sudo mkdir /docker
sudo mkdir /docker/ty-connector
sudo chown -R pi:pi /docker
docker pull fison67/ty-connector-rasp:0.0.3
docker run -d --restart=always -v /docker/ty-connector:/config -v /etc/localtime:/etc/localtime:ro --name=ty-connector-rasp --net=host fison67/ty-connector-rasp:0.0.3
```

### Linux x86 x64

> Docker must be installed and running before continuing the installation.

```
sudo mkdir /docker
sudo mkdir /docker/ty-connector
docker pull fison67/ty-connector:0.0.3
docker run -d --restart=always -v /docker/ty-connector:/config -v /etc/localtime:/etc/localtime:ro --name=ty-connector --net=host fison67/ty-connector:0.0.3
```


#### TY Connector configuration
```
1. Open TY Connector web settings page (http://X.X.X.X:30110/settings) default id/pwd [admin/12345]
2. Select a system address & Press a register button
3. Restart TY Connector Docker container
4. Open TY Connector smartapp & Fill in the server address & Press a Save button
5. Open TY Connector web settings page again. Check if there are smartthings api info is filled
```
<br/><br/>
### Device Type Handler (DTH)

#### Manual install
```
Go to the SmartThings IDE
Click My Device Handlers
Click Create New Device Handlers
Copy content of file in the devicetypes/fison67 folder to the area
Click Create
Loop until all of file is registered
```

#### Install DTH using the GitHub Repo integration

> Enable the GitHub integration before continuing the installation. Perform step 1 and 2 in the [SmartThings guide](https://docs.smartthings.com/en/latest/tools-and-ide/github-integration.html#step-1-enable-github-integration) to enable the GitHub integration for your SmartThings account.

```
1. Go to the SmartThings IDE
2. Select the My Device Handlers tab
3. Click on the "Settings" button
4. Click on the "Add new repository" option and fill in the following information:
    Owner: fison67
    Name: TY-Connector
    Branch: master
5. Click on the "Save" button
6. Click on the "Update from Repo" button and select the "TY-Connector (master)" option
7. Check the checkbox for the device types you need (or all of them) in the "New (only in GitHub)" column
8. Check the "Publish" checkbox and click on the "Execute Update" button
```
<br/><br/>

### SmartApp

#### Manual install
```
Connect to the SmartThings IDE
Click My SmartApps
Click New SmartApp
Click From Code
Copy content of ty-connector.groovy & Paste
Click Create
Click My SmartApps & Edit properties (TY Connector)
Enable OAuth
Update Click
```

#### Install SmartApp using the GitHub Repo integration
> Enable the GitHub integration before continuing the installation. Perform step 1 and 2 in the [SmartThings guide](https://docs.smartthings.com/en/latest/tools-and-ide/github-integration.html#step-1-enable-github-integration) to enable the GitHub integration for your SmartThings account.

```
1. Go to the SmartThings IDE
2. Select the My SmartApps tab
3. Click on the Settings button
4. Click on the "Add new repository" option and fill in the following information:

    Owner: fison67
    Name: TY-Connector
    Branch: master
5. Click on the "Save" button
6. Click on the "Update from Repo" button and select the "TY-Connector (master)" option
7. Check the checkbox for the device types you need (or all of them) in the "New (only in GitHub)" column
8. Check the "Publish" checkbox and click on the "Execute Update" button
9. Select the My SmartApps tab
10. Click on the "Edit Properties" button for the TY Connector SmartApp (fison67 : TY Connector)
11. Click on the "OAuth" option and click on the "Enable OAuth" button
12. Click on the "Update" button
```
Step 3 and 4 are only needed if the repo has not been added earlier (e.g. in the DTH installation).



<br/><br/>

## Troubleshooting

### No update from device
> If data can not be polled from the device:
1. Don't use a app anymore as Tuya or SmartLife.
   Cuz this TY Connector is working locally. It cann't be work together at same time.
   
> If device's MCU firmware version is higher than 1.0.4:
1. Select a version 3.3(Not 3.1) on device add page.


# Library
- https://github.com/codetheweb/tuyapi

