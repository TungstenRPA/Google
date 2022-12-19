# Authenticating with Google for Kofax RPA
This guide shows how to get Kofax RPA working with Google Services like GMail, Google Calendar, Google Translate etc. It uses the example of Google Calendar.  
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
* Search for **Calendar** and open **Google Calendar API**.
![image](https://user-images.githubusercontent.com/47416964/208407451-80887782-adc7-4799-8d5f-91bb12e522fc.png)  
*  Click **ENABLE**.  
![image](https://user-images.githubusercontent.com/47416964/208407539-2ff9a4bd-ee73-4fe2-932d-359bd270e859.png)
* Cick **CREDENTIALS** and Enable **Kofax RPA Calendar Robot**.  
![image](https://user-images.githubusercontent.com/47416964/208407727-75889799-99f1-4117-bb8b-746ce5a9b5be.png)
## Add Calender SCopes
* Open **OAuth Consent Screen** (https://console.cloud.google.com/apis/credentials/consent).
* Click **EDIT APP**.  
![image](https://user-images.githubusercontent.com/47416964/208409952-67be182a-c7ce-412c-b487-ef512ff81d43.png)
* Fill in the App Information however you like.
* Add the ngrok URL to the **Authorized Domains**.  
![image](https://user-images.githubusercontent.com/47416964/208410173-0dd87ddd-1dd2-40d8-80bb-97826b576273.png)
* Click **SAVE AND CONTINUE**  
![image](https://user-images.githubusercontent.com/47416964/208410238-1b984a52-d580-4657-a50e-bdd471889f88.png)
* Click **ADD OR REMOVE SCOPES**  
![image](https://user-images.githubusercontent.com/47416964/208410358-bb12af7f-3756-4670-a1b9-5999e419b916.png)
* In **Filter** search for **Calendar**.  
![image](https://user-images.githubusercontent.com/47416964/208410678-fa114cc0-f4b8-4638-8613-720f32c24a35.png)
* Select **Gogle Calendar API**, type **events** and press ENTER.  
* Select **See, create, change, and delete events on Google calendars you own**.  
![image](https://user-images.githubusercontent.com/47416964/208410950-dc927d42-c9df-49d5-ab06-4b6e06ff22c0.png)
*  Click **UPDATE**.

## Create OAuth Application in Management Console
* Open https://console.cloud.google.com/apis/credentials and click "Kofax RPA Calendar Robot" to see your **Client ID** and **Client Secret**.  
![image](https://user-images.githubusercontent.com/47416964/208408456-77f3d962-72d7-4c3f-9a1e-5f7bacdfa662.png)
* Open Management Console from your public IP address with HTTPS.  
* Click **Repository/OAuth** and create a new **OAuth Application**.  
![image](https://user-images.githubusercontent.com/47416964/208408066-9f81b067-2b23-42d0-9bf8-82f9232df543.png)
* Copy the **Client ID** into the **Consumer Key** and **Client Secret** into the **Consumer Secret**. Be careful that you don't copy any trailing spaces!!
* Enter **https://www.googleapis.com/auth/calendar.events.owned** as Scope.  
![image](https://user-images.githubusercontent.com/47416964/208411329-37a90031-7a7b-418c-baa4-9388b2f5e0cb.png)
* Press OK.
## Create OAuth User in Management Console
* Create a new **OAuth User** in Management Console.  
![image](https://user-images.githubusercontent.com/47416964/208411505-053264ca-5e4f-482d-8240-75cddf2ed2f1.png)
* Select the Application and enter a user name.  
![image](https://user-images.githubusercontent.com/47416964/208411736-7e9f242f-f96b-4ca0-ab63-5b6a834b0b8d.png)
* Click **Next**.
* Click **Authorization Link** to open a new window.  
![image](https://user-images.githubusercontent.com/47416964/208411876-7a20a08e-ba5f-43d5-8c36-833382597bd6.png)
* Choose a Google Account to continue.  
![image](https://user-images.githubusercontent.com/47416964/208415138-c5ad4d32-1cbe-4239-9b25-b2768cdcc92f.png)
* Click **Continue** to ignore the warning about this being a test app.  
![image](https://user-images.githubusercontent.com/47416964/208415227-5d83f919-1acc-4e0a-895a-f16727e1d8c5.png)
* You are now at the OAuth screen. Google is asking your permission to allow Management Console to be able to **see, create, change and delete events on Google Calender**. Click **Continue**.  
![image](https://user-images.githubusercontent.com/47416964/208415444-c83f98ec-9b11-4f2a-8a01-d26aa4ec9176.png)  
* Close the Browser Tab.  
![image](https://user-images.githubusercontent.com/47416964/208415672-8ce52d14-aa34-4478-88d1-68754f1aa3aa.png)
* Click **Next**.  
![image](https://user-images.githubusercontent.com/47416964/208415765-5e6d5090-14f8-4cad-867d-bea72e1b1bd0.png)
* Management Console will now show you the **Access Token** an **Refresh token** needed by the robot to access Google Calendar
* Copy both of these tokens **NOW**! You won't see them again. You need to copy them to test your robot in Design Studio. A robot in Design Studio cannot retrieve oAuth credentials from the Management Console.  
* You will not see these tokens again, so if you want to copy them you need to do it now*.
![image](https://user-images.githubusercontent.com/47416964/208416041-52ee85c4-54bd-4d9d-bc78-097a117955a2.png)
* you can now stop **ngrok**, it is no longer needed.
## Test your Robot
* Download and open the robot **GoogleCalendar_CreateEvent.robot** along with **GoogleCalendar_Event.type**
* Open the variable **oAuth** and paste in the key, secret and two tokens from above.
![image](https://user-images.githubusercontent.com/47416964/208424843-6695b40c-64dc-4f5f-8a9a-836f83b90696.png)
* Open the **event** variable and Change the *start* and *end* dates to Now() and then adjust them to later today or tomorrow. Edit any other attributes you like.
* The robot creates to JSON needed to send to the Google Calendar API.
* Google Calender API is called from the **Create Event** step, which is a REST POST step, with JSON body and OAuth Authetication.  If the result is successful, the Google returns the data for the created event.  
![image](https://user-images.githubusercontent.com/47416964/208425355-3dfe1704-2ed7-4404-8713-9eaa68173dc5.png)
* You can also see the event in [Google Calendar](https://calendar.google.com)  
![image](https://user-images.githubusercontent.com/47416964/208425509-6345ab93-5ded-40c3-8019-8441403cb861.png)




