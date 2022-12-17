    # # # Distribution Statement A. Approved for public release. Distribution unlimited.
    # # # 
    # # # Author:
    # # # Naval Research Laboratory, Marine Meteorology Division
    # # # 
    # # # This program is free software: you can redistribute it and/or modify it under
    # # # the terms of the NRLMMD License included with this program. This program is
    # # # distributed WITHOUT ANY WARRANTY; without even the implied warranty of
    # # # MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the included license
    # # # for more details. If you did not receive the license, for more information see:
    # # # https://github.com/U-S-NRL-Marine-Meteorology-Division/

Scatterometer Winds Test Datasets
==================================

This repository contains test datasets for use with the Geolocated Information Processing System.

Please see the 
[GeoIPS Documentation](https://github.com/NRLMMD-GEOIPS/geoips/blob/main/README.md)
for more information on the GeoIPS plugin architecture and base infrastructure.

Sample Dataset Sources
-----------------------

* BYU ASCAT Ultra High Resolution data obtained from https://www.nesdis.noaa.gov/
    * Brigham Young University SCP, Provo, UT
* MetOp ASCAT Level 2 Coastal Ocean Surface Wind Vector Product obtained from EUMETSAT / KNMI
    * ASCAT Wind Product User Manual, http://www.osi-saf.org/, http://www.knmi.nl/scatterometer/
* ScatSat-1 OSCAT Level 2 25.0 km Ocean Surface Wind Vector Product obtained from EUMETSAT / KNMI
    * ScatSat-1 Wind Product User Manual, http://www.osi-saf.org/, http://www.knmi.nl/scatterometer/

System Requirements
---------------------

* geoips >= 1.5.3
* Test data repos contained in $GEOIPS_TESTDATA_DIR for tests to pass.


IF REQUIRED: Install base geoips package
------------------------------------------------------------
SKIP IF YOU HAVE ALREADY INSTALLED BASE GEOIPS ENVIRONMENT 

If GeoIPS Base is not yet installed, follow the
[installation instructions](https://github.com/NRLMMD-GEOIPS/geoips/blob/main/docs/installation.rst)
within the geoips source repo documentation.


Obtain test repo
----------------
```bash
    # Assuming you followed the fully supported installation,
    # using $GEOIPS_TESTDATA_DIR and $GEOIPS_CONFIG_FILE:
    source $GEOIPS_CONFIG_FILE
    git clone $GEOIPS_REPO_URL/test_data_scat $GEOIPS_TESTDATA_DIR/test_data_scat

```

Run sample test scripts
-----------------------
```bash

    # Assuming you followed the fully supported installation,
    # using $GEOIPS_TESTDATA_DIR, $GEOIPS_PACKAGES_DIR, and $GEOIPS_CONFIG_FILE:
    source $GEOIPS_CONFIG_FILE

    # GeoIPS-based test scripts should successfully return 0 if everything is set up properly.
    $GEOIPS/tests/scripts/ascat_uhr.tc.wind-ambiguities.imagery_windbarbs.sh   # ULTRA HIGH RESOLUTION!
    $GEOIPS/tests/scripts/ascat_knmi.tc.windbarbs.imagery_windbarbs_clean.sh   # 12.5km
    $GEOIPS/tests/scripts/ascat_low_knmi.tc.windbarbs.imagery_windbarbs.sh     # 25km
    $GEOIPS/tests/scripts/oscat_knmi.tc.windbarbs.imagery_windbarbs.sh         # 25km
```
