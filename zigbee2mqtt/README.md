
## Find out the path to the USB Dongle

1. Unplug the USB Dongle (if you have one plugged in already)
2. Run `lsusb` and `ls -la /dev` to see what devices are available
3. Plug in the USB Dongle
4. Run `lsusb` and `ls -la /dev` again to see which device is new  
   a. From `lsusb`:
   ```
   ...
   Bus 001 Device 004: ID 1a86:55d4 QinHeng Electronics:unknown device 55d4
   ```
   b. From `ls -la /dev`:
   ```
    ...
    crw-rw----    1 root     root      166,   0 Jan 30 06:44 ttyACM0
    ...
    crw-rw----    1 root     root      189,   3 Jan 30 06:44 usbdev1.4
    ...
    ```
    The device is `/dev/ttyACM0` (the `ACM0` part is the important part)


## zigbee2mqtt config

configuration.yaml (not yml), will be overwritten/extended on startup (keep a backup for reference):
```
# Home Assistant integration (MQTT discovery)
homeassistant: true # default config, advanced see: https://www.zigbee2mqtt.io/guide/configuration/homeassistant.html#advanced-configuration

# allow new devices to join
permit_join: true

# MQTT settings
mqtt:
  # MQTT base topic for zigbee2mqtt MQTT messages
  base_topic: zigbee2mqtt
  # MQTT server URL
  server: 'mqtt://192.168.0.211'
  # MQTT server authentication, uncomment if required:
  # user: my_user
  # password: my_password

# Serial settings
serial:
  # Location of CC2531 USB sniffer
  port: /dev/ttyACM0
  adapter: ezsp # as described for my adapter, otherwise zigbee herdsman won't start
```


## Hue Button Setup:

https://community.home-assistant.io/t/philips-hue-smart-button-5-press-actions-hold-to-dim/413705/122

