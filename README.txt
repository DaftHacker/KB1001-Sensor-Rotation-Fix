KB1001 Sensor Rotation Fix
===========================

This module persists the exact live-tested fix that corrected auto-rotation:

  ro.vendor.gsi_gsen_rotation=180
  ro.vendor.sf.rotation=90

It intentionally DOES NOT modify:
  ro.surface_flinger.primary_display_orientation

That display property must remain at ORIENTATION_90 because changing it caused
touch/swipe coordinates and SystemUI input to become misaligned.

Install:
  Magisk -> Modules -> Install from storage -> select this ZIP -> Reboot

Verify after reboot:
  adb shell getprop ro.vendor.sf.rotation
  adb shell getprop ro.vendor.gsi_gsen_rotation
  adb shell getprop ro.surface_flinger.primary_display_orientation

Expected:
  90
  180
  ORIENTATION_90

If auto-rotation does not react immediately after boot:
  adb shell su -c "stop vendor.sensors-default"
  adb shell su -c "start vendor.sensors-default"

Removal:
  Disable/remove this module in Magisk and reboot.
