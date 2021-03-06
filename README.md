# USB-Microphone
## Based on Microphones


## Table of Contents
1. [Introduction](#introduction)
2. [Bill of Materials/Budget](#bill-of-materialsbudget)
3. [Time Commitment](#time-commitment)
4. [Mechanical Assembly](#mechanical-assembly)
5. [Soldering](#soldering)
6. [Power up](#power-up)
7. [Unit Testing](#unit-testing)
8. [Production Testing](#production-testing)
9. [Is it Reproducible?](#reproducible)


### Introduction

Welcome to the introduction part of my Project i.e. USB-Microphone(Alexa-Skills Based).USB-Microphone is basically a microphone that we plug into the raspberry pi and it is being used for the Voice Recognition. 

The motive of this project is to replicate the skills of Alexa and make a device that reads your audio and give feedback accordingly. I have added speakers to my Project materials as we want the audible and clear feedback. This Project provides step-by-step instructions for setting up AVS on a Raspberry Pi. It also demonstrates how to access and test AVS using Java sample app (running on a Raspberry Pi), a Node.js server, and a third-party wake word engine. You will use the Node.js server to obtain a Login with Amazon (LWA) authorization code by visiting a website using your Raspberry Pi's web browser.

For extra credit, I have posted the link below on how to connect Raspberry PI to LAPTOP using Ethernet cable, eliminating the need for a monitor, keyboard and mouse.
* [Remote Connection](https://www.youtube.com/watch?v=AJ7skYS5bjI)

#### System Diagram

![System Diagram](https://github.com/PRana02/USB-Microphone-Alexa-Skills-Based-/blob/master/system%20diagram%20alexa.jpg)


### Bill of Materials/Budget
The materials required to build the USB-Microphone are Raspberry Pi 3, SunFounder USB 2.0 Mini Microphone for Raspberry Pi 3 and Logitech Z130 Compact Computer Speakers.

1) Raspberry Pi 3 (CanaKit Starter Kit):

* [Amazon](https://www.amazon.ca/CanaKit-Raspberry-Complete-Starter-Kit/dp/B01CCF6V3A/ref=sr_1_2?s=electronics&ie=UTF8&qid=1516549400&sr=1-2&keywords=rapberry+pi) CAD $99.99

2) USB 2.0 Mini Microphone:
 
* [Amazon](https://www.amazon.ca/SunFounder-Microphone-Raspberry-Recognition-Software/dp/B01KLRBHGM/ref=sr_1_1?s=electronics&ie=UTF8&qid=1516549033&sr=8-1&keywords=sunfounder+usb+microphone) CAD $39.46 
* [Ebay](https://www.ebay.ca/itm/SunFounder-USB-2-0-Mini-Microphone-for-Raspberry-Pi-3-2-Module-B-RPi-1-Model/232430660307?hash=item361df26ad3:g:bYIAAOSwySFZf1pf) US $8.62

3) Logitech Z130 Compact Computer Speakers:

* [The Source](https://www.thesource.ca/en-ca/computers-and-tablets/computer-accessories/computer-speakers/logitech-z130-compact-computer-speakers/p/108008204) CAD $39.99

* Apart from above hardware, a USB Keyboard & Mouse, and an external HDMI Monitor. I also recommend having a USB keyboard and mouse as well as an HDMI monitor handy if you're unable to remote(SSH) into your Pi.
* When I was planning my budget, the prices of the materials were slightly different from the present. 

### Time Commitment
* Time to complete this project would be around 3 days if you have everything handy with the build instruction. It took me couple of weeks to complete this project.In the first week,I had to research about my project, plan my budget accordingly and wait for the items to be delivered. During that time I learned how to connect my Raspberry Pi remotely and researched about Alexa Skills provided by Amazon.

* Well, if you are free for couple of days and want to make something interesting, I would suggest you to try this and let me know if you have any questions. My email address is piyushr97@gmail.com. Feel free to contact me.

### Mechanical Assembly

* Since this Project requires no more than two components, we just have to connect them to Raspberry Pi. Below is picture of my connection.

![Connections](https://github.com/PRana02/USB-Microphone-Alexa-Skills-Based-/blob/master/Inkedproject_LI.jpg)

* As you can see I have connected my RaspberryPi with Powerbank. The USB microphone and speakers are connected to their respective points on the RaspberryPi.

### Power Up
* Before power up the Raspberry pi, check the micro SD card to see if it has the contents of NOOBS operation system installer which contains Raspbian. If not, you can download, unzip and copy the folder contents of [NOOBS](https://downloads.raspberrypi.org/NOOBS_latest) into the root directory of the micro SD card.
* On the first boot you will be prompted to install the operating system and configure the wifi setting. Once the raspberry pi is done installing the operating system. 

* The USB audio device should be automatically installed. Go in SSH or LXTerminal window and type the following and press Enter
```
sudo apt-get install alsa-utils
```
* You may already have this package on your system, but entering this command won't do any harm even if you do. This will install a package of ALSA utilities if you don't already have them (ALSA stands for Advances Linux Sound Architecture). If you want to know more about ALSA then follow the [link](http://www.alsa-project.org/main/index.php/Main_Page).


### Unit Testing

* Now, to make sure that the USB audio device is being detected by both the hardware and software. Enter the following command and press enter. 
```
lsusb
```

* This will display information regarding attached USB devices. As you can see, the last device listed in the image below is the USB audio device labelled as C-Media Electronics, Inc. Audio Adapter. So far, so good.

![USB Microphone detection](https://github.com/PRana02/USB-Microphone-Alexa-Skills-Based-/blob/master/usb%20microphone%20detection.jpg)
 
* Now follow the steps:

##### Step 1 : Register for an Amazon developer account.
* Unless you already have one, go ahead and create a free developer account at [developer.amazon.com](https://www.amazon.com/ap/signin?openid.return_to=https%3A%2F%2Fdeveloper.amazon.com%2Fap_login.html&openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.assoc_handle=mas_dev_portal&openid.mode=checkid_setup&openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&pageId=amzn_developer_portal&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0&language=en_US&openid.pape.max_auth_age=1)

##### Step 2 : Create a device and security profile.
* Follow the steps [here](https://github.com/alexa/alexa-avs-sample-app/wiki/Create-Security-Profile) to register your product and create a security profile.

* Make note of the following parameters: ProductID,ClientID and ClientSecret.
* Allowed Origins: https://localhost:3000
* Allowed Return URLs: https://localhost:3000/authresponse

##### Step 3 : Clone the sample app
* Open terminal, and type the following command in particular folder or wherever you like. 
```
git clone https://github.com/alexa/alexa-avs-sample-app.git
```

##### Step 4: Update the install script with your credentials
* Update the script with the credentials that you got in step 2 - ProductID, ClientID, ClientSecret. Type the following in terminal:
```
cd ~/Desktop/alexa-avs-sample-app
nano automated_install.sh
```
* A window will pop with the script like below.

![script](https://github.com/PRana02/USB-Microphone-Alexa-Skills-Based-/blob/master/script.PNG)

* Paste the values for ProductID, ClientID, and ClientSecret.
* Type ctrl-X and then Y, and then press Enter to save the changes to the file.

##### Step 5: Run the install script
* You are now ready to run the install script. This will install all dependencies, including the two wake word engines from Sensory and KITT.AI.
* Note: The install script will install all project files in the folder that the script is run from.
* To run the script, open terminal and navigate to the folder where the project was cloned. Then run the following command:
```
cd ~/"foldername"/alexa-avs-sample-app
. automated_install.sh
```
* You'll be prompted to answer a few simple questions. These help to ensure that you've completed all necessary prerequisites before continuing. 
* Once you answer the questions, it will start installation. It will take some time so meanwhile grab a coffee for me.

##### Step 6: Run your web service, sample app and wake word engine
* Now that installation is complete, you'll need to run three commands in 3 separate terminal windows:

* Terminal Window 1: to run the web service for authorization
* Terminal Window 2: to run the sample app to communicate with AVS
* Terminal Window 3: to run the wake word engine which allows you to start an interaction using the phrase "Alexa".(optional)
Note: These commands must be run in order.

* Terminal Window 1
Open a new terminal window and type the following commands to bring up the web service which is used to authorize your sample app with AVS:
```
cd ~/"foldername"/alexa-avs-sample-app/samples
cd companionService && npm start
```
Once you have run the above command : The server starts running on port 3000 and you are ready to start the client.

* Terminal Window 2
Open a new terminal window and type the following commands to run the sample app, which communicates with AVS:
```
cd ~/"foldername"/alexa-avs-sample-app/samples
cd javaclient && mvn exec:exec
```
When you run the client, a window should pop up with a message.

![client](https://github.com/PRana02/USB-Microphone-Alexa-Skills-Based-/blob/master/client.PNG)

Click on "Yes" to open the URL in your default browser.

If you're running Raspbian with Pixel desktop (and with Chromium browser), you may get a warning from the browser. You can get around it by clicking on Advanced -> Proceed to localhost(unsafe)

You'll be taken to a Login with Amazon web page. Enter your Amazon credentials there.
You'll be taken to a Dev Authorization page, confirming that you’d like your device to access the Security Profile created earlier.
Click Okay.

You will now be redirected to a URL beginning with https://localhost:3000/authresponse followed by a query string. The body of the web page will say device tokens ready.

Return to the Java application and click the OK button. The client is now ready to accept Alexa requests. 

![confirm](https://github.com/PRana02/USB-Microphone-Alexa-Skills-Based-/blob/master/connfirm.PNG)


* Terminal Window 3
Note: Skip this step to run the same app without a wake word engine.

This project supports two third-party wake word engines: Sensory's TrulyHandsFree and KITT.AI's Snowboy.
Open a new terminal window and use the following commands to bring up a wake word engine from Sensory or KITT.AI. The wake word engine will allow you to initiate interactions using the phrase "Alexa".

To use the Sensory wake word engine, type -
```
cd ~/Desktop/alexa-avs-sample-app/samples
cd wakeWordAgent/src && ./wakeWordAgent -e sensory
```
or, type this to use KITT.AI's wake word engine -
```
cd ~/Desktop/alexa-avs-sample-app/samples
cd wakeWordAgent/src && ./wakeWordAgent -e kitt_ai
```

* The wait is over. After all the work and effort, you have successfully replicate the project. Now enjoy.

##### Step 7: Talk to Alexa
You can now talk to Alexa by simply using the wake word "Alexa". Try the following -

* Say "Alexa", then wait for the beep. Now say "what's the time?"

* Say "Alexa", then wait for the beep. Now say "what's the weather in Seattle?"

### Production Testing:
If we want to produce the project on large scale, we can do it in different ways.
* By creating single account for multiple users. OR
* By creating individual account for each user.

### Reproducible?
* By following this build instruction, I believe you will be able to reproduce the Alexa skills USB microphone.I have provided budget,schedule and other required details on my [GitHub](https://github.com/PRana02/USB-Microphone-Alexa-Skills-Based-) regarding this project.
