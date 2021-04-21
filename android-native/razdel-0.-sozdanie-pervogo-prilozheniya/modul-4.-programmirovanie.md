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

* в переменной `editMessage` вызываем функцию `findViewById` с аргументов R.id.editText. У каждого объекта `View` есть уникальный ID, мы используем функцию `findViewById` чтобы найти необходимый элемент через класс `R`, в котором хранятся эти значения.
* в переменной message хранится значение текстового блока, которое мы конвертировали в строку при помощи функции `toString()`.
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

Задание: сделайте текстовый блок на втором макете как на скриншоте ниже. Тактовый блок должен иметь constraints справа, слева и сверху, находится в верхней части экрана.

![The text view centered at the top of the layout.](https://developer.android.com/training/basics/firstapp/images/constraint-textview_2x.png)

### Показать сообщение <a id="DisplayMessage"></a>

В этом шаге мы модифицируем второе Activity таким образом, что будет .

1. В `DisplayMessageActivity`, добавьте следующий код в метод `onCreate()`

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
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
{% endtab %}

{% tab title="Java" %}
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_display_message);
    
    // Get the Intent that started this activity and extract the string
    Intent intent = getIntent();
    String message = intent.getStringExtra(MainActivity.EXTRA_MESSAGE);

    // Capture the layout's TextView and set the string as its text
    TextView textView = findViewById(R.id.textView);
    textView.setText(message);
}
```
{% endtab %}
{% endtabs %}

2. Кликните Alt+Enter, для того, чтобы импортировать необходимые классы и убрать ошибки.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
import androidx.appcompat.app.AppCompatActivity
import android.content.Intent
import android.os.Bundle
import android.widget.TextView
```
{% endtab %}

{% tab title="Java" %}
```java
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.widget.TextView;
```
{% endtab %}
{% endtabs %}

Добавленный код означает следующее:

1. Переменная `message` принимает сообщение, которое было отправлено намерением в прошлом `Activity`.
2. В переменной `textView` - была найдено по ID текстовый блок и в него записано значение переменной `message`

###  <a id="Up"></a>

