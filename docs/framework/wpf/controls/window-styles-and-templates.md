---
title: Стили и шаблоны элемента Window
ms.date: 03/30/2017
helpviewer_keywords:
- parts [WPF], Window
- templates [WPF], Window
- styles [WPF], Window
- ControlTemplate [WPF], Window
- Window [WPF], styles and templates
- states [WPF], Window
ms.assetid: 2dfdf025-347b-4342-bf28-95206c273f35
ms.openlocfilehash: ebd21829591b8fefe87aeba0b86280f18eff4f06
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62023836"
---
# <a name="window-styles-and-templates"></a>Стили и шаблоны элемента Window
В этом разделе описываются стили и шаблоны для <xref:System.Windows.Window> элемента управления. Вы можете изменить значение по умолчанию <xref:System.Windows.Controls.ControlTemplate> предоставить уникальный внешний вид элемента управления. Подробнее см. в разделе [Настройка внешнего вида существующего элемента управления путем создания объекта ControlTemplate](customizing-the-appearance-of-an-existing-control.md).  
  
## <a name="window-parts"></a>Элементы окна  
 <xref:System.Windows.Window> Управления не имеет частей с именами.  
  
## <a name="window-states"></a>Состояния окна  
 В следующей таблице перечислены визуальные состояния <xref:System.Windows.Window> элемента управления.  
  
|Имя VisualState|Имя VisualStateGroup|Описание|  
|-|-|-|  
|Valid|ValidationStates|Элемент управления использует <xref:System.Windows.Controls.Validation> класс и <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> присоединенное свойство `false`.|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Присоединенное свойство `true` имеет элемент управления имеет фокус.|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> Присоединенное свойство `true` имеет элемент управления не имеет фокуса.|  
  
## <a name="window-controltemplate-example"></a>Пример шаблона элемента управления окна  
 В следующем примере показано определение <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Window> элемента управления.  
  
 [!code-xaml[ControlTemplateExamples#Window](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/window.xaml#window)]  
  
 <xref:System.Windows.Controls.ControlTemplate> Использует один или несколько из следующих ресурсов.  
  
 [!code-xaml[ControlTemplateExamples#ResizeGrip](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/resizegrip.xaml#resizegrip)]  
[!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Полный пример см. в разделе [Пример задания стиля с помощью ControlTemplates](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating).  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [Стили и шаблоны элемента управления](control-styles-and-templates.md)
- [Настройка элементов управления](control-customization.md)
- [Стилизация и использование шаблонов](styling-and-templating.md)
- [Настройка внешнего вида существующего элемента управления путем создания объекта ControlTemplate](customizing-the-appearance-of-an-existing-control.md)
