---
title: События изменения свойств
ms.date: 03/30/2017
helpviewer_keywords:
- dependency properties [WPF], change events
- property value changes [WPF]
- change events [WPF], property
- events [WPF], change in property values
- creating property triggers [WPF]
- property change events [WPF], types of
- property change events [WPF]
- property triggers [WPF]
- identifying changed property events [WPF]
- property triggers [WPF], definition of
ms.assetid: 0a7989df-9674-4cc1-bc50-5d8ef5d9c055
ms.openlocfilehash: b6f625f76e230b7d6bf0488bfa75c227de31a5d0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62030307"
---
# <a name="property-change-events"></a>События изменения свойств
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] определяет несколько событий, которые возникают в ответ на изменение значения свойства. Часто этим свойством является свойство зависимостей. Самим событием иногда является перенаправляемое событие, а иногда — стандартное событие [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]. Определение события зависит от сценария, так как некоторые изменения свойств лучше перенаправлять через дерево элементов, тогда как другие в основном влияют только на объект, в котором это свойство изменено.  
  
## <a name="identifying-a-property-change-event"></a>Определение события изменения свойства  
 Не все события, сообщающие об изменении свойства, явным образом определяются как событие изменения свойства на основании шаблона сигнатуры или именования. Как правило, в описании события в документации [!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] указывается, связано ли событие непосредственно с изменением значения свойства, и предоставляются перекрестные ссылки между свойством и событием.  
  
### <a name="routedpropertychanged-events"></a>События RoutedPropertyChanged  
 Некоторые события используют тип данных события и делегат, которые явно используются для событий изменения свойств. Тип данных события является <xref:System.Windows.RoutedPropertyChangedEventArgs%601>, а делегатом — <xref:System.Windows.RoutedPropertyChangedEventHandler%601>. Данные события и делегат имеют параметр универсального типа, который используется для указания фактического типа изменяющегося свойства при определении обработчика. Данные события содержат два свойства <xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A> и <xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>, который затем передаются как аргумент типа событий данных.  
  
 "Перенаправляемая" часть имени указывает, что событие изменения свойства зарегистрировано как перенаправляемое событие. Преимуществом перенаправления события изменения свойства является то, что верхний уровень элемента управления может получать события изменения свойств, если свойства дочерних элементов (составные части элемента управления) изменяют значения. Например, можно создать элемент управления, который включает в себя <xref:System.Windows.Controls.Primitives.RangeBase> элементов управления, такие как <xref:System.Windows.Controls.Slider>. Если значение <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> изменения свойств в части ползунка, может потребоваться обработка этого изменения в родительском элементе управления, а не на части.  
  
 Поскольку имеется старое и новое значение, то может казаться заманчивым использовать этот обработчик событий в качестве проверяющего элемента управления для значения свойства. Однако большинство событий изменения свойств создается не для этого. Как правило, предоставляются значения, на основе которых можно действовать в других логических областях кода, но на самом деле изменение значений из обработчика событий не рекомендуется и может привести к непреднамеренной рекурсии в зависимости от реализации обработчика.  
  
 Если свойство является пользовательское свойство зависимости, или вы работаете с производным классом где определен код создания экземпляра, существует гораздо лучший механизм отслеживания изменений свойств, встроенной в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] системы свойств: обратные вызовы системы свойств <xref:System.Windows.CoerceValueCallback> и <xref:System.Windows.PropertyChangedCallback>. Дополнительные сведения об использовании системы свойств [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] для проверки и приведения см. в разделах [Проверка и обратные вызовы свойства зависимостей](dependency-property-callbacks-and-validation.md) и [Пользовательские свойства зависимостей](custom-dependency-properties.md).  
  
### <a name="dependencypropertychanged-events"></a>События DependencyPropertyChanged  
 Другая пара типов, которые являются частью сценария события изменения свойств является <xref:System.Windows.DependencyPropertyChangedEventArgs> и <xref:System.Windows.DependencyPropertyChangedEventHandler>. События для этих изменений свойств не перенаправляются; это стандартные события [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]. <xref:System.Windows.DependencyPropertyChangedEventArgs> является типом отчетов, так как он является производным от данных необычные события <xref:System.EventArgs>; <xref:System.Windows.DependencyPropertyChangedEventArgs> — это структура, а не класс.  
  
 События, которые используют <xref:System.Windows.DependencyPropertyChangedEventArgs> и <xref:System.Windows.DependencyPropertyChangedEventHandler> немного более распространены, чем `RoutedPropertyChanged` события. Например, событие, которое использует эти типы <xref:System.Windows.UIElement.IsMouseCapturedChanged>.  
  
 Как и <xref:System.Windows.RoutedPropertyChangedEventArgs%601>, <xref:System.Windows.DependencyPropertyChangedEventArgs> также сообщает старое и новое значение для свойства. Аналогично это относится и к тому, что вы можете делать со значениями. Обычно не рекомендуется пытаться снова изменить значения в отправителе в ответ на это событие.  
  
## <a name="property-triggers"></a>Триггеры свойств  
 С событием изменения свойств тесно связана другая концепция — триггер свойств. Триггер свойств создается внутри стиля или шаблона и позволяет создавать условное поведение на основе значения свойства, которому назначается триггер.  
  
 У триггера свойств должно быть свойство зависимостей. Оно может быть (и часто является) свойством зависимостей только для чтения. Хорошим указанием на то, что свойство зависимостей, предоставляемое элементом управления, хотя бы частично разработано как триггер свойства, является Is в начале имени свойства. Свойства с таким именованием часто являются логическим свойством зависимостей только для чтения, а основной сценарий для свойства — предоставление состояния элемента управления, которое может иметь последствия для пользовательского интерфейса реального времени и, следовательно, является кандидатом на роль триггера свойств.  
  
 Некоторые из этих свойств также имеют специальное событие изменения свойства. Например, свойство <xref:System.Windows.UIElement.IsMouseCaptured%2A> имеет событие изменения свойства <xref:System.Windows.UIElement.IsMouseCapturedChanged>. Само свойство доступно только для чтения, его значение системой ввода, и система ввода создает <xref:System.Windows.UIElement.IsMouseCapturedChanged> при каждом изменении в режиме реального времени.  
  
 По сравнению с истинным событием изменения свойства, использование триггера свойств для реагирования на изменение свойства имеет некоторые ограничения.  
  
 Триггеры свойств работают через логику точного соответствия. Нужно указать свойство и конкретное значение, для которого будет срабатывать триггер. Например: `<Setter Property="IsMouseCaptured" Value="true"> ... </Setter>`. Из-за этого ограничения большая часть триггеров свойств будет использоваться для логических свойств или свойств, которые принимают определенное значение перечисления, когда возможный диапазон значений достаточно управляем, чтобы определить триггер для каждого случая. Триггеры свойств могут существовать только для специальных значений, например когда количество элементов достигает нуля, а также нет триггера, который учитывает случаи, когда значение свойства изменяется от нуля (вместо триггеров для всех случаев вам может понадобиться обработчик события кода или поведение по умолчанию, которое снова возвращается из состояния триггера, когда значение отлично от нуля).  
  
 Синтаксис триггера свойств аналогичен оператору if в программировании. Если условие триггера истинно, тогда "тело" триггера свойств "выполняется". "Тело" триггера свойств является не кодом, а разметкой. Разметка ограничена использованием одного или нескольких <xref:System.Windows.Setter> элементы для задания других свойств объекта, где применяется стиль или шаблон.  
  
 Чтобы сместить условие «if» триггера свойства, которое имеет широкий выбор возможных значений, обычно рекомендуется установить это же значение свойства по умолчанию с помощью <xref:System.Windows.Setter>. Таким образом, <xref:System.Windows.Trigger> метод задания будет иметь приоритет в случае, когда условие триггера истинно и <xref:System.Windows.Setter> , не находится в <xref:System.Windows.Trigger> , будет иметь приоритет всякий раз, когда условие триггера не выполняется.  
  
 Триггеры свойств, как правило, подходят для сценариев, в которых одно или несколько свойств Appearance должны изменяться в зависимости от состояния другого свойства в том же элементе.  
  
 Дополнительные сведения о триггерах свойств см. в разделе [Использование стилей и шаблонов](../controls/styling-and-templating.md).  
  
## <a name="see-also"></a>См. также

- [Общие сведения о перенаправленных событиях](routed-events-overview.md)
- [Общие сведения о свойствах зависимости](dependency-properties-overview.md)
