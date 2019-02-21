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

**2018-01-31** - Started the calculator assignment.

* You can assign the `onClick` for multiple buttons to a single method. The view passwed into the method is the button that was click you can fetch it's id using `view.getID()`.
* In previous apps I had been using startActivityForResult when I only needed to call startActivity. I only realized this now that I need to return a result from an actiity.

**2018-02-01** - Continuing the calculator assignment.

* I was missing my vim keybindings so I install the [IdeaVim plugin](https://github.com/JetBrains/ideavim). Works nicely.
* Started working with Shared Preferences which is a nice way to save app-level key/value pairs that persist across activities and the full activity life-cycle.

**2018-02-22** - Completing the calculator assignment and starting the Google Maps assignment.

* Part of the assignment asks for string values of two text edit widgets to be returned to the main activity when the user presses up/home or the HW back button. I accomplished this by opening the activity using `startActivityForResult` and implementing the `onActivityResult` callback in the main activity. In most cases with `startActivityForResult` results are returned from an activity after the user clicks a button, and then `setResult` is called from the button click callback. I had to mess around a bit to have `setResult` triggered by back and up. Back was pretty straight forward, I overrided the `onBackPressed` callback. For up I had to override `onOptionsItemSelected` and then check if it was the home button being pressed. If so I call `onBackPressed` and force an early return. [See code](https://github.com/StungEye-RRC/Android-User-Prefs-and-Activity-Results/blob/master/app/src/main/java/com/stungeye/calculator/CalendarActivity.java#L38)

* For the birthday selection I used a `DatePickerDialog` with the context activity implementing the `OnDateSet` listener. [See code](https://github.com/StungEye-RRC/Android-User-Prefs-and-Activity-Results/blob/master/app/src/main/java/com/stungeye/calculator/CalendarActivity.java#L48).

* In order to import a colour image to use as a custom google map marker I needed to use a plugin. Without the plugin, images imported using the standard asset studio get their colour stripped out. The plugin I used was the [Android Drawable Importer](http://www.javahelps.com/2015/02/android-drawable-importer.html). 

* Created an app bar using xml action menu. [See app bar code](https://github.com/stungeye/Android-Google-Maps/blob/master/app/src/main/java/com/example/mapwithmarker/MapsMarkerActivity.java#L44). [See xml menu](https://github.com/stungeye/Android-Google-Maps/blob/master/app/src/main/res/menu/actions.xml). A++++ Straight Foward! Would app bar menu again.

**2018-02-23** - Completing the Google Maps assignment. Starting the RRS assignment.

* Minor issue when implememting the "My Location Layer" on the Google Map. After enabling location permissions for the first time the "My Location" button doesn't re-centre the screen on the location. However, if you close the app and start it again the button works. Tried tracing code with the debugger put I couldn't locate the problem.

* Instead of baseing the RSS assignment off a SAX parser I wanted to use an established RSS library. Some options include [prof18/RSS-Parser](https://github.com/prof18/RSS-Parser), [crazyhitty/Rss-Manager](https://github.com/crazyhitty/Rss-Manager?utm_source=android-arsenal.com&utm_medium=referral&utm_campaign=2954) and [rometools/rome](https://github.com/rometools/rome). Rome looks like the most established library to start it can be used with the standard Java `Url` class, but for a more robust HTTP solution I'll likely add a dependency to [Ion](https://github.com/koush/ion), [OkHTTP](https://square.github.io/okhttp/) or [Volley](https://github.com/google/volley). 

* Decided to try the Rome RSS reader. It's [hosted as a Maven repo](https://mvnrepository.com/artifact/com.rometools/rome). Started a new Android project and added the following to the app `build.gradle` file in the `dependencies` block:

    `compile group: 'com.rometools', name: 'rome', version: '1.9.0'`
    
* I've got a sample app going with an Async task to load up a feed using Rome. The problem right now is that I keep getting an "unknown host" IOException thrown when a try to load *any* URL. Something to continue debugging another day!

**2018-02-26** - Continuing work on the RSS assignment

* The unknown host IOException I was getting on Friday was due to the Android emulator not being properly connected to the internet. For some reason I had to go into the emulated device settings and complete the Wifi setup process. This solved the problem with the code, but also points to the fact that I should be checking for connectivity before trying to load any URLs. 

* I've now got a si ngle RSS feed loading and I'm displaying all the feed titles within a ListView activity. The odd thing with the ListView is that it doesn't show an appbar. Turns out that in AppCompact mode I need to use a AppCompact Activity and have it load up a ListView Fragment instead. [See Related Stack Overflow Question](https://stackoverflow.com/questions/20524008/combining-listactivity-and-actionbaractivity/20528156)

**2018-02-27** - Continuing work on the RSS assignment

* The ListView Fragment worked really nicely. I also added a progress spinner when loading the feed. At first I used a `ProgressDialog` but then I realized that it's been deprecated. So now I'm just turning on the built in spinner for the listview by using `setListShow(false)`. 

* I also added a check for network connectivity:

      private boolean isNetworkConnected() {
        ConnectivityManager cm = (ConnectivityManager) this.getSystemService(Context.CONNECTIVITY_SERVICE);
        NetworkInfo activeNetwork = cm.getActiveNetworkInfo();
        return activeNetwork != null && activeNetwork.isConnected();
      }
      
* I've got the feed items loading up in a `WebView` on click. Working nicely. Now I have to work on a main list view for where the user can select amongst multiple feeds. I also want better exception handling throughout the app. A custom list item for feeds that include images might be nice too. A progress bar would be nice when loading the webview too.

**2018-02-28** - Continuing work on the RSS assignment / Winnipeg New App

* I've got the progress bar going for the webview. I'm using an indeterminant horizontal progress bar which I hide once the webview is loaded. I did this be overriding the `onPageFinished` callback of my webview's `WebViewClient`. 

* Currently I'm trying to figure out why my listview is re-created (causing the RSS feed to be refetched) after I use the up button from the webview, where it's not re-created if I use the HW back button. (The answer was to set the parent activity's `launchMode` to `singleTop` in the manifest. [Details here](https://developer.android.com/training/implementing-navigation/ancestral.html).

**2018-02-28** - Continuing work on the RSS assignment / Winnipeg News App

* Because I plan to launch this app to the app store I wanted a user friendly way to monitor my exception and app crashes. I've decided to test out [BugSnag](http://bugsnag.com) integration. Setup and integration was really simple. All caught and uncaught exceptions are now being funneled to BugSnap. I'll probably set up a Slack channel so that I can get exception notifications via Slack.

* I'm now testing for internet connectivity in multiple places. To do this I extracted my `isNetworkConnected()` into a helper class and made it a static method. In the same class I've made a static method to display a "No Internet" alert dialog.

* Work still to be done before I can release the app to the Play store:
    * Welcome message for new users. Message displayed once. (done)
    * About page with information about the app and me. (done)
    * Feedback form via embedded Google Drive Form (done)

**2018-03-13** - Continuing work on the Winnipeg News App

* I've completed all the tasks that I wanted to finish before releasing the app to the Play store. 

* I just have to figure out the processing of building a keystore signed app for Play store publication. Luckily I still have the keystore I used to sign my Cordova versions of the Winnipeg News App, otherwise I wouldn't be able to publish this as a new version of the old app.

**2018-03-15** - Releasing Winnipeg News App to Play Store

* The app has been released to the Play store with a 100% update rollout. So far it seems like the rollout is going well.

* I left the old Cordova APK in place for older phones (phones with Android < 4.1) but I might end up pulling this APK because a number of the feeds are broken. Users with the old APK on their phones will not be affected, but if pulled I won't get any new users with older phones. I'm fine with this considering that less than 2% of my current users are using Android 4.0 or lower. 

* Note to self: The font I used for the app icon is [Sonsie One](https://fonts.google.com/specimen/Sonsie+One).

* Another to self: My Winnipeg News keystore has a two passwords on it. A store pass and a key pass.

**2018-03-16** - Setting up Android Studio at Home

* I installed Android Studio and the emulator at home on my [Manjaro Linux](https://manjaro.org/) laptop. I had to do the following to get things working:

    * Install the [trizen AUR package manager](https://github.com/trizen/trizen) using a git clone:
    
          git clone https://aur.archlinux.org/trizen.git
          cd trizen/
          makepkg -si
    
    * Install Android Studio from the AUR: `trizen -S android-studio`
    
    * Install an Android Emulator by first changing the default tmp folder which was too small:
    
          mkdir /home/stungeye/tmp
          Android Studio => Help => Edit Custom VM Options
          Add to file: -Djava.io.tmpdir=/home/stungeye/tmp

    * Force the emulator to use one of the sytem libraries rather than it's own due to "[unable to load driver i965_dri.so](https://bbs.archlinux.org/viewtopic.php?id=213192)"
    
          mv Sdk/emulator/lib64/libstdc++/libstdc++.so.6 Sdk/emulator/lib64/libstdc++/libstdc++.so.6.bak
          ln -s /usr/lib64/libstdc++.so.6 Sdk/emulator/lib64/libstdc++/
          
    * I've heard that Android Studio runs better with the Oracle JDK vs the default Open JDK:
    
          trizen -s jdk
          sudo archlinux-java set java-x-jdk (Where x is the major version of the jdk you installed)

**2018-03-17** - Refining Winnipeg News App

* I want to start adding images to the news app starting with logos for the news sources. 

* To obtain the logo I'm using the [Clearbit free Logo API](https://clearbit.com/logo) and I'm storing all the Clearbit logo URLs in the same XML as the RSS feed URLs.

* To load the logo images I will be using [the Picasso library developed by Square](https://github.com/square/picasso). This library makes loading images into an `ImageView` a snap, and it also handles caching the images to memory and disk automatically.

      Picasso.get().load("http://i.imgur.com/DvpvklR.png").into(someImageView);
      
* I also need to implement a custom list view item layout (image and text) to use with my `ListView`s.

* Once I get the logos work I'll work on loading images from the RSS feeds (if provided).

**2018-03-27** - Winnipeg NEws Exceptional Exceptions 

* I paused work on the image loading to review the exceptions that are being logged by in production via Bugsnag.

* There have been 4 unhandled exceptions (which would have crashed the app) and a large number of handled exceptions (which would have resulted in a poor user experience).  I decided to sort these exceptions by the number of times they occured and try to address the top ten. Of the top ten 2 were unhandled (crashes!) and 8 were handled. 

* The two unhandled excepts were the direct result of trying to access resources before they were ready. In both cases the code was trying to access an Activity/View before it had been fully created. Life-cycle issues. In one case an early press of a menubar option would trigger a network connectivity test via a null `Activity`. In the other case an Async task was trying to update a view fragment that wasn't yet ready. Both problems were addressed with guard conditions and a bit of a rejigging of when/where code was added to the various activity lifecycles.

* Most of the handled exceptions were centred around retrieval and parsing of RSS feeds. Unkown host exceptions, connection exceptions, socket exceptions, SSL handshaking / certificate exceptions, XML and feed parsing exceptions... In most of these cases I was able to trace the problem down to captive WiFi hotspots. By this I mean Wifi hotspots where you need to login via a web browser before you can use the network. The problem with these is that you can partially connect to them (when you see a ! beside your wifi indicator). In this pre-logged-in-to-hotspot state Android's connectivity tester will show that a network is present and therefore my app will attempt to download and parse RSS feeds. Behind the scenes, however, the HTTP request to the RSS feed will be silently redirect to a wifi login screen. My app will only see an HTTP 200 OK, and either get a certificate error (if using https) or will take the login page for the RSS XML and try to parse it. Solved this problem with more robust network connectivity testing and the disabling of auto-following redirects. The downside of this is if one of the feed URLs gets changed and the news orgs puts a rediret into place. In this case the app will need to be updated with the new feed URL.

Here are the steps required to rebuild a signed version of the APK for Play store release:

* Update the `versionCode` (int) and the `versionName` (string) to the next version. These can be found in your `build.gradle` file or your manifest. For me the are in the Module level `build.gradle` file.
* Change the build variant from `debug` to `release`. I do this in a "Build Variants" window below my project navigator. This widget wasn't always there and I'm not sure how I made it appear. Perhaps it was "Build" => "Build Variants..."
* Build => Generate Signed APK.
* Ensure that the key store path points to your keystore file. Ensure you enter the correct key alias, key store password, and key password. I used the same value for both passwords. And FYI my key alias is `meowreader`. :P
* Ensure that you are using V1 and V2 Signature versions.
* Note the output path and generate the release.
* Sign-in to the Google Play Console, select the app, select "Release Management" then "App Releases" then "Manage Production".
* Click the "Create Release" button. 
* Upload APK, select which legacy APKs (if any) to retain, and write release notes.
* Review release and select percentage of devices to roll out to. (I usually just go with 100%).

**2018-04-14** - Night Mode for Winnipeg News

* Working on implementing a dark theme or a "night mode" for the Winnipeg News app using  `Theme.AppCompat.DayNight`. [Details]().

* While implementing this feature I also refactored how I was working with `SharedPreference`s and built a singleton helper class to make working with shared prefs easier. This also meant refactoring how I detect and display different welcome messages for new and upgraded users.

* Another thing I was working on was solving a few more of the exceptions I was seeing in the wild. The most interesting being `android.os.TransactionTooLargeException` which was happening when I was trying to save activity state when webviews were being paused or stopped. The only reason I had the webviews attempt to save their state (rather than say reload on orientation chanage) was for the google form I'm using for feedback. So now I only preserve state for the feedback form. A bit of a hacky solution, but it'll do. Eventually I'll change the feedback mechanism to a native android form and remove the need to preserve webview state entirely. 

**2018-04-16** - Logo Icons for News Sources

* Added icons for all news sources on the main list view. Had to create a custom list view item layout to accomodate this change, along with a custom array adaptor for the list view. I ended up implementing the ViewHolder pattern for the array adaptor. [View Holder Tutorial 1](http://lucasr.org/2012/04/05/performance-tips-for-androids-listview/). [View holder Tutorial 2](https://www.androidcode.ninja/android-viewholder-pattern-example/).

* When adding the news sources logos as images to the project I added them in various sizes to support the varying pixel densities of different Android devices. I wanted each icon to display in a 50dp (dp = device independent pixels) ImageView. Android's baseline pixel density is mdpi mode (~160dpi). Based on my research it's best to include high density versions all app images and let Android auto-scale for lower densities. I provided images for Androids xhdpi (2 times mdpi), xxhdpi (3 times mdpi) and xxxhdpi (4 times mdpi). Since I wanted the baseline imagine to be 50px, the logos I put in the `res/xhdpi` folder were 100px, the images in the `res/xxhdpi` were 150px, and 200px images in the `res/xxxhdpi` folder. I manually resized the images. I used the [Clearbit Logo API](https://clearbit.com/logo) to find the logos.



**2018-04-17** - Enabling/Disabling News Sources

* Oh boy, this was a Yak shaving session, but it turned out okay in the end. Based on user feedback I wanted a way for users to be able to select which news sources would be displayed on the home screen. I initially envisonage this "manage feeds" page as being a list view (similar to the home screen) with news logo and name, and then on the right a checkbox or toggle switch. I already had a ListFragment for the home screen that I wanted to repurpose as it already used a custom list item layout and a custom array adaptor. Here's what I did:

* I could have created my own way of handling checkable lists, but it turns out that Android already includes ui elements that implement a `Checkable` interface. When I looked at the default layout for checkable lists [android.R.layout.simple_list_item_multiple_choice](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_multiple_choice.xml) it's a single `CheckableTextView` element. My existing layout for list items on the home screen was a `LinearLayout` with an `ImageView` for the news logo and a `TextView` for the news source name. Since I wanted to leverage Android's existing support I needed to simplify my custom layout. Turns out all I needed was a `CheckableTextView` since `TextView`s already support inline images. I just had to use  `textViewElement.setCompoundDrawablesWithIntrinsicBounds()` within my custom array adapator when populating list items.

* With my checkable textview in place I needed some way to use this list view once without checkmarks for the home screen and once with checkmarks for the manage feeds screen. Luckily I implemented the list view as a `Fragment` so I figure I could just sub-class it, but it turns out that Fragment constructors must be empty! So, no overloading the constructor to pass in a boolean to control the presence of checkmarks. The best practice I turned up for handling this was to add a static "Fragment Factor" method to the Fragment class that accepted `Bundle` arguments and returned an instance of the fragment:

      public static FeedView newInstance(boolean checkmode_active) {
          FeedView fragment = new FeedView();
          final Bundle args = new Bundle(1);
          args.putBoolean(EXTRA_CHECKMODE, checkmode_active);
          fragment.setArguments(args);
          return fragment;
      }

* Within the fragments `onViewCreated` I use this boolean flag to see the `ListView`'s choice mode (`CHOICE_MODE_MULTIPLE` vs `CHOICE_MODE_NONE`). I also use the flag within the fragments `onListItemClick` callback to change the behaviour of list clicks for the home screen vs the manage feeds activity.

* Next I had to update my POJO FeedItem class that I use as the model objects for my custom array adaptor. This class holds the name, logo drawable and url for each news source item. I added a boolean `active` property as well. Now within the custom array adaptor, when populating list items, I can check the choice mode (`setCheckMarkDrawable(null)` if we are supressing checkmarks) and set the item checked based on this flag. Strangely I couldn't set the item checked directly but instead I had to go to it's parent (avaiable as the third arg `parent` in the adapators `getView`):

        ListView listView = (ListView)parent;

        if (listView.getChoiceMode() == ListView.CHOICE_MODE_NONE) {
            viewHolder.newsSourceName.setCheckMarkDrawable(null);
        } else {
            // Using setChecked on viewHolder.newsSourceName didn't work!
            listView.setItemChecked(position, feedItem.active());
        }

* Lastly I needed a way to persist these settings. I ened up using Shared Preferences. At first I tried to figure out a way to store a Map of booleans where the keys were the news source names, but Shared Preferences doesn't like storing complex data types. Then I realized that a share pref was just a map itself, so I made a standalone shared pref file (within my existing shared prefs singleton helper) to store these settings. 

**2018-04-25** - Cordova Exploration

* After spending the term exploring Native Android development I thought I'd spend a few days reaquainting myself with [Cordova hybrid development](https://cordova.apache.org/). Specifically, I plan on redeveloping [my Meow Reader app](https://play.google.com/store/apps/details?id=com.stungeye.meowreader), which pulls images from the Tumblr API.

* Started by following [the Cordova "Your First App" guide](https://cordova.apache.org/docs/en/latest/guide/cli/index.html).

* I'm using VS Code as my editor along with the "Cordova Tools" extension.

Some of the differences I've noticed since I last dabbled in Cordova development:

* The tooling is much nicer. This includes the Cordova CLI but also the above mentioned VS Code extension, which allows for in-editor debugging of the app using adb.

* WebView click delays may no longer be an issue if zooming is disable and the width is set to the device-width in the viewport meta tag. [details](https://www.sitepoint.com/5-ways-prevent-300ms-click-delay-mobile-devices/)

**2019-01-30** - One Year Later

My hard drive on my work laptop died last month. At first I thought I lost the source to the Winnipeg News App (along with the crypto signing key). Luckily I was able to recover both. I had forgotten that I had bitbucket set up as a private git remote. Yay!

Anyway, I install Android Studio to my new laptop and loaded up the project source. Android Studio prompted me to upgraded my version of gradle as well a few of my dependencies. The edits were:

* In `\gradle\wrapper\gradle-wrapper.properties` I updated the `distributionURL` to point to `gradle-4.10.1-all.zip`
* In `\build.gradle` the dependencies classpath needed to be updated to `com.android.tools.build:gradle:3.3.0`
* In `\app\build.gradle` the `compileSdkVersion` and `targetSdkVersion` got bumped from 26 to 27 (even though 28 is available... more on that later) and then in the `dependencies` the `com.android.support:appcompat` library was bumbed to `v7:27.1.1`.

I tried bumping the SDK to version 28, but there were a bunch of deprecations and breaking changes so I rolled back to 27. 

Some things to look into when I eventually move to version 28:

* Cleartext http is no longer supported by default. This is a problem since some RSS feeds and news sources still use http instead of https. 
* `ListFragment` and `getFragmentManager` have been moved to `androidx` / Jetpack support libraries.

There is also a new way to build and release apps called [Android App Bundles](https://developer.android.com/guide/app-bundle/) that I am going to look into, as well as the potential for the app to be an [Instant-Enabled App](https://developer.android.com/topic/google-play-instant/getting-started/instant-enabled-app-bundle). 

**2019-01-30** - App Bundle Internal Test Release

I setup and built an Android App Bundle for the Winnipeg News App. This meant exporing my private signing key from my keystore file and uploading it to the Play Dev Console. The Play Console will now manage APK generation for me. I just have to upload signed App Bundles.

I then set myself up as a internal tester for the app and uploaded the app bundle for an internal test track release. The hope is that it will now be automatically deployed to my phone, but not yet deployed to the rest of my users. Fingers crossed.

I also updated my use of the Bugsnag API so that when FeedException or IOException are thrown when parsing an RSS feed the feedURL is added a metadata when notifying Bugsnag:

        Bugsnag.notify(e, new Callback() {
            @Override
            public void beforeNotify(Report report) {
                report.getError().getMetaData().addToTab("user", "feedURL", feedUrl);
            }
        });
