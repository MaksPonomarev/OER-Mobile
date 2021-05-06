# УФ2. Верстка

### Настройка графического редактора

Для настройки графического редактора:

1. В окне проекта откройте **app &gt; res &gt; layout &gt; activity\_main.xml**.
2. Чтобы было больше места для окна графического редактора скройте структуру проекта. Для того чтобы сделать это, кликните по кнопке слева сверху **View &gt; Tool Windows &gt; Project**, или кликните по вертикальной кнопке **Project,** которая находится в левом краю экрана Android Studio .
3. Если редактор показывает исходный XML-код, то кликните по кнопке **Design**, которая находится в правом верхнем углу окна.
4. Кликните по ![](https://developer.android.com/studio/images/buttons/layout-editor-design.png) \(**Select Design Surface**\) и выберите **Design + Blueprint**.
5. Кликните![](https://developer.android.com/studio/images/buttons/layout-editor-show-constraints.png) \(**View Options**\) и убедитесь, что активна опция **Show All Constraints**.
6. Убедитесь в том, что автоматическое подсоединение элементов выключено ![](https://developer.android.com/studio/images/buttons/layout-editor-autoconnect-on.png) \(**Enable Autoconnection to Parent**\).
7. Click ![](https://developer.android.com/studio/images/buttons/default-margins.png) \(**Default Margins**\) и выберите **16**. Если необходимо, то вы можете настроить отступы для каждого **View** позже.

![&#x420;&#x438;&#x441;.2. &#x41E;&#x43A;&#x43D;&#x43E; &#x440;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440;&#x430; &#x43F;&#x43E;&#x441;&#x43B;&#x435; &#x43D;&#x430;&#x441;&#x442;&#x440;&#x43E;&#x439;&#x43A;&#x438;](../../.gitbook/assets/2.2.2-editor_main_elements.png)

В результате выполненных шагов мы настроили редактор для дальнейшей работы на основе макета под названием **ConstraintLayout,** который определяет позицию объекта **View** на основе создания ограничений \(constraints\) по отношению к другим объектам **View** и макету. Вы можете увидеть такие constraints, посмотрев на текстовый блок "Hello, World!" - у него есть 4 constraints, которые цепляются за каждую границу макета.

### Создание интерфейса





