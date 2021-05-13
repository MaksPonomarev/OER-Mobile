# Контроль Модуля

Создайте пользовательский интерфейс для приложение, в котором коробки невидны, однако при нажатии на экран они появляются. Добавьте 3 кнопки, которые будут раскрашивать коробки.

Требования к приложению:

1. Макет - 5 объектов TextView, 3 объекта Button. Каждый Button означает цвет.
2. Объекты TextView не видны при запуске приложения. При нажатии на них они появляются.
3. При нажатии на Button случайная коробка окрашивается в выбранный цвет.
4. Для каждого цвета создайте ресурс цвета.
5. Для каждой надписи создайте ресурс строки.
6. 
Пользовательский интерфейс представлен на рис.1.

![&#x420;&#x438;&#x441;. 1. &#x41F;&#x440;&#x438;&#x43C;&#x435;&#x440; &#x440;&#x435;&#x430;&#x43B;&#x438;&#x437;&#x430;&#x446;&#x438;&#x438;](../../.gitbook/assets/image%20%288%29.png)

Для того, чтобы на действия пользователя реагировали не только кнопки, необходимо использовать функцию `view.setOnClickListener()`. Например, в коде ниже вы можете увидеть 

```kotlin
package com.example.android.colormyviews

import android.graphics.Color
import android.os.Bundle
import android.support.v7.app.AppCompatActivity
import android.view.View
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        setListeners()
    }

    private fun setListeners() {
        val clickableViews: List<View> =
                listOf(box_one_text, box_two_text, box_three_text,
                        box_four_text, box_five_text, constraint_layout,
                        red_button, green_button, yellow_button)

        for (item in clickableViews) {
            item.setOnClickListener { makeColored(it) }
        }
    }

    private fun makeColored(view: View) {
        when (view.id) {

        // Boxes using Color class colors for background
            R.id.box_one_text -> view.setBackgroundColor(Color.DKGRAY)
            R.id.box_two_text -> view.setBackgroundColor(Color.GRAY)

        // Boxes using Android color resources for background
            R.id.box_three_text -> view.setBackgroundResource(android.R.color.holo_green_light)
            R.id.box_four_text -> view.setBackgroundResource(android.R.color.holo_green_dark)
            R.id.box_five_text -> view.setBackgroundResource(android.R.color.holo_green_light)

        // Boxes using custom colors for background
            R.id.red_button -> box_three_text.setBackgroundResource(R.color.my_red)
            R.id.yellow_button -> box_four_text.setBackgroundResource(R.color.my_yellow)
            R.id.green_button -> box_five_text.setBackgroundResource(R.color.my_green)

            else -> view.setBackgroundColor(Color.LTGRAY)
        }
    }
}
```

