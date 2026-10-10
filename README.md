# AY Lightning Pro v5.1 — Fast Wake & Optional Deep Sleep

**Developed by Eng. Ahmed Yasir**

AY Lightning Pro is a customizable Android performance and power-management module designed for KernelSU Next. It combines five distinct CPU governor profiles with fast screen-state monitoring and an optional, one-shot Deep Sleep feature.

### Key Features

- **Five CPU Profiles:** Maximum Performance, Balanced, Stability, Economy, and Ultra Saver.
- **Fast Wake Monitoring:** Targets approximately one-second screen-state checks while the display is off, helping the module respond more quickly when the screen turns on.
- **Optional Deep Sleep:** Temporarily enables Airplane Mode and disables Wi-Fi, with optional Bluetooth control, when the screen turns off.
- **Automatic Restoration:** Attempts to restore the previous wireless settings when the screen wakes up or the configured safety timeout expires.
- **Battery-Aware Stability:** Includes configurable safeguards for battery level and battery temperature in the Stability profile.
- **Interactive WebUI:** Manage profiles, configure Deep Sleep, and access diagnostic information through the module interface.
- **Safety-Focused Design:** Preserves Android's essential services and does not intentionally disable thermal protections or SELinux.

### Compatibility & Important Notes

Designed for KernelSU Next on compatible Android devices. Actual behavior depends on the device, kernel, ROM, and available CPU governors. Testing has primarily used mocked Android services; real-device compatibility should be verified after installation.

**Important:** Deep Sleep can interrupt incoming calls, SMS, mobile data, and network-dependent notifications while Airplane Mode is enabled. Use this feature only when temporary network disconnection is acceptable. Always keep a recovery method available.

**Version:** 5.1.0  
**Developer:** Eng. Ahmed Yasir
