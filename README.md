Control-Robot-Movement-with-Spacebrew
=====================================
This Repo is for the code required to control simple movement of a dual- continuous motion servo motor propelled robot.
It will create Forward, Backward, Left, Right, and Stop buttons, with a toggle-background function to indicate that your mousepresses have been detected. 

In it are the files required for Spacebrew, Processing, and Arduino.

This repo contains the Spacebrew Library for Javascript along with documentation and code for the button press app. This library was designed to work on front-end (browser) environments, and back-end (server) environments. Below is a brief overview about Spacbrew, followed by a short tutorial on how to use this library.

Current Version: 1.2.0
Latest Update: April 20, 2013
Main Contributors: Brett Renfer, Eric Eckhard-Ishii, Julio Terra

About Spacebrew
Spacebrew is an open, dynamically re-routable software toolkit for choreographing interactive spaces. Or, in other words, a simple way to connect interactive things to one another. Every element you hook up to the system can subscribe to, and publish data feeds. Each data feed has a data type. There are three different data types supported by Spacebrew: boolean (true/false), number range (0-1023) or string (text). Once elements are set up, you can use a web based visual switchboard to connect or disconnect publishers and subscribers to each other.

Learn more about Spacebrew here.

Using Javascript Library
Before you get started you need to download the spacebrew library, and add it to your project's directory so that you can import it into your web app's code. To download the latest version of the library just click the "ZIP" button above.

1. Import javascript library into your project

Import the javascript library into your project using a script tag in the appropriate html page. We usually include the page's javascript code in a separate file as well. This file should be imported after the library.

<script src="path/sb-1.2.0.js"></script>
<script src="path/your_scripts.js"></script>

2. Create a Spacebrew object

In your_scripts.js file, the first thing you need to do is create new instance of a Spacebrew Client object using the Spacebrew.Client constructor and assign it to a variable or object attribute.

var sb = new Spacebrew.Client( server, name, description, options );
Constructor Parameters The constructor parameters, server, name, description, and options are all optional. The options parameter supports two options: port, an integer that specifies the port number of the spacebrew server, debug, a boolean value that turns on console messages when set to true, and reconnect, a boolean variable that turns off automatic reconnect when set to false. When running in a browser, the Spacebrew Client library will look for the server hostname, app name, app description, and server port setting in the query string; using server, name, description, port as keys.

If server is not specified in the query string or constructor, then the app will attempt to connect to a Spacebrew server hosted locally. The name will default to the app's full URL, if no name is provided via the query string or constructor. The description will remain blank if no description is specified. If you want to connect to the cloud server just point spacebrew to sandbox.spacebrew.cc.

3. Configure Base Name and Description Feeds

You can also set the base app name and description using the Spacebrew.Client library's name() and description() methods. The app's name and description must be set before the Spacebrew connection is established.

sb.name("myApp")
sb.description("this is a spacebrew app.")

4. Configure Data Subscription and Publication Feeds

The next step is adding the subscription and publication data feeds. Each one needs to be labelled and assigned an appropriate data type - "string", "range", "boolean" (custom data types are also supported, the names for these data types are arbitrary, as long as the publisher and subscriber feature the same name). You can also optionally define a default value for any publication feed.

sb.addPublish( name, type, default );
sb.addSubscribe( name, type );

5. Define lifecycle and message event handler methods

Spacebrew offers lifecycle event hooks for connection open and close events - onOpen, and onClose; and for incoming message events of each data type - onStringMessage, onRangeMessage, of onBooleanMessage. You need to define the message handler methods in order to capture data from your subcriptions data feeds.

sb.onStringMessage = function onString( name, value );
sb.onRangeMessage = function onRange( name, value );
sb.onBooleanMessage = function onBoolean( name, value );
sb.onCustomMessage = function onBoolean( name, value, type );
sb.onOpen = function onOpen();
sb.onClose = function onClose();

6. Connect to Spacebrew

Now that you have configured the Spacebrew object it is time to connect to the Spacebrew server.

sb.connect();

7. Send messages

The send method enables you to publish messages via one of the publication data feeds. It accepts three mandatory parameters, a channel name, a data type, and a value. The value needs to correspond to the data type, otherwise the message will be ignored by the server.

sb.send( name, type, value )
Javascript Library Examples
Here is a list of the core examples that are included in this repo. These examples were designed to help you get started building web apps that connect to other applications, objects and spaces via Spacebrew.

The Button (Boolean Example) is a web app with a button that publishes a boolean value every time the button is clicked. It also subscribes to boolean messages, which change the web app's background color.


Using Spacebrew Admin Library
You can also integrate admin functionality directly into yor spacebrew client applications using the Spacebrew admin library along with the standard javascript library. Please note that this library is still in early development phases, which means that it will change and evolve a lot over the coming months. we will document the process for adding admin functionality into your client apps in the coming weeks.



