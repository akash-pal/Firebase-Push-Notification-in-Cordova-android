# Firebase-Push-Notification-in-Cordova-
Firebase Push Notification in Cordova 


Cordova Firebase Push Notification Plugin

https://www.npmjs.com/package/cordova-plugin-fcm

For obtaining the access token:

        FCMPlugin.getToken(
          function(token){
            alert(token);
          },
          function(err){
            console.log('error retrieving token: ' + err);
          }
        );
        
Callback for receiving push notification:

        FCMPlugin.onNotification(
          function(data){
            if(data.wasTapped){
              //Notification was received on device tray and tapped by the user.
              alert( JSON.stringify(data) );
            }else{
              //Notification was received in foreground. Maybe the user needs to be notified.
              alert( JSON.stringify(data) );
            }
          },
          function(msg){
            console.log('onNotification callback successfully registered: ' + msg);
          },
          function(err){
            console.log('Error registering onNotification callback: ' + err);
          }
        );
        
  Place the get access token and callback for receiving push notification inside index.js file within receivedEvent function
  
  Sending Push Notification via REST API
  
        //POST: https://fcm.googleapis.com/fcm/send 
        //HEADER: Content-Type: application/json 
        //HEADER: Authorization: key=AIzaSyAMMh0mdVIRXPcBejyatAtdZgmklepwoNs //key is server-key
        {
          "notification":{
            "title":"Notification title",  //Any value 
            "body":"Notification body",  //Any value 
            "sound":"default", //If you want notification sound 
            "click_action":"FCM_PLUGIN_ACTIVITY",  //Must be present for Android 
            "icon":"fcm_push_icon"  //White icon Android resource
          },
          "data":{
            "param1":"value1", /Any data to be retrieved in the notification callback 
            "param2":"value2"
          },
            "to":"eRImo7algBM:APA91bHSxSOdmgsOi9su_XytEtCbei0Zi0ODgm76VHvbqeb-WPoZcLyNVpnaLWPLw7U1u93hO0ZhtBxn_hVGxPAwxXXfc-yNy6_kkfzUdTpcI2QPB0vzJBmOFzX3RRZ15wmFkCUFtyhc", //Topic or single device 
            "priority":"high", //If not set, notification won't be delivered on completely closed iOS app
            "restricted_package_name":"com.zensar.fcm" //Optional. Set for application filtering 
        }
        
  Configure the above REST API using Postman rest client.
  
How it works
Send a push notification to a single device or topic.

1.a Application is in foreground:
The user receives the notification data in the JavaScript callback without notification alert message (this is the normal behaviour of mobile push notifications).

1.b Application is in background:
The user receives the notification message in its device notification bar.
The user taps the notification and the application is opened.
The user receives the notification data in the JavaScript callback'.
  
  
