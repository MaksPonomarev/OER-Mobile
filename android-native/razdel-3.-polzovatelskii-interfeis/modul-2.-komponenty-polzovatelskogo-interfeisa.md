# УФ4. Компоненты пользовательского интерфейса

Существует 3 основных объекта, которые используются для создания пользовательского интерфейса:

* `TextView` - простое текстовое поле, куда обычно выводят информацию;
* `EditText` - поле ввода информации;
* `Button` - кнопка, по нажатию на которую введённая информация выводится в текстовое поле.

Важно помнить, что данные компоненты наследуются от класса View, а значит большинство атрибутов для них общие. Например, `TextView` может использовать атрибут `onClick`, хоть обычно для нажатия и существует компонент `Button`.

Каждый объект при объявлении в коде XML должен обладать открывающим и закрывающий тегом. Рассмотрим эти объекты на примере проекта из "Модуль 2. Компоненты приложений".

## TextView

Данный объект обладает следующими основными атрибутами:

* `android:text`: устанавливает текст элемента;
* `android:textSize`: устанавливает высоту текста, в качестве единиц измерения для указания высоты используются sp;
* `android:background`: задает фоновый цвет элемента в виде цвета в шестнадцатиричной записи или в виде цветового ресурса;
* `android:textColor`: задает цвет текста;
* `android:textAllCaps`: при значении true делает все символы в тексте заглавными;
* `android:textDirection`: устанавливает направление текста. По умолчанию используется направление слева направо, но с помощью значения rtl можно установить направление справо налево;
* `android:textAlignment`: задает выравнивание текста;
* `android:fontFamily`: устанавливает тип шрифта.

Данный объект мы использовали для вывода информации в `MessageActivity`.

```markup
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
```

## EditText

Данный объект является подклассом класса `EditText`. Это значит, что кроме особенности ввода текста, он обладает всеми возможностями объекта `TextView`. Данный объект обладает всеми отличительными атрибутами `TextView`. Следует выделить разве что атрибуты:

* `android:hint` - задает подсказку по вводу информации. При вводе текста подсказка не будет видна;
* `android:inputType` - позволяет выбрать тип вводимого текста и используемую для этого клавиатуру.

Данный объект мы использовали для ввода информации в `MainActivity`.

```markup
<EditText
        android:id="@+id/editText"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="16dp"
        android:layout_marginTop="16dp"
        android:hint="Введите текст"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toLeftOf="@+id/button"
        app:layout_constraintTop_toTopOf="parent" />
```

## Button

Данный объект взаимодействует с пользователем через нажатие. Обладает следящими основными атрибутами:

* `text`: задает текст на кнопке;
* `textColor`: задает цвет текста на кнопке;
* `background`: задает фоновый цвет кнопки;
* `textAllCaps`: при значении true устанавливает текст в верхнем регистре. По умолчанию как раз и применяется значение true;
* `onClick`: задает обработчик нажатия кнопки.

Данный объект мы использовали для отправки информации, введённой в поле `EditText` в `MainActivity`. Обратите внимание на то, как мы это делали. В атрибуте `android::onClick` мы написали имя функции, которую используем для отправки информации.

```markup
<Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="sendMessage"
        android:text="Отправить"
        app:layout_constraintLeft_toRightOf="@+id/editText"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
```

## Контроль

1. Модифицируйте TextView в MessageActivity таким образом, чтобы выводимая информация была выравнена по середине, шрифт был курсивным. Также настройте размер текста, цвет текста и цвет фона по своему желанию.
2. EditText - настройте размер текста, цвет текста и цвет фона по своему желанию. Выберите тип вводимого текста - номер телефона.
3. Button - настройте размер текста, цвет текста и цвет фона по своему желанию. Напишите функцию, которая будет генерировать случайное число и привяжите эту функцию к кнопке.

