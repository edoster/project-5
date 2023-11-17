# UOCIS322 - Project 5 #
Brevet time calculator with MongoDB!

Evan Doster

edoster@uoregon.edu
 
 # Brevet Time Calculator

## Outline of the Application

You will reimplement RUSA ACP controle time calculator with Flask and AJAX.
The calculations should populate the open and close time after pressing enter without refreshes!
Inside of the applciation, there should be rigourous nose tests that outline potential weaknesses in the algorithm. 

### ACP controle Algorithm

This project consists of a web application that is based on RUSA's online calculator. The algorithm for calculating controle times is described here [https://rusa.org/pages/acp-brevet-control-times-calculator](https://rusa.org/pages/acp-brevet-control-times-calculator). Additional background information is given here [https://rusa.org/pages/rulesForRiders](https://rusa.org/pages/rulesForRiders). The description is ambiguous, but the examples help. Part of finishing this project is clarifying anything that is not clear about the requirements, and documenting it clearly. 

We are essentially replacing the calculator here [https://rusa.org/octime_acp.html](https://rusa.org/octime_acp.html). We can also use that calculator to clarify requirements and develop test data. 

### Outline of Algorithm

Depending on the control location, we can expect the minimum and maximum speed (km/hour) to change as a result of this distance. Refer to the table here [https://rusa.org/pages/acp-brevet-control-times-calculator](https://rusa.org/pages/acp-brevet-control-times-calculator).

The open time is calculate by dividing control distance by the maximum speed. The algorithm can be generalized as (control distance - (previous interval)) / (current maximum speed) + (last intervals control distance - previous interval) / (last intervals maximum speed) + ...

Similarly the close time is calculated by dividing control distance by the minimum speed. The algorithm can be generalized as (control distance - (previous interval)) / (current minimum speed) + (last intervals control distance - previous interval) / (last intervals minimum speed) + ... Except for when control distance is equal to brevet distance which both are equal to 200. This special rule dictates that our close time is 13H30. 

## Running the Program

There are two ways to run the program. 

#### Docker 

Inside of your terminal, navigate to your project-5 folder, then run 'docker compose up'. Once the container is running you can run the application by searching http://localhost:XXXX on your browser where XXXX is the port number specified in your docker-compose.yml file.

#### Python 
Inside your code editor, navigate to the folder called "brevets", then run flask_brevets.py. You can run the program on a browser by typing in http://localhost:XXXX where XXXX is the port number you have indicated in your credentials file. 

## Usage

The web interface allows the brevet organizer to enter the brevet distance, start time, and checkpoint locations. As checkpoint distances are entered, the app will automatically calculate and populate the open and close time for each one.

The app provides a Submit button to save these calculated times to a database for later retrieval.

The Display button will fetch the latest saved brevet info and populate the form.

This allows organizers to save and restore the controle times for their events.

The backend uses MongoDB to store the brevet data. Docker Compose is used to run the Flask app and MongoDB containers to run the application.

## Tests

In order to run the tests, start the container then run 'docker exec -it <container id> \bin\bash' then navigate to the tests folder and run the command 'nosetests'. If successful,  



## Authors

Michal Young, Ram Durairajan. Updated by Ali Hassani.
