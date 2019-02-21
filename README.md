# AEM Firebase - Send WebPush

This project will help you in enabling AEM site for webpush which will require user permission to allow for Push Notifications in browser (chrome/firefox).

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

## 4. Demo

Watch Live Demo 

# Help
This project is created using AEM Project Archetype(https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

_Side note: The profile "adobe-public" must be activated when using profiles like "autoInstallPackage" mentioned above. You can ignore if you have Included the Adobe Public Maven Repository in your maven settings_
