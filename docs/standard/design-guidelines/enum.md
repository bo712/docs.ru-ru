---
title: Разработка перечислений
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, enumerations
- simple enumerations
- enumerations [.NET Framework], design guidelines
- class library design guidelines [.NET Framework], enumerations
- flags enumerations
ms.assetid: dd53c952-9d9a-4736-86ff-9540e815d545
author: KrzysztofCwalina
ms.openlocfilehash: 36e1f62ab1b236d48a55f7c255ed406cc0efa488
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615249"
---
# <a name="enum-design"></a>Разработка перечислений
Перечисления являются это специальный тип значения. Существует два вида перечислений: простой перечислимые типы и флага перечисления.  
  
 Простые перечисления представляют небольшой закрытых совокупностях вариантов. Распространенным примером простое перечисление — это набор цветов.  
  
 Флаг перечисления предназначены для поддержки побитовых операций над значений enum. Распространенным примером перечисление флагов приведен список параметров.  
  
 **✓ DO** использовать enum для строго типизированных параметров, свойств и возвращаемых значений, которые представляют собой наборы значений.  
  
 **✓ DO** предпочтительнее использовать вместо статических констант перечисления.  
  
 **X DO NOT** использовать enum для открытых наборов (например, версия операционной системы, имена друзьями, и т. д.).  
  
 **X DO NOT** предоставляют значения зарезервированных перечисления, которые предназначены для использования в будущем.  
  
 Значения можно всегда просто добавить в существующий перечисление на более позднем этапе. См. в разделе [Добавление значения к перечислениям](#add_value) Дополнительные сведения о добавлении значений к перечислениям. Зарезервированные значения просто засоряет набор реальных значений и стремятся привести к ошибкам пользователей.  
  
 **X AVOID** открытым доступом перечислений с только одним значением.  
  
 Распространенной практикой для обеспечения будущего расширения интерфейсов API C — Добавление зарезервированного параметров в сигнатуры методов. Такие зарезервированные параметры может быть выражен как перечисления с одним значением по умолчанию. Это не должно выполняться в управляемых интерфейсов API. Перегрузка методов позволяет добавление параметров в будущих выпусках.  
  
 **X DO NOT** включать значения sentinel в перечислениях.  
  
 Несмотря на то, что они иногда полезно разработчикам framework, значения-метки не всегда понятны пользователям платформы. Они используются для отслеживания состояния, перечисление, а не выполняется одно из значений из набора, представленный перечисления.  
  
 **✓ DO** укажите значение 0 в простые перечисления.  
  
 Рассмотрите возможность вызова значение нечто вроде «None». Если такое значение не подходит для этого конкретного перечисления, наиболее распространенные по умолчанию для перечисления должно быть назначено значение базовое значение ноль.  
  
 **✓ CONSIDER** с помощью <xref:System.Int32> (по умолчанию в большинстве языков программирования) как базовый тип перечисления, если верно любое из следующих:  
  
- Перечисление является перечисление флагов, и более 32 флагов, или планируется в будущем.  
  
- Базовый тип должен отличаться от <xref:System.Int32> для более простого взаимодействия с неуправляемым кодом, ожидается перечисления другого размера.  
  
- Базовый тип меньшего размера приведет к значительной экономии пространства. Если ожидается, что перечисление для использования в основном в качестве аргумента для потока управления, размер имеет небольшое значение. Размер экономии может привести к значительной если:  
  
    - Предполагается, что перечисление для использования в качестве поля в очень часто экземпляра структуры или класса.  
  
    - Предполагается, что пользователям создавать большие массивы или коллекции, перечисления экземпляров.  
  
    - Предполагается, что большое количество экземпляров, перечисления, подлежащий сериализации.  
  
 Для использования в памяти, следует помнить, что управляемые объекты всегда `DWORD`-aligned, поэтому вам эффективно несколько перечислений или других небольших структур в экземпляре для упаковки меньшего размера перечисление с чтобы вашу жизнь, так как размер всего экземпляра всегда будет округлено до `DWORD`.  
  
 **✓ DO** имя флага перечисления с множественного числа существительных и субстантивных словосочетаний и простые перечисления атрибутом существительные в единственном числе или субстантивные словосочетания.  
  
 **X DO NOT** расширить <xref:System.Enum?displayProperty=nameWithType> напрямую.  
  
 <xref:System.Enum?displayProperty=nameWithType> Это специальный тип используется в среде CLR для создания определяемых пользователем перечислений. Большинство языков предоставляют программный элемент, который предоставляет доступ к этой функции. Например, в C# `enum` ключевое слово используется для определения перечисления.  
  
<a name="design"></a>   
### <a name="designing-flag-enums"></a>Разработка перечислений флаг  
 **✓ DO** применить <xref:System.FlagsAttribute?displayProperty=nameWithType> для перечислений флагов. Этот атрибут не применяются к простые перечисления.  
  
 **✓ DO** используют степень числа 2 для значений перечисления флагов, поэтому они могут быть свободно объединены с помощью битовой операции или.  
  
 **✓ CONSIDER** предоставляет специальные перечислимых значений для часто используется сочетание флагов.  
  
 Побитовые операции являются перспективным и не требуется для простых задач. <xref:System.IO.FileAccess.ReadWrite> является примером специальное значение.  
  
 **X AVOID** Создание перечисления флага, где определенные комбинации значений являются недопустимыми.  
  
 **X AVOID** с помощью флага нулевые значения перечисления, если значение представляет «все флаги сняты» и соответствующим образом, как предписано следующем правиле с именем.  
  
 **✓ DO** имя нулевое значение флага перечисления `None`. Для перечисления флага значение всегда должно означать «будут удалены все флаги».  
  
<a name="add_value"></a>   
### <a name="adding-value-to-enums"></a>Добавив значение перечисления  
 Это очень часто, чтобы узнать, что необходимо добавить значения для перечисления, после его уже были доставлены. Нет на потенциальную проблему совместимости приложений при созданное значение возвращается из существующего API, так как плохо написанных приложений может неправильно обрабатывает новое значение.  
  
 **✓ CONSIDER** Добавление значения перечислений, несмотря на риск совместимость небольших.  
  
 При наличии реальные данные о совместимости приложений, из-за дополнения к перечисления, рассмотрите возможность добавления новых API, который возвращает старое и новое значения и отказаться от старых API, который следует продолжить возврат только старые значения. Это позволит гарантировать, что существующие приложения оставаться совместимым.  
  
 *Фрагменты: © Корпорация Майкрософт (Microsoft Corporation), 2005, 2009. Все права защищены.*  
  
 *Перепечатано разрешением Пирсона для образовательных учреждений, Inc. из [рекомендации по разработке Framework: Условные обозначения, стили и шаблоны для библиотеки .NET для повторного использования, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Кшиштов Квалина и Брэд Абрамс, опубликованных 22 октября 2008 г., издательство Addison-Wesley Professional как части цикла разработки Microsoft Windows.*  
  
## <a name="see-also"></a>См. также

- [Рекомендации по разработке типов](../../../docs/standard/design-guidelines/type.md)
- [Рекомендации по проектированию на основе Framework](../../../docs/standard/design-guidelines/index.md)
