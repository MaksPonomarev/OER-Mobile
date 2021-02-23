# Модуль 1. Activity



An activity is the entry point for interacting with the user. It represents a single screen with a user interface. For example, an email app might have one activity that shows a list of new emails, another activity to compose an email, and another activity for reading emails. Although the activities work together to form a cohesive user experience in the email app, each one is independent of the others. As such, a different app can start any one of these activities if the email app allows it. For example, a camera app can start the activity in the email app that composes new mail to allow the user to share a picture. An activity facilitates the following key interactions between system and app:

* Keeping track of what the user currently cares about \(what is on screen\) to ensure that the system keeps running the process that is hosting the activity.
* Knowing that previously used processes contain things the user may return to \(stopped activities\), and thus more highly prioritize keeping those processes around.
* Helping the app handle having its process killed so the user can return to activities with their previous state restored.
* Providing a way for apps to implement user flows between each other, and for the system to coordinate these flows. \(The most classic example here being share.\)

You implement an activity as a subclass of the [`Activity`](https://developer.android.com/reference/android/app/Activity) class. For more information about the [`Activity`](https://developer.android.com/reference/android/app/Activity) class, see the [Activities](https://developer.android.com/guide/components/activities) developer guide.

