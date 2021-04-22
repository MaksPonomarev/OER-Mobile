# УФ3. Intent

### Создание Intent

Intent переводится как намерение. Intent является объектом, который позволяет взаимодействовать различным компонентам как внутри одного приложения, там и компонентам между приложениями. Несмотря на то, что существует много способов использования Intent выделяют 3 ключевых способа:

* Запуск Активити;
* Запуска сервиса;
* Доставка трансляции.

Существует два вида намерений:

*  **Explicit intents** \(явное намерение\) - в данном намерении указывается конкретный компонент, который мы хоти вызвать, будь то Activity, Service или Broadcast. Обычно такие намерения используются с компонентами вашего собственного приложения, потому что вы точно знаете какое Активити или сервис вы хотите запустить. Например, запустить Активити для вывода текста или запустить сервис, который будет скачивать файл.
*  **Implicit intents** \(скрытое намерение\) - в данном намерении не указывается конкретный компонент, который вы хотите использовать, но указывается действие, которое вы хотите сделать и выбирается приложение, которому вы хотите поручить это действие. Например, если вы хотите показать место на карте пользователю приложения, то вы можете выбрать соответствующее приложение, которое может быть установлено на устройстве пользователя.  Android самостоятельно подбирает подходящие для этой задачи приложения. В настройках вашего приложения можно задать фильтры по которым будет производится поиск.

### Запуск Активити

Создадим Intent для нашего приложения, которое будет передавать текст из `MainActivity` в `MessegeActivity`. Для этого мы будем использовать следующий код

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

### Контроль



