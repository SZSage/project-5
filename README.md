# UOCIS322 - Project 5 #
Brevet time calculator with MongoDB!

## Overview

This project expands on project 4: https://github.com/SZSage/project-4 by implementing MongoDB and `docker-compose` as storage containers. When used together, these tools allow us to easily manage and connect multiple containers, resulting in a single service comprised of different sub-services. The goal is to copy the `brevets/` directory from Project 4 over to Project 5 and add a MongoDB service to `docker-compose` and Flask app. Two additional buttons `Submit` and `Display` are added to the webpage.

- `Submit`: Stores data (brevet distance, start time, checkpoints, and open and close time) in the database while overwriting the existing ones.

- `Display`: Fetches the data from the database and fills the form.


## Getting Started
These commands are used to run and stop the project.

- `docker compose up --build -d`: is used to start a Docker Compose application in detached mode, while also rebuilding the containers if any changes are made in the files. 
-  `docker compose down`: is used to stop and remove containers that are created by Docker Compose.


## Tasks
The steps used to complete this project are as follows,

- Add MongoDB services to `docker-compose.yml` and connect them together
- Add a PyMongo interface to `flask_breveys.py`
- Write tests to ensure that the database components are working
- Add `Submit` and `Display` buttons to the web interface in `brevets/templates/calc.html`
- Write the JavaScript interaction for `Submit` and `Display`

### Back-end
The file `mypymongo.py` was created to include the MondoDB functions `brevet_insert()` and `brevet_find()`.

- The `brevet_insert()` function takes in a brevet distance, a begin time, and a list of checkpoints as a list of dictionaries, and inserts them into the database. It then returns the primary key assigned to the document by MongoDB.
- The `brevet_find()` function retrieves the newest brevet from the database and returns its brevet distance, begin time, and checkpoints as a tuple.

Two additional Flask routes and functions `_insert_brevet()` and `_find_brevet` were added to `flask_brevets.py`.

- The `_insert_brevet()` function accepts a JSON request, extracts the relevant data, passes it to brevet_insert() to insert it into the database, and returns a JSON response indicating success or failure.
- The `_find_brevet()` function returns a JSON response containing the latest brevet information obtained by calling brevet_find().

### Front-end
The buttons and functionality `Submit` and `Display` were added to `brevets/templates/calc.html`. 

- The `Submit` buttons functionality has an click event listener. When the button is clicked, the function sends a POST request to a specified URL, containing data entered into the form, and then clears the form fields.
- The `Display` button also has a click event listener that sends a GET request to a specified URL, retrieves data, and then populates form fields with miles, km, location, open and close times.

### Testing

`test_insert()` and `test_find()` were implemented to `brevets/tests/test_mypymongo.py` to test that we can insert and retrieve data from the database. 

## Authors

Michal Young, Ram Durairajan. Updated by Ali Hassani.

Completed by Simon Zhao: simonz@uoregon.edu
