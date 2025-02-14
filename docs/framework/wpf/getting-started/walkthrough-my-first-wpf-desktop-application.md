---
title: Создание приложения WPF в Visual Studio
ms.date: 03/20/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- getting started [WPF], WPF
- WPF [WPF], getting started
ms.assetid: b96bed40-8946-4285-8fe4-88045ab854ed
author: mairaw
ms.author: mairaw
ms.custom: vs-dotnet
ms.openlocfilehash: c3440ddf6cdae6b24bcf1059ab2c76d8fb957263
ms.sourcegitcommit: 11deacc8ec9f229ab8ee3cd537515d4c2826515f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2019
ms.locfileid: "66003855"
---
# <a name="walkthrough-my-first-wpf-desktop-application"></a>Пошаговое руководство. Создание классического приложения WPF

В этой статье показано, как для разработки классического приложения Windows Presentation Foundation (WPF), который содержит элементы, которые являются общими для большинства приложений WPF: Расширяемый язык разметки приложений (XAML) разметки, кода, определения приложений, элементы управления, макет, привязки данных и стили. При разработке приложения, можно использовать Visual Studio. 

В этом пошаговом руководстве включает следующие шаги:

- Используйте XAML для разработки приложения пользовательского интерфейса (UI).

- Напишите код для создания поведения приложения.

- Создайте определение приложения для управления приложением.

- Добавление элементов управления и создание макета для создания пользовательского интерфейса приложения.

- Создания таблиц стилей для согласованное отображение пользовательского интерфейса приложения.

- Привязка пользовательского интерфейса к данным, для заполнения пользовательского интерфейса на основе данных и хранить данные и пользовательский Интерфейс.

В конце пошагового руководства будет создать автономное приложение Windows, которое позволяет пользователям просматривать отчеты о расходах для выбранных пользователей. Приложение состоит из нескольких страниц WPF, размещаемых в окне обозревателя.

> [!TIP]
> Пример кода, который используется в этом пошаговом руководстве доступен для обоих Visual Basic и C# в [код образца приложения WPF пошагового руководства](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/WalkthroughFirstWPFApp).
>
> Можно переключать язык кода примера кода между C# и Visual Basic с помощью **\< />** раскрывающееся меню в верхней правой части в этой статье.

## <a name="prerequisites"></a>Предварительные требования

- Visual Studio 2017 или более поздней версии (в этой статье используется Visual Studio 2019 г.)

   Дополнительные сведения об установке последней версии Visual Studio, см. в разделе [установка Visual Studio](/visualstudio/install/install-visual-studio).

## <a name="create-the-application-project"></a>Создание проекта приложения

Первым шагом является создание инфраструктуры приложений, который включает в себя определение приложения, две страницы и изображение.

1. Создание нового проекта приложения WPF в Visual Basic или Visual C# с именем **`ExpenseIt`**:

   1. Откройте Visual Studio и выберите **создайте новый проект** под **приступить к работе** меню.

      **Создайте новый проект** откроется диалоговое окно.

   2. В **языка** раскрывающемся списке выберите либо **C#** или **Visual Basic**.
      
   3. Выберите **приложение WPF (.NET Framework)** шаблона, а затем выберите **Далее**. 
     
      ![Создать диалоговое окно нового проекта](./media/walkthrough-my-first-wpf-desktop-application/create-new-project-dialog.png)
    
      **Настроить новый проект** откроется диалоговое окно.

   4. Введите имя проекта **`ExpenseIt`** , а затем выберите **создать**.

      ![Настройте диалоговое окно нового проекта](./media/walkthrough-my-first-wpf-desktop-application/configure-new-project-dialog.png)

      Visual Studio создаст проект и открывает конструктор для окна приложения по умолчанию с именем **MainWindow.xaml**.

2. Откройте *Application.xaml* (Visual Basic) или *App.xaml* (C#).

    Этот файл XAML определяет WPF-приложение и все его ресурсы. Этот файл также используется для указания пользовательского интерфейса, в данном случае *MainWindow.xaml*, автоматически отображаемого при запуске приложения.

    В XAML должен выглядеть как следующий код в Visual Basic:

    [!code-xaml[ExpenseIt#1_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/Application.xaml#1_a)]

    И, как показано ниже в C#:

    [!code-xaml[ExpenseIt#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/App.xaml#1)]

3. Откройте *MainWindow.xaml*.

    Этот файл XAML представляет главное окно приложения и отображает созданное содержимое страниц. <xref:System.Windows.Window> Класс определяет свойства окна, такие как заголовок, размер и значок и обрабатывает события, такие как открытие и закрытие окна.

4. Изменение <xref:System.Windows.Window> элемент <xref:System.Windows.Navigation.NavigationWindow>, как показано в следующем XAML:

   ```xaml
   <NavigationWindow x:Class="ExpenseIt.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        ...
   </NavigationWindow>
   ```

   Это приложение переходит к различному содержимому вводимых пользователем данных. Вот почему основной <xref:System.Windows.Window> должно быть изменено <xref:System.Windows.Navigation.NavigationWindow>. <xref:System.Windows.Navigation.NavigationWindow> наследует все свойства <xref:System.Windows.Window>. <xref:System.Windows.Navigation.NavigationWindow> В файле XAML создает экземпляр класса <xref:System.Windows.Navigation.NavigationWindow> класса. Дополнительные сведения см. в разделе [Общие сведения о переходах](../app-development/navigation-overview.md).

5. Удалить <xref:System.Windows.Controls.Grid> элементов из между <xref:System.Windows.Navigation.NavigationWindow> теги.

6. Измените следующие свойства в коде XAML для <xref:System.Windows.Navigation.NavigationWindow> элемент:

    - Задайте <xref:System.Windows.Window.Title%2A> свойства "`ExpenseIt`«.

    - Задайте <xref:System.Windows.FrameworkElement.Height%2A> свойство значение 350 пикселей.

    - Задайте <xref:System.Windows.FrameworkElement.Width%2A> значение 500 пикселей.

    В XAML должен выглядеть как показано ниже для Visual Basic:

    [!code-xaml[ExpenseIt#2_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt/MainWindow.xaml#2_a)]

    И, как показано ниже для C#:

    [!code-xaml[ExpenseIt#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/MainWindow.xaml#2)]

7. Откройте *MainWindow.xaml.vb* или *MainWindow.xaml.cs*.

    Этот файл является файлом кода, который содержит код для обработки событий, объявленных в *MainWindow.xaml*. Этот файл содержит разделяемый класс для окна, определенного в XAML-коде.

8. Если вы используете C#, изменить `MainWindow` класса для наследования от <xref:System.Windows.Navigation.NavigationWindow>. (В Visual Basic это происходит автоматически при изменении окна в XAML.) Ваш C# код теперь должен выглядеть следующим образом:

   [!code-csharp[ExpenseIt#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/MainWindow.xaml.cs?highlight=21)]

## <a name="add-files-to-the-application"></a>Добавление файлов в приложение

В этом разделе вы добавите в приложение две страницы и изображение.

1. Добавьте новую страницу в проект и назовите его *`ExpenseItHome.xaml`*:

   1. В **обозревателе решений**, щелкните правой кнопкой мыши **`ExpenseIt`** узел проекта и выберите **добавить** > **страницы**.

   1. В **Добавление нового элемента** диалоговое окно, **страницу (WPF)** шаблон уже выбран. Введите имя **`ExpenseItHome`**, а затем выберите **добавить**.

    Эта страница является первой страницей, которое отображается при запуске приложения. Появится список пользователей для выбора, чтобы просмотреть отчет о расходах для.

1. Откройте *`ExpenseItHome.xaml`*.

1. Задайте <xref:System.Windows.Controls.Page.Title%2A> для "`ExpenseIt - Home`«.

1. Задайте `DesignHeight` и `DesignWidth` значения элементов до 300 пикселей.

    XAML теперь выглядит следующим образом для Visual Basic:

    [!code-xaml[ExpenseIt#6_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml#6_a)]

    И, как показано ниже для C#:

    [!code-xaml[ExpenseIt#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml#6)]

1. Откройте *MainWindow.xaml*.

1. Добавить <xref:System.Windows.Navigation.NavigationWindow.Source%2A> свойства <xref:System.Windows.Navigation.NavigationWindow> элемент и задайте для него значение "`ExpenseItHome.xaml`«.

    Этот параметр задает *`ExpenseItHome.xaml`* в качестве первой страницы, открываемой при запуске приложения. 

    Пример XAML в Visual Basic.

    [!code-xaml[ExpenseIt#7_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/MainWindow.xaml#7_a)]

    И в C#:

    [!code-xaml[ExpenseIt#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/MainWindow.xaml#7)]

   > [!TIP]
   > Можно также задать **источника** свойство в **Разное** категории **свойства** окна.
   >
   > ![Свойства Source в окно "Свойства"](./media/properties-source.png)

1. Добавьте другую новую страницу WPF в проект и назовите его *ExpenseReportPage.xaml*::

   1. В **обозревателе решений**, щелкните правой кнопкой мыши **`ExpenseIt`** узел проекта и выберите **добавить** > **страницы**.

   1. В **Добавление нового элемента** диалоговом окне выберите **страницу (WPF)** шаблона. Введите имя **ExpenseReportPage**, а затем выберите **добавить**.

    Эта страница будет отображаться отчет по расходам для человека, выбранного на **`ExpenseItHome`** страницы.

1. Откройте файл *ExpenseReportPage.xaml*.

1. Задайте <xref:System.Windows.Controls.Page.Title%2A> для "`ExpenseIt - View Expense`«.

1. Задайте `DesignHeight` и `DesignWidth` значения элементов до 300 пикселей.

    *ExpenseReportPage.xaml* теперь выглядит как следующий код в Visual Basic:

    [!code-xaml[ExpenseIt#4_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml#4_a)]

    И, как показано ниже в C#:

    [!code-xaml[ExpenseIt#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml#4)]

1. Откройте *ExpenseItHome.xaml.vb* и *ExpenseReportPage.xaml.vb*, или *ExpenseItHome.xaml.cs* и *ExpenseReportPage.xaml.cs*.

    При создании нового файла страницы Visual Studio автоматически создает его *кода* файл. Эти файлы кода программной части обрабатывают логику, реагирующую на действия пользователя.

    Код должен выглядеть, как показано ниже для **`ExpenseItHome`**:

    [!code-csharp[ExpenseIt#2_5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml.cs#2_5)]

    [!code-vb[ExpenseIt#2_5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml.vb#2_5)]

    И, как показано ниже для **ExpenseReportPage**:

    [!code-csharp[ExpenseIt#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml.cs#5)]

    [!code-vb[ExpenseIt#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml.vb#5)]

1. Добавить образ с именем *watermark.png* в проект. Можно создать собственный образ, скопируйте файл из образца кода или его [здесь](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/WalkthroughFirstWPFApp).

    1. Щелкните правой кнопкой мыши узел проекта и выберите **добавить** > **существующий элемент**, или нажмите клавишу **Shift**+**Alt** + **Объект**.

    2. В **добавить существующий элемент** диалоговое окно, установить фильтр файлов **все файлы** или **файлы изображений**, перейдите к файлу образа, который вы хотите использовать, а затем выберите **добавить** .

## <a name="build-and-run-the-application"></a>Построение и запуск приложения

1. Чтобы построить и запустить приложение, нажмите клавишу **F5** или выберите **начать отладку** из **Отладка** меню.

    На следующем рисунке показано приложение с помощью <xref:System.Windows.Navigation.NavigationWindow> кнопки:

    ![Приложение, выполнив сборку и запустите его.](./media/walkthrough-my-first-wpf-desktop-application/build-run-application.png)

2. Закройте приложение, чтобы вернуться в Visual Studio.

## <a name="create-the-layout"></a>Создание макета

Макет позволяет упорядочивать размещение элементов пользовательского интерфейса и также управлять их размером и положением при изменении размера пользовательского интерфейса. Обычно макет создается с одним из следующих элементов управления макетом.

- <xref:System.Windows.Controls.Canvas> -Определяет область, внутри которой можно явным образом разместить дочерние элементы, используя координаты относительно области полотна.
- <xref:System.Windows.Controls.DockPanel> -Определяет область, где можно упорядочивать дочерние элементы горизонтально либо вертикально относительно друг друга.
- <xref:System.Windows.Controls.Grid> -Определяет гибкую область сетки, состоящей из столбцов и строк.
- <xref:System.Windows.Controls.StackPanel> -Дочерние элементы размещаются в одну линию, ориентированную горизонтально или вертикально.
- <xref:System.Windows.Controls.VirtualizingStackPanel> -Упорядочивает и виртуализирует содержимое на одной строке, ориентированную горизонтально или вертикально.
- <xref:System.Windows.Controls.WrapPanel> -Размещает дочерние элементы последовательно слева направо, перенося содержимое на следующую строку на границе содержащего поля. Дальнейшее упорядочивание происходит последовательно сверху вниз или справа налево, в зависимости от значения свойства Orientation.

Каждая из этих элементов управления макетом поддерживает определенный тип макета дочерних элементов. `ExpenseIt` размер страницы может быть изменен, и каждая страница имеет элементы, которые упорядочены по горизонтали и вертикали рядом с другими элементами. В этом примере <xref:System.Windows.Controls.Grid> используется как элемент макета для приложения.

> [!TIP]
> Дополнительные сведения о <xref:System.Windows.Controls.Panel> элементов, см. в разделе [Общие сведения о панелях](../controls/panels-overview.md). Дополнительные сведения о макете см. в разделе [макета](../advanced/layout.md).

В этом разделе описано, создании одного столбца таблицы с тремя строками и полями шириной 10 пикселей путем добавления определений столбцов и строк для <xref:System.Windows.Controls.Grid> в *`ExpenseItHome.xaml`*.

1. В *`ExpenseItHome.xaml`*, задайте <xref:System.Windows.FrameworkElement.Margin%2A> свойство <xref:System.Windows.Controls.Grid> элемент «10,0,10,10», который соответствует слева, сверху, справа и нижнего полей:

   ```xaml
   <Grid Margin="10,0,10,10">
   ```

   > [!TIP]
   > Можно также задать **Margin** значения в **свойства** окна в разделе **макета** категории:
   >
   > ![Значения полей в окно "Свойства"](./media/properties-margin.png)

2. Добавьте следующий XAML между <xref:System.Windows.Controls.Grid> теги, чтобы создать определения строк и столбцов:

    [!code-xaml[ExpenseIt#8](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#8)]

    <xref:System.Windows.Controls.RowDefinition.Height%2A> Двух строк имеет значение <xref:System.Windows.GridLength.Auto%2A>, означающее, что размер строки на основе содержимого в строках. Значение по умолчанию <xref:System.Windows.Controls.RowDefinition.Height%2A> является <xref:System.Windows.GridUnitType.Star> изменения размера, это означает, что высота строки — это взвешенная пропорция доступного пространства. Например, если две строки имеют <xref:System.Windows.Controls.RowDefinition.Height%2A> из «*», каждый из них имеет высоту, половина доступного пространства.

    Ваш <xref:System.Windows.Controls.Grid> теперь должно содержать следующие XAML:

    [!code-xaml[ExpenseIt#9](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#9)]

## <a name="add-controls"></a>Добавление элементов управления

В этом разделе вы обновите на домашней странице пользовательский Интерфейс для отображения списка пользователей, где выбран один пользователь, для отображения отчета о расходах. Элементы управления — это объекты пользовательского интерфейса, позволяющие пользователям взаимодействовать с приложением. Более подробную информацию см. в разделе [Элементы управления](../controls/index.md).

Чтобы создать этот пользовательский Интерфейс, нужно добавить следующие элементы для *`ExpenseItHome.xaml`*:

- Объект <xref:System.Windows.Controls.ListBox> (для списка пользователей).
- Объект <xref:System.Windows.Controls.Label> (для заголовков списка).
- Объект <xref:System.Windows.Controls.Button> (чтобы щелкните, чтобы просмотреть отчет по расходам для человека, выбранного в списке).

Каждый элемент управления помещается в строке <xref:System.Windows.Controls.Grid> , задав <xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType> вложенного свойства зависимостей. Дополнительные сведения о вложенных свойствах см. в разделе [зависимостей](../advanced/attached-properties-overview.md).

1. В *`ExpenseItHome.xaml`*, добавьте следующий XAML где-то между <xref:System.Windows.Controls.Grid> теги:

   [!code-xaml[ExpenseIt#10](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt4/ExpenseItHome.xaml#10)]

   > [!TIP]
   > Также можно создать элементы управления, перетащив их из **элементов** окна в окне конструктора, а затем задав их свойства в **свойства** окна.

2. Выполните сборку и запуск приложения.

    На следующем рисунке показано элементы управления, что вы создали:

![Снимок экрана примера ExpenseIt, отображение списка имен](./media/walkthrough-my-first-wpf-desktop-application/add-application-controls.png)

## <a name="add-an-image-and-a-title"></a>Добавить изображение и заголовок

В этом разделе вы обновите интерфейсе пользователя домашней страницы изображение и заголовок страницы.

1. В *`ExpenseItHome.xaml`*, добавьте еще один столбец для <xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> с фиксированным <xref:System.Windows.Controls.ColumnDefinition.Width%2A> 230 пикселей:

    [!code-xaml[ExpenseIt#11](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=52-55)]

2. Добавить другую строку для <xref:System.Windows.Controls.Grid.RowDefinitions%2A>, всего четыре строки:

    [!code-xaml[ExpenseIt#11b](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=57-62)]

3. Переместите элементы управления во второй столбец, задав <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType> свойство в значение 1, в каждом из трех элементов управления (границы, ListBox и кнопка).

4. Переместите каждый элемент управления вниз на одну строку, увеличивая его <xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType> значение на 1 для каждого из трех элементов управления (границы, ListBox и кнопка), а также для элемента.

   XAML для трех элементов управления теперь выглядит следующим образом:

    [!code-xaml[ExpenseIt#12](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#12)]

5. Задайте <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType> свойства *watermark.png* файл изображения, добавив следующий XAML в любом месте между `<Grid>` и `</Grid>` теги:

    [!code-xaml[ExpenseIt#14](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#14)]

6. Прежде чем <xref:System.Windows.Controls.Border> элемента, добавьте <xref:System.Windows.Controls.Label> с содержимым «View Expense Report». Эта метка — это заголовок страницы.

    [!code-xaml[ExpenseIt#13](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#13)]

7. Выполните сборку и запуск приложения.

На следующем рисунке показано только что добавленную результаты:

![Пример ExpenseIt снимок экрана, показывающий новый образ фона и заголовок страницы](./media/walkthrough-my-first-wpf-desktop-application/add-application-image-title.png)

## <a name="add-code-to-handle-events"></a>Добавьте код для обработки событий

1. В *`ExpenseItHome.xaml`*, добавьте <xref:System.Windows.Controls.Primitives.ButtonBase.Click> в обработчике событий <xref:System.Windows.Controls.Button> элемент. Дополнительные сведения см. в разделе [Практическое руководство. Создание простого обработчика событий](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb675300(v=vs.100)).

    [!code-xaml[ExpenseIt#15](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml#15)]

2. Откройте *`ExpenseItHome.xaml.vb`* или *`ExpenseItHome.xaml.cs`*.

3. Добавьте следующий код, чтобы `ExpenseItHome` класс, чтобы добавить кнопку обработчик события щелчка. Обработчик событий открывает **ExpenseReportPage** страницы.

    [!code-csharp[ExpenseIt#16](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml.cs#16)]
    [!code-vb[ExpenseIt#16](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt6/ExpenseItHome.xaml.vb#16)]

## <a name="create-the-ui-for-expensereportpage"></a>Создание пользовательского интерфейса для страницы ExpenseReportPage

*ExpenseReportPage.xaml* отображается отчет по расходам для человека, выбранного на **`ExpenseItHome`** страницы. В этом разделе вы создадите пользовательский Интерфейс для **ExpenseReportPage**. Вы также добавите фона и цвета для различных элементов пользовательского интерфейса заливки.

1. Откройте файл *ExpenseReportPage.xaml*.

2. Добавьте следующий XAML между <xref:System.Windows.Controls.Grid> теги:

    [!code-xaml[ExpenseIt#17](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseReportPage.xaml#17)]

    Этот пользовательский Интерфейс аналогичен *`ExpenseItHome.xaml`*, за исключением, что данные отчета отображаются в <xref:System.Windows.Controls.DataGrid>.

3. Выполните сборку и запуск приложения.

4. Выберите **представление** кнопки.

    Появится страница отчета по расходам. Также Обратите внимание на то, что кнопка возврата включено.

На следующем рисунке показан элементы пользовательского интерфейса, добавленные *ExpenseReportPage.xaml*.

![ExpenseIt образец снимок экрана пользовательского интерфейса для страницы ExpenseReportPage только что создали.](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

## <a name="style-controls"></a>Определение стиля элементов управления

Внешний вид различных элементов часто является одинаковым для всех элементов одного типа в пользовательском Интерфейсе. Пользовательский Интерфейс использует [стили](../controls/styling-and-templating.md) чтобы варианты внешнего вида многократного использования для нескольких элементов. Повторное использование стилей помогает упростить создание XAML и управление ими. В этом разделе атрибуты, установленные ранее для каждого элемента, заменяются стилями.

1. Откройте *Application.xaml* или *App.xaml*.

2. Добавьте следующий XAML между <xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> теги:

    [!code-xaml[ExpenseIt#18](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/App.xaml#18)]

    Этот код XAML добавляет следующие стили:

    - `headerTextStyle`: Для форматирования заголовка страницы <xref:System.Windows.Controls.Label>.

    - `labelStyle`: Для форматирования <xref:System.Windows.Controls.Label> элементов управления.

    - `columnHeaderStyle`: Для форматирования <xref:System.Windows.Controls.Primitives.DataGridColumnHeader>.

    - `listHeaderStyle`: Форматирование заголовка списка <xref:System.Windows.Controls.Border> элементов управления.

    - `listHeaderTextStyle`: Форматирование заголовка списка <xref:System.Windows.Controls.Label>.

    - `buttonStyle`: Для форматирования <xref:System.Windows.Controls.Button> на `ExpenseItHome.xaml`.

    Обратите внимание на то, что стили представляют собой ресурсы и являются дочерними <xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> элемент свойства. Здесь стили применяются ко всем элементам в приложении. Пример использования ресурсов в приложении .NET, см. в разделе [использование ресурсов приложения](../advanced/how-to-use-application-resources.md).

3. В *`ExpenseItHome.xaml`*, замените весь код между <xref:System.Windows.Controls.Grid> элементов при помощи следующих XAML:

    [!code-xaml[ExpenseIt#19](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseItHome.xaml#19)]

    Свойства, определяющие внешний вид элементов управления, такие как <xref:System.Windows.VerticalAlignment> и <xref:System.Windows.Media.FontFamily> , при применении стилей удаляются и заменяются. Например `headerTextStyle` применяется к «View Expense Report» <xref:System.Windows.Controls.Label>.

4. Откройте файл *ExpenseReportPage.xaml*.

5. Замените весь код между <xref:System.Windows.Controls.Grid> элементов при помощи следующих XAML:

    [!code-xaml[ExpenseIt#20](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseReportPage.xaml#20)]

    Этот XAML добавлены стили <xref:System.Windows.Controls.Label> и <xref:System.Windows.Controls.Border> элементы.

6. Выполните сборку и запуск приложения. Внешний вид окна совпадает с ранее.

    ![Снимок экрана примера ExpenseIt в таком же виде, как и в предыдущем разделе.](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

7. Закройте приложение, чтобы вернуться в Visual Studio.

## <a name="bind-data-to-a-control"></a>Привязка данных к элементу управления

В этом разделе вы создадите XML-данных, привязанный к различным элементам управления.

1. В *`ExpenseItHome.xaml`*, открыв <xref:System.Windows.Controls.Grid> элемента, добавьте следующий XAML для создания <xref:System.Windows.Data.XmlDataProvider> , содержащий данные для каждого пользователя:

    [!code-xaml[ExpenseIt#23](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,16-40,49)]

    Данные создаются как <xref:System.Windows.Controls.Grid> ресурсов. Обычно эти данные могут загружаться как файл, но для простоты данные добавлены в код.

2. В рамках `<Grid.Resources>` элемента, добавьте следующий `<xref:System.Windows.DataTemplate>` элемент, который определяет способ отображения данных в <xref:System.Windows.Controls.ListBox>после `<XmlDataProvider>` элемент:

    [!code-xaml[ExpenseIt#24](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,43-46,49)]

    Дополнительные сведения о шаблонах данных см. в разделе [Общие сведения о шаблонах данных](../data/data-templating-overview.md).

3. Замените существующий <xref:System.Windows.Controls.ListBox> с следующем XAML:

    [!code-xaml[ExpenseIt#25](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#25)]

    Этот XAML привязывает <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> свойство <xref:System.Windows.Controls.ListBox> к источнику данных и применяет шаблон данных как <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>.

## <a name="connect-data-to-controls"></a>Подключение данных к элементам управления

Далее добавим код для извлечения имени, выбранного на **`ExpenseItHome`** странице и передать его конструктору **ExpenseReportPage**. **ExpenseReportPage** задает контекст данных для переданного элемента, который является то, что элементы управления, определенные в *ExpenseReportPage.xaml* привязки.

1. Откройте файл *ExpenseReportPage.xaml.vb* или *ExpenseReportPage.xaml.cs*.

2. Добавьте конструктор, принимающий объект, чтобы можно было передавать данные отчета о затратах выбранного человека.

    [!code-csharp[ExpenseIt#26](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseReportPage.xaml.cs#26)]
    [!code-vb[ExpenseIt#26](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseReportPage.xaml.vb#26)]

3. Откройте *`ExpenseItHome.xaml.vb`* или *`ExpenseItHome.xaml.cs`*.

4. Изменение <xref:System.Windows.Controls.Primitives.ButtonBase.Click> обработчик событий для вызова новый конструктор, передавая отчета о затратах выбранного человека.

    [!code-csharp[ExpenseIt#27](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml.cs#27)]
    [!code-vb[ExpenseIt#27](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseItHome.xaml.vb#27)]

## <a name="style-data-with-data-templates"></a>Стиль данных с помощью шаблонов данных

В этом разделе вы обновите пользовательский Интерфейс для каждого элемента в списках с привязкой к данным с помощью шаблонов данных.

1. Откройте файл *ExpenseReportPage.xaml*.

2. Привяжите содержимое «Name» и «Отдел» <xref:System.Windows.Controls.Label> свойство источника элементов, соответствующих данных. Дополнительные сведения о привязке данных см. в разделе [Общие сведения о привязке данных](../data/data-binding-overview.md).

    [!code-xaml[ExpenseIt#31](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#31)]

3. После открывающего <xref:System.Windows.Controls.Grid> элемента, добавьте следующие шаблоны данных, которые определяют способ отображения данных отчета о расходах:

    [!code-xaml[ExpenseIt#30](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#30)]

4. Замените <xref:System.Windows.Controls.DataGridTextColumn> элементов при помощи <xref:System.Windows.Controls.DataGridTemplateColumn> под <xref:System.Windows.Controls.DataGrid> элемента и примените шаблоны к ним.

    [!code-xaml[ExpenseIt#32](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#32)]

5. Выполните сборку и запуск приложения.

6. Выберите "person", а затем выберите **представление** кнопки.

На следующем рисунке показан обе страницы `ExpenseIt` приложения с помощью элементов управления, макет, стили, привязку данных и примененными шаблонами данных:

![Обе страницы приложения в список имен и отчет о расходах.](./media/walkthrough-my-first-wpf-desktop-application/application-data-templates.png)

> [!NOTE]
> В этом примере демонстрируется конкретная функциональная возможность WPF и не выполните все рекомендации по безопасности, локализации и специальных возможностей. Исчерпывающая информация о WPF и рекомендации по разработке приложений .NET см. в следующих разделах:
>
> - [Специальные возможности](../../ui-automation/accessibility-best-practices.md)
>
> - [Безопасность](../security-wpf.md)
>
> - [Глобализация и локализация WPF](../advanced/wpf-globalization-and-localization-overview.md)
>
> - [Производительности WPF](../advanced/optimizing-wpf-application-performance.md)

## <a name="next-steps"></a>Следующие шаги

В этом пошаговом руководстве вы узнали ряд методов для создания пользовательского интерфейса с помощью Windows Presentation Foundation (WPF). Теперь вы должны основные стандартные блоки приложения .NET с данными. Более подробную информацию об архитектуре и моделях программирования WPF см. в следующих разделах:

- [Архитектура WPF](../advanced/wpf-architecture.md)
- [Обзор XAML (WPF)](../advanced/xaml-overview-wpf.md)
- [Общие сведения о свойствах зависимостей](../advanced/dependency-properties-overview.md)
- [Макет](../advanced/layout.md)

Более подробную информацию о создании приложений см. в следующих разделах:

- [Разработка приложений](../app-development/index.md)
- [Элементы управления](../controls/index.md)
- [Общие сведения о привязке данных](../data/data-binding-overview.md)
- [Графика и мультимедиа](../graphics-multimedia/index.md)
- [Документы в WPF](../advanced/documents-in-wpf.md)

## <a name="see-also"></a>См. также

- [Общие сведения о панелях](../controls/panels-overview.md)
- [Общие сведения о шаблонах данных](../data/data-templating-overview.md)
- [Построение приложения WPF](../app-development/building-a-wpf-application-wpf.md)
- [Стили и шаблоны](../controls/styles-and-templates.md)
