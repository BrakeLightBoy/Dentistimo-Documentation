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
For this project we have been tasked with creating a dentist website which will allow the people of Gothenburg to book appointments through our application. From this we have been provided with some requirements, whilst we have also come up with additional requirements based upon the descriptions which we have been given.

Functional Decomposition Model:

![FDM](images/Functional%20Decomposition%20Model.drawio%20(3).png "Functional Decomposition Model")

**Functional Requirements:**

Account-Management:

1. The system shall allow users to register an account
2. The system shall allow users to login under an account which they have created
3. The system shall allow users to change their password or email address

Make-Appointments:

4. The system shall allow users to navigate to different pages through the navigational bar at the top of the page
5. The system shall provide a map where users can click on different clinics, also revealing the clinics information
6. The system shall allow users to book specific appointment slots once a clinic is clicked on the map

View-Appointments:

7. The system shall allow users to see appointments that they have made along with their details
8. The system shall allow users to delete appointments that they have made


**Nonfunctional Requirements:**
1. The website shall maintain a consistent User Interface, allowing users to access any of the website's core functionality within 4 clicks
2. The user shall receive confirmation of the booking within a second of pressing the ‘Book’ button
3. The website shall be able to correctly handle multiple concurrent booking attempts to the same slot
4. The website shall have an availability of 99% (2-nines)

## Software Architecture Document (SAD)
Here we have decided to include some of the diagrams which we haven chosen to create. We have decided upon these as we felt they were important in helping us to determine the architectural structure, functionality, and help us with building the overall project. We started with an ER diagram to try to map how our database and models would look like as this would be our base. 

ER Diagram:

![ER diagram](images/ER%20Diagram.drawio.png?raw=true "ER Diagram")

For our system, we have decided to use the architectural styles which have been recommended to us, which are Pipe-and-Filter, Publish/Subscribe and Client/Server. 

**Pipe and Filter**  
- As we know with the Pipelines style architecture, this follows a set of pipes and filters in the structure with 4 different types of filters that exist. In our project, we use this structure in our backend components in order to transform and forward messages, allowing us to call the correct method. We start off with the producer which is the starting point, which for our system would be represented through our requestFilter class. The requestFilter class also serves as a Transformer filter as here we have a “transform” method which parses the payload of the MQTT message received and then forwards it. The next class which the message travels through is the serviceTypeFilter, which can be compared to a Tester filter in the pipelines style. Here we have a switch case which compares the messages operation-category to determine which type of entity it belongs to (whether that be user, dentist or appointment) and from there forward it to the correct entity filter class. The entity type filters, such as userServFilter, can also be compared to Tester filters as here we compare against the operation, which we consider as the method to be performed on the data such as login, or get-user. Based upon this operation, we call upon the correct Service class and its method. The pipelines style helps create a clear workflow within our project, allowing us to better understand the communication between the frontend and backend of our application. Furthermore, as proven through its lifetime, it has also provided nice maintainability as any errors could be tracked down easily.


**Publish/Subscribe**
- For the Publish/Subscribe style this is implemented through the usage of MQTT in our project. MQTT is what allows communication between our client component and the other 3 distributed backend components. For this a component can publish messages to a certain topic which other components can subscribe to, allowing all of the subscribers to receive the message.


**Service-Based**
- The last architectural style which our project uses is the Service-based architecture style. For our project, we follow this style with a topology containing 1 user interface (our client), 3 different backend services (which are distributed components) and a singular monolithic database. This acts as the main structure behind our distributed architecture and was chosen for its lower cost, simplicity, but also its higher ratings with other Quality Attributes like deployability and reliability.

Furthermore, for this project we have decided upon 4 different distributed which will act together to create our functioning dentist web application. The 4 components consist of:

Component Diagram:

![Component diagram](images/Component%20Diagram.drawio.png "Component Diagram")

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

After this is installed and setup on your computer, it is important to make sure that all the dependencies are installed:
1. Open a terminal tab (either Command Prompt for Windows or Terminal for Mac) at the root folder for all of the components (Client, Account-Manager, Booking-Manager and Clinic-Tracker)
2. Install the dependencies (through the command 'npm install')


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

Each components repository will also have a ReadMe file specifying how to get that component running, but in simplistic terms:

To run the front-end you simply need to open a terminal in the directory of the client folder and enter 'npm start'. If it does not open in your browser automatically you can go to http://localhost:3000 to open it manually.  

To run the back-end you need to open a terminal in the directory of each backend component folder (Account-Manager, Booking-Manager and Clinic-Tracker) and enter 'node main.js'. 

Now your application should be up and running!

## Project Management Report (PMR)

From the start we have decided to follow **Scrum** very closely, almost using every practice which Scrum follows. During each sprint, we host Sprint Planning meetings (before each sprint), and Sprint Review and Retrospective meetings at the end of each sprint in order to discuss how the process and product developed. 

One part of Scrum which we have modified slightly is the Scrum Daily meetings. For this we have opted to not have daily meetings but instead check in on the team 3-5 times a week to ensure that everything is going to plan. A point which should be made clear is that we emphasize the importance of speaking up rather than waiting to be checked in on. What this means is that, if a member is struggling or having difficulties with a user story or task, we encourage them to speak up and ask the group for help rather than wait for our scrum meetings. 

Furthermore we also do follow Scrum roles with one Product Owner (Wojciech Pechmann), one Scrum Master (Michael Larsson) and then the rest of the team acts as the Scrum team. We have chosen to follow the defined roles, but to re-iterate, our Product Owner acts as the expert on our Product, working with our team to define most of the user stories. The PO also keeps track of the products development and ensures that it satisfies the needs of the customer. The Scrum Master will take charge of the weekly sprints, deciding with the PO which user stories to take on during the sprint, and also taking charge during the 3 meetings (Planning, Review and Retrospective).


