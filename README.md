# Cisco SD-WAN ServiceNow Integration

A Flask demo application that automatically creates and resolves incidents in ServiceNow when as an alarm happens in SD-WAN. Additionally, it is possible to send Webex notifications to an admin.

> Note: This demo is an updated version of the former GVE DevNet use case: https://github.com/gve-sw/GVE_Devnet_CiscoSDWAN_ServiceNow


## Contacts
* Ramona Renner
* Efe Evyapan
* Eda Akturk


## Solution Components
* Cisco SD-WAN
* ServiceNow 
* Webex 
* Python


## Solution Overview
![/IMAGES/image1.PNG](/IMAGES/image1.PNG)


## Setup

### Webhook Receiver URL
1. vManage webhooks allow to send an HTTP POST request to an external system once an alarm happens. Therefore, this demo app requires being reachable over an internet accessible URL. It can be deployed on different IaaS platforms like Heroku, Amazon Web Services Lambda, Google Cloud Platform (GCP) and more. Alternatively, a simple way to create a public URL for a locally running demo app is to use [ngrok](https://ngrok.com/).

> Note: Assuming you kept the default parameters of this Flask application, the script will run at: http://localhost:3333


### Cisco SD-WAN
2. Configure a webhook in vManage:
* In the main menu, click **Monitor** > **Logs**
* Click **Alarm Notifications** > **Add Alarm Notification** and fill in the form fields:
    * **Name**  
    * **Severity**, e.g. All
    * **Alarm Name:**, e.g. System Reboot Issued 
    * Select the **Webhook** checkbox 
    * Public **Webhook URL** of the webhook receiver 
    * **Webhook Threshold**, e.g. 100
    * **Username**
    * **Password**
    * (Optional) **Device** to receive alarms for.

For older vManage versions, see [instructions here.](https://www.cisco.com/c/en/us/support/docs/routers/sd-wan/214615-vmanage-configure-alarm-email-notificat.html)

### ServiceNow   
3. If you do not have a ServiceNow instance, you can sign up for the developer program to obtain one [here.](https://developer.servicenow.com/dev.do)

### (Optional) Webex Bot   
4. If you would like to additionally receive Webex notifications on alarms:   
Create a Webex bot from [here.](https://developer.webex.com/my-apps/new/bot) 


# Installation

5. Make sure Python 3.8 and Git are installed in your environment, and if not, you may download Python [here](https://www.python.org/downloads/) and Git as described [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
7. (Optional) Create and activate a virtual environment for the project ([Instructions](https://docs.python.org/3/tutorial/venv.html)).
8. Access the created virtual environment folder
    ```
    cd [add name of virtual environment here] 
    ```
9. Clone this Github repository:  
  ```git clone [add github link here]```
  * For Github link: 
      In Github, click on the **clone or download** button in the upper part of the page > click the **copy icon**  
      ![/IMAGES/giturl.png](/IMAGES/giturl.png)
  * Or simply download the repository as a zip file using 'Download ZIP' button and extract it
10. Access the downloaded folder:  
    ```cd gve_devnet_sd-wan_servicenow_integration```

11. Install all dependencies:  
  ```pip3 install -r requirements.txt```


12. Configure the environment variables in the .env file:  
      
    ```
    SERVICENOW_USERNAME="<username of ServiceNow instance account (see step 3)>"
    SERVICENOW_PASSWORD="<password of ServiceNow instance account (see step 3)>"
    SERVICENOW_INSTANCE="<URL of ServiceNow instance (see step 3)>"

    WEBEX_NOTIFICATION="<enable or disable Webex notifications - 1 for enable, 0 for disable>"
    WEBEX_ACCESS_TOKEN="<Webex bot token (see step 4)>"
    WEBEX_ALERT_USER="<Webex user to receive the notifications>"
    ``` 

> Note: Mac OS hides the .env file in the finder by default. View the demo folder for example with your preferred IDE to make the file visible. 


## Usage
```
python3 app.py
```

When you start the demo application, ServiceNow tickets/incidents and Webex notifications will be created for Webhook notifications from vManage. 

<b>Please note:</b> The alarms that have been tested for the project are as follows:
- BFD TLOC DOWN/UP
- BFD BETWEEN SITES DOWN/UP
- BFD NODE DOWN/UP
- BFD SITE DOWN/UP
- Control TLOC DOWN/UP
- System Reboot Issued
- Control Node DOWN/UP


#### *(Optional) Edit Webex Teams Card Message :*
The application will send adaptive card messages based on the alarms. You can use the card designer [here](https://developer.webex.com/buttons-and-cards-designer) to change the format of the adaptive card. 

Once you create your card, you can edit the servicenow.json file to be modified according to the new format. 

### LICENSE

Provided under Cisco Sample Code License, for details see [LICENSE](LICENSE.md)

### CODE_OF_CONDUCT

Our code of conduct is available [here](CODE_OF_CONDUCT.md)

### CONTRIBUTING

See our contributing guidelines [here](CONTRIBUTING.md)

#### DISCLAIMER:
<b>Please note:</b> This script is meant for demo purposes only. All tools/ scripts in this repo are released for use "AS IS" without any warranties of any kind, including, but not limited to their installation, use, or performance. Any use of these scripts and tools is at your own risk. There is no guarantee that they have been through thorough testing in a comparable environment and we are not responsible for any damage or data loss incurred with their use.
You are responsible for reviewing and testing any scripts you run thoroughly before use in any non-testing environment.
