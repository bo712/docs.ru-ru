---
title: Функциональная классификация элементов управления Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], by function
- Windows Forms, controls by function
- Windows Forms controls, list of
ms.assetid: 5e65a6c3-5d6f-480d-beb8-b28f865f07e3
ms.openlocfilehash: 3a82642c985b7ec1cee885cdda7b054adbe3dfee
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61969472"
---
# <a name="windows-forms-controls-by-function"></a>Функциональная классификация элементов управления Windows Forms
Windows Forms предоставляет элементы управления и компоненты, которые выполняют несколько функций. Ниже перечислены элементы управления Windows Forms и компоненты в соответствии с основной функцией. Кроме того Если существуют несколько элементов управления, которые выполняют одинаковую функцию, рекомендуемый элемент управления отображается с примечание, касающееся элемент управления, который он заменен. В отдельной таблице с их рекомендуемые замены перечислены устаревшие элементы управления.  
  
> [!NOTE]
>  В следующих таблицах перечислены не в случае, каждый элемент управления или компонента, которые можно использовать в Windows Forms; более полный список, см. в разделе [элементы управления для использования в формах Windows Forms](controls-to-use-on-windows-forms.md)  
  
## <a name="recommended-controls-and-components-by-function"></a>Рекомендуемые элементы управления и компоненты по функциям  
  
|Функция|Элемент управления|Описание|  
|--------------|-------------|-----------------|  
|Отображение данных|Элемент управления <xref:System.Windows.Forms.DataGridView>|<xref:System.Windows.Forms.DataGridView> Управления предоставляет настраиваемую таблицу для отображения данных. <xref:System.Windows.Forms.DataGridView> Класс обеспечивает возможность настройки ячеек, строк, столбцов и границ. **Примечание.**  <xref:System.Windows.Forms.DataGridView> Элемент управления предоставляет множество основных и дополнительных компонентов, отсутствующих в <xref:System.Windows.Forms.DataGrid> элемента управления. Дополнительные сведения см. в разделе [различия между Windows Forms DataGridView и DataGrid-элементы управления](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)|  
|Привязка данных и навигации|<xref:System.Windows.Forms.BindingSource> |Упрощает привязку элементов управления в форме к данным за счет управления валюты, уведомления об изменениях и другие службы.|  
||Элемент управления <xref:System.Windows.Forms.BindingNavigator>|Предоставляет интерфейс тип панели инструментов для работы с данными в форме.|  
|Редактирование текста|Элемент управления <xref:System.Windows.Forms.TextBox>|Отображает текст, введенный во время разработки, который может редактироваться пользователями во время выполнения или изменяться программно.|  
||Элемент управления <xref:System.Windows.Forms.RichTextBox>|Позволяет текста, отображаемого с форматированием в виде обычного текста или rich text format (RTF).|  
||Элемент управления <xref:System.Windows.Forms.MaskedTextBox>|Ограничивает формат вводимых пользователем данных|  
|Отображение информации (только для чтения)|Элемент управления <xref:System.Windows.Forms.Label>|Отображает текст, недоступный для непосредственного изменения пользователем.|  
||Элемент управления <xref:System.Windows.Forms.LinkLabel>|Отображает текст в виде веб-ссылки и вызывает событие, когда пользователь щелкает этот текст. Обычно текст является ссылкой на другое окно или веб-сайта.|  
||Элемент управления <xref:System.Windows.Forms.StatusStrip>|Отображает сведения о текущем состоянии приложения в рамках области обычно в нижней части родительской формы.|  
||Элемент управления <xref:System.Windows.Forms.ProgressBar>|Отображает текущее состояние операции для пользователя.|  
|Отображение веб-страницы|Элемент управления <xref:System.Windows.Forms.WebBrowser>|Предоставляет пользователю возможность осуществлять навигацию по веб-страницам внутри формы.|  
|Выбор из списка|Элемент управления <xref:System.Windows.Forms.CheckedListBox>|Отображает прокручиваемый список элементов с флажками.|  
||Элемент управления <xref:System.Windows.Forms.ComboBox>|Отображает список элементов раскрывающегося списка.|  
||Элемент управления <xref:System.Windows.Forms.DomainUpDown>|Отображение списка текстовых элементов, который можно прокручивать с помощью кнопок со стрелками.|  
||Элемент управления <xref:System.Windows.Forms.ListBox>|Отображает список текстовых и графических элементов (значки).|  
||Элемент управления <xref:System.Windows.Forms.ListView>|Отображает элементы в одном из четырех различных представлений. Включает в себя только текст, текст с маленькими значками, текст с крупные значки и представление сведений.|  
||Элемент управления <xref:System.Windows.Forms.NumericUpDown>|Отображение списка чисел, который можно прокручивать с помощью кнопок со стрелками.|  
||Элемент управления <xref:System.Windows.Forms.TreeView>|Отображает иерархическую коллекцию объектов-узлов, которые могут включать текст с помощью флажков и значков.|  
|Отображение графики|Элемент управления <xref:System.Windows.Forms.PictureBox>|Отображает графические файлы, например точечные рисунки и значки, в кадре.|  
|Хранение графики|Элемент управления <xref:System.Windows.Forms.ImageList>|Выступает в качестве репозитория для изображений. <xref:System.Windows.Forms.ImageList> элементы управления и образы, содержащиеся в них могут использоваться повторно из одного приложения к другому.|  
|Значение параметра|Элемент управления <xref:System.Windows.Forms.CheckBox>|Отображает флажок и надпись для текста. Обычно используется для задания параметров.|  
||Элемент управления <xref:System.Windows.Forms.CheckedListBox>|Отображает прокручиваемый список элементов с флажками.|  
||Элемент управления <xref:System.Windows.Forms.RadioButton>|Отображает кнопку, можно включить или отключить.|  
||Элемент управления <xref:System.Windows.Forms.TrackBar>|Позволяет пользователям задавать значения на шкале, перемещая «ползунок» на шкале.|  
|Настройка даты|Элемент управления <xref:System.Windows.Forms.DateTimePicker>|Отображает графический календарь, позволяющий пользователю выбрать дату или время.|  
||Элемент управления <xref:System.Windows.Forms.MonthCalendar>|Отображает графический календарь, чтобы разрешить пользователям выбирать диапазон дат.|  
|Диалоговые окна|Элемент управления <xref:System.Windows.Forms.ColorDialog>|Отображает диалоговое окно выбора цвета, позволяющего задать цвет элемента интерфейса.|  
||Элемент управления <xref:System.Windows.Forms.FontDialog>|Отображает диалоговое окно, которое позволяет задавать шрифт и его атрибуты.|  
||Элемент управления <xref:System.Windows.Forms.OpenFileDialog>|Отображает диалоговое окно, которое позволяет пользователям перейдите и выберите файл.|  
||Элемент управления <xref:System.Windows.Forms.PrintDialog>|Отображает диалоговое окно, которое позволяет пользователям выбирать принтер и задайте его атрибуты.|  
||Элемент управления <xref:System.Windows.Forms.PrintPreviewDialog>|Отображает диалоговое окно, которое отображается как элемент управления <xref:System.Drawing.Printing.PrintDocument> компонент будет выглядеть при печати.|  
||Элемент управления <xref:System.Windows.Forms.FolderBrowserDialog>|Отображает диалоговое окно, в котором пользователи могут просматривать, создавать и выбора папки.|  
||Элемент управления <xref:System.Windows.Forms.SaveFileDialog>|Отображает диалоговое окно, которое позволяет пользователю сохранить файл.|  
|Элементы управления меню|Элемент управления <xref:System.Windows.Forms.MenuStrip>|Создание пользовательских меню. **Примечание.**  <xref:System.Windows.Forms.MenuStrip> Предназначен для замены <xref:System.Windows.Forms.MainMenu> элемента управления.|  
||Элемент управления <xref:System.Windows.Forms.ContextMenuStrip>|Создание пользовательского контекстного меню. **Примечание.**  <xref:System.Windows.Forms.ContextMenuStrip> Предназначен для замены <xref:System.Windows.Forms.ContextMenu> элемента управления.|  
|Команды|Элемент управления <xref:System.Windows.Forms.Button>|Запускает, останавливает или прерывания процесса.|  
||Элемент управления <xref:System.Windows.Forms.LinkLabel>|Отображает текст в виде веб-ссылки и вызывает событие, когда пользователь щелкает этот текст. Обычно текст является ссылкой на другое окно или веб-сайта.|  
||Элемент управления <xref:System.Windows.Forms.NotifyIcon>|Отображает значок в области уведомлений панели задач, который представляет приложение, работающее в фоновом режиме.|  
||Элемент управления <xref:System.Windows.Forms.ToolStrip>|Создание панелей инструментов, которые могут иметь Microsoft Windows XP, Microsoft Office, Microsoft Internet Explorer или пользовательский интерфейс, с или без темы и поддержка переполнения и переупорядочения элементов во время выполнения. **Примечание.**  <xref:System.Windows.Forms.ToolStrip> Элемент управления предназначен для замены <xref:System.Windows.Forms.ToolBar> элемента управления.|  
|Справка по пользовательскому|<xref:System.Windows.Forms.HelpProvider> |Обеспечивает для элементов управления всплывающее окно справки или окно оперативной справки.|  
||<xref:System.Windows.Forms.ToolTip> |Предоставляет всплывающее окно, которое отображает краткое описание назначения элемента управления при наведении указателя мыши на элементе управления.|  
|Группировки других элементов управления|Элемент управления <xref:System.Windows.Forms.Panel>|Группирует набор элементов управления в прокручиваемый фрейм без подписи.|  
||Элемент управления <xref:System.Windows.Forms.GroupBox>|Группирует набор элементов управления (например, переключателей) в непрокручиваемый фрейм.|  
||Элемент управления <xref:System.Windows.Forms.TabControl>|Предоставляет страницы с вкладками для организации и доступ к сгруппированные объекты эффективно.|  
||Элемент управления <xref:System.Windows.Forms.SplitContainer>|Предоставляет две панели, разделенных подвижной строки. **Примечание.**  <xref:System.Windows.Forms.SplitContainer> Элемент управления предназначен для замены <xref:System.Windows.Forms.Splitter> элемента управления.|  
||Элемент управления <xref:System.Windows.Forms.TableLayoutPanel>|Представляет панель, в которой содержимое динамически отображается в сетке, состоящей из строк и столбцов.|  
||Элемент управления <xref:System.Windows.Forms.FlowLayoutPanel>|Представляет панель, которая динамически располагает содержимое по горизонтали или вертикали.|  
|Звук|Элемент управления <xref:System.Media.SoundPlayer>|Воспроизводит звук в формате WAV. Звуки можно загружать и воспроизводить асинхронно.|  
  
## <a name="superseded-controls-and-components-by-function"></a>Устаревшие элементы управления и компоненты по функциям  
  
|Функция|Устаревший элемент управления|Рекомендуется на замену|  
|--------------|------------------------|-----------------------------|  
|Отображение данных|<xref:System.Windows.Forms.DataGrid>|<xref:System.Windows.Forms.DataGridView>|  
|Отображение информации (только для чтения элементы управления)|<xref:System.Windows.Forms.StatusBar>|<xref:System.Windows.Forms.StatusStrip>|  
|Элементы управления меню|<xref:System.Windows.Forms.ContextMenu>|<xref:System.Windows.Forms.ContextMenuStrip>|  
||<xref:System.Windows.Forms.MainMenu>|<xref:System.Windows.Forms.MenuStrip>|  
|Команды|<xref:System.Windows.Forms.ToolBar>|<xref:System.Windows.Forms.ToolStrip>|  
||<xref:System.Windows.Forms.StatusBar>|<xref:System.Windows.Forms.StatusStrip>|  
|Макет формы|<xref:System.Windows.Forms.Splitter>|<xref:System.Windows.Forms.SplitContainer>|  
  
## <a name="see-also"></a>См. также

- [Элементы управления для использования в Windows Forms](controls-to-use-on-windows-forms.md)
- [Разработка пользовательских элементов управления Windows Forms в .NET Framework](developing-custom-windows-forms-controls.md)
