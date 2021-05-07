# УФ5. Использование ресурсов

Ресурсом в приложении Android являюся изображения, макеты, шрифты, стили и т.д. В рамках данного модуля будут рассмотрен ресурс строк.

На примере проекта, созданного в "Модуль 2. Компоненты приложения" мы можем увидеть следующие ресурсы. Все ресурсы находятся в папке /res проекта.

![&#x420;&#x438;&#x441;. 1. &#x420;&#x435;&#x441;&#x443;&#x440;&#x441;&#x44B; &#x43F;&#x440;&#x43E;&#x435;&#x43A;&#x442;&#x430;](../../.gitbook/assets/image%20%2826%29.png)

Обращение к ресурам из кода происходит через класс R и ссылкой на нужный ресурс. Например:

```java
setContentView(R.layout.activity_main);
```

В данном коде устанавливается интерфейс Activity. Для этого через класс R мы обращаемся к папке layout и выбираем макет activity\_main.

## Строки

Одним из важнейших ресурсов являются строки. Они используются для названия приложения, текста кнопок и т.д.

Файл строк находится в папке `res/values/strings.xml`.

Строка создается следующим образом:

1. Пишется тег `<string`.
2. Вводится имя строки через `name=" "`.
3. Открывающий тег закрывается `>`, вводится содержание строки.
4. Вводится закрывающий тег `</string>`.

Ниже можно увидеть пример строки, в которой написано имя приложения.

```markup
<string name="app_name">View and ViewGroup</string>
```

До сих пор мы задавали значение объектов интерфейса напрямую через атрибут text, однако как-правило значением атрибута text является строки. Вот несколько правил при оформлении строк:

* разделяте комментриями строки, которые относятся к разным экранам;
* не используйте одни и те же строки повторно.

![&#x420;&#x438;&#x441;. 2. &#x41E;&#x431;&#x44A;&#x44F;&#x432;&#x43B;&#x435;&#x43D;&#x438;&#x435; &#x441;&#x442;&#x440;&#x43E;&#x43A;](../../.gitbook/assets/image%20%2824%29.png)

Для того, чтобы присваивать атрибуту `text` или `hint` значение откройте xml-код макета и присвойте параметру `text` или `hint` значение `"@string/<имя_строки>"`. В коже ниже пример присваивание атрибуту hint значения строки.

```markup
android:hint="@string/hint"
```

## Цвета

Также как и со строками можно назначать цвета. В файле `res/values/colors.xml` назначаются цвета.

```markup
<?xml version="1.0" encoding="utf-8"?>
<resources>

    <color name="colorBackgroundContainer">@color/colorMoonYellow</color>

    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>

    <color name="colorTransparent">#FFFFFFFF</color>
    <color name="colorBlack">#FF000000</color>
    <color name="colorWhite">#FFFFFFFF</color>

    <color name="colorMyGray">#444444</color>
    <color name="colorLightGray">#D6D7D7</color>
    <color name="colorMyRed">#E54304</color>
    <color name="colorMyGreen">#12C700</color>
    <color name="colorMyBlue">#425A73</color>
    <color name="colorMyYellow">#FFC107</color>
    <color name="colorMoonYellow">#FDF8DF</color>

</resources>
```

По умолчанию уже определены некоторые цвета в файле.

Назначаются цвета соответсвующему атрибуту также, как и строки, разница лишь в том, что идет обращение к `@color`, а не к `@string`.

```markup
android:textColor="@color/colorBlack"
```

## Контроль

