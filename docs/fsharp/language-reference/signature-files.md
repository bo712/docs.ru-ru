---
title: Файлы сигнатур
description: Сведения об использовании F# файлы сигнатур для хранения сведений об открытых сигнатурах набора F# программировать элементы, такие как типы, пространства имен и модули.
ms.date: 06/15/2018
ms.openlocfilehash: 88938309a7c2bd12428f06ba8088141fd5349e80
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770452"
---
# <a name="signatures"></a>Сигнатуры

В файле сигнатур содержатся сведения об открытых сигнатурах набора элементов программы на языке F#, таких как типы, пространства имен и модули. Файл сигнатур можно использовать для указания доступности этих элементов программы.

## <a name="remarks"></a>Примечания

Для каждого файла кода F# может иметься *файл сигнатур*— файл с тем же именем, что и файл кода, но с расширением FSI вместо FS. Файлы сигнатур также можно добавлять в командную строку компиляции, если командная строка используется напрямую. Для различения файлов кода и файлов сигнатур файлы кода иногда называют *файлами реализации*. В проекте файл сигнатур должен предшествовать связанному с ним файлу кода.

Файл сигнатур описывает пространства имен, модули, типы и члены в соответствующем файле реализации. Информацию в файле сигнатур можно использовать для указания того, к каким частям кода в соответствующем файле реализации возможен доступ из кода, находящегося за пределами файла реализации, и какие части являются внутренними по отношению к файлу реализации. Пространства имен, модули и типы, включаемые в файл сигнатур, должны представлять собой подмножество имен пространств, модулей и типов, включаемых в файл реализации. За некоторыми исключениями, рассмотренными ниже в этом разделе, языковые элементы, отсутствующие в файле сигнатур, считаются закрытыми по отношению к файлу реализации. Если в проекте или в командной строке не найден файл сигнатур, используется доступность по умолчанию.

Дополнительные сведения о доступности по умолчанию, см. в разделе [контроля доступа](access-control.md).

В файле сигнатур не нужно повторять определение типов и реализаций для каждого метода или функции. Вместо этого для каждого метода и функции используется сигнатура, выступающая в качестве полной спецификации функциональности, реализуемой фрагментом модуля или пространства имен. Синтаксис сигнатуры типа идентичен используемому в объявлениях абстрактных методов в интерфейсах и абстрактных классах; он также отображается IntelliSense и интерпретатором языка F# (fsi.exe) при выводе правильно скомпилированных входных данных.

Если в сигнатуре типа недостаточно информации для определения того, является ли тип запечатанным или типом интерфейса, нужно добавить атрибут, по которому компилятор сможет определить природу типа. Используемые с этой целью атрибуты приведены в таблице ниже.

|Атрибут|Описание|
|---------|-----------|
|`[<Sealed>]`|Для типа, который не имеет абстрактных членов или не должен расширяться.|
|`[<Interface>]`|Для типа, являющегося интерфейсом.|

Компилятор выдает ошибку, если атрибуты в сигнатуре и в объявлении в файле реализации не соответствуют друг другу.

Для создания сигнатуры для значения или значения функции используется ключевое слово `val` . Сигнатура типа предваряется ключевым словом `type` .

Сформировать файл сигнатур можно с помощью параметра `--sig` компилятора. Как правило, вручную FSI-файлы не пишутся. Вместо этого вы создаете FSI-файлы с помощью компилятора, добавляете их в проект (при работе с проектом) и редактируете их, удаляя методы и функции, которые не должны быть доступными.

В отношении сигнатур типов действует ряд правил.

- Аббревиатуры типов в файле реализации не должны совпадать с полными названиями типов в файле сигнатур.

- Записи и размеченные объединения должны предоставлять либо все свои поля и конструкторы, либо никакие из них, и порядок в сигнатуре должен совпадать с порядком в файле реализации. Классы могут открывать некоторые, все или никакие из своих полей и методов в сигнатуре.

- Классы и структуры, имеющие конструкторы, должны предоставлять объявления своих базовых классов (объявление `inherits` ). Кроме того, классы и структуры, имеющие конструкторы, должны предоставлять все свои абстрактные методы и объявления интерфейсов.

- Типы интерфейсов должны открывать все свои методы и интерфейсы.

К сигнатурам значений применяются приведенные ниже правила.

- Модификаторы доступности (`public`, `internal`и т. д.) и модификаторы `inline` и `mutable` в сигнатуре должны совпадать с модификаторами в реализации.

- Количество параметров универсального типа (неявно выведенных или явно объявленных) должно совпадать. Также должны совпадать типы и ограничения типов в параметрах универсального типа.

- Если используется атрибут `Literal` , он должен присутствовать и в сигнатуре, и в реализации, и в обоих случая должно использоваться одно и то же литеральное значение.

- Шаблон параметров (также называемый *арностью*) сигнатур должен соответствовать шаблону параметров реализаций.

- Если имена параметров в файле сигнатур отличаются от соответствующий файл реализации, имя в файле сигнатур будет использоваться вместо этого, что может вызвать проблемы при отладке или профилировании. Если вы хотите получать уведомления о таких несоответствия, включить предупреждение 3218 в файле проекта или при вызове компилятора (см. в разделе `--warnon` под [параметры компилятора](compiler-options.md)).

В приведенном ниже примере показан файл сигнатур, содержащий сигнатуры пространства имен, модуля, значения функции и типов вместе с соответствующими атрибутами. Показан также соответствующий файл реализации.

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssignatures/snippet9002.fs)]

В приведенном ниже коде показан файл реализации.

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssignatures/snippet9001.fs)]

## <a name="see-also"></a>См. также

- [Справочник по языку F#](index.md)
- [Управление доступом](access-control.md)
- [Параметры компилятора](compiler-options.md)
