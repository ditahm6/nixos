For booting NixOS from USB on your Acer laptop, the key fix was adding these boot parameters at the initial NixOS installer menu:

```
edd=off nomodeset video=1024x768 debug console=tty0 i915.modeset=0
```

The steps were:
1. Press F12 at startup to get boot menu
2. Select the USB drive
3. At the NixOS installer menu, press 'e' to edit
4. Add those parameters to the line starting with "linux" or "linuxefi"
5. Press F10 or Ctrl+X to boot with the parameters

This combination worked because:
- `edd=off` disabled Enhanced Disk Device detection that was causing the initial hang
- `nomodeset` and `i915.modeset=0` handled the Intel graphics issues
- `video=1024x768` forced a safe display mode
- `console=tty0` ensured output went to the right display
- `debug` showed the boot messages so we could see what was happening

These parameters were specifically important for your Acer laptop with the Celeron N3060 processor and Intel graphics.