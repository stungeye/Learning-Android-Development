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

**2018-01-08** - Created [my first Android project](https://github.com/StungEye-RRC/First-Android-App) ([following this tutorial](https://developer.android.com/training/basics/firstapp/index.html)) and configured Android Studio. This included setting up the emulator and associated Android SDK, as well as configuring the IDE to work with git and my Github account. I'm able to build the project and view the "Hello World" app in the emulator. I can also perform git commits and push to a Github repo (this one). Continuing with the tutorial I added a textbox and button to the UI using the Blueprint UI design view. The tutorial drifted a bit from what I was seeing in the editor here, but I was able to make things work. My initial thoughts on the UI editor is that looks very complicated but powerful. Next step for this tutorial is to open a new activity when the button I just added is clicked.

**2018-01-09** - I finished the "Your First App" tutorial after adding a second activity to the app. Somethings I learned today:

* An [Activity](https://developer.android.com/guide/components/activities/index.html) is a single focused thing that a user can do. They are most often paired with a view. When an activity is triggered it's `onCreate` method is called. It's in this `onCreate` method that we load the associated view using `setContentView` which takes a resource ID. `onCreate` is but one method in the collection of [Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle.html) callback methods. 
* The activities that make up an application are declared within the project manifest (`app\manifests\AndroidManifest.xml`). The activities in these manifest are linked to Java classes by way of the `android:name` element attribute. 
* We send data between Activities using [Intents](https://developer.android.com/guide/components/intents-filters.html). An Intent can be used to start an activity within your app or to launch an acitivity in another app.
* There is a class called `R` that we use to locate views (`R.layout.<layout_name>`) and ui items (`R.id.<ui_item_name>`) within views. The `R` stands for [Resource](https://developer.android.com/guide/topics/resources/index.html).
* XML is everywhere. We don't always have to edit it directly, but we can. We use it for saving UI strings (`app\res\values\strings.xml` edited through the Translations Editor), for our activity views (edited more easily using the Blueprint design view), and for our overall app manifest (`app\manifests\AndroidManifest.xml`). 
* Source code isn't king. We don't always turn to our source to add functionality. For example we set `onClick` handlers with the UI design tool (or the associated XML) and we define parent views (allowing for automatic addition of nav bar back buttons) in the manifest XML.
* To create a method that can be bound to an `onClick` event the method must be in the associated `Activity` class, it must be `public`, it must have a return type of `void`, and it must take a single parameter of type `View`.
* If at first Android Studio doesn't recognize a class we ALT-ENTER and import it. From Jody: Turning on "auto import" in Android Studio settings can be very handy. To do so, go to File - Settings - Editor - Auto Import and select "Optimize imports on the fly" as well as "Add unambiguous imports on the fly"
 
I also bought the book [The Busy Coder's Guide to Android Development](https://commonsware.com/Android/). Yes, even with all the free online resources out there I'm still a sucker for a well researched book.

**2018-01-17** - Spent some time looking over Jody's Demo App that he provides for assignment two. There were a few things that I didn't understand, so I sent him the following questions:

*	What’s the difference (or downside/benefit) of implementing something like an on click handler in code (using `setOnClickListen`) versus from a layout onClick property? The demo appears to include code for both, although the onClick layout callback called `startOtherActivity` didn’t seem to be wired up. \[Answer: The only event handler available from the layout tool is onClick, all other handlers need to be set in code.\]
*	What’s the purpose of the `SharedPreference` code in the Main Activity? Or is there no real purpose beyond a quick demo of saving data to a `SharedPreference` and then immediately retrieving it?  \[Answer: This was for demo purposes only. `SharePreference` is a simple key/value store for app settings.\]
*	Your code includes a comment asking why we don’t have to cast view widgets retrieved my `findViewById`. Why is that? \[Answer: Android now uses a newer version of Java that support type inference this method.\]
* Also, while I was researching `findViewById` I came across this blog post: [Say goodbye to findViewById. Say hello to Data Binding Library](https://inthecheesefactory.com/blog/say-goodbye-to-findviewbyid-with-data-binding-library/en) which introduces an interesting alternative to `findViewById` for accessing view widgets.

**2018-01-23** - Almost done assignment three which focuses on [layouts](https://developer.android.com/guide/topics/ui/declaring-layout.html#CommonLayouts). [My repo can be found here](https://github.com/StungEye-RRC/Android-Layout-Practice). Thoughts and questions:

* The linear layout is by far the easiest to work with. I still haven't groked the chains and springs in the constraint layout.
* I tried to build a nested layout (a horizontal linear layout within a vertical linear layout) but I couldn't seem to access the UI elements within the nested layout using `findViewById`. I tried to find the nested layout first and then use that to find the elements, but that didn't work either. The following doesn't error in any way, but I can't set an `onClick` on `showStaticHTMLButton`:

      setContentView(R.layout.activity_with_web_view); 
      LinearLayout ll = findViewById(R.id.webviewButtons); // This layout is nested within the inflated content view.
      showStaticHTMLButton = ll.findViewById(R.id.staticHTMLButton); // This button is nested in the linear layout ll.
  
  \[Answer: No need to find the buttons in a nested way. The problem wasn't actually the buttons anyway, it was the layout. The nested linear layout had a height of `match_parent` which meant it was covering the WebView.\]

* When firing off a `Toast` within an anonymous click handler the first argument to `Toast.makeText` is the current context. I tried `this` but that didn't work, instead I had to do `ActivityWithRelativeLayout.this` where `ActivityWithRelativeLayout` is the Activity class within which the anonymous click handler was defined. I haven't used `this` in Java before as a property of a class. What's up with this? \[Answer: This is how you get to the `this` of the enclosing object of the specified class.\]
* Working with WebViews is pretty slick. Next up I'm going to try to load the HTML and an image from a resource folder.

**2018-01-24** - Continuing my work on [assignment three, layouts](https://github.com/StungEye-RRC/Android-Layout-Practice). 

* Items for spinners can be stored in resource XML files as `item` elements with a `string-array` element with a `name` attribute. [See xml](https://github.com/StungEye-RRC/Android-Layout-Practice/blob/master/app/src/main/res/values/planet_spinner.xml) and associated [code](https://github.com/StungEye-RRC/Android-Layout-Practice/blob/master/app/src/main/java/com/stungeye/assignmentthree_ui/ActivityWithRelativeLayout2.java#L33).
* When a user selects an item from a spinner the returned value of `spinner.getItemAtPosition(pos)` within the `onItemSelected` handler is the type of data that was loaded into the spinner in the first place. In this case I loaded Strings, so I can retrieve the data like: `String selectedPlanet = (String)spinner.getItemAtPosition(pos);`
* Note to self: Don't forget to chain `show()` on to `Toast.makeText` calls. :)
* I'm finding [programcreek.com](https://www.programcreek.com/) and [stacktips.com/topics/tutorials/android](http://stacktips.com/topics/tutorials/android) helpful for finding snippets of example code for parts of the Android API that I can't make sense of from the developer docs. Using a google site search works nicely here. For example: [site:https://www.programcreek.com android alertdialog](https://www.google.com/search?q=site%3Ahttps%3A%2F%2Fwww.programcreek.com+android+alertdialog)
