# Editing sample — Before/After (clarity, consistency, style)

## Context
Short extract from a hypothetical guide describing how to enable an integration and verify it.

## Before (original draft)
The user will need to check that their install is set up alright and maybe reboot. Click the configure thing and then choose your device if it appears, otherwise try again later because discovery can be slow sometimes. If it still doesn’t show then probably it’s your network, which has to be on the same thing as Home Assistant or else it won’t work. When it seems to be added you can test if it works by turning the light on (or off) but note that sometimes there is a delay that can be long.

## After (edited)
**Goal:** Enable the integration and verify basic control.

1. Go to **Settings → Devices & services → + Add integration**.
2. Search for the integration name and select it.
3. If discovery doesn’t find your device within **30 seconds**, click **Add manually** and enter the IP address.
4. Ensure the device and Home Assistant are on the **same network segment** (no guest/AP isolation).
5. After adding, open the device page and click **Turn on** (or **Turn off**).  
   **Expected result:** the device responds within **2 seconds**.

**Notes**
- If control is delayed or fails, check **Settings → Logs** and your router’s client list to confirm IP addressing.
