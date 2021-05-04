# УФ3. Intent

### Что такое Intent?

Intent переводится как намерение. Intent является объектом, который позволяет взаимодействовать различным компонентам как внутри одного приложения, там и компонентам между приложениями. Несмотря на то, что существует много способов использования Intent выделяют 3 ключевых способа:

* Запуск Активити;
* Запуска сервиса;
* Доставка трансляции.

Существует два вида намерений:

*  **Explicit intents** \(явное намерение\) - в данном намерении указывается конкретный компонент, который мы хоти вызвать, будь то Activity, Service или Broadcast. Обычно такие намерения используются с компонентами вашего собственного приложения, потому что вы точно знаете какое Активити или сервис вы хотите запустить. Например, запустить Активити для вывода текста или запустить сервис, который будет скачивать файл.
*  **Implicit intents** \(скрытое намерение\) - в данном намерении не указывается конкретный компонент, который вы хотите использовать, но указывается действие, которое вы хотите сделать и выбирается приложение, которому вы хотите поручить это действие. Например, если вы хотите показать место на карте пользователю приложения, то вы можете выбрать соответствующее приложение, которое может быть установлено на устройстве пользователя.  Android самостоятельно подбирает подходящие для этой задачи приложения. В настройках вашего приложения можно задать фильтры по которым будет производится поиск.

### Создание Intent для MainActivity

Создадим Intent для MainActivity. Для этого перейдите в класс MainActivity.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
package com.android.academy.fundamentals

import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.widget.EditText

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
    
    // Метод обработки нажатия на кнопку
    fun sendMessage(view: View) {
        // действия, совершаемые после нажатия на кнопку
        // Создаем объект Intent для вызова новой Activity
        val intent = Intent(this, MessageActivity::class.java)
        // Получаем текстовое поле в текущей Activity
        val editText = findViewById<EditText>(R.id.editText)
        // Получае текст данного текстового поля
        val message = editText.text.toString()
        // Добавляем с помощью свойства putExtra объект - первый параметр - ключ,
        // второй параметр - значение этого объекта
        intent.putExtra("message", message)
        // запуск activity
        startActivity(intent)
    }
}
```
{% endtab %}

{% tab title="Java" %}
```java
package com.example.helloapp;
 
import androidx.appcompat.app.AppCompatActivity;
 
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
 
public class MainActivity extends AppCompatActivity {
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    // Метод обработки нажатия на кнопку
    public void sendMessage(View view) {
        // действия, совершаемые после нажатия на кнопку
        // Создаем объект Intent для вызова новой Activity
        Intent intent = new Intent(this, MessageActivity.class);
        // Получаем текстовое поле в текущей Activity
        EditText editText = (EditText) findViewById(R.id.editText);
        // Получае текст данного текстового поля
        String message = editText.getText().toString();
        // Добавляем с помощью свойства putExtra объект - первый параметр - ключ,
        // второй параметр - значение этого объекта
        intent.putExtra("message", message);
        // запуск activity
        startActivity(intent);
    }
}
```
{% endtab %}
{% endtabs %}

Разберем, что значит каждая строка функции `sendMessage`:

1. Объявление объекта Intent. Для его объявления требуется 2 параметра - Context и класс, на который будет направлено действие. Значением первого параметра является класс из которого мы начинаем Activity, второй параметр указывает на MessageActivity, в которое отправляется сообщение.
2. Нахождение объекта EditText в который был введен текст.
3. В переменную message записывается значение объекта EditText \(введенный текст\) и данное значение конвертируется в строку.
4. Создается объект с помощью свойства putExtra - первый параметр является ключом объекта, вторым параметром является значение этого объетка, которое берется из переменной message.

### Создание Intent для MessageActivity

Создадим Intent, которое будет получать текст из`MainActivity` в `MessegeActivity`. Для этого мы будем использовать следующий код

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
package com.example.myfirstapp

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        // Получаем сообщение из объекта intent
        val message = intent.getStringExtra("message")
        // Получаем TextView по его id
        val messageText = findViewById<TextView>(R.id.messagetext)
        // устанавливаем текст для TextView
        messageText.text = message
    }
}
```
{% endtab %}

{% tab title="Java" %}
```java
package com.example.helloapp;
 
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.widget.TextView;
 
public class MessageActivity extends AppCompatActivity {
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
 
        setContentView(R.layout.activity_message);
 
        // Получаем объект Intent, который запустил данную activity
        Intent intent = getIntent();
        // Получаем сообщение из объекта intent
        String message = intent.getStringExtra("message");
        // Получаем TextView по его id
        TextView messageText = (TextView) findViewById(R.id.messageText);
        // устанавливаем текст для TextView
        messageText.setText(message);
    }
}
```
{% endtab %}
{% endtabs %}

Разберем, что значат добавленные строки:

1. Объявление переменной message и присваивание значение строки, которое было отправлено при помощи свойства putExtra.
2. Нахождение объекта TextView в который будет введен текст.
3. Присваивание объекту TextView значение переменной message.

Таким образом было создано приложение, которое передает данные из одного экрана приложения в другой экран. Результат работы можно увидеть на рис. 1.

![&#x420;&#x438;&#x441;. 2. &#x413;&#x43E;&#x442;&#x43E;&#x432;&#x43E;&#x435; &#x43F;&#x440;&#x438;&#x43B;&#x43E;&#x436;&#x435;&#x43D;&#x438;&#x435; &#x438; &#x434;&#x435;&#x43C;&#x43E;&#x43D;&#x441;&#x442;&#x440;&#x430;&#x446;&#x438;&#x44F; &#x440;&#x430;&#x431;&#x43E;&#x442;&#x44B;](../../.gitbook/assets/bezymyannyi.png)

### Контроль

Ответьте на вопросы

