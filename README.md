# ⚡ AY KILL APP — LIGHTNING PRO v8.0.0

<p align="center">
  <img src="assets/ay-lightning-v8-banner.png" alt="AY KILL APP — Lightning Pro Studio v8.0.0 | Designed and Developed by Eng. Ahmed Yasir" width="100%">
</p>

<p align="center">
  <strong>The Next Generation of Android Performance Control</strong><br>
  Real-Time Telemetry · Adaptive Automation · Deep Sleep Ultra · Advanced Studio<br>
  <strong>Designed &amp; Developed by Eng. Ahmed Yasir</strong>
</p>

<p align="center">
  <img alt="Version" src="https://img.shields.io/badge/Version-8.0.0-F9C900?style=flat-square&labelColor=101010">
  <img alt="KernelSU Next" src="https://img.shields.io/badge/Platform-KernelSU%20Next-F9C900?style=flat-square&labelColor=101010">
  <img alt="Language" src="https://img.shields.io/badge/WebUI-Arabic%20%7C%20English-F9C900?style=flat-square&labelColor=101010">
</p>

**Version:** `v8.0.0` · **Build:** `800` · **Module ID:** `eng_ahmed_yasir_screen_gov`  
**Primary platform:** KernelSU / KernelSU Next · **Developer:** Eng. Ahmed Yasir

> [!IMPORTANT]
> AY KILL APP is a **root-level Android tuning module**, not a normal Android application. Settings and functions depend on your Android version, ROM, kernel, root manager, and supported hardware interfaces. **v8.0.0 has been tested in simulated environments, but not on a physical Android device.** Keep a backup and recovery method before installation.

## ✨ Meet Lightning Pro 8.0

**AY KILL APP | Lightning Pro v8.0.0** upgrades the v7 performance toolkit with a fully redesigned, responsive **Black & Gold Command Center**. It adds real device-status readouts, local session graphs, optional CPU automation, and richer diagnostics while preserving the original CPU profiles, gaming features, Deep Sleep Ultra behavior, advanced Studio controls, and the existing module identity.

The objective is **transparent, reversible device control**, not guaranteed FPS, battery-life, or benchmark improvements. Unsupported kernel settings are not presented as universally available.

### What's new in v8.0.0

| Upgrade | What it does |
|---|---|
| 🎨 **Command Center WebUI 8.0** | Rebuilt, offline, bilingual interface with new desktop navigation, mobile dock, searchable panels and quick CPU profile switching. |
| 📊 **Live Device Telemetry** | Read-only CPU policy frequency, supported thermal sensor, RAM usage, battery and system-load information. |
| 📈 **Session Performance Analytics** | In-page CPU/thermal/RAM trend charts; adjustable refresh interval and CSV export. |
| ⚡ **Adaptive Automation** | Optional low-battery `powersave` and charging-time `schedutil` governor requests, only on supported kernels. |
| 🧪 **Advanced Diagnostics & Reports** | Compatibility indicators, monitor health, conflict hints, service logs, and exportable/copyable technical reports. |
| 💾 **Backup Improvements** | Newly saved backup slots include v8 automation options; the upgrade retains the same persistent-settings path. |
| 🧩 **Preserved v7 Engine** | All 19 pre-existing control panels remain accessible alongside the 3 new v8 panels: **22 panels in total**. |

## 🖥️ WebUI Preview

<p align="center">
  <img src="assets/webui-v8-desktop.png" alt="AY KILL APP v8 desktop Command Center preview" width="77%">
  <img src="assets/webui-v8-mobile.png" alt="AY KILL APP v8 mobile Command Center preview" width="21%">
</p>

*Previews are browser-rendered with simulated root-bridge responses. They are **not** evidence of running features on a physical Android device.*

## 🚀 Core Feature Overview

| Studio / System | Capabilities |
|---|---|
| **CPU Profiles** | Five modes: Extreme, Normal (Balanced), Stability, Quiet, Ultra (Save); supported governors and CPU frequency limits. |
| **Screen-off Intelligence** | Independent CPU power-saving timer, **60 seconds by default**, with configurable intervals. |
| **Deep Sleep Ultra** | Manual or optional timed offline mode, radio management, eligible user-app force-stop and explicit connectivity restoration. |
| **Auto Gaming** | Managed game list and optional foreground-game CPU optimization on compatible kernel policies. |
| **GPU Studio** | Supported GPU governor / min-max frequency controls with device capability checks and reset tools. |
| **RAM Lab** | RAM, swap, ZRAM and MGLRU readings; supported VM memory tuning. |
| **I/O Studio** | Compatible I/O scheduler and storage read-ahead controls. |
| **Kernel Lab** | Selected scheduling, TCP and wake settings exposed by the current kernel/ROM. |
| **Process Manager** | App standby settings and compatible animation / BLE scan options. |
| **Render Engine** | Per-app ANGLE preferences where supported by Android. |
| **Network Tools** | Private DNS over TLS, supported congestion-control choices and network diagnostics. |
| **Power & Battery** | Battery/thermal status, conservative charging-current limits and device-dependent underclocking. |
| **System Maintenance** | FSTRIM, compatible system options, backup slots, original-value restoration and module conflict hints. |

> A supported kernel interface is not proof that its modification will improve performance. Changes to governors, background behavior, radios or charging settings can have unintended effects.

## 🧠 Adaptive Automation Studio — New

Automation is **disabled by default**. Enable it from **WebUI → Adaptive Automation** only after reviewing device compatibility.

- **Low battery:** choose `20%`, `30%`, `40%`, `50%`, or `off`. On a discharging device with the screen on, automation may request `powersave` if supported.
- **Charging:** optionally request `schedutil` while the device is charging, only if supported.
- **Priority:** Deep Sleep and existing battery/thermal safeguards take precedence; foreground gaming has priority over the charging preference. Screen-off rules remain independent.
- **Saved choice:** runtime automation does **not** overwrite the selected CPU profile; disabling automation returns control to the normal saved policy on the next applicable monitoring cycle.
- **Safety:** automation never intentionally increases charging current or bypasses OEM thermal protection. The monitor must be active for the runtime rules to operate.

## 🌙 Screen-off Intelligence vs Deep Sleep Ultra

These are **two separate behaviors**:

| | Screen-off Intelligence | Deep Sleep Ultra |
|---|---|---|
| Default timing | After **60 seconds** of screen off | Automatic trigger after **60 minutes** of uninterrupted screen off, **if enabled** |
| Main action | Request a supported battery-saving **CPU policy** | Attempt radio shutdown, optional eligible app force-stop, and CPU power saving |
| On screen wake | Restore the selected CPU policy at the next monitor observation | Restore the selected CPU policy after an OFF → ON cycle; **radios remain off** |
| Connection restoration | No normal connection shutdown | Requires manual **Restore Connections / Cancel** except best-effort failure/reboot/uninstall recovery |

> [!WARNING]
> **Deep Sleep Ultra can disable Wi-Fi, mobile connectivity, Bluetooth, NFC and/or hotspot controls, depending on Android support.** Incoming calls, SMS, authentication codes, emergency callbacks and notifications may be missed. Opening the screen **does not automatically restore radio connections**. Never enable automatic offline Deep Sleep if you must remain reachable.

Some ROMs restrict radio commands or prevent reliable restoration. Deep Sleep can report **Pending**, **Active**, **Partial** or **Error**; check the actual outcome before assuming the phone is offline or restored. Force-stop may lose unsaved app work.

## 🔧 Installation / Upgrade

### Requirements

- Rooted Android phone with **KernelSU / KernelSU Next** or a compatible manager.
- Supported WebUI root bridge (the interface detects supported KernelSU and compatible MMRL-style bridges).
- Kernel nodes providing the functions you want to change.
- A recent backup and a tested recovery route.

### Updating from v7.0.0

1. Save a backup using the existing v7 WebUI and note any custom kernel options.
2. Temporarily disable conflicting CPU/GPU/kernel tuning modules.
3. Install `AY_KILL_APP_Lightning_Pro_v8.0.0_Eng_Ahmed_Yasir.zip` through the supported root manager.
4. Reboot and open the module **WebUI** from the root manager. Opening `index.html` directly in a regular browser is a visual preview only; it cannot execute root commands.
5. Visit **Diagnostics / Compatibility**, check the monitor, and test one feature at a time.
6. Test ordinary screen-off CPU saving first. Only test Deep Sleep when you can reliably restore connectivity.

**Upgrade continuity:** the module ID stays `eng_ahmed_yasir_screen_gov`; in-place upgrades are designed to preserve settings stored under `/data/adb/ay_lightning`. **Uninstalling** rather than upgrading intentionally removes module-owned persistent data. Actual upgrade behavior must still be confirmed on your device.

### Action button

The module's **Action** button retains its manual Deep Sleep toggle: request offline mode on activation; request radio restoration on the next toggle. This is a fallback when WebUI control is unavailable.

## 📊 Telemetry, Reports & Privacy

- CPU MHz displays the **average reported CPU frequency policy**, **not** measured CPU utilization or FPS.
- Temperature is read from a supported available sensor, which may **not** represent a universal CPU die temperature.
- Graph samples are held in the WebUI session memory (up to **80 samples**) and discarded when the page closes.
- Refresh options: **12 / 20 / 30 seconds**; CSV export uses collected session values.
- Charts and monitoring are local. **No telemetry is sent to a remote server** by the bundled code.
- Diagnostic reports can contain package names, device/system details and service logs. **Review or redact before sharing publicly.**
- The root manager's WebView may restrict downloads; use **Copy** where offered.

## 🛠️ Root CLI / Troubleshooting

Run these commands only in an **authorized root shell** on a device where the module is installed:

```sh
su
MODULE=/data/adb/modules/eng_ahmed_yasir_screen_gov

sh "$MODULE/control.sh" status
sh "$MODULE/control.sh" telemetry
sh "$MODULE/control.sh" logs
sh "$MODULE/control.sh" set-profile normal
sh "$MODULE/control.sh" screen-delay 120
sh "$MODULE/control.sh" automation-set 1 30 off
sh "$MODULE/control.sh" automation-set 0 off off
sh "$MODULE/control.sh" studio list
sh "$MODULE/control.sh" studio reset-all
sh "$MODULE/control.sh" backup-save 1
sh "$MODULE/control.sh" deep-cancel
```

If Deep Sleep leaves connections off, choose **Restore Connections** in WebUI or run `deep-cancel`. Android/ROM restrictions may still require manual reconnection. If governor choices fail, check exposed kernel governors, the monitor state and overlapping tuning modules. Studio's **Reset All** is best-effort and can only restore values that are still accessible.

## 🛡️ Safety & Compatibility

- No intentional **thermal-protection bypass, SELinux disablement, watchdog deactivation**, unsupported GPU governor injection or arbitrary sysfs editing.
- No uncontrolled charging-voltage/current increase or active ZRAM resizing.
- Kernel, ROM, device and root manager differences affect feature availability; unsupported operations may fail or be rejected.
- Background-process restrictions and app force-stop can delay or prevent notifications and may interrupt ongoing work.
- No guaranteed FPS, latency, power-saving or temperature improvements are claimed for every device.

### Validation status

**Completed for this v8.0.0 build:** shell syntax validation, simulated governor/battery automation tests, mock root-bridge WebUI interactions on mobile and desktop, and ZIP structure checks.

**Not completed:** testing on a physical Android phone, real root-manager compatibility, thermal endurance, long-term battery measurements and real-world gaming benchmarks.

## 📝 Changelog — v8.0.0

- Completely rebuilt offline Black & Gold WebUI with responsive desktop/mobile navigation.
- Introduced new live CPU/thermal/RAM status cards and local charts with CSV export.
- Added opt-in battery/charging adaptive CPU automation with device support checks.
- Added expanded diagnostics, compatibility summary and exportable text report.
- Extended newly saved backups with automation settings while retaining v7 backup compatibility.
- Preserved v7 CPU/GPU/RAM/gaming/network/Deep Sleep features and their underlying control panels.
- Preserved original module ID, configuration storage approach and recovery semantics.

For release notes see [`Description_Changelog.txt`](Description_Changelog.txt).

## 🇸🇦 العربية — ملخص الإصدار

**AY KILL APP | LIGHTNING PRO v8.0.0** هو تحديث لموديول التحكم بأداء هواتف أندرويد المروّتة، مع واجهة جديدة باللونين الأسود والذهبي، ولوحة قراءات مباشرة للمعالج والحرارة والذاكرة، ورسوم بيانية محلية، وتقارير تشخيص وأتمتة اختيارية للمعالج وفق حالة البطارية والشحن.

- **تم الحفاظ** على أوضاع CPU الأساسية، وخصائص GPU وRAM والألعاب والنوم العميق وأدوات الاستعادة من الإصدار السابع.
- **توفير الشاشة المغلقة** يبدأ بعد 60 ثانية افتراضيًا ويغيّر سياسة المعالج فقط، دون فصل الاتصالات بشكل اعتيادي.
- **Deep Sleep Ultra** وضع منفصل قد يفصل الشبكات ويوقف بعض تطبيقات المستخدم، ويمكن تفعيله تلقائيًا بعد 60 دقيقة متصلة من إطفاء الشاشة إذا اخترت ذلك.
- **فتح الشاشة لا يعيد الشبكات** التي فُصلت بواسطة Deep Sleep؛ يجب استخدام **Restore Connections** أو أمر `deep-cancel`.
- **الأتمتة الجديدة معطلة افتراضيًا**، ولا تعمل إلا وفق إمكانيات النواة ووجود خدمة المراقبة.
- **الاختبارات الحالية محاكاة وبرمجية فقط**، ولم يُختبر الإصدار حتى الآن على هاتف أندرويد فعلي.

> ⚠️ **تحذير:** قد يؤدي وضع Deep Sleep إلى فقدان المكالمات والرسائل والإشعارات أو تعذّر عودة الاتصالات تلقائيًا. احتفظ دائمًا بطريقة آمنة للاستعادة والنسخ الاحتياطي قبل التجربة.

---

<p align="center">
  <strong>⚡ AY KILL APP — LIGHTNING PRO 8.0.0</strong><br>
  <em>Optimize · Control · Extend · Unleash</em><br>
  Designed &amp; Developed by <strong>Eng. Ahmed Yasir</strong>
</p>

*No project license or redistribution terms were provided with the supplied release. The project maintainer should select and publish a suitable license if third-party reuse is intended.*
