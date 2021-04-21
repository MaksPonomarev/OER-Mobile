# УФ3. Программирование

В предыдущем фрагменте был создан простой пользовательский интерфейс с текстовым блоком для ввода данных и кнопкой для отправки введенных данных. В данном фрагменте вы научитесь добавлять обработчики элементов, добавлять для них функциональность.

### Функция "Отправить сообщение"

1. В файле **app &gt; java &gt; com.example.myfirstapp &gt; MainActivity**, создайте функцию `sendMessage()`

{% tabs %}
{% tab title="Kotlin" %}
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

{% tab title="Java" %}
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

Возможно вы увидите ошибку, потому что Androd Studio не может понять, что такое класс `View`, который используется как аргумент функции. Для того, чтобы исправить ошибку, кликните по `View` и и нажмите сочетание клавиш Alt+Enter - вам будут предложены пути исправления ошибки. Выберите первый вариант **Import.** Таким образом вы импортируете класс View.

1. Вернитесь к файлу **activity\_main.xml** для вызова метода, нажатием на кнопку:

   1. Выберите кнопку в редакторе.
   2. В окне **Attributes**, найдите атрибут **onClick** и выберите **sendMessage \[MainActivity\]** из выпадающего списка.

   Теперь при нажатии на кнопку, система вызовет метод `sendMessage()`.

   Мы смогли привязать наш метод к атрибуту **onClick** потому, что он обладал следующими свойствами:

   * публичный модификатор.
   * используется метод, или в случае с Kotlin функция, которая возвращает значение с типом Unit.
   * Единственным аргументом является `View` - тот `View`, которому вы назначили выполнение данного метода.

2. Далее напишем код, чтобы наше приложение могло прочитать содержание текстового блока и передать это содержание другому `Activity`.

### Создание Intent <a id="BuildIntent"></a>

`Intent` переводится как **намерение,** в данном случае намерение передать данные между двумя `Activity`. Намерения используются для большого количества задач.

В `MainActivity`, в самом верху кода, перед объявлением класс добавьте константу`EXTRA_MESSAGE` и код для функции `sendMessage()`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
const val EXTRA_MESSAGE = "com.example.myfirstapp.MESSAGE"

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }

    /** Функция вызывается, когда пользователь жмет на кнопку */
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
{% endtab %}

{% tab title="Java" %}
```java
public class MainActivity extends AppCompatActivity {
    public static final String EXTRA_MESSAGE = "com.example.myfirstapp.MESSAGE";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    /** CФункция вызывается, когда пользователь жмет на кнопку */
    public void sendMessage(View view) {
        Intent intent = new Intent(this, DisplayMessageActivity.class);
        EditText editText = (EditText) findViewById(R.id.editText);
        String message = editText.getText().toString();
        intent.putExtra(EXTRA_MESSAGE, message);
        startActivity(intent);
    }
}
```
{% endtab %}
{% endtabs %}

Скорее всего Android Studio покажет очень много ошибок, для их используйте сочетание клавиш Alt+Enter. У вас должны быть представлены следующие импорты.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
import androidx.appcompat.app.AppCompatActivity
import android.content.Intent
import android.os.Bundle
import android.view.View
import android.widget.EditText
```
{% endtab %}

{% tab title="Java" %}
```java
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
```
{% endtab %}
{% endtabs %}

У нас все еще остается ошибка для `DisplayMessageActivity`, но её мы исправим позже.

Написанный код в функции  `sendMessage()` означает следующее:

* Переменная `intent` объявлена как переменная с типом `Intent`, который обязательно принимает два значения `Context` и `Class`.

  Параметр `Context` используется первым и имеет значение `this` . Параметр имеет такое значение, потому что класс `Activity` является подклассом класс `Context`, а значит мы ссылаемся на `MainActivity` как на `Context`.

  Параметр `Class` означает класс, на который нацелено намерение.

* Метод `putExtra()` добавляет значение текстового блока `EditText` к намерению. `Intent` может передавать значения в виде "ключ-значение", такие пары называют _extras_.

  Ключом является публичная константа `EXTRA_MESSAGE`. Хорошей практикой является определение ключей _extras_ для намерений таки образом - это обеспечивает уникальность ключа в случае, если ваше приложение взаимодействует с другими приложениями.

* Метод `startActivity()` запускает экземпляр класса `DisplayMessageActivity` который указан в переменной `intent`. Далее мы создадим этот класс

### Создание второго Activity <a id="CreateActivity"></a>

Для создания второго Activity:

1. В окне **Project**, сделайте клик правой кнопкой мыши по папке **app** и выберите **New &gt; Activity &gt; Empty Activity**.
2. В окне настройки Activity \(**Configure Activity** \), введите "DisplayMessageActivity" для параметра **Activity Name**. Оставьте другие параметры по-умолчанию и кликните **Finish**.

Android Studio автоматически сделает три вещи:

* Создаст файл `DisplayMessageActivity`.
* Создаст файл макета `activity_display_message.xml`, который связан с файлом `DisplayMessageActivity`.
* Добавит необходимый элемент `<activity>` в `AndroidManifest.xml`.

Если вы запустите приложение, то при нажатии на кнопку вы перейдете на другое Активити. Однако дополним приложение таким образом, чтобы при вводе текста и нажатии на кнопку текст выводился во втором окне.

### Верстка второго Activity <a id="TextView"></a>

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

