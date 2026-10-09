# AAtoAndroid-display

**DiPlay plus an experimental wireless Android Auto receiver.** A paired Android phone can project Android Auto to an Android head unit over Bluetooth and Wi-Fi, next to DiPlay's existing wireless CarPlay. Maintained by [@saz-io](https://github.com/saz-io).

This repository is a snapshot of [DiPlay](https://github.com/shihabal3amri/DiPlay), CarPlay for compatible BYD Android head units, with the receiver added. Everything below the Android Auto section describes DiPlay itself.

> **Android Auto status:** experimental and **not yet tested with a real phone or in a car**. It is off by default, and it needs a head-unit identity file that this repository does not and cannot include. Read [docs/ANDROID_AUTO.md](docs/ANDROID_AUTO.md) before using it.

> **BYD support scope:** DiPlay focuses on BYD cars. It may work on other brands, but other brands are unsupported and there are no plans to add support or fix brand-specific incompatibilities.

[Android Auto guide](docs/ANDROID_AUTO.md) · [Report a problem with this repository](https://github.com/saz-io/AAtoAndroid-display/issues) · Upstream DiPlay: [download & website](https://shihabal3amri.github.io/DiPlay/) · [release](https://github.com/shihabal3amri/DiPlay/releases/tag/v0.2.15) · [issues](https://github.com/shihabal3amri/DiPlay/issues/new/choose)

## Android Auto (experimental)

- Wireless only: the phone finds DiPlay's Bluetooth service, joins the Wi-Fi network DiPlay creates, then connects over TCP with TLS.
- Video (H.264, up to 1080p at 30 or 60 fps), media, navigation and system audio, the car microphone, multi-touch and media keys.
- Uses the Wi-Fi mode you already chose for wireless CarPlay. Android Auto and CarPlay cannot run at the same time.
- Found under **Settings → Advanced → Android Auto (experimental)**, off by default.
- Driving status is always sent as restricted, because the car's speed is not read yet.
- Not included: wired USB, turn-by-turn data for the BYD cluster, media and phone metadata.
- The phone only accepts a head-unit TLS identity it recognises. DiPlay does not ship one; you import your own `headunit.pem` (see the guide).

Automated tests run the protocol against a scripted fake phone with real TLS. They do not show that a real phone accepts DiPlay. The guide lists the known risks.

## DiPlay 0.2.15 — public preview (upstream)

Install on the **car**, not the iPhone. No jailbreak, dongle, Mac, account or authentication server is required for use. Core CarPlay does not require ADB; optional dashboard, battery, wheel-speed and parked-video features do. Your head unit must permit APK installation. The APK supports Android 7.1+ (API 25); Android 7.1–8.1 support is new and not yet confirmed on a vehicle. Wireless supports Wi-Fi Direct, the car’s existing hotspot or Existing Wi-Fi / Same LAN. Android 7.1–9 Wi-Fi Direct uses a firmware-dependent legacy path with generated group credentials and unverified requested frequency; see [Android 9 Wi-Fi Direct](docs/ANDROID9_WIFI_DIRECT.md). Android 10+ verifies its negotiated group frequency.

- Wired USB and wireless CarPlay with local authentication.
- BYD HUD navigation with arrows, distance and street names on verified firmware.
- Car hotspot support, improved audio buffering and saved receive diagnostics.
- Automatic address discovery, fixed-channel Wi-Fi fallbacks and successful-configuration memory.
- Icon/text size, resolution and frame rate; applying a display change reconnects CarPlay.
- Local diagnostic export. Reports are sent only if you choose to share them.
- Separate installation alongside DiAuto. Run one projection app at a time.

This is **not an Apple-certified product**. The APK bundles an experimental accessory identity recovered from public Carlinkit firmware, not a newly provisioned MFi identity for DiPlay. A bundled private key is extractable. Acceptance after future iOS updates, reliability across head units and suitability of that identity for general distribution are unresolved. This release invites community testing; it is not a guarantee of universal compatibility.

Earlier releases were tested on the development DiLink5.1 car: live windshield guidance and street names work, Car hotspot now starts CarPlay, and Wi-Fi Direct performance is substantially improved. Audio underrun recovery is improved in 0.2.15; remaining cutouts need current diagnostic reports. The floating-map test build was installed on the development DiLink 5.1 car; feedback led to the pinch corrections in 0.2.9. Earlier wheel-speed and video contributions were tested on a BYD Tang with DiLink 5.0 and an iPhone 15 Pro on iOS 27; wheel-speed dead reckoning in tunnels remains unverified. Broader head-unit and iOS compatibility is not guaranteed. The HUD firmware scope and cleanup limits are documented in [BYD navigation](docs/BYD_NAVIGATION.md).

## What’s new in 0.2.15

- Android 7.1+ compatibility; older head units still need vehicle feedback.
- A first-launch DiLink setup guide and manual update checks in About.
- Light, Dark and Auto appearance, compact layouts and dedicated Language/About settings.
- Music prebuffer recovery after underruns and a main-video decoder hint with compatibility fallback.
- Wi-Fi Direct Auto 5 GHz/2.4 GHz choices and optional launch when the selected iPhone reconnects over Bluetooth.
- More precise dashboard turn-card placement, corrected turning-canvas geometry and optional small-window marker layouts.
- Experimental Bluetooth audio and explicit ADB boot-start repair; firmware-dependent options remain opt-in.

See [0.2.15 release notes](docs/RELEASE-NOTES-0.2.15.md) and [validation](docs/VALIDATION.md) for contribution links and remaining physical tests. General stutter, calls/Siri, decoder and model-specific reports still need current-device evidence. [0.2.14 notes](docs/RELEASE-NOTES-0.2.14.md) remain available as historical guidance.

If a problem remains, reproduce it on **0.2.15**, then use **Settings → Diagnostics → Save diagnostic report**. Android 10+ normally saves to **Downloads/DiPlay**; Android 7.1–9 uses the document picker. If unavailable, use **View report** or **Share** from the confirmation, which identifies external/private fallback storage. Review the `.txt` and add it to a matching [existing issue](https://github.com/shihabal3amri/DiPlay/issues), or [create one](https://github.com/shihabal3amri/DiPlay/issues/new/choose). Include vehicle/head-unit model, exact firmware and Android/DiLink, phone/iOS, connection backend, relevant settings, steps and failure time. Reports are shared only when you choose; never post your hotspot password.

## Documentation

[Existing Wi-Fi / Same LAN](docs/EXISTING_WIFI.md) keeps the iPhone and head unit
on an external router. See the guide for setup, build requirements and the
BYD DiLink 4.0 / Android 10 clean-install validation result.

- [Install and connect](docs/INSTALL.md)
- [Compatibility and troubleshooting](docs/COMPATIBILITY.md)
- [Smooth wireless CarPlay](docs/SMOOTH_WIRELESS.md)
- [Android Auto from an Android phone (experimental)](docs/ANDROID_AUTO.md)
- [Privacy and diagnostic reports](docs/PRIVACY.md)
- [Build from source](docs/BUILD.md) — select `mobile` for the main DiPlay app; `maphost` is a map sample.
- [Validation](docs/VALIDATION.md)
- [Release notes](CHANGELOG.md)
- [Credits and licenses](docs/THIRD_PARTY_NOTICES.md)

The app is available in English, Arabic, Russian, Ukrainian, Spanish, Simplified Chinese and Traditional Chinese (Taiwan). Traditional Chinese uses Taiwan wording; the app also recognizes Hong Kong/Macao and explicit Hant selections without claiming separate regional translations. Choose the app language in Settings; on Android 13+, it stays synchronized with Android’s per-app language setting.

## Source and credits

Based on [xcertplay](https://github.com/shilapi/xcertplay), GPL-3.0. The home/settings UI and website adapt [DiAuto](https://github.com/shihabal3amri/DiAuto), AGPL-3.0; that license is included in `docs/licenses`. Preserve those notices when distributing modifications. CarPlay and its icon belong to Apple Inc.; no Apple or BYD affiliation or endorsement is implied.

The Android Auto receiver was added by [@saz-io](https://github.com/saz-io). Its message layouts were read from the public protocol definitions in [OpenCarDev aasdk](https://github.com/opencardev/aasdk) (GPL-3.0); no code was copied from it. Android Auto is a trademark of Google LLC; no Google affiliation or endorsement is implied.

This repository is a single-commit snapshot, so the commit history of the upstream projects is not included; see their repositories for it. It starts with a clean public source snapshot. Local research, tester reports and release-signing secrets are excluded. The complete source corresponding to the APK is provided with every release; experimental runtime identity assets are described separately in the build instructions and notices.

## Local release packaging

The release APK intentionally contains the experimental accessory identity. The Git repository and source archive exclude all accessory and Android signing keys; tests generate synthetic identities at runtime. Source/CI builds omit runtime identity assets by default. Local release builds explicitly select an external asset directory. Publishing the APK makes its bundled identity extractable; building locally does not preserve that identity's confidentiality.
