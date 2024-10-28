# Home Assistant

See the helm chart docs here
https://github.com/pajikos/home-assistant-helm-chart/tree/main

# Notes For Devices

We have 2 'Smart Plugs' currently

- One Hive Plug -(Integrated with the Hive integration easily)
- One BG Home Plug - This was a pain to get working see [this comment](https://community.home-assistant.io/t/uk-wifi-smart-socket-screwfix-testing/119995/100) which explains what I did.
  - Use BG Home in AP Config as far as 'Device Connected to Wifi' then just bail out before adding device to the BG Home app.
  - Then add the device using the Broadlink integration in Home-Assistant (Remember to set the device to a static IP using Unifi Control Panel)


