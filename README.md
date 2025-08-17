# iOS 18.5 Bluetooth Privacy Vulnerability Report

>  **Silent Bluetooth Scanning, Metadata Exposure, and Covert GPS Harvesting on iOS 18.5**

##  Overview

This repository documents a high-severity set of privacy violations discovered in **iOS 18.5** affecting **Bluetooth Low Energy (BLE)** and **location services** on stock iPhones.

**Affected Version:** iOS 18.5  
**Test Device:** iPhone 14 Pro Max  
**Discovery Date:** 2025-06-24  
**Author:** Joseph Goydish II  
**Severity:** High

---

##  Key Vulnerabilities

| ID     | Component                 | Description                                                |
|--------|---------------------------|------------------------------------------------------------|
| VF-001 | `audioaccessoryd`         | Exposes previously trusted Bluetooth metadata              |
| VF-002 | `SPCBPeripheralManager`   | Triggers silent BLE scans                                  |
| VF-003 | `locationd`               | Activates GPS location harvesting without consent          |
| VF-004 | `tccd`                    | Bypasses TCC privacy framework via `preflight=yes`         |
| VF-005 | `bluetoothd`              | Continues trust logic despite cryptographic failures       |



---

##  Attack Flow (Observed)

```plaintext
1. audioaccessoryd     → Accesses Bluetooth IRKs & trust metadata
2. SPCBPeripheralManager → Starts silent BLE scan
3. locationd            → Triggers GPS data harvesting silently
4. tccd                 → Bypasses TCC permissions using undocumented parameter
5. bluetoothd           → Trust proceeds despite crypto/keychain failure
