# УФ2. Создание Activity

## Добавление новой Activity

Android-приложение состоит из множества Activity, поэтому нужно научится создавать их и связывать друг с другом.

Для того, чтобы создать `Acitivity` кликните правой кнопкой мыши по папке app и выберите  
**New-&gt;Activity-&gt;Empty Activity**.

![&#x420;&#x438;&#x441;. 1. &#x421;&#x43E;&#x437;&#x434;&#x430;&#x43D;&#x438;&#x435; &#x43D;&#x43E;&#x432;&#x43E;&#x433;&#x43E; Activity](../../.gitbook/assets/image%20%2814%29.png)

Нас будут интересовать только два параметра при настройка: **Activity Name** и **Source Language**. Предположим, мы хотим создать `Activity`, которое будет выводить сообщение, которое мы ввели в предыдущем `Activity`, поэтому дадим параметру **Activity Name** значение **MessageActivity**. Параметр **Source Language** определяет язык программирования `Activity`, рекомендуется выбрать Kotlin.

![&#x420;&#x438;&#x441;. 2. &#x421;&#x43E;&#x437;&#x434;&#x430;&#x43D;&#x438;&#x435; MessageActivity](../../.gitbook/assets/image%20%2816%29.png)

Перейдите в режим кода созданного макета для Activity и вставьте код ниже. Он добавляет на экран текстовое поле, которое будет автоматически расширяться в зависимости от переданного текста. Размер текста увеличен. Результат должен быть как на Рис. 3.

```markup
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MessageActivity">
    <TextView
        android:id="@+id/messageText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        android:textSize="18sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

![&#x420;&#x438;&#x441;.3. &#x41C;&#x430;&#x43A;&#x435;&#x442; MessageActivity](../../.gitbook/assets/image%20%2813%29.png)

