# V.ALRT-bluetooth-spec
Bluetooth documentation of the  V.ALRT/V.BTTN device standard.
Can be found in this repo for now it's all in: [V.ALRT-DeveloperQuickStartQuide.pdf](https://github.com/HoyosIntegrity/V.ALRT-bluetooth-spec)
# Battery reading

battery life is dependent on usage of the device.  Going in/out of coverage, turning on LED/buzzer, sending commands to the V.BTTN and receiving notifications from the V.BTTN…. All of these will reduce the battery life of the device.  Here are a few tips regarding battery life.

1. Going in and out of range will draw more current because the button must use the Bluetooth radio more to advertise and/or process commands & notifications.

2. Turning on the LED either by going in/out of range or to indicate some event, will draw more current.  You should consider using the stealth mode 01, 02 or 03 (see section 7a) to disable the LED and/or buzzer.

3. Enabling the accelerometer for fall detect, high G or raw data will draw more current.

4. After connecting to the button, your app should read the battery level just once.  Then it should subscribe for battery notification to get updates to battery level changes.

5. When displaying battery level on your app, we recommend you use a color-coded range

    * Green -- battery level of 30% or higher

    * Yellow – battery level of 10% to 29%

    * Red – battery level of less than 10% 

6. When replacing the battery, we recommend you use a high-quality battery

7. Consider changing the connection parameters (see section 9).  These parameters control how often the button syncs with the phone.  For example, you could increase the connection interval to improve battery life during connection state.

# Few Android and iOS bluetooth  tips

## Android Debugging commands

```setprop log.tag.BluetoothPbapService VERBOSE```
Requires root/ rw filesystem
Android bluetooth stack increased debug level
Every line that says TRC_* set to 6 
```adb shell cat /etc/bluetooth/bt_stack.conf ```

## IOS Core central notes


The battery service UUID is 0000180F-0000-1000-8000-00805f9b34fb

and its characteristic UUID is 00002a19-0000-1000-8000-00805f9b34fb


-----------------

you need to make sure you add support for BLE state preservation and restoration to your app.

Refer to below link for details on how to add this support.

https://developer.apple.com/library/content/documentation/NetworkingInternetWeb/Conceptual/CoreBluetooth_concepts/CoreBluetoothBackgroundProcessingForIOSApps/PerformingTasksWhileYourAppIsInTheBackground.html

 

Here a quick summary of what’s required.

Opt in to state preservation and restoration
Reinstantiate any central manager object after your app is relaunched by the system. https://developer.apple.com/library/content/documentation/NetworkingInternetWeb/Conceptual/CoreBluetooth_concepts/CoreBluetoothBackgroundProcessingForIOSApps/PerformingTasksWhileYourAppIsInTheBackground.html#//apple_ref/doc/uid/TP40013257-CH7-SW13
Implement appropriate restoration delegate method.https://developer.apple.com/library/content/documentation/NetworkingInternetWeb/Conceptual/CoreBluetooth_concepts/CoreBluetoothBackgroundProcessingForIOSApps/PerformingTasksWhileYourAppIsInTheBackground.html#//apple_ref/doc/uid/TP40013257-CH7-SW14
 

Tips for step 3

After you’ve restored the peripheral, be sure to set the peripheral delegate to ensure it receives the appropriate callbacks.
You may also want to retrieve the connected peripheral from the system and then reconnect to them locally.  Refer to the last paragraph in the following link. https://developer.apple.com/library/content/documentation/NetworkingInternetWeb/Conceptual/CoreBluetooth_concepts/BestPracticesForInteractingWithARemotePeripheralDevice/BestPracticesForInteractingWithARemotePeripheralDevice.html#//apple_ref/doc/uid/TP40013257-CH6-SW1
Assuming you’ve implemented the state preservation and restoration feature above, then the willRestoreState method will be invoked first when your app is relaunched into the background, be sure to save the CBPeripheral that is returned in the dictionary.  Subsequently, when the centralManagerDidUpdateState delegate will be called, you should then call discoverServices method on the restored CBPeripheral. 


