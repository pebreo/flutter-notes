
# Understanding the `firebase_core` example

In this tutorial we will go through the example
app in the `firebase_core` plugin. The example
app shows a button and displays the number
of times that button is pressed. As the button
is pressed, the app records two things
into a Firebase database:

1. The number of times the button is pressed. In the database we are storing an integer
2. A message based on the number of times the button is pressed. In the database we are storing a string.

## Create Firebase database

Before we run the program we should setup our development
environment. We need to goto to 


##### `android/build.gradle`


##### `android/app/build.gradle`

## Setup


## DB transactions for the counter


## DB transactions for the message




Sources
---------

https://raw.githubusercontent.com/flutter/plugins/master/packages/firebase_database/example/lib/main.dart