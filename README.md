# Holiday_LEDs_2.0
Decently tested and working, Fire effect still under development.  

this new version is easier to setup and can support 6 zones dynamically

The node-red portion of the configuration is no longer needed, all processing is handled in the arduino code. 




-Fill out the entire USER CONFIGURATION section of the code.

-If you get a linker error while compiling in arduino, update your ESP8266 boards manager


For Openhab 2.4 support take a look at the addditions here (sitemap, things, rules and items files):
https://github.com/JayJayJanssen/openhab-MQTTv2-LED-strip


## Home Assistant YAML

``yaml
##This version of the holiday lights code does not require the node red portion
##The "W" slider under the main "holiday LED" light modifies each effect
##The "W" slider under "Glitter" light modifies the frequency of glitter, the RGB selection changes the color of the glitter
##The "W" slider under "Lightning" switch modifies the frequency of lightning.
##You must replace the [MQTT_CLIENT_ID] with the USER_MQTT_CLIENT_NAME you specified in the arduino USER CONFIGURATION section
sensor:
  - platform: mqtt
    name: "Current LED"
    state_topic: "[MQTT_CLIENT_ID]/locator"

light:
  - platform: mqtt
    name: "Holiday Lights"
    command_topic: "[MQTT_CLIENT_ID]/power"
    state_topic: "[MQTT_CLIENT_ID]/powerState"
    brightness_command_topic: "[MQTT_CLIENT_ID]/brightness"
    brightness_state_topic: "[MQTT_CLIENT_ID]/brightnessState"
    brightness_scale: 255
    white_value_command_topic: "[MQTT_CLIENT_ID]/modifier"
    white_value_state_topic: "[MQTT_CLIENT_ID]/modifierState"
    white_value_scale: 500
    effect_command_topic: "[MQTT_CLIENT_ID]/effect"
    effect_state_topic: "[MQTT_CLIENT_ID]/effectState"
    effect_list:
      - Color_Chase
      - Color_Glitter
      - Single_Race
      - Double_Crash
      - Rainbow
      - Blocked_Colors
      - BPM
      - Twinkle
      - Fire
      - Fill_Solid
      - Spooky_Eyes
      - LED_Locator
    retain: true
  - platform: mqtt
    name: "Color 1"
    command_topic: "[MQTT_CLIENT_ID]/ColorPower"
    state_topic: "[MQTT_CLIENT_ID]/powerState"
    rgb_command_topic: "[MQTT_CLIENT_ID]/color1"
    rgb_state_topic: "[MQTT_CLIENT_ID]/color1State"
    retain: true
  - platform: mqtt
    name: "Color 2"
    command_topic: "[MQTT_CLIENT_ID]/ColorPower"
    state_topic: "[MQTT_CLIENT_ID]/powerState"
    rgb_command_topic: "[MQTT_CLIENT_ID]/color2"
    rgb_state_topic: "[MQTT_CLIENT_ID]/color2State"
    retain: true
  - platform: mqtt
    name: "Color 3"
    command_topic: "[MQTT_CLIENT_ID]/ColorPower"
    state_topic: "[MQTT_CLIENT_ID]/powerState"
    rgb_command_topic: "[MQTT_CLIENT_ID]/color3"
    rgb_state_topic: "[MQTT_CLIENT_ID]/color3State"
    retain: true
  - platform: mqtt
    name: "Glitter"
    state_topic: "[MQTT_CLIENT_ID]/glitter/state"
    command_topic: "[MQTT_CLIENT_ID]/addEffects"
    payload_on: "Glitter On"
    payload_off: "Glitter Off"
    rgb_command_topic: "[MQTT_CLIENT_ID]/glitterColor"
    rgb_state_topic: "[MQTT_CLIENT_ID]/glitterColorState"
    white_value_command_topic: "[MQTT_CLIENT_ID]/glitterChance"
    white_value_state_topic: "[MQTT_CLIENT_ID]/glitterChanceState"
    white_value_scale: 255
    retain: true
  - platform: mqtt
    name: "Lightning"
    state_topic: "[MQTT_CLIENT_ID]/lightning/state"
    command_topic: "[MQTT_CLIENT_ID]/addEffects"
    payload_on: "Lightning On"
    payload_off: "Lightning Off"
    white_value_command_topic: "[MQTT_CLIENT_ID]/lightningChance"
    white_value_state_topic: "[MQTT_CLIENT_ID]/lightningChanceState"
    white_value_scale: 500
    retain: true
  ``
