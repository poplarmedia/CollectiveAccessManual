---
title: app.conf
sidebar_position: 2
---

# app.conf

## Overview
The app.conf configuration file defines general behaviors and settings for a theme. The file has many possible settings affecting a wide-range of functions. Settings grouped broadly by function are described in detail below.

## Login, registration and access control

|Setting|Description|Allowed values|Required?|Default|Synonyms|
|---|---|---|---|---|---|
|dontAllowRegistrationAndLogin|Disable login and registration options|0 or 1|No|0|dont_allow_registration_and_login|
|dontAllowRegistration|Disable registration option|0 or 1|No|0||
|deployBristol|When “Bristol” mode is enabled users must login and have access only to sets for which they have been granted read-level access.|0 or 1|No|0|deploy_bristol|
|pawtucketRequiresLogin|Require all Pawtucket users to login for access.|0 or 1|No|0|pawtucket_requires_login|

## Theme inheritance
Each theme inherits views and configuration from the Pawtucket _default_ theme. You can use the options below to enable inheritance from other themes.

|Setting|Description|Allowed values|Required?|Default|Synonyms|
|---|---|---|---|---|---|
|allowThemeInheritance|Enables theme inheritance|0 or 1|No|0||
|inheritFrom|Name of theme to inherit from|A valid theme name. Ex. itinera|No|None|inherit_from|
