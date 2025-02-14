---
title: Свойства зависимости "только для чтения"
ms.date: 03/30/2017
helpviewer_keywords:
- dependency properties [WPF], read-only
- read-only dependency properties [WPF]
ms.assetid: f23d6ec9-3780-4c09-a2ff-b2f0a2deddf1
ms.openlocfilehash: 327897d50bd23a739d015a4151459d9d4a6fc1a0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64611798"
---
# <a name="read-only-dependency-properties"></a>Свойства зависимости "только для чтения"
В этом разделе описываются свойства зависимостей "только для чтения", включая существующие свойства зависимостей "только для чтения", а также сценарии и методы создания настраиваемого свойства зависимостей "только для чтения".  

<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Предварительные требования  
 В этом разделе предполагается, что вы понимаете основные сценарии реализации свойства зависимостей и способы применения метаданных к настраиваемому свойству зависимостей. Дополнительные сведения см. в разделах [Пользовательские свойства зависимостей](custom-dependency-properties.md) и [Метаданные свойства зависимостей](dependency-property-metadata.md).  
  
<a name="existing"></a>   
## <a name="existing-read-only-dependency-properties"></a>Существующие свойства зависимостей "только для чтения"  
 Некоторые свойства зависимостей, определенные в среде [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], доступны только для чтения. Типичной причиной для указания свойства зависимости "только для чтения" является то, что это свойства, которые должны использоваться для определения состояния там, где это состояние зависит от множества факторов, но простая настройка этого состояния для данного свойства нежелательна с точки зрения дизайна пользовательского интерфейса. Например, свойство <xref:System.Windows.UIElement.IsMouseOver%2A> действительно только отображает состояние, определяемое вводом с помощью мыши. Любая попытка установить это значение программно путем обхода истинного ввода с помощью мыши будет непредсказуемой и вызовет несогласованность.  
  
 Поскольку свойства зависимостей "только для чтения" нельзя устанавливать, они не подходят для многих сценариев, для которых свойства зависимостей обычно предлагают решение (а именно: привязка данных с возможностью прямого использования стилей для значения, проверки, анимации, наследования). Несмотря на то что их нельзя устанавливать, свойства зависимостей "только для чтения" обладают некоторыми дополнительными возможностями, которые поддерживаются свойствами зависимостей в системе свойств. Наиболее важной оставшейся возможностью является то, что свойство зависимости "только для чтения" по-прежнему можно использовать как триггер свойств в стиле. Невозможно включить триггеры с помощью обычного свойства [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]. Оно должно быть свойством зависимостей. Вышеупомянутое <xref:System.Windows.UIElement.IsMouseOver%2A> свойство является отличным примером сценария, в которых может оказаться весьма полезным определение стиля для элемента управления, в котором некоторые свойства visible, такие как фоновый рисунок, основной цвет или похожие свойства сложных элементов в элемент управления изменится, когда пользователь наведет указатель мыши на определенную область элемента управления. Изменения в свойстве зависимостей "только для чтения" также могут обнаруживаться и сообщаться внутренними процессами определения недействительности в системе свойств. Фактически, это внутренняя поддержка функциональности триггера свойств.  
  
<a name="new"></a>   
## <a name="creating-custom-read-only-dependency-properties"></a>Создание пользовательских свойств зависимостей "только для чтения"  
 Обязательно ознакомьтесь с вышеприведенным разделом, описывающим, почему свойства зависимостей "только для чтения" не будут работать для многих типичных сценариев свойств зависимостей. Однако при наличии соответствующего сценария можно создать собственное свойство зависимостей "только для чтения".  
  
 Большая часть процесса создания свойства зависимостей "только для чтения" аналогична описанному в разделах [Пользовательские свойства зависимостей](custom-dependency-properties.md) и [Реализация свойства зависимостей](how-to-implement-a-dependency-property.md). Однако есть три важных отличия.  
  
- При регистрации свойства следует вызвать <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A> вместо обычного метода <xref:System.Windows.DependencyProperty.Register%2A> метод для регистрации свойства.  
  
- При реализации свойства wrapper [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] убедитесь, что в программе-оболочке нет реализации set, и таким образом, отсутствует несогласованность в состоянии "только для чтения" для открытой программы-оболочки.  
  
- Объект, возвращаемый регистрацией только для чтения — <xref:System.Windows.DependencyPropertyKey> вместо <xref:System.Windows.DependencyProperty>. Необходимо сохранить это поле в качестве члена, но обычно не нужно его делать общим членом для типа.  
  
 Любое частное поле или значение, заложенное в свойство зависимостей "только для чтения", может быть полностью записываемым с помощью любой выбранной логики. Однако самый простой способ задать свойство либо изначально, либо в составе логики выполнения — это использовать [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] системы свойств, а не обходить систему свойств и настраивать частное резервное поле напрямую. В частности, имеется подпись <xref:System.Windows.DependencyObject.SetValue%2A> , принимающий параметр типа <xref:System.Windows.DependencyPropertyKey>. Как и где это значение программно в логике приложения повлияет на том, как вы можете установить доступ к <xref:System.Windows.DependencyPropertyKey> создается при первой регистрации свойства зависимостей. Если обрабатывать эту логику внутри класса, то можно сделать ее частной. Если необходимо устанавливать ее из других частей сборки, можно сделать ее внутренней. Одним из подходов является вызов <xref:System.Windows.DependencyObject.SetValue%2A> обработчика событий класса для соответствующего события, сообщающего экземпляру класса, хранимого значения свойства необходимо изменить. Другой подход заключается в связывании свойств зависимости с помощью парных <xref:System.Windows.PropertyChangedCallback> и <xref:System.Windows.CoerceValueCallback> обратные вызовы как часть метаданных этих свойств во время регистрации.  
  
 Поскольку <xref:System.Windows.DependencyPropertyKey> является закрытым и не распространяется системой свойств вне кода, свойство зависимостей только для чтения иметь лучшую безопасность настройки, чем свойство зависимости для чтения и записи. Для свойства зависимостей с возможностью чтения и записи идентифицирующее поле является явно или неявно общим, и таким образом, свойство является широко устанавливаемым. Дополнительные сведения см. в разделе [Безопасность свойства зависимостей](dependency-property-security.md).  
  
## <a name="see-also"></a>См. также

- [Общие сведения о свойствах зависимости](dependency-properties-overview.md)
- [Пользовательские свойства зависимостей](custom-dependency-properties.md)
- [Стилизация и использование шаблонов](../controls/styling-and-templating.md)
