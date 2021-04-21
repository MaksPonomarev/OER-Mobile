# УФ3. Программирование

В предыдущем фрагменте был создан простой пользовательский интерфейс с текстовым блоком для ввода данных и кнопкой для отправки введенных данных. В данном фрагменте вы научитесь добавлять обработчики элементов, добавлять для них функциональность.

### Функция "Отправить сообщение"

1. В файле **app &gt; java &gt; com.example.myfirstapp &gt; MainActivity**, создайте функцию `sendMessage()`

{% tabs %}
{% tab title="First Tab" %}
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }

    /** Функция вызывается, когда пользователь жмет на кнопку */
    fun sendMessage(view: View) {
        // Сделать что-то
    }
}
```
{% endtab %}

{% tab title="Second Tab" %}
```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    /** Функция вызывается, когда пользователь жмет на кнопку */
    public void sendMessage(View view) {
        // Сделать что-то
    }
}
```
{% endtab %}
{% endtabs %}

Возможно вы увидите ошибку, потому что Androd Studio не может понять, что такое класс View, который используется как аргумент функции. Для того, чтобы исправить ошибку, кликните 

You might see an error because Android Studio cannot resolve the `View` class used as the method argument. To clear the error, click the `View` declaration, place your cursor on it, and then press Alt+Enter, or Option+Enter on a Mac, to perform a Quick Fix. If a menu appears, select **Import class**.

1. Return to the **activity\_main.xml** file to call the method from the button:

   1. Select the button in the Layout Editor.
   2. In the **Attributes** window, locate the **onClick** property and select **sendMessage \[MainActivity\]** from its drop-down list.

   Now when the button is tapped, the system calls the `sendMessage()` method.

   Take note of the details in this method. They're required for the system to recognize the method as compatible with the [`android:onClick`](https://developer.android.com/reference/android/view/View#attr_android:onClick) attribute. Specifically, the method has the following characteristics:

   * Public access.
   * A void or, in Kotlin, an implicit [unit](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html) return value.
   * A [`View`](https://developer.android.com/reference/android/view/View) as the only parameter. This is the [`View`](https://developer.android.com/reference/android/view/View) object you clicked at the end of Step 1.

2. Next, fill in this method to read the contents of the text field and deliver that text to another activity.

### Build an intent <a id="BuildIntent"></a>

An [`Intent`](https://developer.android.com/reference/android/content/Intent) is an object that provides runtime binding between separate components, such as two activities. The [`Intent`](https://developer.android.com/reference/android/content/Intent) represents an app’s intent to do something. You can use intents for a wide variety of tasks, but in this lesson, your intent starts another activity.

In `MainActivity`, add the `EXTRA_MESSAGE` constant and the `sendMessage()` code, as shown:[KOTLIN](https://developer.android.com/training/basics/firstapp/starting-activity#kotlin)[JAVA](https://developer.android.com/training/basics/firstapp/starting-activity#java)

```kotlin
const val EXTRA_MESSAGE = "com.example.myfirstapp.MESSAGE"

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }

    /** Called when the user taps the Send button */
    fun sendMessage(view: View) {
        val editText = findViewById<EditText>(R.id.editText)
        val message = editText.text.toString()
        val intent = Intent(this, DisplayMessageActivity::class.java).apply {
            putExtra(EXTRA_MESSAGE, message)
        }
        startActivity(intent)
    }
}
```

Expect Android Studio to encounter **Cannot resolve symbol** errors again. To clear the errors, press Alt+Enter, or Option+Return on a Mac. Your should end up with the following imports:[KOTLIN](https://developer.android.com/training/basics/firstapp/starting-activity#kotlin)[JAVA](https://developer.android.com/training/basics/firstapp/starting-activity#java)

```text
import androidx.appcompat.app.AppCompatActivity
import android.content.Intent
import android.os.Bundle
import android.view.View
import android.widget.EditText
```

An error still remains for `DisplayMessageActivity`, but that's okay. You fix it in the next section.

Here's what's going on in `sendMessage()`:

* The [`Intent`](https://developer.android.com/reference/android/content/Intent) constructor takes two parameters, a [`Context`](https://developer.android.com/reference/android/content/Context) and a [`Class`](https://developer.android.com/reference/java/lang/Class).

  The [`Context`](https://developer.android.com/reference/android/content/Context) parameter is used first because the [`Activity`](https://developer.android.com/reference/android/app/Activity) class is a subclass of [`Context`](https://developer.android.com/reference/android/content/Context).

  The [`Class`](https://developer.android.com/reference/java/lang/Class) parameter of the app component, to which the system delivers the [`Intent`](https://developer.android.com/reference/android/content/Intent)`,` is, in this case, the activity to start.

* The [`putExtra()`](https://developer.android.com/reference/android/content/Intent#putExtra%28java.lang.String,%20java.lang.String%29) method adds the value of `EditText` to the intent. An `Intent` can carry data types as key-value pairs called _extras_.

  Your key is a public constant `EXTRA_MESSAGE` because the next activity uses the key to retrieve the text value. It's a good practice to define keys for intent extras with your app's package name as a prefix. This ensures that the keys are unique, in case your app interacts with other apps.

* The [`startActivity()`](https://developer.android.com/reference/android/app/Activity#startActivity%28android.content.Intent%29) method starts an instance of the `DisplayMessageActivity` that's specified by the [`Intent`](https://developer.android.com/reference/android/content/Intent). Next, you need to create that class.

**Note:** The Navigation Architecture Component allows you to use the Navigation Editor to associate one activity with another. Once the relationship is made, you can use the API to start the second activity when the user triggers the associated action, such as when the user clicks a button. To learn more, see [Navigation](https://developer.android.com/topic/libraries/architecture/navigation).

### Create the second activity <a id="CreateActivity"></a>

To create the second activity, follow these steps:

1. In the **Project** window, right-click the **app** folder and select **New &gt; Activity &gt; Empty Activity**.
2. In the **Configure Activity** window, enter "DisplayMessageActivity" for **Activity Name**. Leave all other properties set to their defaults and click **Finish**.

Android Studio automatically does three things:

* Creates the `DisplayMessageActivity` file.
* Creates the layout file `activity_display_message.xml`, which corresponds with the `DisplayMessageActivity` file.
* Adds the required [`<activity>`](https://developer.android.com/guide/topics/manifest/activity-element) element in `AndroidManifest.xml`.

If you run the app and tap the button on the first activity, the second activity starts but is empty. This is because the second activity uses the empty layout provided by the template.

### Add a text view <a id="TextView"></a>

![The text view centered at the top of the layout.](https://developer.android.com/training/basics/firstapp/images/constraint-textview_2x.png)**Figure 1.** The text view centered at the top of the layout.

The new activity includes a blank layout file. Follow these steps to add a text view to where the message appears:

1. Open the file **app &gt; res &gt; layout &gt; activity\_display\_message.xml**.
2. Click **Enable Autoconnection to Parent** ![](https://developer.android.com/studio/images/buttons/layout-editor-autoconnect-on.png) in the toolbar. This enables Autoconnect. See figure 1.
3. In the **Palette** panel, click **Text**, drag a **TextView** into the layout, and drop it near the top-center of the layout so that it snaps to the vertical line that appears. Autoconnect adds left and right constraints in order to place the view in the horizontal center.
4. Create one more constraint from the top of the text view to the top of the layout, so that it appears as shown in figure 1.

Optionally, you can make some adjustments to the text style if you expand **textAppearance** in the **Common Attributes** panel of the **Attributes** window, and change attributes such as **textSize** and **textColor**.

### Display the message <a id="DisplayMessage"></a>

In this step, you modify the second activity to display the message that was passed by the first activity.

1. In `DisplayMessageActivity`, add the following code to the `onCreate()` method:[KOTLIN](https://developer.android.com/training/basics/firstapp/starting-activity#kotlin)[JAVA](https://developer.android.com/training/basics/firstapp/starting-activity#java)

   ```text
   override fun onCreate(savedInstanceState: Bundle?) {
       super.onCreate(savedInstanceState)
       setContentView(R.layout.activity_display_message)
    
       // Get the Intent that started this activity and extract the string
       val message = intent.getStringExtra(EXTRA_MESSAGE)

       // Capture the layout's TextView and set the string as its text
       val textView = findViewById<TextView>(R.id.textView).apply {
           text = message
       }
   }
   ```

2. Press Alt+Enter, or Option+Return on a Mac, to import these other needed classes:[KOTLIN](https://developer.android.com/training/basics/firstapp/starting-activity#kotlin)[JAVA](https://developer.android.com/training/basics/firstapp/starting-activity#java)

   ```text
   import androidx.appcompat.app.AppCompatActivity
   import android.content.Intent
   import android.os.Bundle
   import android.widget.TextView
   ```

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

