#Appmobi Secure Mobile Platform
---------------------
The Appmobi Secure Mobile Platform provides a level of security never seen in a mobile platform, enabling the development of highly secure Cordova-based applications in minutes versus months. This platform provides your development team with configurable, high-performance security options for every app built, including app and device level shared keys for encryption and identity verification as well as integration with most 3rd party authentication systems such as OAUTH, LDAP, and more.

Quickly and easily build the most secure apps on the market today, in minutes.

##Requirements
--------
In order to utilize the Appmobi platform, you must have a registered Appmobi platform.  [Register for FREE](https://cloud.appmobi.com/) for our public cloud to get up and running fast.  We also offer a PrivateStack install where you can isolate the Appmobi backend on your own Amazon Web Service account; [Register for a PrivateStack Demo](https://licensing.appmobi.com/demo/signup/).  Additional AWS charges may apply depending on the configuration of your PrivateStack platform.

##Features
--------
###Security Kit

Appmobi provides Mobile Application Data Encryption and User Authentication out of the box – securing enterprise mobile applications with 3 levels of security

 - Good: App level shared key encryption
 - Better: App + Device level shared key
 - Best: App + Device Level + Authentication
  This best level of security provides two types of authentication :

###LDAP

For Using LDAP Authentication, A developer must configure his LDAP server for his app in Appmobi Management Portal. That in turn allows user to provide server credentails for login in to the App.

####initializePlugin using LDAP

Initialize the AppMobi Cordova plugin onDeviceReady() event is executed.

```javascript
function onDeviceReady() {
               initializePlugin();
            }
initializePlugin: function () {

//The ldapUserName and ldapPassWord should be obtained from User in index.html.
 //These params can be passed as "" in case of security level 1 and security level 2.
 var ldapUserName="";
 var ldapPassWord="";

       // Show a loading Image while a plugin is initializing. This can be a gif Image showing progress.
      //  var launchImageID = document.getElementById('launchImage');
       // launchImageID.style.display = 'block';
        AppMobiCloud.plugin.initialize(function (data) {//success callback
                    alert("AppMobi library initialized successfully");
                    //Hide the loading Image once Plugin initialise successfully.
                   // var launchImageID = document.getElementById("launchImage");
                   // launchImageID.style.display = 'none';
        }, function (data) {//error callback
                    alert(data.message);
                    //Hide the loading Image if Plugin initialized failed.
                   // var launchImageID = document.getElementById("launchImage");
                   // launchImageID.style.display = 'none';
        }, ldapUserName,ldapPassWord);  document.addEventListener('deviceready', onDeviceReady, false);
```

###OAuth

A developer can use OAuth for App Login. In order to configure OAuth Providers, Developer must configure OAuth for his app in Appmobi Management Portal. So once Providers are configured, OAuth Login buttons are rendered on User Interface.

###Secure PushMobi
----------------------

Secure PushMobi is a cross platform push messaging service for mobile applications. With a single code base you can send and receive push messages on iOS, Android, Windows8 and Windows8 Phone. Along with the 140 characters of message text, you also have the ability to send a data payload that can be accessed by your app and used to control a behavior or provide additional content.

###Secure Live Update
----------------------

Secure LiveUpdate allows you to update your app without submitting your changes to the various app stores. liveUpdate does not require that any additional code be added to your app. However, you do have the option to add liveUpdate code to give you more control regarding how and when updates are applied. When you are ready to apply a liveUpdate, you have several options on how your application handles the update.

**Components of each liveUpdate are:**

- **Message to User :** Message to display to user on update. This parameter is required.
- **Description  :** The description explaining the reason for the liveupdate.This is rendered the Live Update History This parameter is optional.

**Select one of the four behaviours when submitting your liveUpdate**

- **Option 1:** Automatically Install the Update on Next Restart
If this choice was made when the liveUpdate was sent, a pop-up message from the operating system will ask the user whether they want to update their application immediately or not. The liveUpdate message is displayed to the user in this pop-up. If the user selects “Yes”, the application will immediately restart using the updated application. If the user selects “No”, the application will instead notify the application just as if the final choice in this list had been made.
- **Option 2:** Download Update on Restart and Install on following Restart/Resume
If this choice was made when the liveUpdate was sent, a pop-up message from the operating system will notify the user about update of their application immediately. The new bundle will be downloaded and automatically.
- **Option 3:** Prompt the User and request their permission
On app start or resume, the container will be notified of the update. The new bundle will be silently downloaded in the background and will be installed on the following app start.
- **Option 4:** Notify the Application
The final option puts control of the update completely in the hands of the developer and allows them to code their application to handle the update by themselves. Once an update is available, the application will be notified either at startup through the AppMobiCloud.updateAvailable parameter or during runtime through the [updateAvailable](https://docs.appmobi.com/liveupdate/javascriptapi/updateavailable.html#luupdateavailable) event. The liveUpdate message is included as the updateMessage property in this event. Once an update has been detected, developers may choose to kick off the update or not depending on how they would like their application to behave. See the [liveUpdate Sample Application](https://docs.appmobi.com/_downloads/ImplementationGuide-LiveUpdate-1-2.zip)  for more information.

####EXAMPLE

```javascript
/* OVER THE AIR UPDATE CODE */
// This event handler captures the event thrown when an update becomes available
// while an application is running document.addEventListener("appMobi.device.update.available",onUpdateAvailable,false);
function onUpdateAvailable(evt) {
   if (evt.type == "appMobi.device.update.available") {
      // There is an update available *while* the application is running - just warn the user
     AppMobiCloud.device.installUpdate();
   }
}
```

**NOTE :**  At the first time of liveUpdate you need to upload all files in bundle and for the next time you can do partial liveUpdate with files that has been changed.


##Secure Data Store
---------------------
SecureDataStore allows you to save your Application Data securely on device and Sync the same to the appmobiServer and also allows to share data to Application server.

###Secure Data Store Methods

####saveData

 saveData method is used to store data securely on the device and/or server. To use this functionality, user needs to enable app data security in your application security settings on the enterprise management portal.

```javascript
AppMobiCloud.secureData.saveData(key, value,isMasterData, saveToServer, isJSON);
```

**Parameters**

 - **key** : The unique identifier for a particular key which user wants to store securely onto the device and/or to server.
 - **value** : Text data which is assigned to a particular key.
 - **isMasterData**  : Pass 1 to store on device as Master Data.OR Pass 0 to store on device as Transactional Data.
 - **saveToServer** : If user wants to store data locally only then set the parameter value to 0 (false). Or if the user wants to store data to the server then set parameter value to 1 (true).
 - **isJSON** : If user wants to store complex JSON objects, then set the parameter value to 1 (true). Or if the user wants to store data as String then set parameter value to 0 (false).


**EXAMPLE**

```javascript
function saveSecureData() {
            var key = prompt("Please enter Key", "BP");
            var dta = {};
            dta.id = 1;
            dta.val = "170";
            dta.key = "BP";
            var value = prompt("Please enter value", JSON.stringify(dta));
            var isMasterData = prompt("Master Data Required: \n\n 0 for No, \n 1 for Yes", "0");
            var saveToServer = prompt("Please enter saveToServer \n\n 0 for No, \n 1 for Yes", "0");
            var isJSON = prompt("Please enter if data is in JSON format \n\n 0 for No, \n 1 for Yes", "0");			
			try{			
				if(typeof(JSON.parse(value))!='object'&&isJSON==1)		
				{
					alert("Please provide valid JSON data");
					return;
				}
			}
			catch(err){
				if(isJSON==1)
				{
					try{
						isArr = Object.prototype.toString.call(value) == '[object Array]';
						if (isArr == false)
						{
							alert("Please provide valid JSON data");
							return;
						}
					}
					catch(err)
					{
						alert("Please provide valid JSON data");
						return;
					}
				}
			}
			AppMobiCloud.secureData.saveData(key, value, isMasterData, saveToServer, isJSON);
		}

      document.addEventListener("appMobi.securedata.save", onSecureDataSave, false);

      function onSecureDataSave(data) {
            if(data.success)
              alert("key : "+data.key+"\n value : "+data.value+"\n message : "+data.message);
            else
               alert("Message : "+data.message);

        }
```

###syncData

 syncData method is used to transfer all the local data from device which is not sync to server. Once data is synced with server, incremental local data will be deleted from device. To use this functionality, user needs to enable app data security in your application security settings on the enterprise management portal.

```javascript
AppMobiCloud.secureData.syncData();
```

**EXAMPLE**
```javascript
// Call  AppMobiCloud.secureData.syncData(); api to sync data to server.
function syncSecureData(){
        AppMobiCloud.secureData.syncData();
}
function onSecureDataSave(data){
        alert(data.message);
}
document.addEventListener("appMobi.securedata.sync", onSecureDataSync, false);
```

###readData

 readData method is used to read stored data from device. To use this functionality, user needs to enable app data security in your application security settings on the enterprise management portal.

```javascript
AppMobiCloud.secureData.readData(key,isMasterData);
```

**Parameters**

 - **key** : The identifier for a particular key which user wants to read the secure data from device.
 - **isMasterData**  : Pass 1 if you want to read data from Master data otherwise pass 0 if you want to read data which is not synced with server yet.

**EXAMPLE**

```javascript
var myKey = “BP”;
        var isMasterData = 0;
        readSecureData(myKey,isMasterData);

        function readSecureData(key,isMasterData){
            AppMobiCloud.secureData.readData(key,isMasterData);
        }

        function onSecureDataRead(data) {
            if (data.success) {
                try {
                    var json = JSON.stringify(data.value);
                    var mySecureList = JSON.parse(json);
                    if (typeof mySecureList == "object"&&(mySecureList.length)) {
                        for (var local_data in mySecureList){
						if(typeof mySecureList[local_data] === 'object')
						       AppMobiCloud.notification.alert( data.key + " : " + JSON.stringify(mySecureList[local_data]), "SecureData", "OK");
                            else
							AppMobiCloud.notification.alert(data.key + " : " + mySecureList[local_data], "SecureData", "OK");

                        }
                    }
                    else
                        AppMobiCloud.notification.alert("No data available with specified key", "SecureData", "OK");
                } catch (e) {
                    AppMobiCloud.notification.alert("Caught Exception For: " + e.message);
                }

            }
            else
                alert(data.message);
        }

        document.addEventListener("appMobi.securedata.read", onSecureDataRead, false);

```

##Secure Analytics
--------------------

Secure analytics delivers real-time intelligence from a fully scalable, secure, and is tested for optimal enterprise us, helping developers know what they’re protecting while they’re protecting it.

##Development Guide
---------------------

New to mobile development and looking for a place to start? Our Quickstart guide for Development will guide you step-by-step from setting up your development environment, managing services and installing all the necessary components of the Cordova development environment.

###QuickStart Guide for Android Development
 - [Enabling Google Services](https://docs.appmobi.com/guides/quickstart-android/index.html#enabling-google-services)
 - [Installing the Android SDK & Cordova](https://docs.appmobi.com/guides/quickstart-android/index.html#installing-the-android-sdk-cordova)
 - [Setup your Appmobi App](https://docs.appmobi.com/guides/quickstart-android/index.html#setup-your-privatestack-app)
 - [Creating an App in Android Studio](https://docs.appmobi.com/guides/quickstart-android/index.html#creating-an-app-in-android-studio)

###Quickstart Guide for iOS Development
-  [Creating a new App on your Appmobi Stack](https://docs.appmobi.com/guides/quickstart-ios/index.html#creating-a-new-app-on-private-stack)
-  [Creating a new iOS App on Cordova using CLI v5.0.0](https://docs.appmobi.com/guides/quickstart-ios/index.html#creating-a-new-ios-app-on-cordova-using-cli-v5-0-0)
-  [Creating a new iOS App on Apple Developer Site](https://docs.appmobi.com/guides/quickstart-ios/index.html#creating-a-new-ios-app-on-apple-developer-site)
-  [Generating Push SSL certificate](https://docs.appmobi.com/guides/quickstart-ios/index.html#generating-push-ssl-certificate)
-  [Generating Provisioning Profiles](https://docs.appmobi.com/guides/quickstart-ios/index.html#generating-provisioning-profiles)

###Quickstart Guide for OAuth Integration
 - [Google OAuth Integration](https://docs.appmobi.com/guides/quickstart-oauth/index.html#google-oauth-integration)
 - [Facebook OAuth Integration](https://docs.appmobi.com/guides/quickstart-oauth/index.html#facebook-oauth-integration)

###Plugin Variables
----------
Our plugin makes use of Cordova plugin variables to communicate with the Appmobi backend.  When installing the plugin you will need to provide 3 parameters:

- **APP_NAME**: The name of the application created on your Appmobi Management Portal.
- **PROJECT_ID**: The unique application indentifier of your Appmobi application.
- **CONFIG_URL**: The HTTP endpoint of your Appmobi Backend (ie. https://cloud.appmobi.com/ for our public cloud, https://127.0.0.1 for an Appmobi PrivateStack )


###Push Methods
-------

####getNotificationsList

 Use this method to get a list of id keys to obtain access to the list of available notifications for this user.
```javascript
var notificationArray = AppMobiCloud.notification.getNotificationsList();
```

**EXAMPLE**

```javascript
var myNotifications = AppMobiCloud.notification.getNotificationsList();
         var len = myNotifications.length;
         if (len > 0) {
             for (i = 0; i < len; i++) {
                 msgObj = AppMobiCloud.notification.getNotificationData(myNotifications[i]);
                 try {
                     if (typeof msgObj == "object" && msgObj.id == myNotifications[i]) {
                         var data = "";
                         if(msgObj.data)
                             data = msgObj.data;
                         AppMobiCloud.notification.alert(msgObj.msg + "\n" + data, "Push Message", "OK");
                         AppMobiCloud.notification.deletePushNotifications(msgObj.id);
                         return;
                     }
                     AppMobiCloud.notification.alert("Invalid Message Object: " + i);
                 } catch (e) {
                     AppMobiCloud.notification.alert("Caught Exception For: " + e.message);
                     //Always mark the messages as read and delete them.
                     //If you dont, your users will get them over and over again.
                     AppMobiCloud.notification.deletePushNotifications(msgObj.id);
                 }
             }
         }
```

####getNotificationData

 Use this method to get any data associated with a notification.
```javascript
var messageObject = AppMobiCloud.notification.getNotificationData(id);
```

**Parameter**

**id :** The id parameter of the message object you would like to get the information from.

**EXAMPLE**

```javascript
var  myNotifications= AppMobiCloud.notification.getNotificationList();
var len=myNotifications.length;
if(len > 0) {
   var strMessages="";
   for(i=0;i< len;i++) {   msgObj= AppMobiCloud.notification.getNotificationData(myNotifications[i]);
      try {
      if(typeof msgObj=="object" && msgObj.id==myNotifications[i]) {
           strMessages+=unescape(msgObj.msg)+"<br>\n";
           clearList.push(msgObj.id);
         }
      } catch(e) {
         alert("Invalid message object");
      }
   }
   alert(strMessages);
   }
```

####readPushNotifications

 Use this method to update notifications status on the server as read by user.
```javascript
AppMobiCloud.notification.readPushNotifications(notificationIDs);
```

**Parameters**

**notificationIDs :** A pipe (“|”) delimited list of notification ids to mark as read and remove from the system. The event object includes a “success” property that is set to true or false. This event will additionally include a “message” property describing the response from server.

**EXAMPLE**
```javascript
AppMobiCloud.notification.readPushNotifications = function(notificationIDs) {
 if( notificationIDs == undefined || notificationIDs == "")
 {
 throw(new Error("Error: AppMobiCloud.notification.readPushNotifications, No notificationIDs specified."));
 }
 exec(null, null, "AppMobiCloud", "readPushNotifications", [notificationIDs]);
 ```

 **appMobi.notification.push.enable**

 This event is fired once a user’s credentials have been confirmed by the application and push notifications are enabled.

**appMobi.notification.push.receive**

This event is fired once the application has gotten a push notification.

 **appMobi.notification.push.disable**

 This event is fired once the user is signed out of the pushMobi messaging system.

 **appMobi.notification.push.delete**

 This event is fired once a push notification is removed from the messaging system.

 **appMobi.notification.push.send**

 This event is fired once a push notification is sent from an applicat

 **appMobi.notification.push.refresh**

 This event is fired once the notification system refreshes the data on an application.

 **appMobi.notification.push.user.editattributes**

 This event is fired once further demographic information is associated with a user.


###User Methods
-----------

####addPushUser

 Use this method to register a new user on a particular appMobi application.

```javascript
AppMobiCloud.notification.addPushUser(userID,password,email);
```

**Parameters**

 - **userID** : A unique string (per appMobi application) for this user to be addressable in the push system. The user id may not contain spaces or periods.
 - **password**  : The user’s chosen password for the push system. The password may not contain spaces or periods.
 -  **email**  : The email address that the [sendPushUserPass](https://docs.appmobi.com/pushmessaging/javascriptapi/sendpushuserpass.html#pmjsmsendpushuserpass) command will use to notify users about their userID and password information.

**EXAMPLE**

```javascript
/* This code runs when user want to be registered */
function addPushUser(){
             var user = prompt("Please enter username", "testUser");
             var pwd = prompt("Please enter password", "password");
             var email = prompt("Please enter email", "abc@appmobi.com");
             AppMobiCloud.notification.addPushUser(user,pwd,email);
         }
```

####editPushUser

 Use this method to change the email address and the password associated with the push notification of an appMobi application.

```javascript
AppMobiCloud.notification.editPushUser(newEmail,newPassword);
```

**Parameters :**

 - **newEmail** : The new email address that the sendPushUserPass command will use to notify users about their userID and password information.
 - **newPassword**  : The user’s chosen password for the push system. The password must not contain spaces or periods.

 **EXAMPLE**
 ```javascript
document.addEventListener("appMobi.notification.push.user.edit",pushMobi.onPushNotificationEvent,false);
 onPushNotificationEvent: function (data) {
          if (data.success == false) {
              alert("error: " + data.message)
          } else {
              alert("success with message : " + data.message);
          }
      }
function editPushUser(){
              var email = prompt("Please enter email", "testUser@appmobi.com");
              var pwd = prompt("Please enter password", "password");
              AppMobiCloud.notification.editPushUser(email,pwd);
          }
```

####findPushUser

 Use this method to allow users to find users of an appMobi application. It provides a kind of “friends” functionality.

```javascript
AppMobiCloud.notification.findPushUser(userID,emailAddress);
```

**Parameters :**

 - **userID** : A unique user id to look for in the messaging database of the application.
 - **emailAddress**  : An email address to look for in the messaging database of the application.

 **EXAMPLE :**
```javascript
function findPushUserByUsername(){
        var user = prompt(“Please enter username”, “testUser”); AppMobiCloud.notification.findPushUserByUsername(user);
    }
    function findPushUserByEmail(){
            var email = prompt(“Please enter email”, “abc@appmobi.com”); AppMobiCloud.notification.findPushUserByEmail(email);
        }
        document.addEventListener(“appMobi.notification.push.user.find”,updateNotificationEvent,false);
        var updateNotificationEvent=function(event) {
    if(event.success==false) {
        alert(“error: ” + event.message)
    } else {
        alert(“success”);
    }
}
```

**appMobi.notification.push.user.edit**

 This event is fired once a user changes their email address or password in the notification system.

 **appMobi.notification.push.user.find**

 This event is fired following a request by an application to find other users of the application.

**appMobi.notification.push.sendpassword**

 This event is fired once a request is made by a user to have their notifications password emailed to them.



##References
----------
 -  [Appmobi Official Website](https://www.appmobi.com/)
 -  [Appmobi Documentation](https://docs.appmobi.com/)
 -  [Apache Cordova](https://cordova.apache.org/)

##Supported Platforms
----------
- Android
- iOS (For Intel XDK the plugin will not work for iOS as it has dependency on cordova-ios v4.0.0 which has not been released yet.)

##Sample Application
----------
Check out our [Appmobi Sample Cordova Application Template](https://github.com/appMobiGithub/sample-appmobi-privatestack) for a quickstart on getting to know the funtionality of the Appmobi platform.  We provide working examples of using many of the different features Appmobi provides which you can either use as a learning tool or a fresh application base.
