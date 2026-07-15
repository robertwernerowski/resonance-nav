# Resonance Nav

An audio-first navigation minigame prototype for a fantasy game about a **blind mage
who navigates by sound**. You follow a continuous magical "resonance" tone toward a
goal while avoiding hazards — guided by **stereo Web Audio and haptic vibration**.
It is designed to be fully playable **with your eyes closed**; the on-screen visuals
exist only for sighted debugging.

Everything lives in a single self-contained [`index.html`](index.html) — no build step,
no dependencies. Open it in a mobile browser (built and tested for **Android Chrome**),
tap **Start**, and put headphones on.

## How to play

- Hold a finger anywhere on the screen. The **angle** from screen-centre to your finger
  is your heading (up = forward); the **distance** is your speed. Release to stop.
- The pure sine **resonance tone** pans toward the goal and rises in pitch as you close in.
  When it feels centred, you're pointed straight at it.
- **Hazards** emit harsh, low, pulsing sounds panned to their position. Get too close and
  you take damage (sound + vibration) and are shoved back. Lose all health and you fail.
- Reach the goal to win.

Pick **Easy / Normal / Hard** on the start screen.

## Structure

Deliberately split into clean modules (this is a prototype for a later **Unity port**):

| Module    | Responsibility |
|-----------|----------------|
| `CONFIG`  | Every tunable value, at the top of the file, heavily commented. |
| `Input`   | Finger-joystick → movement vector. Swappable for device tilt. |
| `Audio`   | Web Audio synthesis (placeholder oscillators; swap for real samples). |
| `Haptics` | `navigator.vibrate` scheduler faking intensity via pulse frequency. |
| `Game`    | State, rules, main loop, debug rendering. |

## Notes / web limitations

- **Haptics** are on/off on the web, so intensity is faked with pulse density. Real
  variable-amplitude vibration is planned for the Unity build.
- **Spatial audio** uses flat stereo panning (no true 3D / front-back). A hazard directly
  ahead and directly behind sound the same; the goal is volume-ducked when behind you.
- Audio/vibration are unlocked from the **Start** button, as mobile browsers require.
- `navigator.vibrate` is **Android-only** (iOS Safari ignores it).
