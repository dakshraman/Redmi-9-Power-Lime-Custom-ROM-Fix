Redmi 9T (lime / chime) post-ROM fixes
======================================

1) Lime_FingerprintOff.zip  (SAFE ON ANY ROM)
   - Disables the broken fingerprint HAL service.
   - Removes the fingerprint feature declaration.
   - Fixes the nav-bar / taskbar flicker caused by the virtual DPAD
     device (ff_key) that the failing HAL creates every ~2 seconds.
   - Does NOT touch the touch firmware.
   - Flash in TWRP: Install -> select the zip -> swipe to flash.
   - Only needed if the nav bar starts refreshing by itself or the
     log shows "Config changes=60" / "ff_key" / "uinput_nav".
   - If a future ROM has a working fingerprint sensor, do NOT flash this.

2) Lime_Touch_Stock.zip  (RECOVERY / SAFETY)
   - Restores the original Tianma touch firmware files:
       /vendor/firmware/nt33672a_tianma_novatek_ts_fw.bin
       /vendor/firmware/nt33672a_tianma_novatek_ts_mp.bin
   - Use this if a touch-firmware change makes the touchscreen dead.
   - On Infinity-X 2.8 this is the firmware that makes touch work.

3) Lime_Touch_TrulyFW_Only.zip  (ONLY FOR THE OLD ROM)
   - Writes the Truly _fw.bin into the Tianma-named file and keeps the
     Tianma _mp.bin.
   - This fixed the phantom touches on the previous ROM, but it KILLS
     TOUCH on Infinity-X 2.8 (the kernel rejects the Truly firmware).
   - Do not flash this on Infinity-X.

How to flash in TWRP
--------------------
- Copy the zip to the phone (or use an OTG drive).
- TWRP -> Install -> select the zip -> swipe to confirm.
- Reboot to system.

Notes
-----
- The fingerprint sensor on this unit is a Goodix sensor. The HAL on
  these ROMs fails with GF_ERROR_SENSOR_NOT_AVAILABLE and falls back to
  FocalTech, which creates the ff_key DPAD. Disabling the HAL is the
  reliable fix.
- A full ROM/vendor flash overwrites these changes, so re-flash
  Lime_FingerprintOff.zip after a full ROM flash if the flicker returns.
- If the touchscreen becomes unresponsive after a firmware change,
  flash Lime_Touch_Stock.zip in TWRP.
