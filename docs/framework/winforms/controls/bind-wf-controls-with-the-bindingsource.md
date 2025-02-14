---
title: Практическое руководство. Связывание элементов управления Windows Forms с компонентом BindingSource с помощью конструктора
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], binding
- BindingSource component [Windows Forms], binding controls
- data binding [Windows Forms], BindingSource component
ms.assetid: 391ae170-de5c-40f8-8233-91cb2ee4683a
ms.openlocfilehash: f8c268c816975fa9b00725d317365c147312b950
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593459"
---
# <a name="how-to-bind-windows-forms-controls-with-the-bindingsource-component-using-the-designer"></a>Практическое руководство. Связывание элементов управления Windows Forms с компонентом BindingSource с помощью конструктора
После добавления элементов управления в форму и определения пользовательского интерфейса для вашего приложения, можно привязать элементы управления к источнику данных, чтобы во время выполнения, пользователи могут изменять и сохранять данные, связанные с приложением.  
  
 Привязка одного или нескольких элементов управления в Windows Forms проще всего с помощью <xref:System.Windows.Forms.BindingSource> управления в качестве моста между элементов управления в форме и источником данных.  
  
 Один или несколько элементов управления в форме можно привязать к данным; в следующей процедуре <xref:System.Windows.Forms.TextBox> привязке элемента управления к источнику данных.  
  
 Чтобы завершить процедуру, предполагается, что будет привязан к источнику данных, производный от базы данных. Дополнительные сведения о создании источников данных из хранилищ данных, см. в разделе [добавляются новые источники данных](/visualstudio/data-tools/add-new-data-sources).  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в разделе [Персонализация интегрированной среды разработки Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-bind-a-control-at-design-time"></a>Для привязки элемента управления во время разработки  
  
1. Перетащите <xref:System.Windows.Forms.TextBox> элемента управления в форму.  
  
2. В **свойства** окна:  
  
    1. Разверните **(DataBindings)** узла.  
  
    2. Щелкните стрелку рядом с полем <xref:System.Windows.Forms.TextBox.Text%2A> свойство.  
  
         **DataSource** открывает редактор типов пользовательского интерфейса.  
  
         Если источник данных ранее был настроен для проекта или формы, он будет отображаться.  
  
3. Щелкните элемент **Добавить источник данных проекта**, чтобы подключиться к данным и создать источник данных.  
  
4. На странице приветствия **Мастер настройки источника данных** нажмите кнопку **Далее**.  
  
5. На **Выбор типа источника данных** выберите **базы данных**.  
  
6. На **Выбор подключения к данным** выберите подключение к данным из списка доступных подключений. Если необходимое подключение данных не доступны выберите **новое подключение** для создания нового подключения к данным.  
  
7. Выберите **Да, сохранить подключение** сохранить строку подключения в файле конфигурации приложения.  
  
8. Выберите объекты базы данных, чтобы перенести их в приложение. В этом случае выберите поле в таблице, в котором вы хотите <xref:System.Windows.Forms.TextBox> для отображения.  
  
9. Если необходимо, замените имя набора данных по умолчанию.  
  
10. Нажмите кнопку **Готово**.  
  
11. В **свойства** окно, щелкните стрелку рядом с полем <xref:System.Windows.Forms.TextBox.Text%2A> свойство еще раз. В **DataSource** редактора типов пользовательского интерфейса, выберите имя поля для привязки <xref:System.Windows.Forms.TextBox> для.  
  
     **DataSource** типа пользовательского интерфейса редактора закроется, а набор данных, <xref:System.Windows.Forms.BindingSource> и адаптер таблицы для что подключение к данным добавляются в форму.  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.BindingNavigator>
- [Добавление новых источников данных](/visualstudio/data-tools/add-new-data-sources)
- [Окно "Источники данных"](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/6ckyxa83(v=vs.120))
