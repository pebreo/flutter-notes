
INSTALLATION (Mac)
-----
* Install Flutter SDK
```
  $ cd ~/development
  $ unzip ~/Downloads/flutter_macos_v0.2.3-beta.zip
  $ export PATH=`pwd`/flutter/bin:$PATH  # better yet, add to your .zshrc
  $ flutter doctor
```
* Install Android studio

* AVD Manager
```
Android Studio>Tools>Android>AVD Manager ; Run
$ flutter run

open -a Simulator.app
```

* VS Code config
```
View -> Command Palette
install
dart code
Reload VS Code

View -> Command Palette
doctor
Select: Flutter: Run Flutter Doctor
```

* Install Dart for commandline (Mac)
```
brew tap dart-lang/dart
brew install dart
dart myprogr.dart
```

## First app 
```
View -> Command Pallette
type: flutter
```

## Upgrading Flutter SDK and VSC extensions
```
$ flutter upgrade
```

## Update flutter packages
```
$ flutter packages get
```

## Firebase
```
console.firebase.google.com


Goto app->src->main->java->com->MainActivity.java
com.yourcompany.friendlychat

Download the google services.jsons

Goto to google-services.json:
  googleAppID: ->  "mobilesdk_app_id":
  apiKey ->  "current_key"
  databaseURL -> "firebase_url"

Goto your app then Database then turn on Real Time Database
```

## Resources

flutterexamples.com

https://flutter.io/get-started/editor/#vscode


https://flutter.io/setup-macos/

https://developer.android.com/studio/install.html