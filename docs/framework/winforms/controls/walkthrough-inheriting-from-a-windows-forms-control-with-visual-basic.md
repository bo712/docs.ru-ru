---
title: Пошаговое руководство. Наследование элементов управления Windows Forms с помощью Visual Basic
ms.date: 03/30/2017
dev_langs:
- vb
helpviewer_keywords:
- inheritance [Windows Forms], custom controls
- inheritance [Windows Forms], control
- Windows Forms controls, inheritance
- inheritance [Windows Forms], walkthroughs
- custom controls [Windows Forms], inheritance
ms.assetid: fb58d7c8-b702-4478-ad31-b00cae118882
ms.openlocfilehash: b606de4b7cf4648fdc7ada3c1f6faec81342d02c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61792188"
---
# <a name="walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic"></a>Пошаговое руководство. Наследование элементов управления Windows Forms с помощью Visual Basic
Visual Basic позволяет создавать эффективные настраиваемые элементы управления *наследования*. Наследование позволяет создавать элементы управления, сохраняющие все унаследованные функциональные возможности элементов управления Windows Forms и в то же время обладающие дополнительными функциями. В этом пошаговом руководстве вы создадите простой производный элемент управления с именем `ValueButton`. Эта кнопка наследует функциональные возможности стандартных форм Windows <xref:System.Windows.Forms.Button> управления и предоставляет настраиваемое свойство `ButtonValue`.  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в разделе [Персонализация интегрированной среды разработки Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
## <a name="creating-the-project"></a>Создание проекта  
 Создавая проект, вы указываете для него имя, чтобы задать корневое пространство имен, имя сборки и имя проекта, и необходимо убедиться в том, что компонент по умолчанию попадет в нужное пространство имен.  
  
#### <a name="to-create-the-valuebuttonlib-control-library-and-the-valuebutton-control"></a>Создание библиотеки элементов управления ValueButtonLib и элемента управления ValueButton  
  
1. В меню **Файл** наведите указатель мыши на пункт **Создать** и выберите **Проект**, чтобы открыть диалоговое окно **Создание проекта**.  
  
2. Выберите **Библиотека элементов управления Windows Forms** шаблон проекта из списка проектов Visual Basic и тип `ValueButtonLib` в **имя** поле.  
  
     Имя проекта, `ValueButtonLib`, по умолчанию также назначается корневому пространству имен. Корневое пространство имен используется для определения имен компонентов в сборке. Например, если в двух сборках содержатся компоненты с именем `ValueButton`, можно указать компонент `ValueButton`, используя `ValueButtonLib.ValueButton`. Дополнительные сведения см. в разделе [Пространства имен в Visual Basic](~/docs/visual-basic/programming-guide/program-structure/namespaces.md).  
  
3. В **обозревателе решений** щелкните правой кнопкой мыши **UserControl1.vb** и выберите в контекстном меню команду **Переименовать**. Измените имя файла на `ValueButton.vb`. Чтобы переименовать все ссылки на элемент кода UserControl1, в соответствующем запросе нажмите кнопку **Да**.  
  
4. В **обозревателе решений** нажмите кнопку **Показать все файлы**.  
  
5. Откройте узел **ValueButton.vb**, чтобы отобразить сформированный конструктором файл кода **ValueButton.Designer.vb**. Откройте этот файл в **редакторе кода**.  
  
6. Найдите `Class` инструкции `Partial Public Class ValueButton`и измените тип, из которого наследуется этот элемент управления из <xref:System.Windows.Forms.UserControl> для <xref:System.Windows.Forms.Button>. Это позволяет элементу управления унаследовать все функции из <xref:System.Windows.Forms.Button> элемента управления.  
  
7. Найдите `InitializeComponent` метод и удалить строку, назначающую <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> свойство. Это свойство не существует в <xref:System.Windows.Forms.Button> элемента управления.  
  
8. Сохраните проект, выбрав в меню **Файл** команду **Сохранить все**.  
  
     Обратите внимание, что визуальный конструктор больше не доступен. Так как <xref:System.Windows.Forms.Button> элемент управления имеет собственное оформление, вы не сможете изменить его внешний вид в конструкторе. Визуальное представление будет иметь точно так же, как он наследует от класса (то есть <xref:System.Windows.Forms.Button>) Если изменения в код.  
  
> [!NOTE]
>  В область конструктора по-прежнему можно добавлять компоненты, не имеющие элементов пользовательского интерфейса.  
  
## <a name="adding-a-property-to-your-inherited-control"></a>Добавление свойства в наследуемый элемент управления  
 Один из возможных способов использования наследуемых элементов управления форм Windows Forms — это создание элементов управления, имеющих такой же внешний вид и функции, как у стандартных элементов управления Windows Forms, но предоставляющих настраиваемые свойства. В этом разделе вы добавите в элемент управления свойство с именем `ButtonValue`.  
  
#### <a name="to-add-the-value-property"></a>Добавьте значение свойства  
  
1. В **обозревателе решений** щелкните правой кнопкой мыши **ValueButton.vb** и выберите в контекстном меню пункт **Просмотреть код**.  
  
2. Найдите оператор `Public Class ValueButton`. Под открывающей скобкой этого оператора введите следующий код.  
  
    ```vb  
    ' Creates the private variable that will store the value of your   
    ' property.  
    Private varValue as integer  
    ' Declares the property.  
    Property ButtonValue() as Integer  
    ' Sets the method for retrieving the value of your property.  
       Get  
          Return varValue  
       End Get  
    ' Sets the method for setting the value of your property.  
       Set(ByVal Value as Integer)  
          varValue = Value  
       End Set  
    End Property  
    ```  
  
     Этот код определяет методы хранения и извлечения свойства `ButtonValue`. Оператор `Get` определяет значение, возвращаемое значению, которое хранится в закрытой переменной `varValue`, а оператор `Set` задает значение закрытой переменной с помощью ключевого слова `Value`.  
  
3. Сохраните проект, выбрав в меню **Файл** команду **Сохранить все**.  
  
## <a name="testing-your-control"></a>Тестирование элемента управления  
 Элементы управления не являются автономными проектами и должны размещаться в контейнере. Чтобы протестировать элемент управления, необходимо предоставить тестовый проект, в котором он будет выполняться. Кроме того, нужно сделать элемент управления доступным для тестового проекта, выполнив сборку (компиляцию). В этом разделе вы выполните сборку элемента управления и протестируете его в Windows Forms.  
  
#### <a name="to-build-your-control"></a>Сборка элемента управления  
  
1. В меню **Сборка** выберите **Собрать решение**.  
  
     Сборка должна быть выполнена без ошибок компилятора и предупреждений.  
  
#### <a name="to-create-a-test-project"></a>Создание тестового проекта  
  
1. В меню **Файл** наведите указатель мыши на пункт **Добавить** и выберите **Проект**, чтобы открыть диалоговое окно **Добавление нового проекта**.  
  
2. Выберите узел проектов Visual Basic и нажмите кнопку **приложение Windows Forms**.  
  
3. В поле **Имя файла** введите `Test`.  
  
4. В **обозревателе решений** нажмите кнопку **Показать все файлы**.  
  
5. В **обозревателе решений** щелкните узел **Ссылки** для тестового проекта правой кнопкой мыши и выберите в контекстном меню пункт **Добавить ссылку**, чтобы открыть диалоговое окно **Добавление ссылки**.  
  
6. Щелкните вкладку **Проекты**.  
  
7. Выберите вкладку **Проекты**. Проект `ValueButtonLib` будет указан под полем **Имя проекта**. Дважды щелкните проект, чтобы добавить ссылку на тестовый проект.  
  
8. В **обозревателе решений** щелкните **Тест** правой кнопкой мыши и выберите пункт **Построить**.  
  
#### <a name="to-add-your-control-to-the-form"></a>Добавление элемента управления в форму  
  
1. В **обозревателе решений** щелкните правой кнопкой мыши файл **Form1.vb** и выберите в контекстном меню пункт **Конструктор представлений**.  
  
2. На **панели элементов** выберите **Компоненты ValueButtonLib**. Дважды щелкните **ValueButton**.  
  
     Объект **ValueButton** появится в форме.  
  
3. Щелкните **ValueButton** правой кнопкой мыши и выберите в контекстном меню пункт **Свойства**.  
  
4. В окне **Свойства** проверьте свойства этого элемента управления. Обратите внимание, что они идентичны свойствам стандартной кнопки, кроме дополнительного свойства `ButtonValue`.  
  
5. Задайте для свойства `ButtonValue` значение `5`.  
  
6. На **все формы Windows Forms** вкладке **элементов**, дважды щелкните **метка** добавление <xref:System.Windows.Forms.Label> форму элемента управления.  
  
7. Переместите метку в центр формы.  
  
8. Дважды щелкните файл `ValueButton1`.  
  
     В **редакторе кода** откроется событие `ValueButton1_Click`.  
  
9. Введите следующую строку кода.  
  
    ```vb  
    Label1.Text = CStr(ValueButton1.ButtonValue)  
    ```  
  
10. В **обозревателе решений** щелкните **Тест** правой кнопкой мыши и выберите в контекстном меню команду **Назначить автозагружаемым проектом**.  
  
11. В меню **Отладка** выберите пункт **Начать отладку**.  
  
     Появится `Form1`.  
  
12. Нажмите кнопку `Valuebutton1`.  
  
     В `Label1` появится цифра 5, показывающая, что свойство `ButtonValue` унаследованного элемента управления передано `Label1` с помощью метода `ValueButton1_Click`. Таким образом, ваш элемент управления `ValueButton` наследует функциональные возможности стандартной кнопки Windows Forms и при этом предоставляет дополнительное настраиваемое свойство.  
  
## <a name="see-also"></a>См. также

- [Пошаговое руководство: Создание составного элемента управления с помощью Visual Basic](walkthrough-authoring-a-composite-control-with-visual-basic.md)
- [Практическое руководство. Отображение элемента управления в Выбор элементов панели элементов-диалоговое окно](how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)
- [Разработка пользовательских элементов управления Windows Forms в .NET Framework](developing-custom-windows-forms-controls.md)
- [Основы наследования (Visual Basic)](~/docs/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
