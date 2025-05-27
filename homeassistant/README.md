# Home Assistant 
This is a work in progress, check back for more!

## Add ZigbeeMQTT to Home Assistant in Proxmox

Add zigbee2mqtt to addons (add repositories in top right corner) and install.
Add Sonoff stick to to the configuration

serial
``` 

port: /dev/ttyUSB0

``` 


# Improving Privacy with Amazon Alexa and Pi-hole

## Goal

Enhance the privacy of Amazon Alexa without breaking core functionality (music, voice commands, smart home control). The goal is **not** to block Alexa from the internet entirely, but to **reduce tracking and data collection** through DNS filtering and strict Amazon-side privacy settings.

---

## 1. Amazon Alexa Privacy Settings

Go to your Alexa settings:

**Alexa App → Settings → Alexa Privacy → Manage Your Alexa Data**

Recommended settings:

- **Delete Voice Recordings Automatically** → `Enabled` (e.g., every 3 months)
- **Help Improve Alexa** → `Disabled`
- **Use of Voice Recordings for Development** → `Disabled`
- **Smart Home Device History** → `Disabled` (optional)

These steps reduce the amount of data Amazon stores and uses for analysis or improvement of Alexa services.

---

## 2. Network-Level Filtering with Pi-hole

To reduce tracking and unnecessary external connections, install a DNS filter like **Pi-hole** in your home network.

### 🖥️ Setup: Pi-hole on Proxmox

-
Configure FritzBox to use Pi-hole

- Open FRITZ!Box UI 
- Go to: Home Network → Network → Network Settings
- Scroll to DNS server section
- Set Local DNS server = 192.168.178.250 (or whatever IP your Pi-hole has)
- Save and reboot the router


## 3. Filter Alexa-Specific Domains (Optional)

You can enhance filtering by adding known Alexa tracking domains to Pi-hole’s blacklist. Some examples:
```
device-metrics-us.amazon.com
alexa.amazon.com
softwareupdates.amazon.com
```

⚠️ Do not block all Alexa-related domains — otherwise Alexa will stop working. Test each rule carefully.

