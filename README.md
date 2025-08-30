(Original Fork Network Left)

# iOS 18.5 Bluetooth Privacy Vulnerabilities

> ⚠ Silent BLE Scanning, Metadata Exposure, and Covert GPS Activation on iPhone

---

##  Overview

This repository documents a high-severity set of privacy violations in **iOS 18.5**, where multiple native Apple system processes (daemons) perform unauthorized actions related to Bluetooth and location services — all without user awareness or consent.

The research was performed using official Apple tooling (Console.app) on a **stock iPhone 14 Pro Max** running **iOS 18.5**, with **no jailbreak**, **no MDM**, and **no third-party apps**.

**Log Evidence:** 
(https://ia801505.us.archive.org/16/items/bluetooth-hacks-your-life/ios18.5_silent_tracking_console_capture.mov)

---

##  Report Summary

| ID       | Component              | Description                                      | Impact                                     |
|----------|------------------------|--------------------------------------------------|--------------------------------------------|
| VF-001   | `audioaccessoryd`      | Surfaces Bluetooth trust metadata (e.g. IRKs)   | Passive identity tracking                  |
| VF-002   | `SPCBPeripheralManager`| Triggers silent BLE scans in background          | Device becomes discoverable without notice |
| VF-003   | `locationd`            | Covert GPS harvesting without UI or consent      | Silent location tracking                   |
| VF-004   | `tccd`                 | Bypasses TCC privacy permissions using a flag    | Consent enforcement disabled               |
| VF-005   | `bluetoothd`           | Continues trust logic after crypto failures      | Weakens BLE trust enforcement              |

---

