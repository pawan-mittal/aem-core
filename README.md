# AEM Firebase - Send WebPush

This project will help you in enabling AEM site for webpush which will require user permission to allow for Push Notifications in browser (chrome/firefox).

Quick Demo GIF - https://pawan-mittal.github.io/allassets.github.io/aem-core/firebase/aem-firebase-webpush.gif

# Setup

## 1. Setup Firebase Project
  Create [Firebase Project](https://console.firebase.google.com)

  _**Configurations**_
  * Firebase configurations
  ```
    // Initialize Firebase
    var config = {
      apiKey: "AIzaSyDwirs0hA7NMQhqohKKlOnN8qtrf-cGyVw",
      authDomain: "sample-aem-webpush-8ff66.firebaseapp.com",
      databaseURL: "https://sample-aem-webpush-8ff66.firebaseio.com",
      projectId: "sample-aem-webpush-8ff66",
      storageBucket: "sample-aem-webpush-8ff66.appspot.com",
      messagingSenderId: "459974129772"
    };
    firebase.initializeApp(config);
  ```
  * Server Key
  ```
  AAAAaxiYOGw:APA91bEoUt4NW2EcMhWMA5WJMckR9ulFNdzI-o54f4WVj2rYda217C-3MXNYJJCzA-PkVTFAcPKK5GtHesnbTXc0h-vnbt3oiLULX8RpfQcEy03YhrKAKetEAZIYnScRkWacVkmgSepg
  ```
  * Public key
  ```
  BKOau5sHZyq41UE8SXTZvJq_ntbszyBcStU3WELbiy5pEOQqbpwcdK_crfuHlOmbD347mlyKq9OmfMRRgnfHklc
  ```

## 2. Install AEM Project (Default Port 4502)

  ```
  mvn clean install -PautoInstallPackage -Daem.port=4502 -Dadobe-public
  ```

## 3. Configure AEM Page component with Firebase Webpush settings
  1. Update Firebase configurations at [webpush.html](http://localhost:4502/crx/de/index.jsp#/apps/firebase-webpush/components/structure/firebase-page/webpush.html)
     * Add _**Firebase configuration**_ generated and replace **webpush.html**_(Line 9-18)_
     * Add _**Public Key**_ generated from the console and replace at **webpush.html**_(Line 34)_
     * Add _**Server Key**_ generated from the console and replace at **webpush.html**_(Line 91)_
  2. Update _**Messaging Sender Id**_ at [firebase-messaging-sw.js](http://localhost:4502/crx/de/index.jsp#/apps/firebase-webpush/components/structure/firebase-page/firebase-messaging-sw.js)
      * Add _**messagingSenderId**_ generated and replace **firebase-messaging-sw.js**_(Line 10)_
 
 ## 4. Send Message to multiple devices
   1. Update Firebase configurations at ```http://localhost:4502/crx/de/index.jsp#/apps/firebase- webpush/components/structure/firebase-page/webpush.html```
   
  * Update topic _**firebase-webpush**_ to any value for your project **webpush.html**_(Line 87)_
  * Same topic will be used to send webpush notification
 
    _**Sample POSTMAN Request**_
    ```
    POST https://fcm.googleapis.com/fcm/send
    Headers 
         Content-Type:application/json
         Authorization: key=<SERVER-KEY>
    Body: 
    {
      "to" : "/topics/firebase-webpush",
      "priority" : "high",
      "data" : {
	  	  "notification" : {
	        "body" : "Enjoy!",
	        "title" : "Hello AEM Developers!",
	      }
      }
    }
    ```

## 4. Demo

  Watch Live Demo - https://www.youtube.com/watch?v=GCT-gL2EaMw&t=78s
  
## TroubleShoot
1. Once user allow for Notifications, client browser (Chrome/Safari) should be registered successfully, that can be verified if token is logged on browser console _(logged for debugging, ideally it should be sent to server and saved)_

![Success Token](https://pawan-mittal.github.io/allassets.github.io/aem-core/firebase/success-token.png)

2. If using Chrome browser, then and entry for AEM instance will be added under *Allow* section in setttings [Chrome Settings](chrome://settings/content/notifications), like ```http://localhost:4502``` is shown below in allow settings.

![Chrome Notification Settings](https://pawan-mittal.github.io/allassets.github.io/aem-core/firebase/aem-instance-registration.png)

3. If token is not generated and below error is shown, then first remove AEM Instance URL setting in _(shown above in STEP 2)_ and again referesh same AEM page again.

![Error Token](https://pawan-mittal.github.io/allassets.github.io/aem-core/firebase/error-token.png)

## Resources
  * https://firebase.google.com/docs/cloud-messaging/js/client
  * https://firebase.google.com/docs/cloud-messaging/js/send-multiple

# Help
This project is created using AEM Project Archetype(https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

_Side note: The profile "adobe-public" must be activated when using profiles like "autoInstallPackage" mentioned above. You can ignore if you have Included the Adobe Public Maven Repository in your maven settings_
