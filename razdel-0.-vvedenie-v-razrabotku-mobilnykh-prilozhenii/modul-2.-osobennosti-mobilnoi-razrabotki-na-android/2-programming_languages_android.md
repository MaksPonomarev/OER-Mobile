# Языки программирования

## Java

Java — строго типизированный объектно-ориентированный язык программирования общего назначения. Это означает, что:

* язык не позволяет использовать разные типы в одном выражении \(строгая типизация\),
* язык построен на концепции объектно-ориентированного программирования - в центре этой концепции находится объект, который содержит в себе данные о нем и действия, которые он может выполнять \(объектно-ориентирвоанный\),
* язык предназначен для написания программного обеспечения в самых различных прикладных областях \(общего назначения\).

Программы на Java транслируются в байт-код Java, выполняемый виртуальной машиной Java \(JVM\) — программой, обрабатывающей байтовый код и передающей инструкции оборудованию как интерпретатор.

**Достоинством** подобного способа выполнения программ является полная независимость байт-кода от операционной системы и оборудования, что позволяет выполнять Java-приложения на любом устройстве, для которого существует соответствующая виртуальная машина. Другой важной особенностью технологии **Java** является гибкая система безопасности, в рамках которой исполнение программы полностью контролируется виртуальной машиной. Любые операции, которые превышают установленные полномочия программы \(например, попытка несанкционированного доступа к данным или соединения с другим компьютером\), вызывают немедленное прерывание.

Часто к недостаткам концепции виртуальной машины относят снижение производительности. Ряд усовершенствований несколько увеличил скорость выполнения программ на Java:

* применение технологии трансляции байт-кода в машинный код непосредственно во время работы программы \(JIT-технология\) с возможностью сохранения версий класса в машинном коде,
* обширное использование платформенно-ориентированного кода \(native-код\) в стандартных библиотеках,
* аппаратные средства, обеспечивающие ускоренную обработку байт-кода \(например, технология Jazelle, поддерживаемая некоторыми процессорами архитектуры ARM\).

По данным сайта shootout.alioth.debian.org, для семи разных задач время выполнения на Java составляет в среднем в полтора-два раза больше, чем для C/C++, в некоторых случаях Java быстрее, а в отдельных случаях в 7 раз медленнее. С другой стороны, для большинства из них потребление памяти Java-машиной было в 10—30 раз больше, чем программой на C/C++. Также примечательно исследование, проведённое компанией Google, согласно которому отмечается существенно более низкая производительность и бо́льшее потребление памяти в тестовых примерах на Java в сравнении с аналогичными программами на C++.

Идеи, заложенные в концепцию и различные реализации среды виртуальной машины Java, вдохновили множество энтузиастов на расширение перечня языков, которые могли бы быть использованы для создания программ, исполняемых на виртуальной машине. Эти идеи нашли также выражение в спецификации общеязыковой инфраструктуры CLI, заложенной в основу платформы .NET компанией Microsoft.

Ниже представлен пример кода на Java

```java
class Box {
    int width; // ширина коробки
    int height; // высота коробки
    int depth; // глубина коробки

    // Конструктор
    Box(int a, int b) {
        width = a;
        height = b;
        depth = 10;
    }

    // вычисляем объём коробки
    int getVolume() {
        return width * height * depth;
    }
}
```

{% embed url="https://stepik.org/lesson/12755/step/14?unit=3103" caption="" %}

## Kotlin

Kotlin \(Ко́тлин\) — статически типизированный, объектно-ориентированный язык программирования, работающий поверх Java Virtual Machine. Это означает, что:

* тип данных в программе на этом языке не может быть изменен во время работы программ \(статически типизированны\).

Авторы ставили целью создать язык более лаконичный и типобезопасный, чем Java, и более простой, чем Scala. Следствием упрощения по сравнению со Scala стали также более быстрая компиляция и лучшая поддержка языка в IDE. Язык полностью совместим с Java, что позволяет java-разработчикам постепенно перейти к его использованию; в частности, в Android язык встраивается с помощью Gradle, что позволяет для существующего android-приложения внедрять новые функции на Kotlin без переписывания приложения целиком.

Ниже можно увидеть примеры кода на Kotlin и попробовать решить задачу.

```kotlin
fun main() {
  val scope = "world"
  println("Hello, $scope!")
}
```

```kotlin
fun sayHello(maybe: String?, neverNull: Int) {
   // use of elvis operator
   val name: String = maybe ?: "stranger"
   println("Hello $name")
}
```

{% embed url="https://stepik.org/lesson/46345/step/1?unit=24391" caption="" %}
