## React Native BDS plugin for Bluetooth Low Energy Client Apps 

This is the Bluetooth Developer Studio plugin for React Native Bluetooth Low Energy (BLE) Client App development using [React Native BLE Quick SDK] package (https://github.com/YbrainInc/react-native-ble-quick-sdk/). This plugin generates BLE services javascript source based on BLE profile designed using Bluetooth Developer Studio IDE.

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

1. Assuming that Bluetooth Developer Studio is installed and you have created BLE profile for your device using Bluetooth Developer Studio. Also please remeber to have your react native app ready. If you don't have your react native app ready then please follow link [Getting started React Native Apps] (https://facebook.github.io/react-native/docs/getting-started.html) to create sample react native app and then try our plugin. Please don't forget step 4 and step 8 before trying to generate code.

2. Download React Native BDS plugin for Bluetooth Low Energy Client Apps from [here] (https://github.com/YbrainInc/react-native-ble-quick-sdk-bds-plugin)

3. Copy the downloaded react-native-ble-quick-sdk-bds-plugin folder to Plugins folder of Bluetooth Developer Studio. (i.e {Your Bluetooth Developer Studio Installation Folder}\Plugins)

4. Do npm install react-native-ble-quick-sdk from github as below in your React Native App's root folder. Provide the Bluetooth Developer Studio's root path using argument --bdsPath in npm install command.

```shell
 npm install --save react-native-ble-quick-sdk --bdsPath="{Your Bluetooth Developer Studio Installation Folder i.e. C:\Program Files (x86)\Bluetooth SIG\Bluetooth Developer Studio}" 
```
 
Note: This step needs admin privilege or it will fail.  


5. Open your Bluetooth Developer Studio project.

6. Go to Tools -> Generate Code -> Select "Client" for "Generate Code for" option -> Check if "React Native Client Plugin" is available as Plugin option.

7. Select Plugin "React Native Client Plugin" in Bluetooth Developer Studio.

8. Set output path in "Save To " field to {app_project_root}\node_modules\react-native-ble-quick-sdk\.

9. Press generate button and watch the Bluetooth Developer Studio log window to check if code is generated successfully or not.

10. Go to terminal, change to directory "{app_project_root}\node_modules\react-native-ble-quick-sdk\" and execute below two command sequentially as below: 


```shell
	a.) npm run generate-ble-profile --bleProfileType="characteristic" --bleNamespace="com.{yourcompanynamespace}" --bdsPrjRootPath="{Your Bluetooth Developer Studio project path i.e. C:\\mybdsprojectpath\\}"

	b.) npm run generate-ble-profile --bleProfileType="service" --bleNamespace="com.{yourcompanynamespace}" --bdsPrjRootPath="{Your Bluetooth Developer Studio project path i.e. C:\\mybdsprojectpath\\}"
```

* Note 1: 

  Argument-1:  bleProfileType is type of BLE profile e.g. service or characteristic. You must run generate-ble-profile command for 					bleProfileType="characteristic" and again for bleProfileType="service".

  Argument-2:  bleNamespace is your BLE device profile's namespace as per Bluetooth Developer Studio.

  Argument-3:  bdsPrjRootPath is root folder of your Bluetooth Developer Studio (i.e. where your *.bds file resides). Please note that 
			   this is not the root path of your react native app project.

* Note 2:
	Please use double slash while specifying path.
	
11. If code generation and ble profile generation have completed successfully then React Native BLE Quick SDK is ready to be consumed by BLE Client (Central)react native app.
