# T9 Project

# Dentismo - Gothenburg's Best Dentistry System # 

## Purpose
Finding a dentist that suits you and making a booking for an appointment should be a straight-forward process, but in Sweden today, this is not the case. The project which we are developing allows for people in Gothenburg to seamlessly make and manage bookings to the dentist of their choice. Furthermore, the dentists themselves will have accounts on the website, allowing for them to check the schedule of the clinic which they belong to as well as their individual schedules. 

Our website will allow for both ease in booking as well as ease in determining which dentist is right for you. It will provide users with a map overview showing the different locations of each dentist and when a clinic is clicked on, the clinic information will be displayed. Specific functionality available to users, dentists and clinics is further demonstrated in our Functional Decomposition Model below.

Our team consists of: 
### **Front-end team:** 

- Emil Eriksson - guseriemca@student.gu.se

- Frida Anselin - gusansfr@student.gu.se

### **Back-end team:**

- John Berntsson - gusberjoid@student.gu.se

- Elisa Ahlbäck Norris - gusahlelj@student.gu.se

### **Full-stack team:**

- Noah Manne Johansson - gusnoahjo@student.gu.se

- Wojciech Pechmann - guspecwo@student.gu.se (Also is the Product Owner)

- Michael Larsson - guslarmiad@student.gu.se (Also is the Scrum Master)


### Relevant Links
Trello : https://trello.com/invite/b/0P4o28Sa/ATTIddf007a5e5d13c76d25c4d550162d6f79E4495E6/project-management-mini-project

Git Project :
https://git.chalmers.se/courses/dit355/dit356-2022/t-9

## Software Requirement Specification (SRS)
On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Software Architecture Document (SAD)
Here we have decided to include some of the diagrams which we haven chosen to create. We have decided upon these as we felt they were important in helping us to determine the architectural structure, functionality, and help us with building the overall project. We started with an ER diagram to try to map how our database and models would look like as this would be our base. 

ER Diagram:

![ER diagram](images/ER%20Diagram.drawio.png?raw=true "ER Diagram")

For our system, we have decided to use the architectural styles which have been recommended to us, which are Pipe-and-Filter, Publish/Subscribe and Client/Server. 

**Pipe and Filter**  
- We have created our backend structure to work together with MQTT in order to replicate the Pipe-and-Filter structure, where we firstly have one filter-type class (serviceTypeFilter)that will determine which entity it belongs to from the MQTT messages opCat, and then an entity-based filter class (userServFilter) which will call upon the respective service and method from the MQTT messages operation.

**Publish/Subscribe**
- For Publish/Subscribe, MQTT already deals with this architectural style, as it follows a publish/subscribe protocol with the messages being sent.

**Client/Server**
- For Client/Server, this has been implemented through the structure of our application by seperating the code between the two sides. Our client side is composed of one distributed component, whilst our server side is composed of three different distributed components (these will be discussed in the Component section below).

Furthermore, for this project we have decided upon 4 different distributed which will act together to create our functioning dentist web application. The 4 components consist of:

Component Diagram

1. Client - As the name suggests, the client component will act as the frontend of our web application containing our UI, and small functionalities which will call upon MQQT messages that will eventually communicate with the backend. For the frontend we have decided to use React as this is a popular language that works well with our system.

2. Booking Manager - The booking manager component is one of three components which acts on the backend side of our application dealing with the bookings and appointments for the application. This deals with our appointment entity in our database.

3. Account Manager - The account manager is another component which acts on the backend side, and handles most of the functionality and data regarding both dentist and general user accounts. We have chosen to add both dentists and users into this one component as although there are some slight differences, the majority of the functionality is the same. Hence, this component deals with the dentist and user entity in our database.

4. Clinic Tracker - The clinic tracker is the third and final backend component which deals with keeping track of the clinic information. This includes functionalities such as sending the coordinates and basic clinic information to the frontend. In the database this deals with our clinic entity.

**MQTT**
Our MQTT Broker is also considered as a component part apart of our system, however does not have its own repository and acts more behind the scenes to receive and forward messages.


## Installation 
In order to run our application it is required to have MQTT, MongoDB and Node.js installed.

MongoDB - https://www.mongodb.com/try/download/community-kubernetes-operator. 
Installation steps for [Mac](https://github.com/joe4dev/dit032-setup/blob/master/macOS.md#mongodb), [Windows](https://github.com/joe4dev/dit032-setup/blob/master/Windows.md#mongodb) and [Linux](https://github.com/joe4dev/dit032-setup/blob/master/Linux.md#mongodb)

Node.js - https://nodejs.org/en/download/

MQTT - https://mosquitto.org/download/

After this is installed and setup on your computer, it is important to make sure that all the dependencies are installed on both the front-end and back-end:
1. Open a terminal tab (either Command Prompt for Windows or Terminal for Mac)
2. For both the client and server folder directory install the dependencies (through the command 'npm install')


For the backend to run you will need to make some changes to your mosquitto.conf file:
1. Head to your mosquitto folder in your computer
2. Open the mosquitto.conf file with a text editor
3. Locate the line #socket_domain in this file 
4. Add these lines below and save the file

port 1883

listener 9001

protocol websockets

socket_domain ipv4

allow_anonymous true

5. Ensure that you start up your mosquitto by opening your terminal (you may need to run this in administrator) and typing 'net start mosquitto', for Mac this is different as you will have to run this command '/opt/homebrew/opt/mosquitto/sbin/mosquitto -c /opt/homebrew/etc/mosquitto/mosquitto.conf', if there are issues running this commmand, contact either the product owner and scrum master. 
6. You can check to ensure everything is setup by then entering in the terminal 'netstat -a' and checking to see if the address '0.0.0.0:9001' is there

For further clarity check out this tutorial which inspired these steps on the backend: https://iot4beginners.com/how-to-enable-mosquitto-mqtt-over-websocket-on-windows/

## Run

Now in order to run the front-end you simply need to open a terminal in the directory of the client folder and enter 'npm start'. If it does not open in your browser automatically you can go to http://localhost:3000 to open it manually.  

To run the back-end you need to open a terminal in the directory of the server folder and enter 'node main.js'

Now your application should be up and running!

## Project Management Report (PMR)

From the start we have decided to follow **Scrum** very closely, almost using every practice which Scrum follows. During each sprint, we host Sprint Planning meetings (before each sprint), and Sprint Review and Retrospective meetings at the end of each sprint in order to discuss how the process and product developed. 

One part of Scrum which we have modified slightly is the Scrum Daily meetings. For this we have opted to not have daily meetings but instead check in on the team 3-5 times a week to ensure that everything is going to plan. A point which should be made clear is that we emphasize the importance of speaking up rather than waiting to be checked in on. What this means is that, if a member is struggling or having difficulties with a user story or task, we encourage them to speak up and ask the group for help rather than wait for our scrum meetings. 

Furthermore we also do follow Scrum roles with one Product Owner (Wojciech Pechmann), one Scrum Master (Michael Larsson) and then the rest of the team acts as the Scrum team. We have chosen to follow the defined roles, but to re-iterate, our Product Owner acts as the expert on our Product, working with our team to define most of the user stories. The PO also keeps track of the products development and ensures that it satisfies the needs of the customer. The Scrum Master will take charge of the weekly sprints, deciding with the PO which user stories to take on during the sprint, and also taking charge during the 3 meetings (Planning, Review and Retrospective).




## Project status
Currently Ongoing!