# Anonymized WiFi RSS and RTT 2D Indoor Localization Dataset

This repository contains anonymized WiFi received signal strength (RSS) and WiFi round-trip-time (RTT) measurements collected for two-dimensional indoor localization. It accompanies an empirical study of RSS-only, RTT-only, and fused WiFi fingerprinting methods.

## Collection

RSS-only observations were recorded with a customized version of WiFiAnalyzer. RTT observations were recorded with a separate custom native Android application, which also logged RSS and ranging status. The applications use different CSV schemas and logging behavior; their timestamps should not be assumed to be synchronized.

`distance_mm` is a ranging-derived distance estimate in millimeters, not raw round-trip time. A value of `-1` indicates an unavailable or unsuccessful ranging estimate. Use the `type` field and ranging-status fields when interpreting RTT records.

## Contents

| Folder or file | Contents |
| --- | --- |
| `Location_RSS/` | RSS measurements collected at training reference points |
| `Location_RTT/` | RTT application measurements collected at training reference points |
| `Location_RSS_RTT_test/` | RSS and RTT application measurements from independent test locations |
| `Location_coordinates.csv` | Training reference-point identifiers and 2D coordinates (105 records) |
| `Location_test_coordinates_feet.csv` | Test-point identifiers and 2D coordinates in feet, with image coordinates (21 records) |
| `README.md` | Dataset overview and collection notes |
| `data_dictionary.md` | Definitions of CSV columns and coordinate conventions |

## Coordinate convention

Training reference-point coordinates are stored in `Location_coordinates.csv` as `RP_ID`, `x_floor`, and `y_floor`. The `x_floor` and `y_floor` values are local two-dimensional positions in feet, measured from a scaled floor-plan coordinate system. They are not geographic coordinates.

Test-point coordinates are stored in `Location_test_coordinates_feet.csv` as `rp_id`, `x_ft`, `y_ft`, `x_px`, and `y_px`. The feet columns represent local physical positions; the pixel columns represent positions on the corresponding floor-plan image.

The test-coordinate file contains 21 entries. The study's independent-test evaluation uses 21 locations.

## Anonymization

WiFi access-point identifiers are pseudonymized using labels such as `AP_0001`. SSIDs and access-point coordinate columns are omitted. Timestamps and application-specific measurement fields are retained. 
See [data_dictionary.md](data_dictionary.md) for field definitions.

## License and citation

No reuse license or formal citation is specified in this repository documentation.
