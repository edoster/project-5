# UOCIS322 - Project 5 #
Brevet time calculator with MongoDB!

Evan Doster

edoster@uoregon.edu
 
 # Brevet Time Calculator

## Overview

This web application calculates the open and close times for controls on a randonneuring brevet using rules defined by Randonneurs USA.

Randonneuring is a long-distance cycling event where riders complete courses of 200km or more. Brevets are not races, but rather tests of endurance with time limits that riders must finish within.

This app allows organizers to calculate the control open and close times for their events.

## Brevet Control Time Calculations

The app implements the control time calculations as defined by RUSA here: https://rusa.org/pages/rulesForRiders

The key points:

- Each control has an opening and closing time. Riders must pass during this window to get credit.

- The opening time is based on the maximum speed and the distance to the control from the start.

- The closing time is based on the minimum speed and distance to the next control.

- The first control's opening time is based on 15km/hr. Subsequent openings are based on 15km/hr + 5km/hr for each controle.

- Closing times are based on speeds in this table, using the speed for the next control's distance:

| Distance | Minimum Speed |
|----------|---------------|
| 200KM    | 15km/hr       |   
| 400KM    | 15km/hr       |
| 600KM    | 15km/hr       |
| 1000KM   | 11.428km/hr   |

- The final closing time is 13.5 hours after the start for a 200KM brevet.

- No controle can exceed the max distance or min speed according to this table:

| Distance | Max Distance | Min Speed |
|----------|--------------|-----------|
| 200KM    | 20%          | 15km/hr   |
| 300KM    | 20%          | 15km/hr   |   
| 400KM    | 20%          | 15km/hr   |
| 600KM    | 25%          | 15km/hr   |
| 1000KM   | 25%          | 11.428km/hr |

The app implements these rules to dynamically calculate open and close times as the brevet distance, start time, and controle locations are adjusted.

## Usage

The web interface allows the brevet organizer to enter the brevet distance, start time, and checkpoint locations. As checkpoint distances are entered, the app will automatically calculate and populate the open and close time for each one.

The app provides a Submit button to save these calculated times to a database for later retrieval.

The Display button will fetch the latest saved brevet info and populate the form.

This allows organizers to save and restore the controle times for their events.

The backend uses MongoDB to store the brevet data. Docker Compose is used to run the Flask app and MongoDB containers to run the application.

Automated tests validate the controle time calculations.



## Authors

Michal Young, Ram Durairajan. Updated by Ali Hassani.
