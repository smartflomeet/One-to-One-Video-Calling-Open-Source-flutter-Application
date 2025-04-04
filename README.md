# 1-to-1 RTC: A Sample Flutter mobile App with SmartFloMeet Flutter Toolkit

This is a Sample Flutter mobile App demonstrates the use of [SmartFloMeet platform Server APIs](https://doc.smartflomeet.ttns.in/developer/video-api/server-api/) and Flutter SDK Toolkit to build 1-to-1 RTC (Real-Time Communication) Application. It allows developers to ramp up on app development by hosting on their own devices.

This App creates a virtual Room on the fly hosted on the SmartFloMeet platform using REST calls and uses the Room credentials (i.e. Room Id) to connect to the virtual Room as a mobile client. The same Room credentials can be shared with others to join the same virtual Room to carry out an RTC session.

NOTE: Supported languages: Web and mobile

> SmartFloMeet Developer Center: https://doc.smartflomeet.ttns.in/developer/

## 1. Getting Started

### 1.1 Prerequisites


#### 1.1.2 Sample Flutter Client

- [Clone or download this Repository](https://github.com/smartflomeet/One-to-One-Video-Calling-Open-Source-flutter-Application)

#### 1.1.3 Test Application Server

You need to set up an Application Server to provision Web Service API for your Flutter Application to enable Video Session.


Our Application Server restricts a single Session Durations to 10 minutes, and allows 1 moderator and not more than 3 participants in a Session.

Once you tried SmartFloMeet Flutter SDK Sample Application, you may need to set up your own Application Server and verify your Application to work with your Application Server. Refer to point 2 for more details on this.

#### 1.1.4 Configure Flutter Client

- Open the App
- Go to Main.dart and change the following:

```
 /* To try the App with SmartFloMeet Flutter web/mobile Hosted Service you need to set the kTry = true When you setup your own Application Service, set kTry = false */

     public  static  final  boolean kTry = true;

 /* Your Web Service Host URL. Keet the defined host when kTry = true */

     String kBaseURL = "https://demo.smartflomeet.ttns.in/"

 /* Your Application Credential required to try with SmartFloMeet Hosted Service
     When you setup your own Application Service, remove these */

     String kAppId = "App_Id"
     String kAppkey = "App_Key"

```

### 1.2 Test

#### 1.2.1 Open the App

- Open the App in your Device. You get a form to enter Credentials i.e. Name & Room Id.
- You need to create a Room by clicking the "Create Room" button.
- Once the Room Id is created, you can use it and share with others to connect to the Virtual Room to carry out an RTC Session.

Note:- In case of emulator/simulator your local stream will not create. It will create only on real device.

## 2. Set up Your Own Application Server

You may need to set up your own Application Server after you tried the Sample Application with SmartFloMeet hosted Server. We have different variants of Application Server Sample Code. Pick the one in your preferred language and follow instructions given in respective README.md file.

* NodeJS: [https://github.com/smartflomeet/Video-Conferencing-Open-Source-Web-Application-Sample.git]
* PHP: [https://github.com/smartflomeet/Group-Video-Call-Conferencing-Sample-Application-in-PHP]

Note the following:

* You need to use App ID and App Key to run this Service.
* Your Flutter web Client EndPoint needs to connect to this Service to create Virtual Room and Create Token to join the session.
* Application Server is created using SmartFloMeet Server API, a Rest API Service helps in provisioning, session access and post-session reporting.


## 3. Flutter Toolkit

Flutter Sample App to use Flutter SDK Toolkit to communicate with SmartFloMeet Servers to initiate and manage Real-Time Communications.

- Documentation: https://doc.smartflomeet.ttns.in//developer/video-api/client-api/flutter-toolkit/
- Download: https://doc.smartflomeet.ttns.in//developer/video-api/client-api/flutter-toolkit/

## 4. Application Walk-through

### 4.1 Create Token

We create a Token for a Room Id to get connected to SmartFloMeet Platform to connect to the Virtual Room to carry out a RTC Session.

To create Token, we make use of Server API. Refer following documentation:
https://doc.smartflomeet.ttns.in/developer/video-api/server-api/rooms-route/#create-a-room

### 4.2 Connect to a Room, Initiate & Publish Stream

We use the Token to get connected to the Virtual Room. Once connected, we initiate local stream and publish into the room. Refer following documentation for this process:
https://doc.smartflomeet.ttns.in/developer/video-api/server-api/

### 4.3 Play Stream

We play the Stream into EnxPlayerWidget Object. You can pass local true for local Stream player, and local false for remote stream Players.
Add import for EnxPlayerWideget

```
import 'package:enx_flutter_plugin/enx_player_widget.dart';

EnxPlayerWidget(0, local: true)
```

### 4.4 Handle Server Events

SmartFloMeet Platform will emit back many events related to the ongoing RTC Session as and when they occur implicitly or explicitly as a result of user interaction. We use Call Back Methods to handle all such events.

Add import to handle callbacks and methods:

```

import 'package:enx_flutter_plugin/enx_flutter_plugin.dart';

/* Example of Call Back Methods */

/* Call Back Method: onRoomConnected
Handles successful connection to the Virtual Room */

EnxFlutterPlugin.onRoomConnected = (Map<dynamic, dynamic> map) {
       /* You may initiate and publish stream */
        print('onRoomConnectedFlutter' + jsonEncode(map));
    };

/* Call Back Method: onRoomError
 Error handler when room connection fails */
 EnxFlutterPlugin.onRoomError = (Map<dynamic, dynamic> map) {

    };

/* Call Back Method: onStreamAdded
 To handle any new stream added to the Virtual Room */

 EnxFlutterPlugin.onStreamAdded = (Map<dynamic, dynamic> map) {
      print('onStreamAdded' + jsonEncode(map));
       /* Subscribe Remote Stream */
}


/* Call Back Method: onActiveTalkerList
 To handle any time Active Talker list is updated */

 EnxFlutterPlugin.onActiveTalkerList = (Map<dynamic, dynamic> map) {
     /* Handle Stream Players */
}
```



