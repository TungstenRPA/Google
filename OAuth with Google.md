# Authenticating with Google for Kofax RPA
This guide shows how to get Kofax RPA working with Google Services like GMail, Google Calendar, Google Translate etc.
## Add HTTPS to Management Console
*In order to authenticate with Google, your Management Console needs a public ip address using HTTPS. You only need this for the authentication process. Once you have the OAuth token you can disable public access.*  
*Download free ngrok to give your Management Console a temporary public IP address with https.**  
* Make a free account at https://ngrok.com
* Download and unzip free ngrok from https://ngrok.com/download
* Open a Windows command line and change to download folder.  
![image](https://user-images.githubusercontent.com/47416964/208402679-2012336c-e891-4e26-a887-0d93ee01ef71.png)
* Copy the command from ngrok's website and paste it into the command window.
![image](https://user-images.githubusercontent.com/47416964/208402282-40f252a6-02e7-4942-a913-ddd020280906.png)  
![image](https://user-images.githubusercontent.com/47416964/208402864-a84ac121-5284-4493-ba5b-6db199485c5f.png)

## Create an App in Google
*This guide is following https://developers.google.com/identity/protocols/oauth2*
* Log in to https://console.developers.google.com/
* Click on Credentials  
![image](https://user-images.githubusercontent.com/47416964/208400550-88fa7755-169a-4ac5-9630-ed0aed8475c4.png)
* Click **+ CREATE CREDENTIALS** and **OAuth client ID**  
![image](https://user-images.githubusercontent.com/47416964/208400825-c7a66bcd-49c2-4df2-a703-1d268ca4b705.png)
* Select **Application Type** = **Web application**
* Give a name like **Kofax RPA Calendar Robot**
## Add Services to App
## Authenticate Management Console with Google
