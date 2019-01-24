# V.ALRT-bluetooth-spec
Bluetooth documentation of the  V.ALRT/V.BTTN device standard.
Can be found in this repo for now it's all in: [V.ALRT-DeveloperQuickStartQuide.pdf](https://github.com/HoyosIntegrity/V.ALRT-bluetooth-spec)

# Few Android and iOS bluetooth debugging tips

## Android

```setprop log.tag.BluetoothPbapService VERBOSE```
Requires root/ rw filesystem
Android bluetooth stack increased debug level
Every line that says TRC_* set to 6 
```adb shell cat /etc/bluetooth/bt_stack.conf ```
