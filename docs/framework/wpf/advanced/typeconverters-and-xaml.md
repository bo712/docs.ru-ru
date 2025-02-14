---
title: TypeConverters и XAML
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], TypeConverter class
ms.assetid: f6313e4d-e89d-497d-ac87-b43511a1ae4b
ms.openlocfilehash: 17a4a7f4a514c07280dd5f58935fea3eed1ca4e3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662208"
---
# <a name="typeconverters-and-xaml"></a>TypeConverters и XAML
Этот раздел посвящен цели преобразования типов из строк — одной из основных функций языка XAML. В .NET Framework <xref:System.ComponentModel.TypeConverter> класс служит конкретной цели как часть реализации для управляемого пользовательского класса, который можно использовать в качестве значения свойства в использование атрибута XAML. При написании пользовательского класса, и вы хотите, чтобы экземпляры класса могли использоваться как значения настраиваемого атрибута XAML, может потребоваться применить <xref:System.ComponentModel.TypeConverterAttribute> к классу, написание пользовательского <xref:System.ComponentModel.TypeConverter> класс, или оба.  

## <a name="type-conversion-concepts"></a>Понятия преобразования типов  
  
### <a name="xaml-and-string-values"></a>XAML и строковые значения  
 Когда задается значение атрибута в файле XAML, начальный тип этого значения — строка чистого текста. Даже такие примитивы, такие как <xref:System.Double> изначально являются текстовыми строками для обработчика XAML.  
  
 XAML-обработчику требуется два сообщения для того, чтобы обработать значение атрибута. Первый из них — это тип значения свойства, которое должно быть задано. Любую строку, которая определяет значение атрибута и обрабатывается в XAML, в конечном счете необходимо преобразовать или разрешить в значение этого типа. Если значение — примитивный тип, понятный средству синтаксического анализа XAML (например, числовое значение), выполняется попытка прямого преобразования строки. Если значение является перечислением, то строка используется для проверки совпадения имени в этом перечислении с именем константы. Если значение не является ни примитивом, понятным средству синтаксического анализа, ни перечислением, то этот тип должен обладать возможностью предоставления экземпляра типа или значения, основанного на преобразованной строке. Это делается указанием класса преобразователя типов. Преобразователь типов — это фактически вспомогательный класс, предоставляющий значения другого класса как сценариям XAML, так и потенциально вызовам из кода .NET.  
  
### <a name="using-existing-type-conversion-behavior-in-xaml"></a>Использование поведения преобразования существующего типа в XAML  
 В зависимости от уровня понимания концепций XAML, вы, возможно, уже используете преобразование типа в простом приложении XAML, не реализуя его. Например, WPF определяет сотни свойств, принимающих значение типа <xref:System.Windows.Point>. Объект <xref:System.Windows.Point> является значение, которое описывает координаты в двухмерном пространстве координат и обладает всего два важных свойства: <xref:System.Windows.Point.X%2A> и <xref:System.Windows.Point.Y%2A>. При указании точки в XAML она задается в виде строки с разделителем (обычно запятой) между <xref:System.Windows.Point.X%2A> и <xref:System.Windows.Point.Y%2A> введенными значениями. Например, `<LinearGradientBrush StartPoint="0,0" EndPoint="1,1"/>`.  
  
 Даже этот простой тип <xref:System.Windows.Point> и простое его использование в XAML используют преобразователь типов. В данном случае это класс <xref:System.Windows.PointConverter>.  
  
 Преобразователь типов для <xref:System.Windows.Point> определены на уровне класса и упрощает разметку всех свойств, принимающих <xref:System.Windows.Point>. Без преобразователя типов для создания примера, показанного выше, требуется гораздо больше разметки.  

```xaml
<LinearGradientBrush>
  <LinearGradientBrush.StartPoint>
    <Point X="0" Y="0"/>
  </LinearGradientBrush.StartPoint>
  <LinearGradientBrush.EndPoint>
    <Point X="1" Y="1"/>
  </LinearGradientBrush.EndPoint>
</LinearGradientBrush>
 ```
  
 Использовать преобразование типа строки или более многословный синтаксис — этот выбор диктуется только стилем написания кода. Инструментарий рабочего процесса XAML также может оказывать влияние на то, как задаются значения. Некоторые инструменты XAML склонны создавать очень подробную разметку, так как это облегчает переключение между представлениями конструктора и собственным механизмом сериализации.  
  
 Существующие преобразователи типов могут быть найдены для типов WPF и .NET Framework путем проверки класса (или свойства) на наличие примененного атрибута <xref:System.ComponentModel.TypeConverterAttribute>. Этот атрибут содержит имя класса, поддерживающего преобразование для данного типа, как для XAML, так потенциально и для других целей.  
  
### <a name="type-converters-and-markup-extensions"></a>Преобразователи типов и расширения разметки  
 Расширения разметки и преобразователи типов играют ортогональные роли в терминах поведения обработчика XAML и сценариев, к которым они применяются. Хотя для расширения разметки контекст доступен, поведение преобразования типов свойств, когда расширение разметки предоставляет значение, обычно не включается в реализацию расширения разметки. Другими словами, даже если расширение разметки возвращает текстовую строку в качестве выходных данных `ProvideValue`, преобразование типа для этой строки относительно конкретного свойства или типа значения свойства не применяется. Обычно целью расширения разметки является обработка строки и возврат объекта без использования какого бы то ни было преобразователя типов.  
  
 Одна общая ситуация, где необходимо расширение разметки, а не преобразователь типов, заключается в создании ссылки на объект, который уже существует. В лучшем случае преобразователь типов с неопределенным состоянием может только создать новый экземпляр, что может быть нежелательно. Дополнительные сведения о расширениях разметки см. в разделе [Расширения разметки и XAML WPF](markup-extensions-and-wpf-xaml.md).  
  
### <a name="native-type-converters"></a>Собственные преобразователи типа  
 В реализации средства синтаксического анализа XAML в WPF и платформе .NET Framework существуют несколько типов, поддерживающих собственную обработку преобразования типа, но нет типов, которые можно рассматривать как примитивы. Пример такого типа — <xref:System.DateTime>. Причина зависит работа архитектуры платформы .NET Framework: тип <xref:System.DateTime> определяется в mscorlib, основной библиотеке .NET. <xref:System.DateTime> не может быть снабжены атрибутом атрибут, поступающий из другой сборки, что вводит зависимость (<xref:System.ComponentModel.TypeConverterAttribute> из системы), обычный механизм преобразователя типа обнаружения через атрибут не поддерживается. Вместо этого в средстве синтаксического анализа XAML имеется список типов, для которых необходима такая встроенная обработка; такие типы обрабатываются так же, как настоящие примитивы. (В случае использования <xref:System.DateTime> это подразумевает вызов <xref:System.DateTime.Parse%2A>.)  
  
<a name="Implementing_a_Type_Converter"></a>   
## <a name="implementing-a-type-converter"></a>Реализация преобразователя типов  
  
### <a name="typeconverter"></a>TypeConverter  
 В <xref:System.Windows.Point> ранее примере, класс <xref:System.Windows.PointConverter> ранее был. Для реализации XAML в .NET, все типы преобразователей, используемые для нужд XAML являются классами, производными от базового класса <xref:System.ComponentModel.TypeConverter>. <xref:System.ComponentModel.TypeConverter> Класс существовал в версиях платформы .NET Framework, предшествующих появлению XAML; одной из его исходного использование было преобразование строк для диалогов свойств в визуальных конструкторах. Для XAML роль <xref:System.ComponentModel.TypeConverter> включает базовый класс для преобразований в строку и из строки, позволяющий анализ строчного значения атрибута и возможно во время выполнения значение определенного свойства объекта обратно в строку для сериализации в качестве атрибута.  
  
 <xref:System.ComponentModel.TypeConverter> определены четыре элемента, относящихся к преобразованию в строки для нужд обработки XAML и обратно:  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 Из них является самым важным методом <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>. Этот метод преобразует входную строку к требуемому типу объекта. Строго говоря <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> метод может быть реализован для преобразования более широком диапазоне типов в требуемый конечный тип преобразователя и таким образом обслуживать, выходящим за пределы XAML, таких как поддержка преобразований времени выполнения, но в целях XAML Это только путь кода, который может обрабатывать <xref:System.String> ввод.  
  
 Далее наиболее важным методом является <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>. Если приложение преобразуется в представление разметки (например, если он сохраняется в XAML как файл), <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> отвечает за создание представления разметки. В этом случае правильный для XAML путь кода — при передаче `destinationType` из <xref:System.String> .  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> и <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> — это вспомогательные методы, используемые, когда служба запрашивает возможности реализации <xref:System.ComponentModel.TypeConverter> . Вам необходимо реализовать эти методы для возврата `true` для определенных типов. Они аналогичны методам преобразования для поддержки вашего преобразователя. В целях XAML обычно это означает тип <xref:System.String> .  
  
### <a name="culture-information-and-type-converters-for-xaml"></a>Сведения о языке и преобразователи типов для XAML  
 Каждый <xref:System.ComponentModel.TypeConverter> реализация может иметь собственную интерпретацию того, что составляет допустимую строку для преобразования и можно также использовать или игнорировать описание типа, переданного в качестве параметров. Важное замечание относительно языка и региональных параметров и преобразования типов XAML. Использование локализуемых строк в качестве значений атрибутов полностью поддерживается в XAML. Но использование локализуемых строк в качестве входных данных преобразователя типов с учетом индивидуальных требований для языка и региональных параметров не поддерживается, так как преобразователи типов значений атрибутов XAML по необходимости выполняют анализ с фиксированным языком, используя язык и региональные параметры `en-US`. Дополнительные сведения о причинах этого ограничения с точки зрения проектирования см. в спецификации языка XAML ([\[MS-XAML\]](https://go.microsoft.com/fwlink/?LinkId=114525)).  
  
 Пример того, что учет языка и региональных параметров может быть важен: некоторые языки и региональные параметры используют запятую в качестве десятичного разделителя. Это входит в противоречие с поведением многих преобразователей типов WPF XAML, которые используют запятую в качестве разделителя (исторически в обычной форме X,Y или в списках, разделенных запятыми). Даже передача языка и региональных параметров в окружающий XAML (установка параметра `Language` или `xml:lang` в значение `sl-SI`, как пример языка и региональных параметров, использующих запятую в качестве десятичного разделителя) не решает проблемы.  
  
### <a name="implementing-convertfrom"></a>Реализация ConvertFrom  
 Для использования в качестве реализации <xref:System.ComponentModel.TypeConverter> , поддерживающей XAML, метод <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> данного преобразователя должен принимать строку как параметр `value` . Если строка имеет в допустимых отформатировать и может быть преобразован с <xref:System.ComponentModel.TypeConverter> реализации, то возвращаемый объект должен поддерживать возможность приведения к типу, ожидаемому свойством. В противном случае реализация <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> должна возвращать `null`.  
  
 Каждый <xref:System.ComponentModel.TypeConverter> реализация может иметь собственную интерпретацию того, что составляет допустимую строку для преобразования и можно также использовать или игнорировать типа контекстов описание или язык и региональные параметры, передаваемые в качестве параметров. Тем не менее обработка WPF XAML может не передать значения в контекст описания типа во всех случаях, а также может не передать язык и региональные параметры на основе `xml:lang`.  
  
> [!NOTE]
>  Не используйте фигурные скобки, особенно {, как возможный элемент формата строки. Эти символы зарезервированы как вход и выход для последовательности расширения разметки.  
  
### <a name="implementing-convertto"></a>Реализация ConvertTo  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> может использоваться для поддержки сериализации. Поддержка сериализации с помощью <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> для пользовательского типа и его преобразователя типов не обязательна. Тем не менее, при реализации элемента управления или использовании сериализации как часть функций или класса, необходимо реализовать <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>.  
  
 Для использования в качестве <xref:System.ComponentModel.TypeConverter> реализации, поддерживающей XAML, <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> метода для данного преобразователя должен принимать экземпляр типа (или значение) поддерживаются как `value` параметр. Когда `destinationType` параметр является типом <xref:System.String>, то возвращаемый объект должен иметь возможность быть приведен как <xref:System.String>. Возвращаемая строка должна представлять сериализованное значение `value`. В идеальном случае выбранный формат сериализации должен быть может создать то же значение, если для передачи этой строки <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> реализация того же преобразователя без значительной потери информации.  
  
 Если значение не может быть сериализовано или преобразователь не поддерживает сериализацию, <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> реализация должна возвращать `null`и разрешается создать исключение в данном случае. Но при создании исключения, вам следует сообщать о невозможности использования этого преобразователя, как часть вашего <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> реализации таким образом, рекомендуется проверять с помощью <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> поддерживается сначала Чтобы избежать исключений.  
  
 Если `destinationType` параметр не относится к типу <xref:System.String>, можно выбрать собственную обработку преобразователя. Как правило, вы возвращаетесь к базовой обработке реализации, который в каждый метод <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> вызывает определенное исключение.  
  
### <a name="implementing-canconvertto"></a>Реализация CanConvertTo  
 Ваша реализация <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> должна возвращать `true` для `destinationType` типа <xref:System.String>, а в противном случае обращаться к базовой реализации.  
  
### <a name="implementing-canconvertfrom"></a>Реализация CanConvertFrom  
 Ваша реализация <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> должна возвращать `true` для `sourceType` типа <xref:System.String>, а в противном случае обращаться к базовой реализации.  
  
<a name="Applying_the_TypeConverterAttribute"></a>   
## <a name="applying-the-typeconverterattribute"></a>Применение TypeConverterAttribute  
 Чтобы пользовательский преобразователь типов для использования в качестве действующего преобразователя для пользовательского класса обработчика XAML, необходимо применить [!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute> к определению класса. Имя <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> , указываемое в атрибуте, должно быть именем типа пользовательского преобразователя типов. Если этот атрибут применен, то в случае, когда обработчик XAML обрабатывает значения, в которых тип свойства использует тип пользовательского класса, обработчик может ввести строки и вернуть экземпляры объекта.  
  
 Вы также можете предоставить преобразователь типов для отдельных свойств. Вместо применения [!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute> к определению класса применить его к определению свойства (главному определению, а не реализации `get`/`set` внутри него). Тип свойства должен соответствовать типу, который обрабатывается пользовательским преобразователем типов. Если этот атрибут применен, то в случае, когда обработчик XAML обрабатывает значения этого свойства, он может обработать входные строки и вернуть экземпляры объекта. Метод преобразователь типа каждого свойства особенно полезен, если вы решили использовать типа свойства из Microsoft .NET Framework или из другой библиотеки, где невозможно управлять определением класса и нельзя применять <xref:System.ComponentModel.TypeConverterAttribute> существует.  
  
## <a name="see-also"></a>См. также

- <xref:System.ComponentModel.TypeConverter>
- [Общие сведения о языке XAML (WPF)](xaml-overview-wpf.md)
- [Расширения разметки и XAML WPF](markup-extensions-and-wpf-xaml.md)
- [Подробное описание синтаксиса XAML](xaml-syntax-in-detail.md)
