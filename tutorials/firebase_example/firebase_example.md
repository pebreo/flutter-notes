
# Understanding the `firebase_core` example

In this tutorial we will go through the example
app in the `firebase_core` plugin.
You can find the example (here)[https://github.com/flutter/plugins/tree/master/packages/firebase_core/example].

The example app shows a button and displays the number
of times that button is pressed. As the button
is pressed, the app records two things
into a Firebase database:

1. The number of times the button is pressed. In the database we are storing an integer
2. A message based on the number of times the button is pressed. In the database we are storing a string.

## Create Firebase database

Before we run the program we should setup our development
environment. We need to make sure to sign up to
firebase by going to https://firebase.google.com/ and 
click Get Started. Follow the instructions to creating a account. Once you created an account, we need to make a database.

To create a database click 'Add Project.' then 
you need to add an app. In our case, we will click
"Add Firebase to your Android app".

Now goto your `lib/android/app/src/main/java/com/example/appname/MainActivity.java` and copy the string 
next to the `package` declaration. For example
`package com.example.firebaseexample;`

The `com.example.firebaseexample` is the text we will
paste in the firebase "Android package name".

Leave the other fields as-is then click 'Register App'.

In the next screen, you should choose to download 
`google-services.json` and paste that into the
`lib/android/app` directory.

Now you'll want to configure your gradle files.
Change the `build.gradle`

##### `android/build.gradle`


##### `android/app/build.gradle`

## Setup

There are three steps involved in using the Firebase API. 
The first step is 

In short, the steps are:
1. 
2.
3.


## DB transactions for the counter


## DB transactions for the message




Sources
---------

https://raw.githubusercontent.com/flutter/plugins/master/packages/firebase_database/example/lib/main.dart