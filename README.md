React Native Bluetooth Developer Studio plugin for BLE Client/Central

This plugin is in development phase so please don't use it for production releases until stable version of this sdk is released.

React Native BDS plugin for BLE Client/Central
----------------------------------------------
This is the Bluetooth Developer Studio plugin for React Native BLE Client App development using React Native BLE Quick SDK. This 
plugin generates BLE services javascript source based on BLE profile of Bluetooth Developer Studio project.



Installation and preparation steps.
-----------------------------------

1. Assuming that Bluetooth Developer Studio is installed and you have created BLE profile for your device using Bluetooth Developer Studio.

2. Get React Native BDS plugin from this repo https://github.com/eric2036/react-native-ble-quick-sdk-bds-plugin

3. Copy the downloaded react-native-ble-quick-sdk-bds-plugin folder to Plugins folder of Bluetooth Developer Studio. (i.e {your-pc}\Bluetooth SIG\Bluetooth Developer Studio\Plugins)

4. Open your Bluetooth Developer Studio project.

5. Go to Tools -> Generate Code -> Select "Client" for "Generate Code for" option -> Check if "React Native BLE Quick SDK for Client" is available as Plugin option.

6. Do npm install react-native-ble-quick-sdk from github as below in your React Native App's root folder. Provide the Bluetooth Developer Studio's root path
 using argument --bdsPath in npm install command.

 e.g. npm install -s https://github.com/eric2036/react-native-ble-quick-sdk --bdsPath="C:\\Program Files\\something" 

7. Go back to Bluetooth Developer Studio-> Select Plugin "React Native BLE Quick SDK for Client"

8. Set output path in "Save To " field to {app_project_root}\node_modules\react-native-ble-quick-sdk\.

9. Press generate button and watch the Bluetooth Developer Studio log window to check if code is generated successfully or not.

10. Go to terminal, change to directory "{app_project_root}\node_modules\react-native-ble-quick-sdk\" and execute below two command as below: 


1.) npm run generate-ble-profile --bleProfileType="characteristic" --bleNamespace="com.yourcompany" --bdsPrjRootPath="C:\\mybdsproject\\"

2.) npm run generate-ble-profile --bleProfileType="service" --bleNamespace="com.yourcompany" --bdsPrjRootPath="C:\\mybdsproject\\"

Note: 
Argument 1 : bleProfileType is type of BLE profile e.g. service or characteristic. You must run generate-ble-profile command
			 for bleProfileType="characteristic" and again for bleProfileType="service".
			 
Argument 2 : bleNamespace is your BLE profile's namespace as per Bluetooth Developer Studio.

Argument 3 : bdsPrjRootPath is root folder of your Bluetooth Developer Studio.

11. If code generation and ble profile generation have completed successfully then React Native BLE Quick SDK is ready to be consumed by BLE Client (Central)react native app.
