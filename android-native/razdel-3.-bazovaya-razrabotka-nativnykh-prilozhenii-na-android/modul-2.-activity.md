# УФ 1. Activity

## Activity

Активити является входной точкой для взаимодействия с пользователем. Она представляет собой один экран с пользовательским интерфейсом. Например, email приложение может иметь одну активити, которая показывает список новых email, другое активити составляет email, и третье активити читает email. Несмотря на то , что Активити работают вместе для создания более полного пользовательского опыта в email приложении, каждое Активити независимо друг от друга. Поэтому другое приложение может запустить одно из этих Активити, если приложение электронных писем позволяет это. Например, приложение для управления камерой может запустить Активити email приложения, которое будет содержать новый email, чтобы позволить пользователю поделиться изображением. Активити облегчают следующие ключевые взаимодействия между системой и приложением:

* Отслеживать приложения, которые видны на экране для того, чтобы гарантировать, что система не выключит процесс, который запускает Активити.
* Ранее запускаемые процессы могут содержать вещи, к которым пользователь может вернуться \(остановленные Активити\), поэтому система держит данные процессы в приоритете.
* Помогает приложению обрабатывать завершение процесса таким образом, что пользователь может вернуться к действиям с восстановленным предыдущим состоянием.
* Предоставление приложениям возможности встроить пользовательские запросы между собой и системе контролировать данные запросы \(типичный пример - функция "поделиться"\).

При создании приложения с пустым `Activity` \(`Empty Activity`\) у нас создается один экран со строкой "Hello, World!". Данный экран состоит из двух частей - файл макета activity\_main.xml и MainActivity.

![&#x420;&#x438;&#x441;.1. &#x42D;&#x43A;&#x440;&#x430;&#x43D; &#x43F;&#x43E;-&#x443;&#x43C;&#x43E;&#x43B;&#x447;&#x430;&#x43D;&#x438;&#x44E;](../../.gitbook/assets/image%20%2815%29.png)

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
package com.android.myfirstapp;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```
{% endtab %}
{% endtabs %}

Данный файл называется `Main Activity` - с него начинается работа Android-приложения. Как мы сказали выше, любой экран Android-приложения описывается при помощи Activity и подобного кода. Рассмотрим, что означает каждая строчка приложения.

`package com.example.myfirstapp` означает имя пакета класса `MainActivity`.

Код ниже выполняет импорт классов из других пакетов, функциональность которых использует класс `MainActivity`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
```
{% endtab %}

{% tab title="Java" %}
```java
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
```
{% endtab %}
{% endtabs %}

Определение класса осуществляется следующим образом. Класс MainActivity наследуется от класса AppCompatActivity, выше мы импортировали этот класс, который представляет собой отдельный экран и класс MainActivity наследует весь функционал.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class MainActivity : AppCompatActivity() {
```
{% endtab %}

{% tab title="Java" %}
```java
public class MainActivity extends AppCompatActivity {
```
{% endtab %}
{% endtabs %}

По умолчанию класс MainActivity имеет один метод onCreate, в котором создается весь пользовательский интерфейс при помощи метода `setContentView(R.layout.activity_main)`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
}
```
{% endtab %}

{% tab title="Java" %}
```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
}
```
{% endtab %}
{% endtabs %}

Метод `setContentView(R.layout.activity_main)` отвечает за решение "Какую разметку пользовательского интерфейса использовать?". Разметка передается в виде аргумента `R.layout.activity_main`.

* класс `R` - это динамически генерируемый класс во время создания приложения, который идентифицирует все используемые в проекте ресурсы \(макеты, строки, изображения и т.д.\).
* `layout` - означает конкретную категорию, в которой нужно искать ресурс. В данной случае идет поиск в категории макетов.
* `activity_main` - имя используемого макета. Для каждого Activity автоматически создается макет с расширением XML. На примере данного макета вы рассматривали графический редактор.

В рамках данного модуля мы создадим приложение, которое будет передавать сообщение с одной Activity на другую. Так как основы пользовательского интерфейса будут разбираться в следующем модуле, вставьте код ниже в файл `activity_main.xml`. Результат должен быть как на рис. 2.

```markup
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/editText"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="16dp"
        android:hint="Введите текст"
        app:layout_constraintRight_toLeftOf="@+id/button"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintTop_toTopOf="parent"  />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="16dp"
        android:layout_marginStart="16dp"
        android:text="Отправить"
        android:onClick="sendMessage"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintLeft_toRightOf="@+id/editText" />


</androidx.constraintlayout.widget.ConstraintLayout>
```

![&#x420;&#x438;&#x441;. 2 &#x418;&#x43D;&#x442;&#x435;&#x440;&#x444;&#x435;&#x439;&#x441; MainActivity](../../.gitbook/assets/image%20%2817%29.png)

Таким образом, мы создали `Activity`, на котором будет вводится текст и по нажатию на кнопку отправляться на второе `Activity`. Пока не обращайте внимание на подсвечиваемым красным текст `sendMessage`. Данный текст принадлежит свойству `onClick` кнопки. Данное свойство означает, что по нажатию на кнопку будет вызываться функция `sendMessage`, которую мы объявим позже.

## Контроль

{% embed url="https://learningapps.org/display?v=pi5u94iha21" %}



