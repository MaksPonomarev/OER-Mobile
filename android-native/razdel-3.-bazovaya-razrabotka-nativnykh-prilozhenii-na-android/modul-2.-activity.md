# Модуль 1. Activity

Активити является входной точкой для взаимодействия с пользователем. Она представляет собой один экран с пользовательским интерфейсом. Например, приложение для электронной почты может иметь одну активити, которая показывает список новых электронных писем, другое активити составляет электронное письмо, и третье активити читает электронные письма. Несмотря на то , что активити работают вместе для создания более полного пользовательского опыта в приложении электронных писем, каждое активи независимо друг от друга. Поэтому другое приложение может запустить одно из этих Активити, если приложение электронных писем позволяет это. Например, приложение для упралвения камерой может запустить Активити приложения для управления электронынми письмами, которое будет содержать новое электронное письмо, которое позволит пользователю поделиться изображением. Активити облегчают следующие ключевые взаимодействия между системой и приложением:

* Отслеживать приложения, которые видны на экране для того, чтобы гарантировать, что система не выключит процесс, который запускает Актививти.
* Ранее запускаемые процессы могут содержать вещи, к которым пользователь может вернуться \(например, остановленные Активити\), поэтому система держит данные процессы в приоритете.
* Помогает приложению откючаться таким образом, что если пользователь решит перейти к этому Активити, то предыдущее состяние процесса будет восстановлено.
* Предоставляет путь для приложений встроить пользовательские запросы \(?\) между собой и системе контролировать данные запросы \(типичным примером будет возможность "поделиться"\).

Активити объявляются как подкласс класса Activity.

```java
public class MainActivity extends Activity {
}
```

An activity is the entry point for interacting with the user. It represents a single screen with a user interface. For example, an email app might have one activity that shows a list of new emails, another activity to compose an email, and another activity for reading emails. 

Although the activities work together to form a cohesive user experience in the email app, each one is independent of the others. As such, a different app can start any one of these activities if the email app allows it. For example, a camera app can start the activity in the email app that composes new mail to allow the user to share a picture. An activity facilitates the following key interactions between system and app:

* Keeping track of what the user currently cares about \(what is on screen\) to ensure that the system keeps running the process that is hosting the activity.
* Knowing that previously used processes contain things the user may return to \(stopped activities\), and thus more highly prioritize keeping those processes around.
* Helping the app handle having its process killed so the user can return to activities with their previous state restored.
* Providing a way for apps to implement user flows between each other, and for the system to coordinate these flows. \(The most classic example here being share.\)

You implement an activity as a subclass of the [`Activity`](https://developer.android.com/reference/android/app/Activity) class. For more information about the [`Activity`](https://developer.android.com/reference/android/app/Activity) class, see the [Activities](https://developer.android.com/guide/components/activities) developer guide.

