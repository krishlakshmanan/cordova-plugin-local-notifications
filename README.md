Cordova LocalNotification-Plugin
==================================

A bunch of local notification plugins for Cordova 3.x.x

by Sebastián Katzer ([github.com/katzer](https://github.com/katzer))

## Supported Platforms
- **iOS**<br>
See [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/WhatAreRemoteNotif.html) for detailed informations and screenshots.

- **Android**<br>
See [Notification Guide](http://developer.android.com/guide/topics/ui/notifiers/notifications.html) for detailed informations and screenshots.

## Adding the Plugin to your project
Through the [Command-line Interface](http://cordova.apache.org/docs/en/3.0.0/guide_cli_index.md.html#The%20Command-line%20Interface):
```
cordova plugin add https://github.com/katzer/cordova-plugin-local-notifications.git
```

## Removing the Plugin from your project
Through the [Command-line Interface](http://cordova.apache.org/docs/en/3.0.0/guide_cli_index.md.html#The%20Command-line%20Interface):
```
cordova plugin rm de.appplant.cordova.plugin.local-notifications
```

## Release Notes
#### Version 0.4.0 (not yet released)
- Added Android support<br>
  *Based on the LocalNotifications Android plugin made by* ***Daniël (dvtoever)***

#### Version 0.2.0 (11.08.2013)
- Added iOS support<br>
  *Based on the LocalNotifications iOS plugin made by* ***Rodrigo Moyle***

## Using the plugin
The plugin creates the object ```window.plugin.notification.local``` with the following methods:

### add()
The method allows to add a custom notification. It takes an hash as an argument to specify the notification's properties. All properties are optional. If no date object is given, the notification will popup immediately.
```javascript
window.plugin.notification.local.add({
    date: date, // this expects a date object
    message: message, // the message that is displayed
    repeat: repeat, // has the options of daily', 'weekly',''monthly','yearly')
    badge: badge, // displays number badge to notification
    foreground: forground, // a javascript function to be called if the app is running
    background: background, // a javascript function to be called if the app is in the background
    sound: sound // (only iOS) a sound to be played, the sound must be located in your project's resources and must be a caf file
});
```
**Android:** The `message` property can be devided into *title* and *subtitle* section:
```javascript
message: "Title\r\nSubtitle comes after linebreak"
```

### cancel()
The method cancels a notification which was previously added. It takes the ID of the notification as an argument.
```javascript
window.plugin.notification.local.cancel(__id__);
```

### cancelAll()
The method cancels all notifications which were previously added by the application.
```javascript
window.plugin.notification.local.cancelAll();
```

## Example
```javascript
var now                  = new Date().getTime(),
    _60_seconds_from_now = new Date(now + 60*1000);

window.plugin.notification.local.add({
    date:       _60_seconds_from_now,
    message:    'Hello world!',
    repeat:     'weekly', // will fire every week on this day
    foreground: 'foreground',
    background: 'background'
});

function foreground (id) {
    console.log('I WAS RUNNING ID='+id)
}

function background (id) {
    console.log('I WAS IN THE BACKGROUND ID='+id)
}
```
