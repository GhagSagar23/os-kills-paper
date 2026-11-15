# Session Analysis — zontrageneric dump 2026-11-15

## Tracking Sessions

**Total:** 159

**Columns (49):** id, session_number, customer_id, user_id, manager_id, tracking_mode, status, reason, requested_at, accepted_at, rejected_at, tracking_started_at, paused_at, resumed_at, tracking_ended_at, expires_at, retry_count, last_retry_at, last_waypoint_id, last_latitude, last_longitude, last_accuracy, last_altitude, last_speed, last_heading, last_sequence_index, last_location_at, last_upload_at, total_waypoints, total_distance_meters, moving_duration_seconds, idle_duration_seconds, average_speed, max_speed, last_battery_level, last_network_type, last_charging, last_gps_enabled, remarks, created_at, updated_at, is_deleted, expiring_at, auto_completed_at, grace_period_seconds, ended_by, end_reason, version, attendance_session_id

**Date range:** 2026-08-29 to 2026-10-29


### Session Durations

| Metric | Value |
|--------|-------|
| Min | 0h 0m |
| Max | 9h 6m |
| Avg | 5h 39m |
| Median | 7h 53m |
| Count with duration | 159 |


### Status Distribution

| Status | Count |
|--------|-------|
| 5 | 159 |


### End Reason Distribution

| end_reason | Count |
|------------|-------|
| 1 | 134 |
| 3 | 25 |


### Ended By Distribution

| ended_by | Count |
|----------|-------|
| 1 | 134 |
| 4 | 25 |


### Remarks Distribution

| Remarks | Count |
|---------|-------|
| Auto-created on attendance check-in | 133 |
| Tracking automatically completed after attendance timeout | 25 |
| Sample check-out tracking from Swagger | 1 |


### Waypoint Counts per Session

| Metric | Value |
|--------|-------|
| Min | 0 |
| Max | 651 |
| Avg | 88.6 |
| Sessions with 0 waypoints | 2 |
| Sessions with 1-3 waypoints | 63 |


### Anomalous Sessions (potential kill evidence)

| Session | Started | Ended | Duration | Waypoints | end_reason | Remarks |
|---------|---------|-------|----------|-----------|------------|---------|
| TRK-00001001 | 2026-08-29 11:58 | 16:52 | 4h 53m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001004 | 2026-09-23 07:36 | 16:41 | 9h 5m | 64 | 3 | Tracking automatically completed after attendance  |
| TRK-00001029 | 2026-09-21 04:29 | 13:36 | 9h 6m | 179 | 3 | Tracking automatically completed after attendance  |
| TRK-00001005 | 2026-10-12 08:19 | 17:20 | 9h 0m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001009 | 2026-09-05 05:24 | 05:28 | 0h 4m | 0 | 1 | Sample check-out tracking from Swagger |
| TRK-00001005 | 2026-09-01 17:33 | 17:34 | 0h 1m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001024 | 2026-09-18 06:14 | 06:15 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001013 | 2026-10-13 05:22 | 14:29 | 9h 6m | 67 | 3 | Tracking automatically completed after attendance  |
| TRK-00001025 | 2026-09-18 06:17 | 06:18 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001032 | 2026-09-24 12:07 | 21:12 | 9h 5m | 4 | 3 | Tracking automatically completed after attendance  |
| TRK-00001012 | 2026-10-13 05:22 | 05:22 | 0h 0m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001011 | 2026-10-13 05:22 | 05:22 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001034 | 2026-10-14 09:37 | 09:37 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001030 | 2026-10-14 09:36 | 09:36 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001043 | 2026-10-13 10:47 | 10:49 | 0h 1m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001019 | 2026-10-14 02:57 | 12:02 | 9h 5m | 5 | 3 | Tracking automatically completed after attendance  |
| TRK-00001037 | 2026-10-14 11:53 | 11:53 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001041 | 2026-10-15 02:59 | 12:01 | 9h 1m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001004 | 2026-09-28 06:16 | 15:23 | 9h 6m | 42 | 3 | Tracking automatically completed after attendance  |
| TRK-00001016 | 2026-10-13 11:04 | 11:06 | 0h 1m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001001 | 2026-09-24 12:55 | 12:55 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001007 | 2026-10-13 02:39 | 02:40 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001032 | 2026-10-14 09:37 | 09:37 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001031 | 2026-10-14 09:37 | 09:37 | 0h 0m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001020 | 2026-10-14 02:57 | 12:04 | 9h 6m | 1 | 3 | Tracking automatically completed after attendance  |
| TRK-00001033 | 2026-10-14 09:37 | 09:37 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001047 | 2026-10-15 03:31 | 12:33 | 9h 1m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001038 | 2026-10-15 01:35 | 10:35 | 9h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001008 | 2026-10-13 02:40 | 11:41 | 9h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001016 | 2026-09-10 10:43 | 13:25 | 2h 42m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001017 | 2026-10-13 14:25 | 14:25 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001029 | 2026-10-14 04:24 | 13:30 | 9h 6m | 60 | 3 | Tracking automatically completed after attendance  |
| TRK-00001044 | 2026-10-15 03:09 | 12:15 | 9h 5m | 2 | 3 | Tracking automatically completed after attendance  |
| TRK-00001003 | 2026-09-23 07:31 | 07:32 | 0h 1m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001028 | 2026-09-20 00:43 | 09:49 | 9h 6m | 2 | 3 | Tracking automatically completed after attendance  |
| TRK-00001003 | 2026-09-26 02:52 | 11:57 | 9h 5m | 2 | 3 | Tracking automatically completed after attendance  |
| TRK-00001041 | 2026-10-12 04:39 | 13:40 | 9h 1m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001015 | 2026-10-13 10:42 | 10:43 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001036 | 2026-10-14 10:36 | 10:36 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001018 | 2026-10-14 02:31 | 11:32 | 9h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001040 | 2026-10-15 02:52 | 11:57 | 9h 5m | 2 | 3 | Tracking automatically completed after attendance  |
| TRK-00001058 | 2026-10-16 02:59 | 02:59 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001051 | 2026-10-15 07:35 | 16:41 | 9h 5m | 6 | 3 | Tracking automatically completed after attendance  |
| TRK-00001053 | 2026-10-15 10:36 | 19:41 | 9h 5m | 14 | 3 | Tracking automatically completed after attendance  |
| TRK-00001059 | 2026-10-16 02:59 | 03:00 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001056 | 2026-10-16 02:56 | 02:58 | 0h 1m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001063 | 2026-10-16 03:31 | 12:32 | 9h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001057 | 2026-10-16 02:58 | 02:59 | 0h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001066 | 2026-10-16 10:48 | 10:48 | 0h 0m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001070 | 2026-10-17 03:27 | 12:33 | 9h 5m | 12 | 3 | Tracking automatically completed after attendance  |
| TRK-00001067 | 2026-10-16 11:58 | 11:58 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001078 | 2026-10-17 09:44 | 09:44 | 0h 0m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001082 | 2026-10-21 03:35 | 03:35 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001079 | 2026-10-17 11:20 | 11:24 | 0h 3m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001071 | 2026-10-17 03:32 | 12:33 | 9h 1m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001072 | 2026-10-17 03:37 | 12:43 | 9h 5m | 10 | 3 | Tracking automatically completed after attendance  |
| TRK-00001080 | 2026-10-21 03:00 | 12:05 | 9h 5m | 1 | 3 | Tracking automatically completed after attendance  |
| TRK-00001090 | 2026-10-21 07:28 | 16:34 | 9h 5m | 3 | 3 | Tracking automatically completed after attendance  |
| TRK-00001083 | 2026-10-21 03:35 | 12:36 | 9h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001084 | 2026-10-21 03:35 | 12:35 | 9h 0m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001091 | 2026-10-21 12:22 | 12:22 | 0h 0m | 2 | 1 | Auto-created on attendance check-in |
| TRK-00001092 | 2026-10-21 13:40 | 22:46 | 9h 6m | 1 | 3 | Tracking automatically completed after attendance  |
| TRK-00001001 | 2026-10-29 15:18 | 15:20 | 0h 1m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001094 | 2026-10-22 03:11 | 03:11 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001103 | 2026-10-22 14:01 | 14:01 | 0h 0m | 1 | 1 | Auto-created on attendance check-in |
| TRK-00001095 | 2026-10-22 03:11 | 12:13 | 9h 1m | 3 | 1 | Auto-created on attendance check-in |
| TRK-00001101 | 2026-10-22 09:16 | 18:21 | 9h 5m | 6 | 3 | Tracking automatically completed after attendance  |
| TRK-00001096 | 2026-10-22 03:30 | 12:37 | 9h 6m | 1 | 3 | Tracking automatically completed after attendance  |
| TRK-00001098 | 2026-10-22 03:44 | 12:49 | 9h 5m | 25 | 3 | Tracking automatically completed after attendance  |
| TRK-00001104 | 2026-10-23 03:19 | 12:26 | 9h 6m | 323 | 3 | Tracking automatically completed after attendance  |
| TRK-00001005 | 2026-10-23 06:43 | 15:48 | 9h 5m | 2 | 3 | Tracking automatically completed after attendance  |
| TRK-00001002 | 2026-10-29 15:20 | 00:27 | 9h 6m | 0 | 3 | Tracking automatically completed after attendance  |


### Sessions by Customer

| customer_id | Count |
|-------------|-------|
| ece940c1-010... | 106 |
| 11060bc7-b1e... | 45 |
| 8a5673f9-bf0... | 5 |
| 443eca00-4f9... | 2 |
| 628e6597-091... | 1 |


### Sessions by User

| user_id | Count |
|---------|-------|
| 16f3b277-40f... | 45 |
| e7fb578a-0b1... | 12 |
| a20a7bfa-aa8... | 12 |
| 0c603cc5-c90... | 10 |
| 3517abec-662... | 10 |
| a7a27787-8e7... | 9 |
| ab6cff52-cfc... | 9 |
| d1551fda-901... | 7 |
| cead0032-160... | 6 |
| 8bfffb19-92c... | 5 |
| a6f60bc2-f9a... | 5 |
| f6c5d349-27b... | 4 |
| dcd43420-85a... | 4 |
| e99d00ae-351... | 4 |
| 1cb7e80e-553... | 3 |
| 6f4e897c-9cb... | 3 |
| 17c5a01b-344... | 3 |
| ecc97a08-d94... | 3 |
| f95e000a-b8f... | 2 |
| f4fb4717-7a1... | 1 |
| 4be9513b-ece... | 1 |
| 5fcc2f17-85f... | 1 |


### GPS Enabled at End

- True: 59
- None: 51
- False: 49


### Battery Level at Session End

| Metric | Value |
|--------|-------|
| Min | 4% |
| Max | 100% |
| Avg | 56% |
| Sessions ending ≤15% | 5 |


## Attendance Sessions

**Total:** 211

**Columns (28):** id, customer_id, user_id, policy_id, mode, status, office_id, attendance_date, checkin_time, checkout_time, working_duration_seconds, office_duration_seconds, field_duration_seconds, break_duration_seconds, late, early_exit, remote, manual_entry, remarks, created_at, updated_at, is_deleted, version, expires_at, ended_by, end_reason, checkin_battery_level, checkout_battery_level


### Attendance Status Distribution

| Status | Count |
|--------|-------|
| 2 | 174 |
| 3 | 37 |


### Attendance Session Sample Fields

- **id**: `b2d0a925-5159-42eb-9d3f-6c8708d64e89`
- **customer_id**: `11060bc7-b1e0-452f-914f-50c82f12cf77`
- **user_id**: `826188a8-061f-4635-aa85-c2c9fe885c1e`
- **policy_id**: `c42690d7-78e1-41a8-ad35-7a1741db9300`
- **mode**: `1`
- **status**: `2`
- **office_id**: `7cba5347-6edf-42db-a7ce-497d6e8eba84`
- **attendance_date**: `2026-10-12 18:30:00`
- **checkin_time**: `2026-10-13 08:46:43.895335`
- **checkout_time**: `2026-10-13 10:44:51.375886`
- **working_duration_seconds**: `7087`
- **office_duration_seconds**: `7087`
- **field_duration_seconds**: `0`
- **break_duration_seconds**: `0`
- **late**: `True`
- **early_exit**: `True`
- **remote**: `False`
- **manual_entry**: `False`
- **remarks**: `None`
- **created_at**: `2026-10-13 08:46:43.895335`
- **updated_at**: `2026-10-13 10:44:51.375886`
- **is_deleted**: `False`
- **version**: `2`
- **expires_at**: `2026-10-13 23:16:43.904165+05:30`
- **ended_by**: `1`
- **end_reason**: `1`
- **checkin_battery_level**: `35`
- **checkout_battery_level**: `96`


## Attendance-Tracking Session Link

**Total links:** 159

**Columns:** attendance_session_id, tracking_session_id, customer_id, linked_at


### Sample row

- **attendance_session_id**: `955a084f-127a-49f3-b596-5e1072971230`
- **tracking_session_id**: `857b954a-83b3-4288-addc-8810408f91b1`
- **customer_id**: `11060bc7-b1e0-452f-914f-50c82f12cf77`
- **linked_at**: `2026-08-29 11:58:32.780369`


## Fields Relevant to Kill/Interruption Detection


From tracking_session:
- `end_reason`: integer enum, observed values and counts above
- `ended_by`: integer enum, observed values and counts above
- `remarks`: free text, includes 'Auto-created on attendance check-in', 'Tracking automatically completed after attendance timeout', 'Sample check-out tracking from Swagger'
- `last_gps_enabled`: boolean, NULL in some cases (GPS off or unknown)
- `last_battery_level`: integer %, NULL in some sessions
- `total_waypoints`: 0 means no location data received during session
- `last_location_at` vs `tracking_ended_at`: large gap = location stopped before session ended
- `last_upload_at` vs `tracking_ended_at`: large gap = uploads stopped before session ended
- `auto_completed_at`: NULL in all observed rows (field exists but unused)
- `version`: integer, higher = more updates (more reattachments?)


### Location Gap: last_location_at vs tracking_ended_at

Sessions where location stopped >30min before session ended (potential kill/permission loss):

| Session | last_location_at | tracking_ended_at | Gap | Waypoints | Battery |
|---------|------------------|-------------------|-----|-----------|---------|
| TRK-00001004 | 09-23 07:54 | 09-23 16:41 | 8h 47m | 64 | 100% |
| TRK-00001029 | 09-21 08:37 | 09-21 13:36 | 4h 58m | 179 | 81% |
| TRK-00001013 | 10-13 06:47 | 10-13 14:29 | 7h 41m | 67 | 50% |
| TRK-00001032 | 09-23 18:30 | 09-24 21:12 | 26h 42m | 4 | None% |
| TRK-00001019 | 10-14 03:15 | 10-14 12:02 | 8h 46m | 5 | None% |
| TRK-00001004 | 09-28 04:11 | 09-28 15:23 | 11h 12m | 42 | None% |
| TRK-00001020 | 10-14 02:57 | 10-14 12:04 | 9h 6m | 1 | 42% |
| TRK-00001029 | 10-14 05:51 | 10-14 13:30 | 7h 39m | 60 | None% |
| TRK-00001044 | 10-15 03:09 | 10-15 12:15 | 9h 5m | 2 | 96% |
| TRK-00001028 | 09-20 00:43 | 09-20 09:49 | 9h 6m | 2 | 56% |
| TRK-00001003 | 09-26 02:52 | 09-26 11:57 | 9h 5m | 2 | 7% |
| TRK-00001040 | 10-15 02:52 | 10-15 11:57 | 9h 5m | 2 | 97% |
| TRK-00001051 | 10-15 07:37 | 10-15 16:41 | 9h 3m | 6 | 66% |
| TRK-00001053 | 10-15 08:20 | 10-15 19:41 | 11h 21m | 14 | None% |
| TRK-00001070 | 10-17 07:36 | 10-17 12:33 | 4h 56m | 12 | 56% |
| TRK-00001072 | 10-17 03:40 | 10-17 12:43 | 9h 2m | 10 | 63% |
| TRK-00001080 | 10-21 03:00 | 10-21 12:05 | 9h 5m | 1 | 86% |
| TRK-00001090 | 10-21 07:28 | 10-21 16:34 | 9h 5m | 3 | 60% |
| TRK-00001092 | 10-21 13:40 | 10-21 22:46 | 9h 6m | 1 | 65% |
| TRK-00001101 | 10-22 09:32 | 10-22 18:21 | 8h 49m | 6 | 72% |
| TRK-00001096 | 10-22 03:30 | 10-22 12:37 | 9h 6m | 1 | 88% |
| TRK-00001098 | 10-22 05:05 | 10-22 12:49 | 7h 44m | 25 | 66% |
| TRK-00001104 | 10-23 09:31 | 10-23 12:26 | 2h 55m | 323 | 78% |
| TRK-00001005 | 10-23 06:43 | 10-23 15:48 | 9h 5m | 2 | 39% |
| TRK-00001002 | 10-29 15:20 | 10-30 00:27 | 9h 6m | 0 | 27% |


### Upload Gap: last_upload_at vs tracking_ended_at

Sessions where uploads stopped >30min before session ended:

| Session | last_upload_at | tracking_ended_at | Gap | Waypoints |
|---------|----------------|-------------------|-----|-----------|
| TRK-00001004 | 09-23 07:54 | 09-23 16:41 | 8h 46m | 64 |
| TRK-00001029 | 09-21 08:51 | 09-21 13:36 | 4h 44m | 179 |
| TRK-00001013 | 10-13 06:47 | 10-13 14:29 | 7h 41m | 67 |
| TRK-00001032 | 09-24 12:20 | 09-24 21:12 | 8h 51m | 4 |
| TRK-00001019 | 10-14 03:58 | 10-14 12:02 | 8h 3m | 5 |
| TRK-00001004 | 09-28 06:17 | 09-28 15:23 | 9h 5m | 42 |
| TRK-00001020 | 10-14 02:57 | 10-14 12:04 | 9h 6m | 1 |
| TRK-00001029 | 10-14 06:07 | 10-14 13:30 | 7h 22m | 60 |
| TRK-00001044 | 10-15 03:10 | 10-15 12:15 | 9h 5m | 2 |
| TRK-00001028 | 09-20 00:46 | 09-20 09:49 | 9h 3m | 2 |
| TRK-00001003 | 09-26 02:52 | 09-26 11:57 | 9h 5m | 2 |
| TRK-00001040 | 10-15 02:52 | 10-15 11:57 | 9h 4m | 2 |
| TRK-00001051 | 10-15 07:39 | 10-15 16:41 | 9h 2m | 6 |
| TRK-00001053 | 10-15 10:36 | 10-15 19:41 | 9h 5m | 14 |
| TRK-00001070 | 10-17 07:37 | 10-17 12:33 | 4h 55m | 12 |
| TRK-00001072 | 10-17 03:41 | 10-17 12:43 | 9h 2m | 10 |
| TRK-00001080 | 10-21 03:00 | 10-21 12:05 | 9h 5m | 1 |
| TRK-00001090 | 10-21 07:41 | 10-21 16:34 | 8h 52m | 3 |
| TRK-00001092 | 10-21 13:40 | 10-21 22:46 | 9h 6m | 1 |
| TRK-00001101 | 10-22 09:34 | 10-22 18:21 | 8h 47m | 6 |
| TRK-00001096 | 10-22 03:30 | 10-22 12:37 | 9h 6m | 1 |
| TRK-00001098 | 10-22 05:22 | 10-22 12:49 | 7h 27m | 25 |
| TRK-00001104 | 10-23 09:31 | 10-23 12:26 | 2h 54m | 323 |
| TRK-00001005 | 10-23 06:45 | 10-23 15:48 | 9h 2m | 2 |
| TRK-00001002 | 10-29 15:20 | 10-30 00:27 | 9h 6m | 0 |
