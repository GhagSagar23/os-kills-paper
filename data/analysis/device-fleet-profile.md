# Device Fleet Profile

Source: `zontrageneric` database dump, 2026-11-15. Table: `device` (94 rows).

## Headline numbers

- **94** total device records
- **86** physical devices (`is_emulator=false`)
- **8** emulators (`is_emulator=true`, all Google `sdk_gphone*`)
- **3** customer organisations
- **11** distinct OEMs (physical only)
- Android versions span **8.1.0 to 17**

Org C is a dev/test account: 5 of its 6 entries are emulators. The production fleet is Org A + Org B: **80 physical device records** across two deploying organisations.

Note: the device table stores one row per app install (device_identifier + app_version pair), not per unique physical handset. The same POCO X8 Pro Max appears with different device_identifiers across app version upgrades. Unique physical handsets are fewer than 86. Deduplication by `device_identifier` would give the true count, but several identifiers are UUIDs generated per install rather than stable hardware IDs.

## OEM distribution (physical devices only)

| OEM | Records | Share |
|-----|---------|-------|
| Xiaomi (incl. POCO, Redmi) | 36 | 41.9% |
| Samsung | 16 | 18.6% |
| vivo | 11 | 12.8% |
| OPPO | 7 | 8.1% |
| Google (Pixel, non-emulator) | 1 | 1.2% |
| Infinix | 4 | 4.7% |
| realme | 2 | 2.3% |
| OnePlus | 1 | 1.2% |
| Motorola | 1 | 1.2% |
| LAVA | 1 | 1.2% |

Xiaomi dominates. Combined with OPPO and realme (all BBK/Chinese OEM aggressive battery management), that is 52.3% of the fleet on OEMs rated aggression 3/5 or higher.

Samsung's 16 records are all one model: SM-G990E (Galaxy S21 FE), a single device belonging to Org A used for development and testing. Not representative of Samsung's fleet diversity.

## Model distribution (top models, physical)

| Model | OEM | Records | Notes |
|-------|-----|---------|-------|
| 2602BPC18I (POCO X8 Pro Max) | Xiaomi | 30 | Primary field device, Org A + Org B |
| SM-G990E (Galaxy S21 FE) | Samsung | 14 | Single device, dev/test, Org A only |
| Redmi 8A Dual | Xiaomi | 3 | Budget handset, 3GB RAM, Android 10 |
| V2321 | vivo | 2 | Mid-range, Android 15 |
| All others | mixed | 37 | One record each, 30+ distinct models |

The fleet is heavily skewed: one Xiaomi model (POCO X8 Pro Max) accounts for 34.9% of all records. The long tail of 30+ single-record models is Org B's real-world fleet, which runs whatever phone the worker already owns.

## Android version distribution (physical)

| Android | Records | Share |
|---------|---------|-------|
| 16 | 53 | 61.6% |
| 17 | 6 | 7.0% |
| 15 | 7 | 8.1% |
| 14 | 6 | 7.0% |
| 13 | 2 | 2.3% |
| 12 | 5 | 5.8% |
| 11 | 1 | 1.2% |
| 10 | 4 | 4.7% |
| 9 | 1 | 1.2% |
| 8.1.0 | 1 | 1.2% |

Android 16 dominates because the POCO X8 Pro Max and Galaxy S21 FE (the two most-registered devices) both run it. The older tail (Android 8.1 through 13) is entirely Org B's BYOD fleet: Redmi Note 5, Galaxy J7 Nxt, OPPO A16k, Infinix SMART 4 Plus. These are the devices most likely to experience aggressive OEM kills.

## Organisation distribution (physical, anonymised)

| Org | Records | OEM mix | Notes |
|-----|---------|---------|-------|
| Org A | 45 | Xiaomi 26, Samsung 14, Google 1, Xiaomi (Redmi) 4 | Company-issued devices, mostly POCO X8 Pro Max + one S21 FE |
| Org B | 35 | vivo 11, OPPO 7, Xiaomi 5, Infinix 4, realme 2, Samsung 2, OnePlus 1, Motorola 1, LAVA 1, Google 1 | BYOD fleet, 30+ distinct models |
| Org C | 6 | Google 5 (emulators), Xiaomi 1 | Dev/test account |

Org A runs a controlled fleet (bulk-purchased POCO X8 Pro Max). Org B is BYOD, which is where the OEM diversity and the kill problem lives. A field worker on an Infinix SMART 4 Plus (Android 10, 2GB RAM) is in a different kill-risk category than the POCO X8 Pro Max (Android 16, 12GB RAM).

## Columns present in the device table

`id`, `customer_id`, `device_identifier`, `device_name`, `platform` (1=Android), `platform_version`, `manufacturer`, `model`, `hardware`, `app_version`, `app_build_number`, `timezone`, `locale`, `screen_width`, `screen_height`, `screen_density`, `network_type`, `is_rooted`, `is_emulator`, `extra_specs` (JSON: board, device, display, product, bootloader, isLowRamDevice, supportedAbis), `created_at`, `updated_at`.

No iOS devices in the dump. Platform is exclusively Android.

## Relevance to the paper

The fleet profile confirms three things for the methodology paper:

1. **OEM diversity exists in the field.** Org B's BYOD fleet spans 10 OEMs, from LAVA to Samsung. Any kill measurement framework must handle this heterogeneity.

2. **Android version span is wide.** 8.1 to 17. Doze behaviour, App Standby Buckets, and permission auto-revocation all changed across this range. The instrumentation specification must account for API-level differences.

3. **Device context is captured at login only.** The `device` table has OEM, model, and OS version, but this data is snapshotted at registration time. It is not attached to tracking sessions, permission events, or kill events. This confirms gap 5 from the validation audit.
