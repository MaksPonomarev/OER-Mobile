# УФ4. Декларация приложения \(app manifest\)

### Add upward navigation <a id="Up"></a>

Each screen in your app that's not the main entry point, which are all the screens that aren't the home screen, must provide navigation that directs the user to the logical parent screen in the app's hierarchy. To do this, add an **Up** button in the [app bar](https://developer.android.com/training/appbar).

To add an **Up** button, you need to declare which activity is the logical parent in the [`AndroidManifest.xml`](https://developer.android.com/guide/topics/manifest/manifest-intro) file. Open the file at **app &gt; manifests &gt; AndroidManifest.xml**, locate the `<activity>` tag for `DisplayMessageActivity`, and replace it with the following:

```text
<activity android:name=".DisplayMessageActivity"
          android:parentActivityName=".MainActivity">
    <!-- The meta-data tag is required if you support API level 15 and lower -->
    <meta-data
        android:name="android.support.PARENT_ACTIVITY"
        android:value=".MainActivity" />
</activity>
```

The Android system now automatically adds the **Up** button to the app bar.

### Run the app <a id="run"></a>

Click **Apply Changes** ![](https://developer.android.com/studio/images/buttons/toolbar-apply-changes.svg) in the toolbar to run the app. When it opens, type a message in the text field and tap **Send** to see the message appear in the second activity.![App opened, with text entered on the left screen and displayed on the right.](https://developer.android.com/training/basics/firstapp/images/screenshot-activity2.png)**Figure 2.** App opened, with text entered on the left screen and displayed on the right.

That's it, you've built your first Android app!

To continue to learn the basics about Android app development, go back to [Build your first app](https://developer.android.com/training/basics/firstapp) and follow the other links provided there.

