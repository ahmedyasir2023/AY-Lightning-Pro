# AY KILL APP — Lightning Pro Studio v7.0.0

<p align="center">
  <img width="2752" height="1536" alt="AY7 0 0" src="https://github.com/user-attachments/assets/655d786c-710e-42ff-9f16-693f690d1dd1" />
</p>

<p align="center">
  <strong>Performance control · Intelligent screen-off saving · Deep Sleep Ultra · Kernel tuning</strong><br>
  Designed &amp; Developed by <strong>Eng. Ahmed Yasir</strong>
</p>

**Version:** `v7.0.0` &nbsp;|&nbsp; **Module ID:** `eng_ahmed_yasir_screen_gov` &nbsp;|&nbsp; **Primary platform:** KernelSU / KernelSU Next

> [!IMPORTANT]
> This is a **root-level system tuning module**, not an ordinary Android app. Features depend on Android, OEM firmware, kernel nodes and root-manager WebUI support. The release has undergone **script-level and simulated integration testing**, but has **not been validated on a physical Android device**. Use with care and keep a known-working recovery path.

## Overview

**AY KILL APP v7** (Lightning Pro Studio) combines performance profiles, intelligent screen-off CPU management, a manually controlled offline Deep Sleep mode, gaming optimizations and a searchable, bilingual WebUI. Its advanced Studio panels expose selected GPU, memory, I/O and kernel settings **only where supported by the device**.

The goal is to provide **transparent, reversible controls** rather than claim universally faster performance or guaranteed battery savings. The module checks supported values when possible, reports partial failures and avoids intentional thermal-protection bypasses.

### Key highlights

- **Five performance profiles** with CPU-governor selection and supported frequency controls.
- **Screen-off Intelligence:** power-saving governor after **60 seconds** by default; change or disable the delay.
- **Fast CPU-profile restoration** on screen wake, at the next monitor observation.
- **Deep Sleep Ultra:** request offline mode from **WebUI** or toggle it with the module **Action** button.
- **Independent connection control:** waking the screen restores the chosen CPU profile, **not Wi-Fi/mobile/Bluetooth connections**.
- **Automatic Deep Sleep** after **60 uninterrupted minutes** of screen-off time, if enabled.
- **Optional force-stop of eligible user apps** during Deep Sleep; essential Android services and root managers are protected.
- **GPU Studio, RAM Lab, I/O Studio, Kernel Lab** with device-capability checks and original-value restore options.
- **Auto Gaming, per-app ANGLE options, Private DNS, conservative charging controls, FSTRIM and diagnostics.**
- **Black-and-gold WebUI** with searchable Bento panels, Arabic/English and light/dark appearance settings.

## WebUI previews

| Dashboard | Deep Sleep Ultra | GPU Studio |
|:---:|:---:|:---:|
| <img src="assets/webui-home.png" alt="WebUI dashboard" width="250"> | <img src="assets/webui-deep-sleep.png" alt="Deep Sleep panel" width="250"> | <img src="assets/webui-gpu-studio.png" alt="GPU Studio panel" width="250"> |

*These are browser-rendered design previews with simulated root-bridge responses, not screenshots proving operation on a physical phone.*

## Feature breakdown

| Category | Available controls | Important behavior |
|---|---|---|
| **CPU Profiles** | Extreme, Normal, Stability, Quiet, Ultra; governor and supported CPU-frequency policies | Governor availability varies by kernel; unsupported writes report an error. |
| **Screen-off Intelligence** | Delay: Off, 15, 30, 60, 120, 180, 300, 600, 900 or 1800 seconds | Default is **60 s**. It changes CPU policy, **not** your connectivity. |
| **Deep Sleep Ultra** | WebUI queued activation; Action toggle; connectivity control; optional user-app force-stop; auto sleep | **Manual connection restoration.** See workflow below. |
| **GPU Studio** | GPU governor, minimum and maximum frequency when the kernel exposes supported nodes and choices | Does not deliberately exceed the original GPU maximum. |
| **RAM Lab** | Readouts: RAM, Swap, ZRAM and MGLRU; tunable VM settings such as swappiness, cache pressure and dirty ratios | Active ZRAM is **not** resized or reinitialized by this release. |
| **I/O Studio** | Supported block-device I/O scheduler and read-ahead settings | Storage-device support differs; options appear as unsupported if absent. |
| **Kernel Lab** | Selected scheduler settings, TCP ECN and double-tap-to-wake where exposed | Hardware- and ROM-dependent; no arbitrary sysfs editing. |
| **Process Manager** | Per-app standby buckets, animation scales, BLE background-scan preference | Restricting background apps may delay notifications. |
| **Gaming** | User-managed game list, optional foreground-game CPU boost | Operates on detected apps and supported CPU policies. |
| **Render Engine** | Per-app ANGLE preferences on compatible Android builds | Not every ROM/app supports renderer switching. |
| **Networking** | Private DNS (DoT) providers/custom hostname; compatible TCP congestion control options; network tools | No guaranteed network-speed or ping improvement. |
| **Power & charging** | Battery/thermal readouts; supported underclocking and conservative input-current caps | Does **not** intentionally raise charging current above the device's original setting. |
| **System tools** | Display-size presets, optional core saver, FSTRIM, cache-related controls, module conflict detection | Use caution: display changes and background actions may affect usability. |
| **Maintenance** | Three backup slots, diagnostics, log viewer, original-value reset tools, monitor restart | Reset is best-effort if the ROM or another module changed the same value. |

### CPU profiles

| Profile | Intended purpose | Requested CPU governor |
|---|---|---|
| **Extreme** | Highest available performance policy | `performance` |
| **Normal** | Everyday balance | `schedutil` |
| **Stability** | Balanced policy with conservative battery/temperature safeguards | `schedutil` + guards |
| **Quiet** | More conservative behavior | `conservative` |
| **Ultra** | Maximum supported CPU saving | `powersave` |

A profile can be applied only when the relevant CPU policies support the requested governor. A selected profile is **not** a guaranteed FPS, temperature, or battery-life target.

## How power saving and Deep Sleep work

**There are two independent timers.** This separation is a core design decision in v7.

### A. Normal screen-off CPU saving (default: 60 seconds)

1. Select a performance profile (for example, **Extreme**).
2. Turn the screen off. The selected CPU policy is initially retained.
3. After **60 seconds** of continuous screen-off time (configurable), the module requests the supported power-saving CPU governor.
4. Turn the screen back on. The monitor requests the **previously selected CPU policy** again at its next screen observation.
5. Connectivity is **not intentionally disconnected** by this normal screen-off saver.

Configure this in **WebUI → Screen-off Intelligence**. Available delay values are `off`, `0`, `15`, `30`, `60`, `120`, `180`, `300`, `600`, `900`, and `1800` seconds. `off` disables ordinary delay-based saving; `0` requests the saving governor immediately when the screen turns off.

### B. Deep Sleep Ultra (manual or automatic offline mode)

1. Tap **Activate Deep Sleep** in WebUI, or use the module **Action** button. The WebUI **queues** the request so the interface does not have to wait through long radio commands; the monitor performs it and reports the result.
2. The module attempts the configured connectivity shutdown: airplane mode/mobile connectivity, Wi-Fi, Bluetooth, NFC where supported, and hotspot/SoftAP. One or more radios may be unsupported or controlled differently by the ROM.
3. If enabled, eligible **third-party/user applications** are force-stopped. Root managers, core Android services, the launcher, input method, dialer and critical foreground controller are excluded. Apps can restart later, and unsaved work can be lost.
4. The CPU is requested to switch to `powersave` immediately while the device prepares for sleep.
5. After a genuine **screen OFF → screen ON** cycle, the selected CPU profile (for example, `performance` for Extreme) returns, **while the radios remain disconnected**.
6. **Connections are restored only by a manual Cancel/Restore command**, apart from recovery behavior after a failure, reboot or uninstall.

**Automatic Deep Sleep:** if enabled, it is triggered after **60 uninterrupted minutes** with the screen off. This timer is **separate** from the normal 60-second CPU saver. Do not confuse them.

> [!WARNING]
> While connectivity is disabled you may **miss phone calls, emergency callbacks, SMS, verification codes, mobile data and internet notifications**. Do not enable automatic Deep Sleep when you need to remain reachable. System recovery on reboot may attempt to restore radio states, but ROM restrictions can require manual intervention.

### When Deep Sleep is partial or does not start

- Open **Deep Sleep Ultra** and inspect the displayed **Pending / Active / Partial / Error** state.
- If the request is pending, wait for the monitoring service to finish before retrying.
- If partial, use **Retry**, review the diagnostic warning, or **Cancel** to restore your previous connection states.
- If WebUI is not connected to the supported root bridge, use the module **Action** button or root shell commands below.

## Installation

### Requirements

- A **rooted Android device** with a compatible module manager. The primary target is **KernelSU / KernelSU Next**.
- A compatible WebUI host providing a supported root-command bridge (the bundled interface detects KernelSU and compatible MMRL-style bridges). Opening `index.html` as a normal web page **cannot execute root controls**.
- A kernel exposing supported CPU/GPU/VM/I/O nodes for the features you intend to use.
- A recent backup and access to a working recovery method before changing root-level settings.

### Install / update

1. Back up any important data and note your current kernel settings.
2. Disable or remove **other CPU/GPU/kernel tuning modules** that might overwrite the same settings.
3. In **KernelSU / KernelSU Next**, install the `AY_Kill_App_v7_0_0_Lightning_Studio_Eng_Ahmed_Yasir.zip` module package.
4. Reboot the phone.
5. Open **AY KILL APP | Lightning Pro → WebUI**. Confirm that the monitoring service shows **Running** and that the device capability panel loads.
6. Select a CPU profile, test the **normal screen-off saver**, and only then test **Deep Sleep Ultra** manually, while you can safely restore connectivity.

The module ID remains `eng_ahmed_yasir_screen_gov` to allow an upgrade path from earlier releases. **Manager compatibility and successful upgrade behavior must still be verified on your device.**

### Optional: module Action button

The **Action** button is a manual toggle: the first press attempts to enter Deep Sleep, and the next press attempts to restore your previous radio states. It is a fallback if the WebUI root bridge is unavailable.

## Advanced Studio: supported settings and rollback

Studio reads a **fixed allowlist** of available system nodes rather than allowing arbitrary kernel paths. Examples:

- **GPU:** governor; GPU minimum and maximum supported frequencies.
- **VM:** `swappiness`, `vfs_cache_pressure`, `page-cluster`, dirty-memory ratios and watermark controls.
- **I/O:** storage scheduler and block-device read-ahead.
- **Kernel & network:** scheduler autogroup, supported double-tap-to-wake node and TCP ECN.
- **Android settings:** application standby buckets, animation scales, BLE scanning preference.

For supported writable settings, the module stores the original value, applies the requested change and **reads it back** where possible. Individual **Reset** and **Reset All** options can restore recorded values. Desired Studio settings may be re-applied after reboot, subject to availability and validation.

**A “Supported” label means a usable node was detected; it does not prove that changing it improves the phone.** Some firmware services can override the new value. Rollback is best-effort when a node disappears or other modules interfere.

For safety, the release does **not** deliberately disable OEM thermal controls, SELinux or the kernel watchdog, nor does it apply uncontrolled charging-current/voltage increases. It does not live-resize active ZRAM.

## CLI / troubleshooting

Commands below are intended for an **authorized root shell on your own device**. Adjust the path only if you knowingly installed a renamed module ID.

```sh
su
MODULE=/data/adb/modules/eng_ahmed_yasir_screen_gov

sh "$MODULE/control.sh" status
sh "$MODULE/control.sh" logs
sh "$MODULE/control.sh" screen-delay 120
sh "$MODULE/control.sh" screen-delay off
sh "$MODULE/control.sh" deep-request   # queue through the daemon
sh "$MODULE/control.sh" deep-now       # immediate request (may block)
sh "$MODULE/control.sh" deep-cancel    # restore saved connections
sh "$MODULE/control.sh" studio list
sh "$MODULE/control.sh" studio reset-all
```

**Useful diagnostics:**

- **WebUI → Diagnostics / Logs** shows monitor state and errors reported by the module.
- **WebUI → Device Compatibility** shows read-only or writable support status for individual Studio controls.
- **Deep Sleep Partial** means a requested radio change could not be confirmed; it does **not** mean the phone is guaranteed offline.
- If CPU settings appear unchanged, check the selected profile, supported governors, monitoring service and competing tuning modules.
- If screen state is unknown or the service is stopped, automatic timers may not run reliably.
- If the phone cannot reconnect, invoke `deep-cancel` from a working root shell, then manually restore settings in Android if needed.
- Avoid combining multiple kernel tuners during diagnosis. Test one variable at a time.

## Compatibility and limitations

- **Kernel/ROM-specific:** MIUI, HyperOS, AOSP and different OEM kernels expose different paths and access permissions; not all controls can work universally.
- **Speed of wake restore:** determined by the monitoring interval, screen-state detection and Android service responsiveness; the module does **not** promise zero-millisecond restore.
- **Force-stop:** deliberately excludes protected system and root-related components. It does **not** guarantee that every application remains stopped.
- **Connectivity shutdown:** airplane-mode handling and NFC/SoftAP command availability vary; the **reported state must be checked**.
- **Potential side effects:** blocked calls/notifications, changed app background behavior, unsaved app data, reduced performance, unstable kernel tuning or settings overridden by the ROM.
- **Benchmarks:** no device-specific battery-life, gaming-FPS, temperature or latency gains have been independently measured for this release.
- **WebUI:** the design previews are illustrative. A real, supported root bridge is required to apply controls.

## What changed in v7.0.0?

- New official **AY KILL APP v7.0.0** branding/banner provided by the developer.
- Deep Sleep activation from WebUI now uses a **queued daemon request**, improving responsiveness and providing visible execution status.
- Added independent **Screen-off Intelligence**, with a configurable **60-second default**.
- Retained automatic Deep Sleep after **60 minutes**, separate from the screen-off CPU timer.
- Restores the selected CPU performance profile after wake while keeping manually disabled connections **offline** until cancellation.
- Expanded **GPU Studio, RAM Lab, I/O Studio, Kernel Lab and Process Manager** with support detection and rollback controls.
- Updated black/gold, searchable **WebUI** with detailed panels and diagnostics.
- Preserved existing **gaming, ANGLE, DNS, network, battery, backup, thermal readout and module detection** tools where supported.
- Kept original OEM safety controls; omitted dangerous generic thermal and charging overrides.

For an expanded plain-text changelog, see [`Description_Changelog.txt`](Description_Changelog.txt).

## Testing status

The release was checked with **shell-script tests, simulated Android command/radio behavior, screen-off/screen-on state tests, WebUI-to-root-bridge simulation and ZIP integrity checks**. These checks validate selected flows in a controlled environment, **not on-device compatibility**.

**No real-phone endurance, thermal-safety or battery-consumption testing is claimed.** Community feedback should include device model, Android/ROM version, root manager and redacted logs; do not post personal identifiers or private data in public issues.

## العربية — ملخص سريع

**AY KILL APP v7.0.0** موديول لإدارة أداء المعالج والطاقة والنوم العميق في الهواتف المروّتة، مع واجهة WebUI عربية وإنجليزية.

- بعد إطفاء الشاشة لمدة **60 ثانية افتراضيًا** ينتقل CPU إلى سياسة التوفير المدعومة. يمكن تغيير المدة أو تعطيلها.
- عند تشغيل الشاشة يعود **بروفايل الأداء المختار** في دورة المراقبة التالية.
- وضع **Deep Sleep Ultra** يفصل الاتصالات ويحاول إيقاف تطبيقات المستخدم المؤهلة، مع استثناء تطبيقات الروت وخدمات النظام الضرورية.
- **فتح الشاشة لا يعيد الاتصالات**؛ تتم الاستعادة يدويًا من WebUI أو Action، مع وجود مسارات استرجاع احتياطية بعد فشل العملية أو إعادة التشغيل.
- التفعيل التلقائي للنوم العميق بعد **60 دقيقة متصلة** من إطفاء الشاشة مستقل عن مؤقت توفير CPU.
- جميع إعدادات النواة المتقدمة تعتمد على إمكانيات الجهاز الفعلية، ولم يتم اختبار هذا الإصدار على هاتف حقيقي بعد.

> **تنبيه:** قد لا تستقبل المكالمات أو الرسائل أو الإشعارات أثناء فصل الشبكات. اختبر الموديول يدويًا أولًا ولا تعتمد على النوم العميق عندما تحتاج إلى البقاء متصلًا.

---

**Developer:** Eng. Ahmed Yasir  
**Project:** AY KILL APP — Lightning Pro Studio  
**Release:** v7.0.0 (`versionCode=700`)  
**Root module ID:** `eng_ahmed_yasir_screen_gov`

*License/redistribution terms have not been specified in the supplied release. The project maintainer should choose and publish an appropriate `LICENSE` file before inviting third-party reuse or contributions.*
