# Data dictionary

The dataset contains RSS-only measurements, RTT application measurements, training reference-point coordinates, and test-point coordinates. The tables below define the CSV fields and their meanings.

## RSS-only measurements (customized WiFiAnalyzer)

| Column | Meaning |
| --- | --- |
| `Time Stamp` | Timestamp recorded by the RSS application |
| `apId` | Pseudonymized WiFi access-point identifier (`AP_####`) |
| `Strength` | Received signal strength in dBm |
| `Primary Frequency` | WiFi primary channel frequency in MHz |

## RTT application measurements (custom native Android app)

| Column | Meaning |
| --- | --- |
| `timestamp` | Timestamp recorded by the RTT application |
| `landmark` | Reference-point or test-point label recorded by the application |
| `apId` | Pseudonymized WiFi access-point identifier (`AP_####`) |
| `distance_mm` | Ranging-derived distance estimate in millimeters; `-1` denotes unavailable or failed ranging |
| `stddev_mm` | App-reported ranging distance standard deviation in millimeters; `-1` denotes an unavailable value |
| `rssi_dbm` | Received signal strength in dBm |
| `success_frames` | Count of successful ranging frames reported by the app |
| `attempt_frames` | Count of attempted ranging frames reported by the app |
| `type` | Observation/status category, including `RSS_ONLY`, `RSS_PRE_RTT`, `RTT+RSS`, and `RTT_FAILED` |

Not every RTT application row contains a valid distance estimate. Use `type`, `distance_mm`, and the frame counts to distinguish successful ranging from other observations.

## Training reference-point coordinates

File: `Location_coordinates.csv` (105 records)

| Column | Meaning |
| --- | --- |
| `RP_ID` | Training reference-point identifier |
| `x_floor` | Horizontal coordinate in the local floor-plan system, in feet |
| `y_floor` | Vertical coordinate in the local floor-plan system, in feet |

The coordinates describe surveyed training reference points in a local two-dimensional coordinate system.

## Test-point coordinates

File: `Location_test_coordinates_feet.csv` (23 records)

| Column | Meaning |
| --- | --- |
| `rp_id` | Test-point identifier |
| `x_ft` | Horizontal coordinate in feet |
| `y_ft` | Vertical coordinate in feet |
| `x_px` | Horizontal coordinate on the floor-plan image, in pixels |
| `y_px` | Vertical coordinate on the floor-plan image, in pixels |

The test-coordinate file contains 21 location records. 

## Notes on matching

Training and test measurement filenames identify collection locations. Identifier capitalization and separators can differ between RSS files, RTT files, and coordinate files. Coordinate headers also differ: training coordinates use `RP_ID`, while test coordinates use `rp_id`. Normalize location identifiers before joining measurement records to coordinates.

RSS and RTT application timestamps follow separate logging conventions and are not guaranteed to represent synchronized samples.
