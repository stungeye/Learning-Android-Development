# Learning-Android-Development
A place to keep notes, links, code snippets, etc, while learning Android development.

## General Resources and Tutorials

* [Official Android Developer Site](https://developer.android.com/index.html) - Google's Official Developer Docs
* [Awesome Android](https://github.com/JStumpp/awesome-android) - A curated list of awesome Android packages and resources.
* [CodePath Android Cliffnotes](https://github.com/codepath/android_guides/wiki) - Crowdsourced resource for up-to-date practical Android developer guides for any topic.
* [Beginning Android Resources](https://github.com/codepath/android_guides/wiki/Beginning-Android-Resources) - Lots of "getting started" guides, tutorials and resources.

## Java Coding for Android

* [My First Android App Repo](https://github.com/StungEye-RRC/First-Android-App/tree/master) - Built by following the official ["Build Your First App"](https://developer.android.com/training/basics/firstapp/index.html) tutorial.
* [Treasure Trove of Android Code Samples](https://github.com/commonsguy/cw-omnibus/) - From the book [The Busy Coder's Guide to Android Development](https://commonsware.com/Android/).

## UI Design for Android

* [Android Studio Layout Editor Docs](https://developer.android.com/studio/write/layout-editor.html)
* [Android Layout Tutorial: Layouts and Animations](https://www.codementor.io/lintonye/android-ui-tutorial-layouts-and-animations-85jkhcblt)
* [Build a Responsive UI with ConstraintLayout](https://developer.android.com/training/constraint-layout/index.html)

## Android Studio and Emulator

* [Android Studio User Guide](https://developer.android.com/studio/intro/index.html)

## Hybrid App Development

* [My Mobile HTML5 Blog](http://mobilehtml5.stungeye.com/) - One man's quest to build mobile apps using only HTML5, CSS3, Javascript and Phonegap. ;)

# Learning Android Developer Log

**2018-01-08** - Created my first Android project ([following this tutorial](https://developer.android.com/training/basics/firstapp/index.html)) and configured Android Studio. This included setting up the emulator and associated Android SDK, as well as configuring the IDE to work with git and my Github account. I'm able to build the project and view the "Hello World" app in the emulator. I can also perform git commits and push to a Github repo (this one). Continuing with the tutorial I added a textbox and button to the UI using the Blueprint UI design view. The tutorial drifted a bit from what I was seeing in the editor here, but I was able to make things work. My initial thoughts on the UI editor is that looks very complicated but powerful. Next step for this tutorial is to open a new activity when the button I just added is clicked.

**2018-01-09** - I finished the "Your First App" tutorial after adding a second activity to the app. Somethings I learned today:

 * An [Activity](https://developer.android.com/guide/components/activities/index.html) is a single focused thing that a user can do. They are most often paired with a view. When an activity is triggered it's `onCreate` method is called. It's in this `onCreate` method that we load the associated view using `setContentView` which takes a resource ID. 
 * There is a class called `R` that we use to locate views (`R.layout.<layout_name>`) and ui items (`R.id.<ui_item_name>`) within views. 
 * XML is everywhere. We don't always have to edit it directly, but we can. We use it for saving UI strings (`app\res\values\strings.xml` edited through the Translations Editor), for our activity views (edited more easily using the Blueprint design view), and for our over all app manifest (`app\manifests\AndroidManifest.xml`). 
 * We send data between Activities using [Intents](https://developer.android.com/guide/components/intents-filters.html).
 * Source code isn't king. We don't always turn to our source to add functionality. For example we set `onClick` handlers with the UI design tool (or the associated XML) and we define parent views (allowing for automatic addition of nav bar back buttons) in the manifest XML.
 * To create a method that can be bound to an `onClick` event the method must be in the associated `Activity` class, it must be `public`, it must have a return type of `void`, and it must take a single parameter of type `View`.
 * If at first Android Studio doesn't recognize a class we ALT-ENTER and import it. From Jody: Turning on "auto import" in Android Studio settings can be very handy. To do so, go to File - Settings - Editor - Auto Import and select "Optimize imports on the fly" as well as "Add unambiguous imports on the fly"
 
I also bought the book [The Busy Coder's Guide to Android Development](https://commonsware.com/Android/). Yes, even with all the free online resources out there I'm still a sucker for a well researched book.
