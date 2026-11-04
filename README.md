# DRONE WATCH field simulator

**[Open the live demo](https://pkkshadow.github.io/drone-watch-demo/)**

DRONE WATCH is a homemade, listen-only drone detector. It never transmits anything; it only picks up what drones already put in the air:

- **Remote ID.** Most drones in the US must broadcast an ID, a position and the pilot's location. The detector reads it over Wi-Fi, from both beacon and NAN frames.
- **Drone-maker Wi-Fi.** It flags radios whose hardware address belongs to a drone maker, even without Remote ID.
- **FPV video hints.** It notices 5.8 GHz Wi-Fi-style video links that don't belong to a nearby router.
- **Sound.** Four microphones on a cross-shaped arm hear propeller hum and give the direction it comes from.

This demo runs the device's real firmware in your browser. Both boards are compiled to WebAssembly: the ESP32-S3 main board and the XIAO ESP32-C5 radio scanner. A simulated field of drones, Wi-Fi traffic, wind and noise surrounds them.

<img src="img/screen-home.png" width="480" alt="The device's HOME screen with two Remote ID contacts">

## Using the demo

1. Pick a scenario from **Load a scenario**, or add drones with the colored buttons above the map.
2. Watch the unit on the left. Its screen, its four lights and its buzzer react as drones come into range. Turn your sound on to hear the buzzer.
3. Click a drone on the map to select it, then click anywhere on the map to send it there. You can also use **fly at me**, **orbit me** or **fly away**.
4. Click the unit's screen, then:
   - **Space** is the K0 button: next screen, or hold for HOME.
   - The **arrow keys** turn the knob.
   - **Enter** pushes the knob: open a contact, or push twice on AUDIO to start the array check.
5. Change wind, background noise, phones nearby, the neighbor's router and an air conditioner. Each one affects what the detector picks up.

It works on a phone too.

## How the real device works

The **[user guide](GUIDE.md)** covers:

- Drones 101, for people who have never flown one
- Setting up outdoors and the microphone array check
- Every screen, light and sound
- What to do (and not do) when a drone shows up
- What the detector can't see, and troubleshooting

## How realistic is it?

**Real:**
- The firmware.
- Everything on the screen, the light patterns, the buzzer and the serial output come from the same code that runs on the hardware.

**Modeled:**
- **Remote ID and other Wi-Fi frames:** path loss, random fading and a receiver sensitivity limit. A frame only reaches the scanner if it is tuned to that channel at that moment.
- **Sound for each microphone, sample by sample:**
  - propeller harmonics with Doppler and RPM wobble, and prop noise;
  - wind gusts, an air conditioner and hand claps;
  - each sound arriving with its true delay at each microphone.

**Not exact:**
- Detection ranges depend on these models.
- Treat them as a guide, not a promise for any particular site.

The map location is a field in central Kansas, chosen for the demo.
