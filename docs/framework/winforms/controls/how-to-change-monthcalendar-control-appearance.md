---
title: Практическое руководство. Изменение внешнего вида элемента управления MonthCalendar в Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], calendar controls
- MonthCalendar control [Windows Forms], formatting display
ms.assetid: d09b95c9-e108-4608-9b31-b9100c0677bf
ms.openlocfilehash: 21fa6798c431b71d36c1909937ddad6bf5030782
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053092"
---
# <a name="how-to-change-the-windows-forms-monthcalendar-controls-appearance"></a>Практическое руководство. Изменение внешнего вида элемента управления MonthCalendar в Windows Forms
Windows Forms <xref:System.Windows.Forms.MonthCalendar> элемент управления позволяет настраивать внешний вид календаря во многих отношениях. Например можно установить цветовую схему и выберите для отображения или скрытия номеров недель или текущей даты.  
  
### <a name="to-change-the-month-calendars-color-scheme"></a>Чтобы изменить цветовую схему месячный календарь  
  
- Задать такие свойства как <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A> и <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A>. <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A> Также определяет цвет шрифта для дней недели. <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> Свойство определяет цвет дат, которые предшествуют и следуют за месяц, отображаемый или месяцев.  
  
    ```vb  
    MonthCalendar1.TitleBackColor = System.Drawing.Color.Blue  
    MonthCalendar1.TrailingForeColor = System.Drawing.Color.Red  
    MonthCalendar1.TitleForeColor = System.Drawing.Color.Yellow  
    ```  
  
    ```csharp  
    monthCalendar1.TitleBackColor = System.Drawing.Color.Blue;  
    monthCalendar1.TrailingForeColor = System.Drawing.Color.Red;  
    monthCalendar1.TitleForeColor = System.Drawing.Color.Yellow;  
    ```  
  
    ```cpp  
    monthCalendar1->TitleBackColor = System::Drawing::Color::Blue;  
    monthCalendar1->TrailingForeColor = System::Drawing::Color::Red;  
    monthCalendar1->TitleForeColor = System::Drawing::Color::Yellow;  
    ```  
  
    > [!NOTE]
    >  Начиная с Windows Vista и в зависимости от темы, настроить некоторые параметры могут не изменяться внешний вид календаря. Например, если Windows настроен на использование темы Aero, установка <xref:System.Windows.Forms.MonthCalendar.BackColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A>, или <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> свойства не влияет. Это обусловлено обновленную версию календаря визуализируется с внешний вид, который является производным от текущей темы операционной системы во время выполнения. Если вы хотите использовать эти свойства и включить более раннюю версию календаря, можно отключить визуальные стили для приложения. Отключение визуальных стилей может повлиять на внешний вид и поведение других элементов управления в приложении. Чтобы отключить визуальные стили в Visual Basic, откройте конструктор проектов и снимите флажок **включить визуальные стили XP** "флажок". Чтобы отключить визуальные стили в C#, откройте файл Program.cs и закомментируйте `Application.EnableVisualStyles();`. Дополнительные сведения о стилях см. в разделе [включения визуальных стилей](/windows/desktop/controls/cookbook-overview).  
  
### <a name="to-display-the-current-date-at-the-bottom-of-the-control"></a>Чтобы отобразить текущую дату в нижней части элемента управления  
  
- Задайте для свойства <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> значение `true`. В приведенном ниже примере переключение между отображением и скрытием текущей даты, когда форма будет выполнен двойной щелчок.  
  
    ```vb  
    Private Sub Form1_DoubleClick(ByVal sender As Object, _  
    ByVal e As System.EventArgs) Handles MyBase.DoubleClick  
       ' Toggle between True and False.  
       MonthCalendar1.ShowToday = Not MonthCalendar1.ShowToday  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_DoubleClick(object sender, System.EventArgs e)  
    {  
       // Toggle between True and False.  
       monthCalendar1.ShowToday = !monthCalendar1.ShowToday;  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void Form1_DoubleClick(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // Toggle between True and False.  
          monthCalendar1->ShowToday = !monthCalendar1->ShowToday;  
       }  
    ```  
  
     (Visual C#, Visual C++) Поместите следующий код в конструктор формы для регистрации обработчика событий.  
  
    ```csharp  
    this.DoubleClick += new System.EventHandler(this.Form1_DoubleClick);  
    ```  
  
    ```cpp  
    this->DoubleClick += gcnew System::EventHandler(this,  
       &Form1::Form1_DoubleClick);  
    ```  
  
### <a name="to-display-week-numbers"></a>Для отображения номера недель  
  
- Задайте для свойства <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> значение `true`. Это свойство можно задать в коде или в окне «Свойства».  
  
     Номера недель отображаются в отдельном столбце слева от первого дня недели.  
  
    ```vb  
    MonthCalendar1.ShowWeekNumbers = True  
    ```  
  
    ```csharp  
    monthCalendar1.ShowWeekNumbers = true;  
    ```  
  
    ```cpp  
    monthCalendar1->ShowWeekNumbers = true;  
    ```  
  
## <a name="see-also"></a>См. также

- [Элемент управления MonthCalendar](monthcalendar-control-windows-forms.md)
- [Практическое руководство. Выбор диапазона дат в элементе управления Windows Forms MonthCalendar](how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)
- [Практическое руководство. Отображение определенных дней полужирным шрифтом с Windows Forms в элементе управления MonthCalendar](display-specific-days-in-bold-with-wf-monthcalendar-control.md)
- [Практическое руководство. Отображение более чем одного месяца в элементе управления Windows Forms MonthCalendar](display-more-than-one-month-wf-monthcalendar-control.md)
