# Permission Events & Device Analysis

Source: `zontrageneric` database dump, 2026-11-15 14:25 IST

## 1. permission_event table

**Empty.** The file exists but contains zero rows. This confirms the codebase scan finding: `PermissionEvent` is stored only in SharedPreferences on-device (`permission_log` key) and is never uploaded to the backend. The backend table exists in the schema but has no data. Gap 11 from the paper's validation audit.

## 2. log_attendance table

**Empty.** No rows.

## 3. device table (fleet profile)

76 total device records across 4 customer organisations.

### By manufacturer

| Manufacturer | Count | % |
|---|---|---|
| Xiaomi | 38 | 50.0% |
| vivo | 13 | 17.1% |
| OPPO | 8 | 10.5% |
| Google | 6 | 7.9% (includes emulators: sdk_gphone*) |
| INFINIX | 4 | 5.3% |
| samsung | 2 | 2.6% |
| realme | 2 | 2.6% |
| OnePlus | 1 | 1.3% |
| motorola | 1 | 1.3% |
| LAVA | 1 | 1.3% |

Note: 6 Google devices are emulators (sdk_gphone64_arm64, sdk_gphone16k_arm64). Excluding emulators: 70 physical devices.

### By Android version

| Version | Count | Note |
|---|---|---|
| Android 9 | 1 | |
| Android 10 | 5 | Includes Redmi 8A Dual (budget) |
| Android 11 | 1 | |
| Android 12 | 5 | |
| Android 13 | 2 | |
| Android 14 | 6 | |
| Android 15 | 9 | |
| Android 16 | 41 | Majority of fleet; includes emulators |
| Android 17 | 6 | |

Median: Android 16. Range: 9 to 17.

### By customer

| Customer (truncated UUID) | Devices | Note |
|---|---|---|
| ece940c1... | 38 | Largest org |
| 11060bc7... | 31 | Second org |
| 8a5673f9... | 6 | Third org |
| 443eca00... | 1 | Smallest |

### Dominant model

Xiaomi 2602BPC18I (POCO X8 Pro Max): 32 of 76 devices (42%). This is an active development/test device being re-registered across multiple users; it is a Xiaomi device running Android 16.

### Paper-relevant data points

- **50% Xiaomi** fleet: the most aggressive OEM (5/5 aggression) dominates the deployment
- **Real physical fleet**: 70 devices after excluding 6 emulators
- **Budget devices present**: Redmi 8A Dual (3 GB RAM), LAVA LXX516, Samsung SM-J701F
- **Wide OS range**: Android 9 through 17 (8 major versions)
- **4 distinct customer organisations** (paper says "two deploying organisations"; actual count is 4; the paper may be referring to the two largest which account for 69 of 76)

## 4. user_device table (device churn)

106 total user-device binding records across 44 distinct users.

### Device registration frequency

| User (truncated UUID) | Registrations | Interpretation |
|---|---|---|
| 16f3b277... | 20 | Extreme churn: app reinstalls, device swaps, or service restarts |
| f1716049... | 19 | Same pattern |
| 826188a8... | 14 | Same pattern |
| 8bfffb19... | 5 | Moderate |
| c9a38646... | 4 | Moderate |
| 9fe9a865... | 3 | Normal |
| 87db3629... | 3 | Normal |
| 36 other users | 1 each | Single registration |

- **is_primary=true**: 44 records (current active device per user)
- **is_primary=false**: 62 records (previous devices, superseded)
- **revoked_at**: 0 records have a revoked timestamp (no explicit device revocations recorded)

### Kill-relevant insight

The top 3 users have 53 device registrations combined for ~3 users. Each registration happens when the app re-authenticates on a device. Possible causes:
- Frequent app reinstalls (user or corporate policy)
- Development/testing cycles
- Service restarts that trigger re-authentication (kill-related)

The `created_at` to `updated_at` ranges for these users span Aug-Oct 2026. Some devices are active for only minutes before being superseded (e.g., `36eba025...` created 2026-09-21 07:34, updated 2026-09-21 08:50 = 76 minutes). This could indicate app reinstalls triggered by OEM kill frustration, or testing. Without additional context (permission_log data), the cause is ambiguous.

## Summary for paper

1. **permission_event table is empty** (confirms gap 11: no backend sink)
2. **Device fleet is 70 physical devices** (paper says 30; actual is larger; verify which subset the paper's "six months" covers, or update the paper number)
3. **50% Xiaomi fleet** validates the aggression table's focus on Xiaomi
4. **3 users show extreme device churn** (14-20 re-registrations) which is indirect evidence of kill/reinstall cycles but cannot be classified without the missing telemetry
5. **4 customer orgs, not 2** (paper may need updating, or clarify that "two deploying organisations" refers to the two largest)
