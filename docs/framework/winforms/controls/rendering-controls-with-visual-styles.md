---
title: Отрисовка элементов управления с применением визуальных стилей
ms.date: 03/30/2017
helpviewer_keywords:
- professional appearance [Windows Forms], rendering Windows Forms controls
- themes [Windows Forms], XP visual styles in Window Forms
- custom controls [Windows Forms], rendering
- custom controls [Windows Forms], painting
- visual themes [Windows Forms], rendering Windows Forms controls
- user controls [Windows Forms], painting
- visual styles [Windows Forms], rendering Windows Forms controls
ms.assetid: a5b178ba-610e-46c4-a6c0-509c0886a744
ms.openlocfilehash: 4dbccfc881e777309394aed9711a93b8a25315be
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592604"
---
# <a name="rendering-controls-with-visual-styles"></a>Отрисовка элементов управления с применением визуальных стилей
.NET Framework обеспечивает поддержку для отрисовки элементов управления и других Windows элементы интерфейса (UI), с использованием стилей оформления в операционных системах, которые их поддерживают. В этом разделе описано несколько уровней поддержки в .NET Framework для отрисовки элементов управления и других элементов пользовательского интерфейса с учетом текущего визуального стиля операционной системы.  
  
## <a name="rendering-classes-for-common-controls"></a>Классы отрисовки для общих элементов управления  
 Отрисовкой элемента управления называется рисование пользовательского интерфейса для элемента управления. Пространство имен <xref:System.Windows.Forms?displayProperty=nameWithType> предоставляет класс <xref:System.Windows.Forms.ControlPaint> для отрисовки некоторых общих элементов управления Windows Forms. Однако этот класс рисует элементы управления в классическом стиле Windows, что может затруднять обеспечение согласованности пользовательского интерфейса при рисовании пользовательских элементов управления в приложениях с включенными стилями оформления.  
  
 [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] включает классы в пространство имен <xref:System.Windows.Forms?displayProperty=nameWithType> , которое отрисовывает части и состояния общих элементов управления с применением стилей оформления. Каждый из этих классов содержит методы `static` для рисования элемента управления или его частей в определенном состоянии с использованием текущего стиля оформления операционной системы.  
  
 Некоторые из этих классов предназначены для рисования связанного элемента управления независимо от доступности стилей оформления. Если стили оформления включены, элементы класса будут рисовать связанный элемент управления с применением стилей оформления. Если стили оформления отключены, элементы класса будет рисовать элемент управления в классическом стиле Windows. К таким классам относятся следующие:  
  
- <xref:System.Windows.Forms.ButtonRenderer>  
  
- <xref:System.Windows.Forms.CheckBoxRenderer>  
  
- <xref:System.Windows.Forms.GroupBoxRenderer>  
  
- <xref:System.Windows.Forms.RadioButtonRenderer>  
  
 Другие классы могут нарисовать связанный элемент управления только при доступных стилях оформления, в противном случае их элементы выдают исключение. К таким классам относятся следующие:  
  
- <xref:System.Windows.Forms.ComboBoxRenderer>  
  
- <xref:System.Windows.Forms.ProgressBarRenderer>  
  
- <xref:System.Windows.Forms.ScrollBarRenderer>  
  
- <xref:System.Windows.Forms.TabRenderer>  
  
- <xref:System.Windows.Forms.TextBoxRenderer>  
  
- <xref:System.Windows.Forms.TrackBarRenderer>  
  
 Дополнительные сведения об использовании этих классов для рисования элемента управления, см. в разделе [как: Использование класса отрисовки элемента управления](how-to-use-a-control-rendering-class.md).  
  
## <a name="visual-style-element-and-rendering-classes"></a>Элемент стиля оформления и классы отрисовки  
 Пространство имен <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> содержит классы, которые можно использовать для рисования любого элемента управления или элемента пользовательского интерфейса, поддерживаемого стилями оформления, и получения сведений о нем. К поддерживаемым элементам управления относятся общие элементы управления с классом отрисовки в пространстве имен <xref:System.Windows.Forms?displayProperty=nameWithType> (см. предыдущий раздел), а также другие элементы управления, такие как элементы управления "Вкладка" и элементы управления "Главная панель". В число других поддерживаемых элементов пользовательского интерфейса входят части меню **Пуск** , панели инструментов и неклиентской области окон.  
  
 Главными классами пространства имен <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> являются <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> и <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer>. <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> — это класс платформы для идентификации любого элемента управления или элемента пользовательского интерфейса, поддерживаемого стилями оформления. В дополнение к самому <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> пространство имен <xref:System.Windows.Forms.VisualStyles?displayProperty=nameWithType> содержит много вложенных классов <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> со свойствами `static` , которые возвращают <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> для каждого состояния элемента управления, части элемента управления или другого элемента пользовательского интерфейса, поддерживаемого стилями оформления.  
  
 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> предоставляет методы для рисования каждого <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> , определяемого текущим стилем оформления операционной системы, и получения сведений о нем. Сведения, которые можно получить об элементе, включают его размер по умолчанию, тип фона и определения цвета. <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> использует программу-оболочку для функций API стилей оформления (UxTheme) из части оболочки Windows пакета SDK платформы Windows. Дополнительные сведения см. в разделе [включения визуальных стилей](/windows/desktop/controls/cookbook-overview).  
  
 Дополнительные сведения об использовании <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> и <xref:System.Windows.Forms.VisualStyles.VisualStyleElement>, см. в разделе [как: Элемент визуального стиля отрисовки](how-to-render-a-visual-style-element.md).  
  
## <a name="enabling-visual-styles"></a>Включение стилей оформления  
 Чтобы включить визуальные стили для приложения, написанного для платформы .NET Framework версии 1.0, программистам следует включить манифест приложения, которое указывает, что для рисования элементов управления будет использоваться ComCtl32.dll версии 6 или более поздней версии. Приложения, созданные с помощью .NET Framework версии 1.1 или более поздней, могут использовать <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> метод <xref:System.Windows.Forms.Application> класса.  
  
## <a name="checking-for-visual-styles-support"></a>Проверка поддержки стилей оформления  
 Свойство <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> класса <xref:System.Windows.Forms.Application> указывает, будет ли текущее приложение рисовать элементы управления с помощью стилей оформления. При рисовании пользовательского элемента управления можно проверить значение <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> , чтобы определить, следует ли учитывать стили оформления при отрисовке элемента управления. В следующей таблице перечислены четыре условия, которые должны выполняться, чтобы <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A> возвратил `true`.  
  
|Условие|Примечания|  
|---------------|-----------|  
|Операционная система поддерживает стили оформления.|Чтобы проверить это условие отдельно, используйте свойство <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsSupportedByOS%2A> класса <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation> .|  
|Пользователь включил стили оформления в операционной системе.|Чтобы проверить это условие отдельно, используйте свойство <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation.IsEnabledByUser%2A> класса <xref:System.Windows.Forms.VisualStyles.VisualStyleInformation> .|  
|Стили оформления включены в приложении.|Стили оформления можно включить в приложении, вызвав метод <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> или воспользовавшись манифестом приложения, указывающим, что для рисования элементов управления будет применяться ComCtl32.dll версии 6 или более поздней.|  
|Стили оформления используются для рисования клиентской области окон приложений.|Чтобы проверить это условие отдельно, используйте свойство <xref:System.Windows.Forms.Application.VisualStyleState%2A> класса <xref:System.Windows.Forms.Application> и убедитесь, что оно имеет значение <xref:System.Windows.Forms.VisualStyles.VisualStyleState.ClientAreaEnabled?displayProperty=nameWithType> или <xref:System.Windows.Forms.VisualStyles.VisualStyleState.ClientAndNonClientAreasEnabled?displayProperty=nameWithType>.|  
  
 Чтобы определить, когда пользователь включает или отключает стили оформления или переключается между ними, проверьте наличие значения <xref:Microsoft.Win32.UserPreferenceCategory.VisualStyle?displayProperty=nameWithType> в обработчиках для событий <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging?displayProperty=nameWithType> или <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged?displayProperty=nameWithType> .  
  
> [!IMPORTANT]
>  Если вы хотите использовать <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> для отрисовки элемента управления или элемента пользовательского интерфейса, когда пользователь включает стили оформления или переключается между ними, это нужно сделать при обработке события <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanged> вместо <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging> . Если вы используете класс <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> при обработке <xref:Microsoft.Win32.SystemEvents.UserPreferenceChanging>, возникнет исключение.  
  
## <a name="see-also"></a>См. также

- [Рисование и отрисовка пользовательского элемента управления](custom-control-painting-and-rendering.md)
