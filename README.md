    # # # Distribution Statement A. Approved for public release. Distribution unlimited.
    # # # 
    # # # Author:
    # # # Naval Research Laboratory, Marine Meteorology Division
    # # # 
    # # # This program is free software:
    # # # you can redistribute it and/or modify it under the terms
    # # # of the NRLMMD License included with this program.
    # # # 
    # # # If you did not receive the license, see
    # # # https://github.com/U-S-NRL-Marine-Meteorology-Division/
    # # # for more information.
    # # # 
    # # # This program is distributed WITHOUT ANY WARRANTY;
    # # # without even the implied warranty of MERCHANTABILITY
    # # # or FITNESS FOR A PARTICULAR PURPOSE.
    # # # See the included license for more details.

Testing Guide
=============

This testing guide has steps specific to installing and testing geoips for purposes of testing datasets
contained within this test data repository.  This includes installing the base geoips conda environment
if not already installed.


Sample Dataset Sources
-----------------------

* BYU ASCAT Ultra High Resolution data obtained from https://www.nesdis.noaa.gov/
    * Brigham Young University SCP, Provo, UT
* MetOp ASCAT Level 2 Coastal Ocean Surface Wind Vector Product obtained from EUMETSAT / KNMI
    * ASCAT Wind Product User Manual, http://www.osi-saf.org/, http://www.knmi.nl/scatterometer/
* ScatSat-1 OSCAT Level 2 25.0 km Ocean Surface Wind Vector Product obtained from EUMETSAT / KNMI
    * ScatSat-1 Wind Product User Manual, http://www.osi-saf.org/, http://www.knmi.nl/scatterometer/


Setup System Environment Variables
----------------------------------

```bash

    # GEOIPS_BASEDIR will contain all source, output, and external dependencies
    # Ensure this is consistently set for all installation / setup steps below
    export GEOIPS_BASEDIR=$HOME/geoproc

    # GEOIPS_REPO_URL should point to the base URL for git clone commands
    export GEOIPS_REPO_URL=https://github.com/NRLMMD-GeoIPS

    # This config file must be sourced ANY TIME you want to run geoips
    export GEOIPS_CONFIG_FILE=$GEOIPS_BASEDIR/geoips_packages/geoips/setup/config_geoips

```

Obtain geoips source repo and test data repo
---------------------------------------------
```bash
    mkdir -p $GEOIPS_BASEDIR/geoips_packages/

    git clone $GEOIPS_REPO_URL/geoips.git $GEOIPS_BASEDIR/geoips_packages/geoips
    
    git -C $GEOIPS_BASEDIR/geoips_packages/geoips pull
    git -C $GEOIPS_BASEDIR/geoips_packages/geoips checkout -t origin/dev
    git -C $GEOIPS_BASEDIR/geoips_packages/geoips checkout dev
    git -C $GEOIPS_BASEDIR/geoips_packages/geoips pull

    git clone ${GEOIPS_REPO_URL}/test_data_scat.git ${GEOIPS_BASEDIR}/test_data/test_data_scat
    git -C ${GEOIPS_BASEDIR}/test_data/test_data_scat pull
    git -C ${GEOIPS_BASEDIR}/test_data/test_data_scat checkout -t origin/dev
    git -C ${GEOIPS_BASEDIR}/test_data/test_data_scat checkout dev
    git -C ${GEOIPS_BASEDIR}/test_data/test_data_scat pull
```

IF REQUIRED: Install and test base geoips conda environment
------------------------------------------------------------
```bash
    # SKIP IF YOU HAVE ALREADY INSTALLED BASE GEOIPS CONDA ENVIRONMENT 
    # This prompts you through all the steps of installing the geoips conda environment from scratch,
    # using the parameters specified above.  This only needs to be done once per system, skip if you
    # already ran this step.
    $GEOIPS_BASEDIR/geoips_packages/geoips/base_install_and_test.sh dev
```

Run sample test scripts
-----------------------
```bash
    # Setup geoips environment variables
    source $GEOIPS_CONFIG_FILE

    # These test commands should all successfully return 0 if everything is set up properly.
    $GEOIPS/tests/scripts/ascat_uhr.tc.wind-ambiguities.imagery_windbarbs.sh   # ULTRA HIGH RESOLUTION!
    $GEOIPS/tests/scripts/ascat_knmi.tc.windbarbs.imagery_windbarbs_clean.sh   # 12.5km
    $GEOIPS/tests/scripts/ascat_low_knmi.tc.windbarbs.imagery_windbarbs.sh     # 25km
    $GEOIPS/tests/scripts/oscat_knmi.tc.windbarbs.imagery_windbarbs.sh         # 25km
```
