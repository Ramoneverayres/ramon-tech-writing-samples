# Automate a lamp with Home Assistant, a motion sensor and time-of-day

Automate a smart lamp to turn on when motion is detected **after sunset**, and turn off when no motion is detected for 2 minutes.

## Prerequisites
- A running **Home Assistant** instance.
- One motion sensor integrated (e.g., Zigbee) exposed as `binary_sensor.hall_motion`.
- One smart lamp/switch exposed as `light.hall_lamp`.
- The **Sun** integration enabled (for sunset).
- You have **edit permissions** to create automations.

## Steps
1. In Home Assistant, go to **Settings → Automations & Scenes → + Create Automation**.
2. Choose **Create new automation**.
3. **Trigger**: Select **State** → Entity: `binary_sensor.hall_motion` → From: `off` → To: `on`.
4. **Condition**: Add **Sun** → **After sunset**.
5. **Action**: Choose **Device** → Entity: `light.hall_lamp` → **Turn on**.
6. Add a second **Action** to turn the lamp off after inactivity:
   - Action type: **Wait for trigger** → **State** of `binary_sensor.hall_motion` → From: `on` → To: `off`.
   - Add **For**: `00:02:00`.
   - Next action: **Device** → `light.hall_lamp` → **Turn off**.
7. Click **Save** and name it: “Hall lamp: motion after sunset”.

## Validation
- Walk in front of the motion sensor **after sunset** → the lamp should turn on within 1–2 seconds.
- Stay out of the sensor’s field for 2 minutes → the lamp should turn off automatically.
- Check **Settings → Logs** if behaviour differs.

## Troubleshooting
- **Lamp doesn’t turn on**: Confirm the entity IDs are correct in **Developer Tools → States**.
- **Turns on during the day**: Ensure the **Sun** condition is present and you tested after sunset.
- **Doesn’t turn off**: Verify the **Wait for trigger** step includes **For: 00:02:00** and the sensor returns to `off`.
