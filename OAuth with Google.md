# Authenticating with Google for Kofax RPA
This guide shows how to get Kofax RPA working with Google Services like GMail, Google Calendar, Google Translate etc.
## Add HTTPS to Management Console
This guide was created on 19 December 2022. Google may have made some changes since then. Please report any changes by opening an [issue](https://github.com/KofaxRPA/Google/issues/new)!  
*In order to authenticate with Google, your Management Console needs a public ip address using HTTPS. You only need this for the authentication process. Once you have the OAuth token you can disable public access.*  
*Download free ngrok to give your Management Console a temporary public IP address with https.**  
* Make a free account at https://ngrok.com
* Download and unzip free ngrok from https://ngrok.com/download
* Open a Windows command line and change to download folder.  
![image](https://user-images.githubusercontent.com/47416964/208402679-2012336c-e891-4e26-a887-0d93ee01ef71.png)
* Copy the command from ngrok's website and paste it into the command window.
![image](https://user-images.githubusercontent.com/47416964/208402282-40f252a6-02e7-4942-a913-ddd020280906.png)  
![image](https://user-images.githubusercontent.com/47416964/208402864-a84ac121-5284-4493-ba5b-6db199485c5f.png)
* Give Management Console a public IP address by typing **ngrok http 50080**  
![image](https://user-images.githubusercontent.com/47416964/208403175-6e0da069-3c07-4809-a941-83715da69878.png)
![image](https://user-images.githubusercontent.com/47416964/208403507-c94911e1-4e82-4d78-bce2-cc676b3f8639.png)

* Open your Management Console in a new browser window using this IP address. This is VERY important to authenticate with OAuth.
![image](https://user-images.githubusercontent.com/47416964/208403660-8c82e9c0-0031-4920-98ed-3912f29fee14.png)

## Create an OAuth client ID on Google Cloud
*This guide is following https://developers.google.com/identity/protocols/oauth2*
* Log in to https://console.developers.google.com/ with the Google Account connected to the Google Calendar you want to control.
* Click on Credentials  
![image](https://user-images.githubusercontent.com/47416964/208400550-88fa7755-169a-4ac5-9630-ed0aed8475c4.png)
* Click **+ CREATE CREDENTIALS** and **OAuth client ID**  
![image](https://user-images.githubusercontent.com/47416964/208400825-c7a66bcd-49c2-4df2-a703-1d268ca4b705.png)
* Select **Application Type** = **Web application**
* Give a name like **Kofax RPA Calendar Robot**
* Add the ngrok url to **Authorized Javascript Origins**  
![image](https://user-images.githubusercontent.com/47416964/208404398-e4e9a09b-511e-48e5-8e87-6317871b0b5d.png)
* Add the Callback URL to **Authorized redirect URIs** with /OAuthCallback  
![image](https://user-images.githubusercontent.com/47416964/208404528-f8bbce0a-4660-4fbf-86ba-a4300d1c1288.png)
* Click **CREATE**
## Add test user to your OAuth consent screen.
* Click **OAuth consent screen**
![image](https://user-images.githubusercontent.com/47416964/208404740-0a64b2a1-63c4-42da-94a1-5057f8d3295f.png)
* Click **+ ADD USERS** and add the Google email address that you will use for the Management Console.
![image](https://user-images.githubusercontent.com/47416964/208405351-3c006b61-5f70-4b41-b538-0c5e48ebf3d8.png)
## Enable Google Calender API
* Click on **Enabled APIs & services** and **+ ENABLE APIS AND SERVICES**.  
![image](https://user-images.githubusercontent.com/47416964/208407182-6750f8fd-497a-4250-a4e7-25c249067bc4.png)


## Authenticate Management Console with Google
