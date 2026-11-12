# Drive Sound

One web page that gives a car an engine sound (or a sci-fi one) that follows its real speed.
It reads speed from the browser's GPS, runs a virtual gearbox, synthesises the sound with the
Web Audio API, and draws a scene that moves with you. No sound files, no libraries, no account.

## Use it in the car

1. It is published by GitHub Pages at https://incorruptibleyt.github.io/drive-sound/ on every push to `main`. To host it elsewhere:
   Settings → Pages → Deploy from a branch → pick the branch and the `/evsound` folder, or copy the
   file into its own repository and pick `/ (root)`. The page then lives at
   `https://<your-name>.github.io/<repo>/evsound/`.
2. Open that link in the car's browser (or a phone on Bluetooth to the car).
3. Tap **Start engine** and allow location when asked. Tap the scene to hide the controls.
4. Settings (the gear): GPS or Demo, mph or km/h, how late the gearbox shifts, response,
   calibration (match the dash), the trip (distance, top speed, best 0–60), scenery on or off,
   keep screen awake. On a phone, "Add to Home Screen" gives it a full-screen icon.

Tapping an engine on the start screen plays a short rev of it. In the field, a tap on the scene
hides the controls (space bar on a keyboard); keys 1 to 6 pick an engine, Esc closes settings.

## Try it on a couch

Open the file, pick **Demo** in settings, then drag the slider, press **Auto drive**, or use the
up and down arrow keys.

## How it works

- **Speed:** `watchPosition` gives speed directly; when a browser leaves that field empty the
  page derives it from the distance between fixes. Readings are smoothed, and acceleration gives a
  throttle estimate (lifting off goes to overrun: pops on the V8, blow-off on the turbo).
- **Gearbox:** six gears, each with a top speed at redline; it shifts up by throttle and down by rpm.
- **Scene:** the engines drive a night road (moon, hills, city lights, lit lamp posts); the Jet and the
  Starship fly over a neon grid with a low sun. A tap on the scene hides the controls and leaves a small
  speed readout. Shift lights over the tachometer light up toward the redline.
- **Sound:** oscillators at harmonics of the firing frequency (rpm/60 × cylinders/2) → soft-clip
  waveshaper → lowpass that opens with throttle → compressor. Filtered noise for exhaust and intake;
  a sine "whine" for the turbo, turbine and inverter. Each preset is one row in `PRESETS`.
- **Accuracy:** GPS speed is usually within ±1 mph in open sky, better than the dash, which reads
  high by design. The display trails a hard change by about half a second. Calibration in Settings
  shifts it by a percentage if you want it to agree with the dash.
- **Loudness:** idle sits about 11 dB under full throttle, and a compressor acts only as a safety
  limiter (peaks stay under 0.7 of full scale). A screen that cannot hold 25 fps drops to 1x pixels,
  then turns the scenery off, so the sound never stutters for the picture.
- **Limits:** like every product of this kind, it plays inside the car only. It does not drive the
  car's outside pedestrian speaker. Keep the volume where you can still hear the road.
