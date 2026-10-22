---
name: mobil-oyun-test
description: Use before calling a change done or before releasing a phone-first web game or app. Checks screen sizes, touch, tilt sensors, microphone, sound, pause/resume and saved data, separating emulation from real-device results. Reports in Turkish.
---

# Mobil Oyun Testçisi (Mobile Web Game Tester)

Phone-first web games fail in the same places: tiny screens, iOS sensor permissions, audio that never starts, loops that keep running in the background. This skill runs one structured pass and is honest about what emulation cannot prove.

## Core rules (always)
- Testing is not fixing. Report first; change code only if asked, with the smallest change.
- Never upload the user's code to online testing services.
- Never claim a real device was tested unless the user tested it and reported back.
- One pass, a short report, then fixes if asked — no endless test loops.
- Ask before installing a large tool the environment does not already have.

## Test matrix

**Screen** (portrait; landscape only if supported): 320, 375, 390, 430 px wide.
- No sideways page scroll. Nothing clipped under the notch or home bar (`env(safe-area-inset-*)`).
- Tap targets ≥ 44×44 px. Text readable without zoom.

**Touch**
- Tap, hold and drag work as designed. No double-tap zoom, pull-to-refresh or text-selection menu during play.

**Tilt** (`deviceorientation` / `devicemotion`)
- HTTPS only. On iOS, call `DeviceOrientationEvent.requestPermission()` from a user tap.
- Denied or missing sensor (desktop) → friendly Turkish message + alternative control (slider or buttons).
- Values are smoothed; no jitter when the phone lies still.

**Microphone**
- Requested only after a user tap, on HTTPS. Denied → clear message and a way to keep playing.
- Tracks are stopped when leaving the screen or ending the game.

**Sound**
- Audio starts after a user gesture (`AudioContext.resume()` on tap). Mute works and is remembered.

**Lifecycle and saving**
- App switch / screen lock pauses the loop, timers and sensors; returning resumes without double speed.
- `localStorage` access is inside `try/catch`; data from an older version does not crash the game.

## How to test here
- If Playwright (or similar) is available: open the page with phone emulation at each width and save one screenshot per width.
- Simulate sensors by dispatching synthetic `deviceorientation` events; stub `getUserMedia` to return a fake stream and to reject (denied path).
- Read the console during each scenario.
- If no browser automation exists, review the code against the matrix and state that the checks were **code review only**.

## Real-phone checklist
End with at most 6 short Turkish steps the user can do on their own phone (open the link, allow tilt, deny the mic once, lock and unlock the phone…) for everything emulation cannot prove.

## Required report (Turkish, short)
1. **Test ortamı:** emülasyon / kod incelemesi / kullanıcının gerçek cihazı.
2. **Geçenler.**
3. **Kalanlar:** failures with reproduction steps and the width or scenario.
4. **Gerçek cihazda denenmesi gerekenler.**
5. **Sonraki adım:** the most important single fix.
