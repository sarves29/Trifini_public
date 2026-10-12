# Robo Pet

Trifini is more than a screen. The Robo Pet is a companion that lives wherever you are, built so that the product feels like a relationship, not a dashboard.

One companion, three forms:

| Form | What it is |
|---|---|
| **Virtual pet** | A living character on web and mobile |
| **Floating widget** | A small companion bubble on every page and, on Android, over other apps |
| **Physical robot** | A desk companion with a round display, expressions and voice, built on a custom SG2002-based board |

![Robo Pet](../assets/screenshots/dark/robo-pet.png)

## The virtual pet

The pet is **a mirror of your real life**, not a game you have to feed to keep alive.

- **Mood** follows how you have been feeling (from your recent mood logs).
- **Energy** follows how you slept and how much you have completed today.
- **Bond** grows with care: feeding, playing and keeping up routines.
- It **bounces** when you hold a streak and gets **droopy or sleepy** when things slip, a gentle nudge rather than a guilt trip.
- With no data yet, the pet starts neutral instead of sad.
- Interactions have sensible cooldowns, and naming the pet passes through the same crisis-safety screening as every other text input.

### Companion behaviours

- 26+ shared expressions across virtual and physical forms
- Configurable proactivity: passive (only when tapped), semi-proactive (important events), or active (periodic encouragement)
- Idle life: breathing, blinking, small activities of its own
- Notifications can arrive "from" the companion with personality
- Multilingual voice, with a user-chosen name

## The physical robot

A compact desk companion that brings the coach into the room.

- **Hardware:** a custom PCB built around the SG2002 system-on-chip (a camera-capable RISC-V/Arm SoC with on-chip AI acceleration), paired with a 1.28-inch round AMOLED display, speaker, microphone and servos
- **Modular by design:** sensors and peripherals sit on a shared bus with plug-in connectors, so parts can be swapped without soldering
- **Why custom silicon-level design:** earlier prototypes on a general-purpose microcontroller ran into limits on pins, display interfaces and on-device speech, which is what led to the custom board
- **Design:** custom board schematic, enclosure and assembly documentation
- **Experience:** 100+ planned behaviours and 26+ expressions shared with the virtual pet; the robot handles setup and routines, and expresses what the coach notices
- **Connectivity:** an authenticated WebSocket link to the Trifini backend; the robot receives expressions and speech, and reports events

The physical robot is in development and included in the Premium plan. The virtual pet and widget are what users can try today.

## Why a companion

A coach that lives in a chat tab is easy to forget. A character that visibly reacts to your week is not. The companion makes progress and balance visible at a glance and gives people a reason to open the app that is not obligation.
