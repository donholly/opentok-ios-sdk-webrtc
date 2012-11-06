OpenTok WebRTC for iOS SDK
==========================

This package contains what you need to get you started using the OpenTok WebRTC for iOS SDK.

The OpenTok WebRTC for iOS SDK lets you use OpenTok video sessions in apps you build for iPad, iPhone, and iPod touch devices.
This means you can use OpenTok video sessions that connect iOS users with each other and with web clients that use the OpenTok
WebRTC library for web, available at [OpenTok labs](http://labs.opentok.com).

Using the OpenTok WebRTC for iOS SDK
------------------------------------

The OpenTok WebRTC for iOS SDK is available at the [webrtc branch](https://github.com/opentok/opentok-ios-sdk/tree/webrtc) of
the opentok-ios-sdk project at github.

Documentation for the OpenTok iOS SDK is available here:

<http://www.tokbox.com/opentok/ios/docs/index.html>

The most important difference in using the OpenTok WebRTC for iOS SDK (compared with the non-WebRTC version of the
OpenTok iOS SDK) is that you must use an OpenTok session that supports peer-to-peer streaming. For example, in the
[OpenTok Session and Token Generator page](http://www.tokbox.com/opentok/api/tools/generator),
select "Peer-to-Peer Enabled" as an Advanced Option when creating a session. You must also specify
when generating a session using the
[OpenTok server-side libraries](http://www.tokbox.com/opentok/api/tools/documentation/api/server_side_libraries.html).
(Use the OpenTok Session and Token Generator page for test apps only.)

If you use a session that does not support peer-to-peer streaming, calling `[OTSession connectWithApiKey:token:]`
results in the `[OTSessionDelegate session:didFailWithError:]` message. The error message is defined by the
`OTP2PSessionRequired` enum in the OTError.h file.

If a session already has two connected clients, calling `[OTSession connectWithApiKey:token:]`
results in the `[OTSessionDelegate session:didFailWithError:]` message. The error message is defined by the
`OTP2PSessionMaxParticipants` enum in the OTError.h file.

You cannot subscribe to a stream published by your own app. If you call `[OTSubscriber initWithStream:delegate:]`
passing in a stream you publish, the OTSubscriberDelegate sends the `[OTSubscriberDelegate subscriber:didFailWithError:]`
message. The error message is defined by the `OTSelfSubscribeFailure` enum in the OTError.h file.

Supported devices
-----------------

The OpenTok WebRTC for iOS SDK is supported on the following devices:

* iPhone 4S
* iPhone 5
* iPad 2
* iPad 3

The OpenTok WebRTC for iOS SDK is supported on wifi connections.

Hello World test app
--------------------

You can test the OpenTok WebRTC for iOS SDK using the OpenTok-iOS-Hello-World sample, available at GitHub:

<https://github.com/opentok/OpenTok-iOS-Hello-World>


1. Use `git clone recursive` to obtain the OpenTok-iOS-Hello-World project.
2. In the opentok-ios-sdk subdirectory of the project, run `git pull webrtc`.
3. Generate an OpenTok session that supports peer-to-peer streaming. For example, in the
[OpenTok Session and Token Generator page](http://www.tokbox.com/opentok/api/tools/generator),
select "Peer-to-Peer Enabled" as an Advanced Option when creating a session. (You will also
need to generate a token that support publishing.)
4. Open the OpenTokHelloWorld project in XCode.
5. Remove armv7s from the Valid Architectures section of the Build Settings for your project.
6. Edit the ViewController.m file in the OpenTokHelloWorld project.

    Change the values of the `kApiKey`, `kSessionId`, and `kToken` constants to match your API key, the peer-to-peer session ID
you generated, and the token you generated.

    Change the `subscribeToSelf` variable to be set to `NO`.
7. Compile the app using the OpenTok WebRTC for iOS SDK. (Be sure that you have checked out the
[webrtc branch](https://github.com/opentok/opentok-ios-sdk/tree/webrtc) of the opentok-ios-sdk project,
so that you are compiling with the WebRTC version of the SDK.)
8. You will test the app using the browser\_demo.html file, included in the OpenTokHelloWorld project. 
Edit the browser_demo.html file:

    Edit the `apiKey`, `sessionId`, and `token` variables to use your API key, the peer-to-peer session ID you generated,
    and a generated token (for the session).

    Also load the OpenTok WebRTC library in the `script` tag:

    `<script src="http://static.opentok.com/v0.92-alpha/js/TB.min.js" type="text/javascript"></script>`
    
     (This script tag loads [the OpenTok WebRTC library for web](http://labs.opentok.com/try).)
9. Open the browser_demo.html file in a web browser and open the iOS app on a supported device.
10. You can also test the app on two iOS devices (instead of an iOS device and a web browser).

Known Issues
------------

The following features are currently unsupported in this version of the OpenTok WebRTC for iOS SDK:

* The `[OTPublisher publishAudio]` and `[OTPublisher publishVideo]` messages
* The `[OTSubscriber subscribeToAudio]` and `[OTSubscriber subscribeToVideo]` messages
* The mute button in the Publisher and Subscriber video user interface
* You cannot target the iOS Simulator. Build and deploy to a supported iOS device.
* When debugging on a device running iOS 6, there are some warnings when you rotate the device. Please ignore these.

In XCode, you need to remove armv7s from the Valid Architectures section of the Build Settings for your project.

Support
-------

Support is available at the OpenTok iOS forum: <http://www.tokbox.com/forums/ios>