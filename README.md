## React Native BDS plugin for Bluetooth Low Energy Client Apps 

This is the Bluetooth Developer Studio plugin for React Native Bluetooth Low Energy (BLE) Client App development using [React Native BLE Quick SDK package](https://github.com/YbrainInc/react-native-ble-quick-sdk/). This plugin generates BLE services javascript source based on BLE profile designed using Bluetooth Developer Studio IDE.

## Plugin Version
*  v0.1.0

## Requirements
* Node v6.10.0+
* NPM v3.10.0+
* React Native Framework from Facebook
* Bluetooth Developer Studio IDE from Bluetooth SIG organization
* BLE profile (xml files) of bluetooth device designed using using Bluetooth Developer Studio.
* Windows 7/8.1/10 and Mac OS Yosemite/El Capitan/Sierra .

## Caution: 
This plugin is in development phase so please don't use it for production releases until stable version of this sdk is released.


## Install & Prepare on Windows OS
----------------------------------

1. Assuming that Bluetooth Developer Studio is installed and you have created BLE profile for your device using Bluetooth Developer Studio. Also please remeber to have your react native app (or sample test app) ready on your Windows Machine. Lets say your react native app project root on Windows Machine is {app_react_nativeproject_root} 

* Note: If you don't have your react native app ready then please follow link [Getting started React Native Apps](https://facebook.github.io/react-native/docs/getting-started.html) to create sample react native app and then try our plugin. Please don't forget step 4 and step 8 before trying to generate code.

2. Download React Native BDS plugin for Bluetooth Low Energy Client Apps from [here](https://github.com/YbrainInc/react-native-ble-quick-sdk-bds-plugin)

3. Copy the downloaded react-native-ble-quick-sdk-bds-plugin folder to Plugins folder of Bluetooth Developer Studio. (i.e {Your Bluetooth Developer Studio Installation Folder}\Plugins)

4. Do npm install react-native-ble-quick-sdk as below in your React Native App's root folder {app_react_nativeproject_root} . Provide the Bluetooth Developer Studio's root path using argument --bdsPath in npm install command.

```shell
 cd {app_react_nativeproject_root}
 npm install --save react-native-ble-quick-sdk --bdsPath="{Your Bluetooth Developer Studio Installation Folder i.e. C:\Program Files (x86)\Bluetooth SIG\Bluetooth Developer Studio}" 
```
 
* Note: 
This step needs admin privilege or it will fail. 


5. Open your Bluetooth Developer Studio project.

6. Go to Tools -> Generate Code -> Select "Client" for "Generate Code for" option -> Check if "React Native Client Plugin" is available as Plugin option.

7. Select Plugin "React Native Client Plugin" in Bluetooth Developer Studio.

8. Set output path in "Save To " field to {app_react_nativeproject_root}\node_modules\react-native-ble-quick-sdk\.

9. Press generate button and watch the Bluetooth Developer Studio log window to check if code is generated successfully or not.

10. Go to terminal, change to directory "{app_react_nativeproject_root}\node_modules\react-native-ble-quick-sdk\" and execute below two command sequentially as below: 


```shell
	>cd {app_react_nativeproject_root}\node_modules\react-native-ble-quick-sdk
	
	a.) >npm run generate-ble-profile --bleProfileType="characteristic" --bleNamespace="com.{yourcompanynamespace}" --bdsPrjRootPath="{Your Bluetooth Developer Studio project profile folder i.e. C:\\mybdsprojectpath\\}"

	b.) >npm run generate-ble-profile --bleProfileType="service" --bleNamespace="com.{yourcompanynamespace}" --bdsPrjRootPath="{Your Bluetooth Developer Studio project profile folder i.e. C:\\mybdsprojectpath\\}"
```

* Note 1: 

  Argument-1:  bleProfileType is type of BLE profile e.g. service or characteristic. You must run generate-ble-profile command for 					bleProfileType="characteristic" and again for bleProfileType="service".

  Argument-2:  bleNamespace is your BLE device profile's namespace as per Bluetooth Developer Studio.

  Argument-3:  bdsPrjRootPath is root folder of your Bluetooth Developer Studio profile project (i.e. where your *.bds file resides). Please note that 
			   this is not the root path of your react native app project.

* Note 2:
	Please use double slash while specifying path.
	
11. If code generation and ble profile generation have completed successfully then React Native BLE Quick SDK is ready to be consumed by BLE Client (Central)react native app.


## Running on iOS (Android not yet supported, To be supported soon )
* Copy React Native project including \node_modules\react-native-ble-quick-sdk\ from Windows Machine to Mac Machine to prepare and run on iOS. 


## Link the native library
---------------------------
You need to link the native library. You can either:
* Link native library with `react-native link`, or
* Link native library manually

Both approaches are described below.

### Link Native Library with `react-native link`

```shell
react-native link react-native-ble-quick-sdk
```

### Link Native Library Manually

#### iOS
- Open the node_modules/react-native-ble-quick-sdk/comm_admins/ble/ios folder and drag RNBluetoothLE.xcodeproj into your Libraries group.
- Check the "Build Phases"of your project and add "libRNBluetoothLE.a" in the "Link Binary With Libraries" section.


## Your Devcie Specific Example
--------------------------------
	Please refer to folder {app_project_root}\node_modules\react-native-ble-quick-sdk\example\ to find auto generated sample app using this sdk.

	
## Basic Example 
-----------------
** Below example is for for Battery Service as per Bluetooth Specification for type org.bluetooth.service.battery_service(0x180F)
	
```js

import React, {Component} from 'react'; 
 import { 
     Text, 
     View, 
     Alert, 
     StyleSheet, 
     ScrollView 
 } from 'react-native'; 
 import Button from 'apsl-react-native-button' 
 import {getSDKServiceMgrInstance} from 'react-native-ble-quick-sdk';

 var deviceId = ''; // Assign your device's iOS specific CBUUID here. You can find it in the scan api's console log output by your device name.
 
 var objSDKSvcMgr = getSDKServiceMgrInstance(false);
  
 export default class BLEHelloWorldView extends Component { 

     constructor(props) { 
         super(props); 
     } 

     async scanNearbyBleDevices() { 
			let listenerScan = (deviceID, deviceName, rssi) => {
				console.log(' Device Found iOS CBUUID = ' + deviceID + '/' + deviceName + '[' + rssi + ']');
 			};
         try { 
             await objSDKSvcMgr.getDevAdmin().getDeviceScanner().scanAllServices(5, listenerScan); 
             console.log('Initiated scanning task successfully'); 
         } 
         catch (err) { 
             console.log('Failed to start scanning task'); 
         } 
     } 

     async connect2BleDevice() { 
         try { 
             await objSDKSvcMgr.getDevAdmin().getDeviceAccessor().connectToDevice(deviceId); 
             console.log('device connected'); 
         } 
         catch (err) { 
             console.log('device connection failed'); 
         } 
     } 


     async readBatteryLevel() { 

         let listenerBatteryLevel = (BatteryLevel) => { 
             Alert.alert(' BatteryLevel is ' + BatteryLevel); 
         }; 

         try { 
             await objDevSvcMgr.getService('BatteryService').get_battery_level(listenerBatteryLevel); 
             console.log('readBatteryLevel api call success'); 
         } 
         catch (err) { 
             console.log('readBatteryLevel api call failed'); 
         } 

     } 

     render() { 
         return ( 
             <ScrollView style={styles.page}> 
                 <Text style={styles.tabText}>BLE Hello World </Text> 
                 <Button 
                     style={styles.Button} 
                     onPress={ () => { 
                         this.scanNearbyBleDevices(); 
                     } 
                     }> 
                     1-Scan 
                 </Button> 
                 <Button 
                     style={styles.Button} 
                     onPress={ () => { 
                         this.connect2BleDevice(); 
                     } 
                     }> 
                     2-Connect 
                 </Button> 
                 <Button 
                     style={styles.Button} 
                     onPress={ () => { 
                         this.readBatteryLevel(); 
                     } 
                     }> 
                     3-Read BatteryLevel 
                 </Button> 
             </ScrollView> 
         ); 
     } 
 } 
 var styles = StyleSheet.create({ 
	  page: {
		  backgroundColor: '#edf0f5',
		  flex: 1,
	  }, 
     tabText: { 
         color: 'black', 
         margin: 5, 
    }, 
     Button: { 
         backgroundColor: 'green', 
         margin: 30 
     }, 

 }); 
 

```

