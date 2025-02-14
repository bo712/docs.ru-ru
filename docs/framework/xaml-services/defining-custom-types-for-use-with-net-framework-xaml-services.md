---
title: Определение пользовательских типов для использования со службами XAML .NET Framework
ms.date: 03/30/2017
helpviewer_keywords:
- defining custom types [XAML Services]
ms.assetid: c2667cbd-2f46-4a7f-9dfc-53696e35e8e4
ms.openlocfilehash: fea5c656cf5e793ca0717cf3ef60016128a942be
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64617296"
---
# <a name="defining-custom-types-for-use-with-net-framework-xaml-services"></a>Определение пользовательских типов для использования со службами XAML .NET Framework
При определении пользовательских типов, которые являются бизнес-объектов или типов, которые не зависят от конкретных платформ, существуют определенные рекомендации для XAML, необходимо выполнить. При выполнении этих рекомендаций, служб XAML .NET Framework и средства чтения XAML и записи XAML может обнаружить характеристики XAML пользовательского типа и предоставить ему соответствующее представление в потоке узлов XAML использование системы типов XAML. В этом разделе описываются рекомендации для определения типов, определения членов и типов или элементов с атрибутами среды CLR.  
  
## <a name="constructor-patterns-and-type-definitions-for-xaml"></a>Шаблоны конструктора и определения типов для XAML  
 Возможность создания в качестве объектного элемента в XAML, пользовательский класс должен соответствовать следующим требованиям:  
  
- Пользовательский класс должен быть открытым и должен предоставлять открытый конструктор по умолчанию (без параметров). (Примечания о структурах см. в следующем разделе.)  
  
- Пользовательский класс не должен быть вложенным классом. Лишние «точка» в пути полного имени делает неоднозначных имен класса деления и препятствует работе других функций XAML, такими как присоединенные свойства.  
  
 Если объект может быть создан как объектный элемент, созданный объект может заполнить элемент формы свойства любого из свойств, которые принимают объект как базовый тип.  
  
 По-прежнему можно предоставить объект значения для типов, которые не удовлетворяют этим критериям, при включении преобразователь значений. Дополнительные сведения см. в разделе [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md).  
  
### <a name="structures"></a>Структуры  
 Структуры являются всегда следует создавать в XAML, по определению среды CLR. Это потому, что компилятор CLR неявно создает конструктор по умолчанию для структуры. Этот конструктор инициализирует все значения свойств по умолчанию.  
  
 В некоторых случаях поведение конструктора по умолчанию для структуры является нежелательным. Возможно, когда структура используется для заполнения значений и, по существу, как объединение. Значения могут обладать взаимоисключающие объединения, и таким образом, ни один из его свойства могут устанавливаться. Примером такой структуры в словаре WPF является <xref:System.Windows.GridLength>. Таких структурах необходимо реализовать преобразователь типов, таким образом, чтобы значения можно было представить в виде атрибутов, используя преобразования строк для создания различных интерпретаций или режимов значений структуры. Структура также должна реализовывать аналогичное поведение для конструкции кода с помощью конструктора, не являющегося конструктором по умолчанию.  
  
### <a name="interfaces"></a>интерфейсов,  
 Интерфейсы можно использовать как базовые типы членов. Система типов XAML проверяет список может быть назначен и ожидает, что объект, который предоставляется в качестве значения могут быть назначены интерфейс. Отсутствует понятие из интерфейса представления как тип XAML до тех пор, пока соответствующий присваиваемый тип поддерживает требования к созданию XAML.  
  
### <a name="factory-methods"></a>Фабричные методы  
 Фабричные методы являются компонентом XAML 2009 г. Они модифицируют принцип XAML, что объекты должны иметь конструкторы по умолчанию. Фабричные методы не документированы в этой статье. См. в разделе [директива x: FactoryMethod](x-factorymethod-directive.md).  
  
## <a name="enumerations"></a>Перечисления  
 Перечисления имеют поведение преобразования собственного типа XAML. Имена констант перечисления, указанные в XAML разрешаются по базовым типом перечисления и возвращают значение перечисления средству записи объектов XAML.  
  
 XAML поддерживает использование флагов стилей для перечисления с <xref:System.FlagsAttribute> применения. Дополнительные сведения см. в разделе [XAML подробное описание синтаксиса](../wpf/advanced/xaml-syntax-in-detail.md). ([XAML подробное описание синтаксиса](../wpf/advanced/xaml-syntax-in-detail.md) адресован WPF, но большая часть информации в этом разделе относится к XAML, не относящиеся к конкретной платформе реализации.)  
  
## <a name="member-definitions"></a>Определения элементов  
 Типы могут определять элементы для использования XAML. Вполне возможно, для типов, которые определяют элементы, которые могут использоваться для XAML, даже если этого конкретного типа не может использоваться XAML. Это стало возможным благодаря наследованию CLR. При условии, что такому типу, который наследует член поддерживает использование XAML как тип, и член поддерживает использование XAML для своего базового типа или имеет собственный синтаксис XAML доступны, что он может использоваться XAML.  
  
### <a name="properties"></a>Свойства  
 При определении свойств в качестве открытого свойства среды CLR, с помощью обычной CLR `get` и `set` шаблоны доступа и соответствующей языку языку, можно сообщить о системе типов XAML указано свойство как элемент с соответствующими сведениями для <xref:System.Xaml.XamlMember> свойства, такие как <xref:System.Xaml.XamlMember.IsReadPublic%2A> и <xref:System.Xaml.XamlMember.IsWritePublic%2A>.  
  
 Некоторые свойства могут включать текстового синтаксиса, применяя <xref:System.ComponentModel.TypeConverterAttribute>. Дополнительные сведения см. в разделе [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md).  
  
 В отсутствие текстового синтаксиса или собственного преобразования XAML и в отсутствие дальнейшего косвенное обращение, например использование расширения разметки, тип свойства (<xref:System.Xaml.XamlMember.TargetType%2A> системе типов XAML) должен иметь возможность возвращать экземпляр средству записи объектов XAML, рассматривая t конечный тип как тип CLR.  
  
 Если используется XAML 2009 г., [x: Reference Markup Extension](x-reference-markup-extension.md) может использоваться для предоставления значений, если указанные выше требования не выполнены; тем не менее, это скорее вопрос использования, чем с проблемой определения типа.  
  
### <a name="events"></a>События  
 При определении событий в качестве открытого события CLR, система типов XAML может сообщать о событии как член с <xref:System.Xaml.XamlMember.IsEvent%2A> как `true`. Привязка обработчиков событий выходит за рамки возможностей служб XAML .NET Framework. Это отводится отдельным платформам и реализациям.  
  
### <a name="methods"></a>Методы  
 Встроенный код для методов не требует XAML по умолчанию. В большинстве случаев вы не ссылаются напрямую метод членов из XAML, и методы в XAML является только для предоставления поддержки для конкретных шаблонов XAML. [Директива x: FactoryMethod](x-factorymethod-directive.md) является исключением.  
  
### <a name="fields"></a>Поля  
 Рекомендации по проектированию среды CLR не допустить нестатические поля. Для статических полей, значения статического поля доступны только при помощи [расширение разметки x: Static](x-static-markup-extension.md); в этом случае вы не выполняете ничего особенного в определении CLR, чтобы открыть поле для [x: Static](x-static-markup-extension.md) данные об использовании.  
  
## <a name="attachable-members"></a>Присоединяемые члены  
 Присоединяемых членов предоставляются для XAML посредством шаблона на определяющий тип метода доступа. Сам определяющий тип не требуется для использования XAML, как объект. На самом деле, стандартная — Чтобы объявить класс службы, которая является владельцем присоединяемого члена и реализовывать соответствующие поведения, но обслуживать никакой другой функции, такие как представление пользовательского интерфейса. В следующих разделах, заполнитель *PropertyName* представляет имя пользовательского присоединяемого члена. Это имя должно быть допустимым в [Грамматика XamlName](xamlname-grammar.md).  
  
 Будьте осторожны при конфликта имен между этими шаблонами и другие методы типа. Если существует элемент, соответствующий одному из шаблонов, он может интерпретироваться как путь использования присоединяемого члена обработчиком XAML даже если не желает.  
  
#### <a name="the-getpropertyname-accessor"></a>Метод доступа GetИмяСвойства  
 Сигнатура для метода доступа `Get`*ИмяСвойства* должна быть следующей.  
  
 `public static object Get` *ИмяСвойства* `(object` `target` `)`  
  
- Объект `target` можно указать как более конкретный тип в реализации. Это можно использовать для определения области использования присоединяемого члена; Использование за пределами этих границ, исключения недопустимого приведения, которые затем отображаются ошибку синтаксического анализа XAML. Имя параметра `target` не является обязательным, но называется `target` по соглашению в большинстве реализаций.  
  
- Возвращаемое значение можно указать как более конкретный тип в реализации.  
  
 Для поддержки <xref:System.ComponentModel.TypeConverter> поддержкой текстовый синтаксис для использования атрибутов присоединяемого члена, применяются <xref:System.ComponentModel.TypeConverterAttribute> для `Get` *PropertyName* метода доступа. Применение к `get` вместо `set` может показаться неинтуитивным; Однако это соглашение может поддерживать концепцию только для чтения присоединяемых членов, которые могут быть сериализованы, что полезно в сценарии конструктора.  
  
#### <a name="the-setpropertyname-accessor"></a>Метод доступа SetИмяСвойства  
 Подпись для набора*PropertyName* должен быть метод доступа:  
  
 `public static void Set` *ИмяСвойства* `(object` `target` `, object` `value` `)`  
  
- `target` Объекта можно указать как более конкретный тип в реализации, с тем же логикой и последствия, как описано в предыдущем разделе.  
  
- Объект `value` можно указать как более конкретный тип в реализации.  
  
 Помните, что значение для этого метода — входные данные, поступающие от использования XAML, обычно в виде атрибута. Из формы атрибута должно быть поддержка преобразователя значения для текстового синтаксиса, и атрибут `Get` *PropertyName* метода доступа.  
  
### <a name="attachable-member-stores"></a>Хранилища присоединяемых членов  
 Методы доступа, обычно не настолько, чтобы обеспечивать для размещения значений присоединяемого члена в граф объектов или извлечения значений из графа объектов и сериализации их должным образом. Для обеспечения данной функциональности `target` объекты в предыдущих сигнатурах метода доступа должны быть способны хранить значения. Механизм хранения должно быть согласовано с принципом присоединяемого члена, член может быть присоединен к целевым объектам, где присоединяемого члена не находится в списке элементов. Службы XAML .NET framework предоставляет методику реализации хранилищ присоединяемых членов через API <xref:System.Xaml.IAttachedPropertyStore> и <xref:System.Xaml.AttachablePropertyServices>. <xref:System.Xaml.IAttachedPropertyStore> используется средствами записи XAML для обнаружения реализации хранилища и должен быть реализован в тип, являющийся `target` методов доступа. Статический <xref:System.Xaml.AttachablePropertyServices> API-интерфейсы используются внутри тела методов доступа и ссылаться на присоединяемого элемента с его <xref:System.Xaml.AttachableMemberIdentifier>.  
  
## <a name="xaml-related-clr-attributes"></a>Относящиеся к XAML атрибуты среды CLR  
 Правильное назначение атрибутов типов, членов и сборки важно для передачи информации о системе типов XAML для служб XAML .NET Framework. Это важно в том случае, если вы типы предназначены для использования с системами XAML напрямую на основе средства чтения XAML служб XAML платформы .NET и записи XAML, или при определении или используется платформа, использующая XAML, который основан на эти средства чтения XAML и записи XAML.  
  
 Пример для каждого атрибута, связанного с XAML, относящиеся к XAML поддержки для пользовательских типов, см. в разделе [XAML-Related атрибуты среды CLR для пользовательских типов и библиотек](xaml-related-clr-attributes-for-custom-types-and-libraries.md).  
  
## <a name="usage"></a>Использование  
 Использование пользовательских типов требует, что автор разметки необходимо сопоставить префикс для сборки и пространства имен CLR, которые содержат пользовательского типа. Эта процедура не описаны в этом разделе.  
  
## <a name="access-level"></a>Уровень доступа  
 XAML предоставляет средства для загрузки и создания экземпляров типов, имеющих `internal` уровень доступа. Эта возможность предоставляется, чтобы пользовательский код можно определить собственные типы, а затем создавать экземпляры этих классов из разметки, который также является частью той же области кода пользователя.  
  
 Пример из WPF — всякий раз, когда пользовательский код определяет <xref:System.Windows.Controls.UserControl> , предназначенного как способ рефакторинга поведения пользовательского интерфейса, но не в рамках любой механизм возможные расширения, который может быть подразумевать объявление поддерживающего класса с `public` уровень доступа. Такие <xref:System.Windows.Controls.UserControl> может быть объявлен с `internal` доступ к Если вспомогательного кода компилируется в той же сборке, из которого он указывается в качестве типа XAML.  
  
 Для приложения, которое загружает XAML в режиме полного доверия и использует <xref:System.Xaml.XamlObjectWriter>, загрузка классов с `internal` уровень доступа всегда включен.  
  
 Для приложения, которое загружает XAML в режиме частичного доверия, можно управлять характеристиками уровня доступа с помощью <xref:System.Xaml.Permissions.XamlAccessLevel> API. Кроме того механизмов отсрочки (например, в системе шаблон WPF) должен иметь возможность распространять все разрешения уровня доступа и сохранять их для вычисления оценки во время выполнения; внутренне обрабатывается путем передачи <xref:System.Xaml.Permissions.XamlAccessLevel> сведения.  
  
### <a name="wpf-implementation"></a>Реализация WPF  
 XAML WPF использует модель доступа частичного доверия, где Если BAML загружается в режиме частичного доверия, доступ будет ограничен <xref:System.Xaml.Permissions.XamlAccessLevel.AssemblyAccessTo%2A> для сборки, которая является источником BAML. Для отсрочки, WPF использует <xref:System.Xaml.IXamlObjectWriterFactory.GetParentSettings%2A?displayProperty=nameWithType> как механизм для передачи информации об уровне доступа.  
  
 В терминах XAML WPF *внутренний тип* — это тип, который определен в сборке, которая также включает ссылающейся XAML. Такого типа могут быть сопоставлены через пространство имен XAML, в котором намеренно пропущены сборки = часть сопоставления, например, `xmlns:local="clr-namespace:WPFApplication1"`.  Если BAML ссылается на внутренний тип, и этот тип имеет `internal` обращаться к уровню, это приводит к возникновению ошибки `GeneratedInternalTypeHelper` класса для сборки. Если вы хотите избежать `GeneratedInternalTypeHelper`, необходимо либо использовать `public` обращаться к уровню, или необходимо выносить соответствующий класс в отдельную сборку и сделать зависимым этой сборки.  
  
## <a name="see-also"></a>См. также

- [Относящиеся к XAML атрибуты среды CLR для пользовательских типов и библиотек](xaml-related-clr-attributes-for-custom-types-and-libraries.md)
- [Службы XAML](index.md)
