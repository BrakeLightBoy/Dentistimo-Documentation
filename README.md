# T9 Project



## Getting started

To make it easy for you to get started with GitLab, here's a list of recommended next steps.

Already a pro? Just edit this README.md and make it your own. Want to make it easy? [Use the template at the bottom](#editing-this-readme)!

## Add your files

- [ ] [Create](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#create-a-file) or [upload](https://docs.gitlab.com/ee/user/project/repository/web_editor.html#upload-a-file) files
- [ ] [Add files using the command line](https://docs.gitlab.com/ee/gitlab-basics/add-file.html#add-a-file-using-the-command-line) or push an existing Git repository with the following command:

```
cd existing_repo
git remote add origin https://git.chalmers.se/courses/dit355/dit356-2022/t-9/t9-project.git
git branch -M main
git push -uf origin main
```

## Integrate with your tools

- [ ] [Set up project integrations](https://git.chalmers.se/courses/dit355/dit356-2022/t-9/t9-project/-/settings/integrations)

## Collaborate with your team

- [ ] [Invite team members and collaborators](https://docs.gitlab.com/ee/user/project/members/)
- [ ] [Create a new merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html)
- [ ] [Automatically close issues from merge requests](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically)
- [ ] [Enable merge request approvals](https://docs.gitlab.com/ee/user/project/merge_requests/approvals/)
- [ ] [Automatically merge when pipeline succeeds](https://docs.gitlab.com/ee/user/project/merge_requests/merge_when_pipeline_succeeds.html)

## Test and Deploy

Use the built-in continuous integration in GitLab.

- [ ] [Get started with GitLab CI/CD](https://docs.gitlab.com/ee/ci/quick_start/index.html)
- [ ] [Analyze your code for known vulnerabilities with Static Application Security Testing(SAST)](https://docs.gitlab.com/ee/user/application_security/sast/)
- [ ] [Deploy to Kubernetes, Amazon EC2, or Amazon ECS using Auto Deploy](https://docs.gitlab.com/ee/topics/autodevops/requirements.html)
- [ ] [Use pull-based deployments for improved Kubernetes management](https://docs.gitlab.com/ee/user/clusters/agent/)
- [ ] [Set up protected environments](https://docs.gitlab.com/ee/ci/environments/protected_environments.html)

***

# Dentismo - Gothenburg's Best Dentistry System # 

## Description
Finding a dentist that suits you and making a booking for an appointment should be a straight-forward process, but in Sweden today, this is not the case. The project which we are developing allows for people in Gothenburg to seamlessly make and manage bookings to the dentist of their choice. Furthermore, the dentists themselves will have accounts on the website, allowing for them to check the schedule of the clinic which they belong to as well as their individual schedules. 

Our website will allow for both ease in booking as well as ease in determining which dentist is right for you. It will provide users with a map overview showing the different locations of each dentist and when a clinic is clicked on, the clinic information will be displayed. Specific functionality available to users, dentists and clinics is further demonstrated in our Functional Decomposition Model below.

## Badges
On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Visuals
Here we have decided to include some of the diagrams which we haven chosen to create. We have decided upon these as we felt they were important in helping us to determine the structure, functionality, and help us with building the overall project.

ER Diagram:

![ER diagram](images/ER%20Diagram.drawio.png?raw=true "ER Diagram")

Functional Decomposition Model:

![FDM](images/Functional%20Decomposition%20Model.drawio%20(2).png?raw=true "FDM")

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

## Authors and acknowledgment

Product Owner: Wojciech Pechmann
Scrum Master: Michael Larsson

Documentation: The whole team

### **Front-end team:** 

Emil Eriksson - guseriemca@student.gu.se

Frida Anselin - gusansfr@student.gu.se

### **Back-end team:**

John Berntsson - gusberjoid@student.gu.se

Elisa Ahlbäck Norris - gusahlelj@student.gu.se

### **Full-stack team:**

Noah Manne Johansson - gusnoahjo@student.gu.se

Wojciech Pechmann - guspecwo@student.gu.se

Michael Larsson - guslarmiad@student.gu.se


## Project status
Currently Ongoing!