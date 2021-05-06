# УФ3. Программирование

Для создания обработчиков кнопок необходимо знать следующие особенности:

1. Необходимо создать несколько глобальных переменных, которые будут: отвечать за поле вывода вычислений, отвечать за поле вывода результата вычислений, отвечать за выполняемую операцию, проверять совершается ли операция. Возможно потребуются дополнительные переменные для промежуточных операций.
2. В функции onCreate кроме задания интерфейса через senContentView необходимо будет найти текстовые поля через функцию findViewById для того, чтобы с этими объектами можно было взаимодействовать.
3. Не нужно создавать отдельную функцию для взаимодействия с каждой кнопкой. Например, можно создать 4 функции для взаимодействия с кнопками - для цифр, для операций, для кнопки удаления, для кнопки равенства.

Главное условие для создания калькулятора:

1. Операции работают без ошибок.
2. Есть промежуточные вычисления.
3. При нажатии на кнопку равенства вычисления прекращаются, записывается окончательный результат.

Ниже представлен один из примеров реализации для простого калькулятора.

```kotlin
package com.android.academy.fundamentals

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.widget.Button
import android.widget.TextView

class SimpleCalculatorActivity : AppCompatActivity() {

    lateinit var result: TextView
    lateinit var equation: TextView
    var action = false
    var lastoperation: String = "+"
    var operand: Array<Double> = arrayOf(0.0, 0.0)
    var strOperand: Array<String> = arrayOf("", "")
    var num = 0


    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_simple_calculator)

        equation = findViewById(R.id.result)
        result = findViewById(R.id.equation)
    }


    fun numberClick (number: View) {
        var numberButton: Button = number as Button
        result.append(number.text)
        action = false
        strOperand[num] += number.text.toString()
    }

    fun operationClick (operation: View) {
        if (action) {
            val str = result.text.toString()
            if (str.isNotEmpty()) {
                result.text = str.substring(0, str.length - 1)
                var operationButton: Button = operation as Button
                result.append(operation.text)
                lastoperation = operation.text.toString()
            }
        } else {
            if (result.text.toString().isNotEmpty()) {
                var operationButton: Button = operation as Button
                result.append(operation.text)

                operand[num] = strOperand[num].toDouble()

                performOperation(operation)

                lastoperation = operation.text.toString()
            }
            action = true
        }
        num=1
    }

    private fun performOperation(operation: View) {

        if (strOperand[1].isNotEmpty()) {
            when (lastoperation) {
                "+" -> {
                    equation.text = ((operand[0] + operand[1]).toString())
                    operand[0] = operand[0] + operand[1]
                    strOperand[1] = ""
                }
                "-" -> {
                    equation.text = ((operand[0] - operand[1]).toString())
                    operand[0] = operand[0] - operand[1]
                    strOperand[1] = ""
                }
                "*" -> {
                    equation.text = ((operand[0] * operand[1]).toString())
                    operand[0] = operand[0] * operand[1]
                    strOperand[1] = ""
                }
                "/" -> {
                    if (operand[1] != 0.0) {
                        equation.text = ((operand[0] / operand[1]).toString())
                        operand[0] = operand[0] / operand[1]
                        strOperand[1] = ""
                    } else {
                        equation.text = ("infinity")
                        operand[0] = 0.0
                        operand[1] = 0.0
                        strOperand[1] = ""
                    }
                }
            }
        }

    }

    fun cClick (number: View) {
        if (result.text.isEmpty()) {
            equation.text = ""
            reset()
        }
        val str = result.text.toString()
        if (str.isNotEmpty()) {
            result.text = str.substring(0, str.length-1)
        }
        action = false
    }

    fun equally (operation: View) {
        if (result.text.toString().isNotEmpty()) {
            operand[num] = strOperand[num].toDouble()

            performOperation(operation)

            result.text = ""
            reset()
        }
    }

    fun reset() {
        action = false
        lastoperation = "+"
        operand[0]=0.0
        operand[1]=0.0
        strOperand[0]=""
        strOperand[1]=""
        num = 0
    }

}
```



