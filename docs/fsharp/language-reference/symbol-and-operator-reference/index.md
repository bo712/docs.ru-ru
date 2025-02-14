---
title: Справочник символов и операторов
description: Дополнительные сведения о символах и операторах, используемых в F# языка программирования.
ms.date: 02/11/2019
ms.openlocfilehash: 0ea8337a9055c8df639fe6abdb6c79445d189d64
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490815"
---
# <a name="symbol-and-operator-reference"></a>Справочник символов и операторов

> [!NOTE]
> Ссылки на справочник по API в этой статье ведут на сайт MSDN.  Работа над справочником по API docs.microsoft.com не завершена.

В этом разделе приведена таблица символов и операторов, которые используются в языке F#.

## <a name="table-of-symbols-and-operators"></a>Таблица символов и операторов

Следующая таблица содержит описание символов, которые используются в языке F#, ссылки на разделы с более подробной информацией и краткое описание возможностей использования этих символов. Символы упорядочены в соответствии с порядком кодировки ASCII.

|Символ или оператор|Ссылки|Описание|
|------------------|-----|-----------|
|`!`|[Ссылочные ячейки](../reference-cells.md)<br /><br />[Выражения вычисления](../computation-expressions.md)|<ul><li>Разыменовывает ссылочную ячейку.<br /></li><li>Находясь после ключевого слова, указывает измененное поведение ключевого слова согласно контролю рабочим процессом.<br /></li></ul>|
|`!=`|Неприменимо.|<ul><li>Не используется в F#. Для операций неравенства используйте оператор `<>`.<br /></li></ul>|
|`"`|[Литералы](../literals.md)<br /><br />[Строки](../strings.md)|<ul><li>Разделяет текстовую строку.<br /></li></ul>|
|`"""`|[Строки](../strings.md)|Разделяет буквальную текстовую строку. Отличается от `@"..."` тем, что можно указать символ кавычки с помощью одинарной кавычки в строке.|
|`#`|[Директивы компилятора](../compiler-directives.md)<br /><br />[Гибкие типы](../flexible-types.md)|<ul><li>Выступает как префикс директивы препроцессора или компилятора, например `#light`.<br /></li><li>При использовании с типом указывает *гибкий тип*, который относится к типу или любому его производному типу.<br /></li></ul>|
|`$`|Дополнительные сведения недоступны.|<ul><li>Для внутреннего использования, применяется для определенных создаваемых компилятором имен переменных и функций.<br /></li></ul>|
|`%`|[Арифметические операторы](arithmetic-operators.md)<br /><br />[Цитирование кода](../code-quotations.md)|<ul><li>Вычисляет целочисленный остаток.<br /></li><li>Используется для объединения выражений в типизированные цитаты кода.<br /></li></ul>|
|`%%`|[Цитирование кода](../code-quotations.md)|<ul><li>Используется для объединения выражений в нетипизированные цитаты кода.<br /></li></ul>|
|`%?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Вычисляет целочисленный остаток, если правая часть является обнуляемым типом.<br /></li></ul>|
|`&`|[Выражения match](../match-expressions.md)|<ul><li>Вычисляет адрес изменяемого значения, используется при взаимодействии с другими языками.<br /></li><li>Используется в шаблонах И.<br /></li></ul>|
|`&&`|[Логические операторы](boolean-operators.md)|<ul><li>Вычисляет значение логической операции И.<br /></li></ul>|
|`&&&`|[Побитовые операторы](bitwise-operators.md)|<ul><li>Вычисляет значение побитовой операции И.<br /></li></ul>|
|`'`|[Литералы](../literals.md)<br /><br />[Автоматическое обобщение](../generics/automatic-generalization.md)|<ul><li>Разделяет односимвольный литерал.<br /></li><li>Указывает параметр универсального типа.<br /></li></ul>|
|<code>&#96;&#96;...&#96;&#96;</code>|Дополнительные сведения недоступны.|<ul><li>Разделяет идентификатор, который в противном случае не будет допустимым идентификатором, например ключевое слово языка.<br /></li></ul>|
|`( )`|[Тип единиц](../unit-type.md)|<ul><li>Представляет одно значение типа единицы.<br /></li></ul>|
|`(...)`|[Кортежи](../tuples.md)<br /><br />[Перегрузка операторов](../operator-overloading.md)|<ul><li>Указывает порядок, в котором вычисляются выражения.<br /></li><li>Разделяет кортеж.<br /></li><li>Используется в определениях операторов.<br /></li></ul>|
|`(*...*)`||<ul><li>Разделяет комментарий, который может занимать несколько строк.<br /></li></ul>|
|<code>(&#124;...&#124;)</code>|[Активные шаблоны](../active-patterns.md)|<ul><li>Разделяет активный шаблон. Также называются *скобками с вертикальной чертой*.<br /></li></ul>|
|`*`|[Арифметические операторы](arithmetic-operators.md)<br /><br />[Кортежи](../tuples.md)<br /><br />[Единицы измерения](../units-of-measure.md)|<ul><li>При использовании в качестве бинарного оператора перемножает левую и правую части.<br /></li><li>В типах указывает на спаривание в кортеже.<br /></li><li>Используется в единицах типов измерения.<br /></li></ul>|
|`*?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Перемножает левую и правую части, если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|`**`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>Вычисляет операцию возведения в степень (`x ** y` означает `x` в степени `y`).<br /></li></ul>|
|`+`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>При использовании в качестве бинарного оператора складывает левую и правую части.<br /></li><li>При использовании в качестве унарного оператора обозначает положительное количество. (Формально выдает то же значение без изменения знака.)<br /></li></ul>|
|`+?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Складывает левую и правую части, если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|`,`|[Кортежи](../tuples.md)|<ul><li>Отделяет элементы кортежа или параметры типа.<br /></li></ul>|
|`-`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>При использовании в качестве бинарного оператора вычитает из левой части правую.<br /></li><li>При использовании в качестве унарного оператора выполняет операцию отрицания.<br /></li></ul>|
|`-`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Вычитает правую часть из левой, если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|`->`|[Функции](../functions/index.md)<br /><br />[Выражения match](../match-expressions.md)|<ul><li>В типах функций разделяет аргументы и возвращаемые значения.<br /></li><li>Получает результат выражения (в выражениях последовательности); эквивалент ключевому слову `yield`.<br /></li><li>Используется в выражениях сопоставления<br /></li></ul>|
|`.`|[Члены](../members/index.md)<br /><br />[Типы-примитивы](../primitive-types.md)|<ul><li>Обращается к члену и отделяет индивидуальные имена в полном имени.<br /></li><li>Задает десятичный разделитель в числах с плавающей запятой.<br /></li></ul>|
|`..`|[Циклы. `for...in` Выражение](../loops-for-in-expression.md)|<ul><li>Задает диапазон.<br /></li></ul>|
|`.. ..`|[Циклы. `for...in` Выражение](../loops-for-in-expression.md)|<ul><li>Задает диапазон вместе с приращением.<br /></li></ul>|
|`.[...]`|[Массивы](../arrays.md)|<ul><li>Обращается к элементу массива.<br /></li></ul>|
|`/`|[Арифметические операторы](arithmetic-operators.md)<br /><br />[Единицы измерения](../units-of-measure.md)|<ul><li>Делит левую часть (делимое) на правую часть (делитель).<br /></li><li>Используется в единицах типов измерения.<br /></li></ul>|
|`/?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Делит левую часть на правую, если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|`//`||<ul><li>Обозначает начало однострочного комментария.<br /></li></ul>|
|`///`|[Документация XML](../xml-documentation.md)|<ul><li>Обозначает XML-комментарий.<br /></li></ul>|
|`:`|[Функции](../functions/index.md)|<ul><li>В аннотации типа отделяет имя параметра или члена от его типа.<br /></li></ul>|
|`::`|[Списки](../lists.md)<br /><br />[Выражения match](../match-expressions.md)|<ul><li>Создает список. Элемент в левой части добавляется в начало списка в правой части.<br /></li><li>Используется в сопоставлениях с шаблоном для отделения частей списка.<br /></li></ul>|
|`:=`|[Ссылочные ячейки](../reference-cells.md)|<ul><li>Назначает значение ссылочной ячейке.<br /></li></ul>|
|`:>`|[Приведение и преобразование](../casting-and-conversions.md)|<ul><li>Преобразует тип в тип, находящийся на более высоком уровне иерархии.<br /></li></ul>|
|`:?`|[Выражения match](../match-expressions.md)|<ul><li>Возвращает `true` Если значение совпадает с указанным типом (включая, если он является подтипом); в противном случае возвращает `false` (оператор проверки типа).<br /></li></ul>|
|`:?>`|[Приведение и преобразование](../casting-and-conversions.md)|<ul><li>Преобразует тип в тип, находящийся на более низком уровне иерархии.<br /></li></ul>|
|`;`|[Подробный синтаксис](../verbose-syntax.md)<br /><br />[Списки](../lists.md)<br /><br />[Записи](../records.md)|<ul><li>Отделяет выражения (в основном используется в подробном синтаксисе).<br /></li><li>Отделяет элементы списка.<br /></li><li>Отделяет поля записи.<br /></li></ul>|
|`<`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>Вычисляет значение операции "меньше чем".<br /></li></ul>|
|`<?`|[Операторы, допускающие значение NULL](nullable-operators.md)|Вычисляет значение операции "меньше чем", если правая часть является типом, допускающим значение NULL.|
|`<<`|[Функции](../functions/index.md)|<ul><li>Объединяет две функции в обратном порядке. Вторая функция выполняется первой (оператор обратного соединения).<br /></li></ul>|
|`<<<`|[Побитовые операторы](bitwise-operators.md)|<ul><li>Сдвигает биты в количестве в левой части влево на количество бит, указанное в правой части.<br /></li></ul>|
|`<-`|[Значения](../values/index.md)|<ul><li>Присваивает значение переменной.<br /></li></ul>|
|`<...>`|[Автоматическое обобщение](../generics/automatic-generalization.md)|<ul><li>Разделяет параметры типа.<br /></li></ul>|
|`<>`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>Возвращает значение `true`, если левая часть не равна правой части; в противном случае возвращает значение false.<br /></li></ul>|
|`<>?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Вычисляет значение операции "не равно", если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|`<=`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>Возвращает значение `true`, если левая часть меньше или равна правой части; в противном случае возвращает значение `false`.<br /></li></ul>|
|`<=?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Вычисляет значение операции "меньше или равно", если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|<code>&lt;&#124;</code>|[Функции](../functions/index.md)|<ul><li>Передает результат выражения в правой части в функцию левой части (оператор обратного конвейера).<br /></li></ul>|
|<code>&lt;&#124;&#124;</code>|[Функция Operators.&#40; &#60;&#124;&#124; &#41;&#60;'T1,'T2,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-%5bhh-%5d%5b%27t1%2c%27t2%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Передает кортеж из двух аргументов в правой части в функцию в левой части.<br /></li></ul>|
|<code>&lt;&#124;&#124;&#124;</code>|[Функция Operators.&#40; &#60;&#124;&#124;&#124; &#41;&#60;'T1,'T2,'T3,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-%5bhhh-%5d%5b%27t1%2c%27t2%2c%27t3%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Передает кортеж из трех аргументов в правой части в функцию в левой части.<br /></li></ul>|
|`<@...@>`|[Цитирование кода](../code-quotations.md)|<ul><li>Разделяет типизированную цитату кода.<br /></li></ul>|
|`<@@...@@>`|[Цитирование кода](../code-quotations.md)|<ul><li>Разделяет нетипизированную цитату кода.<br /></li></ul>|
|`=`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>Возвращает значение `true`, если левая часть равна правой части; в противном случае возвращает значение `false`.<br /></li></ul>|
|`=?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Вычисляет значение операции "равно", если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|`==`|Неприменимо.|<ul><li>Не используется в F#. Используйте `=` для операции равенства.<br /></li></ul>|
|`>`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>Возвращает значение `true`, если левая часть больше правой части; в противном случае возвращает значение `false`.<br /></li></ul>|
|`>?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Вычисляет значение операции «больше», если правая часть является обнуляемым типом.<br /></li></ul>|
|`>>`|[Функции](../functions/index.md)|<ul><li>Объединяет две функции (оператор прямого соединения).<br /></li></ul>|
|`>>>`|[Побитовые операторы](bitwise-operators.md)|<ul><li>Сдвигает биты в количестве в левой части влево на количество позиций, указанное в правой части.<br /></li></ul>|
|`>=`|[Арифметические операторы](arithmetic-operators.md)|<ul><li>Возвращает `true` при левой стороны больше или равна правой части; в противном случае возвращает `false`.<br /></li></ul>|
|`>=?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Вычисляет значение операции "больше чем или равно", если правая часть является типом, допускающим значение NULL.<br /></li></ul>|
|`?`|[Параметры и аргументы](../parameters-and-arguments.md)|<ul><li>Задает необязательный аргумент.<br /></li><li>Используется как оператор для вызова динамических методов и свойств. Необходимо предоставить собственную реализацию.<br /></li></ul>|
|`? ... <- ...`|Дополнительные сведения недоступны.|<ul><li>Используется как оператор для настройки динамических свойств. Необходимо предоставить собственную реализацию.<br /></li></ul>|
|`?>=`, `?>`, `?<=`, `?<`, `?=`, `?<>`, `?+`, `?-`, `?*`, `?/`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Эквивалент соответствующих операторов без суффикса ?, где тип, допускающий значение NULL, находится слева.<br /></li></ul>|
|`>=?`, `>?`, `<=?`, `<?`, `=?`, `<>?`, `+?`, `-?`, `*?`, `/?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Эквивалент соответствующих операторов без суффикса ?, где тип, допускающий значение NULL, находится справа.<br /></li></ul>|
|`?>=?`, `?>?`, `?<=?`, `?<?`, `?=?`, `?<>?`, `?+?`, `?-?`, `?*?`, `?/?`|[Операторы, допускающие значение NULL](nullable-operators.md)|<ul><li>Эквивалент соответствующих операторов без окружающих вопросительных знаков, где обе стороны являются типами, допускающими значение NULL.<br /></li></ul>|
|`@`|[Списки](../lists.md)<br /><br />[Строки](../strings.md)|<ul><li>Объединяет два списка.<br /></li><li>При размещении перед строковым литералом, указывает, что строку следует интерпретировать буквально, без интерпретации escape-символов.<br /></li></ul>|
|`[...]`|[Списки](../lists.md)|<ul><li>Разделяет элементы списка.<br /></li></ul>|
|<code>[&#124;...&#124;]</code>|[Массивы](../arrays.md)|<ul><li>Разделяет элементы массива.<br /></li></ul>|
|`[<...>]`|[Атрибуты](../attributes.md)|<ul><li>Разделяет атрибут.<br /></li></ul>|
|`\`|[Строки](../strings.md)|<ul><li>Указывает на пропуск следующего символа; используется в символьных и строковых литералах.<br /></li></ul>|
|`^`|[Статически разрешаемые параметры типов](../generics/statically-resolved-type-parameters.md)<br /><br />[Строки](../strings.md)|<ul><li>Задает параметры типа, которые должны разрешаться во время компиляции, а не во время выполнения.<br /></li><li>Объединяет строки.<br /></li></ul>|
|`^^^`|[Побитовые операторы](bitwise-operators.md)|<ul><li>Вычисляет значение операции побитового исключающего ИЛИ.<br /></li></ul>|
|`_`|[Выражения match](../match-expressions.md)<br /><br />[Универсальные шаблоны](../generics/index.md)|<ul><li>Обозначает шаблон с подстановочными знаками.<br /></li><li>Задает анонимный универсальный параметр.<br /></li></ul>|
|<code>&#96;</code>|[Автоматическое обобщение](../generics/automatic-generalization.md)|<ul><li>Для внутреннего использования, указывает параметр универсального типа.<br /></li></ul>|
|`{...}`|[Последовательности](../sequences.md)<br /><br />[Записи](../records.md)|<ul><li>Разделяет выражения последовательности и вычислительные выражения.<br /></li><li>Используется в определениях записей.<br /></li></ul>|
|<code>&#124;</code>|[Выражения match](../match-expressions.md)|<ul><li>Разделяет отдельные случаи соответствия, отдельные случаи размеченного объединения и значения перечисления.<br /></li></ul>|
|<code>&#124;&#124;</code>|[Логические операторы](boolean-operators.md)|<ul><li>Вычисляет значение логической операции ИЛИ.<br /></li></ul>|
|<code>&#124;&#124;&#124;</code>|[Побитовые операторы](bitwise-operators.md)|<ul><li>Вычисляет значение побитовой операции ИЛИ.<br /></li></ul>|
|<code>&#124;></code>|[Функции](../functions/index.md)|<ul><li>Передает результат левой части в функцию в правой части (оператор прямого конвейера).<br /></li></ul>|
|<code>&#124;&#124;></code>|[Функция Operators.&#40; &#124;&#124;&#62; &#41;&#60;'T1,'T2,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-hh%5d-%5d%5b%27t1%2c%27t2%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Передает кортеж из двух аргументов в левой части в функцию в правой части.<br /></li></ul>|
|<code>&#124;&#124;&#124;></code>|[Функция Operators.&#40; &#124;&#124;&#124;&#62; &#41;&#60;'T1,'T2,'T3,'U&#62;](https://msdn.microsoft.com/visualfsharpdocs/conceptual/operators.%5b-hhh%5d-%5d%5b%27t1%2c%27t2%2c%27t3%2c%27u%5d-function-%5bfsharp%5d)|<ul><li>Передает кортеж из трех аргументов в левой части в функцию в правой части.<br /></li></ul>|
|`~~`|[Перегрузка операторов](../operator-overloading.md)|<ul><li>Используется для объявления перегрузки для оператора унарного отрицания.<br /></li></ul>|
|`~~~`|[Побитовые операторы](bitwise-operators.md)|<ul><li>Вычисляет значение операции побитового НЕ.<br /></li></ul>|
|`~-`|[Перегрузка операторов](../operator-overloading.md)|<ul><li>Используется для объявления перегрузки для оператора унарного минуса.<br /></li></ul>|
|`~+`|[Перегрузка операторов](../operator-overloading.md)|<ul><li>Используется для объявления перегрузки для оператора унарного плюса.<br /></li></ul>|

## <a name="operator-precedence"></a>Приоритет операторов

В следующей таблице указана очередность применения операторов и других ключевых слов выражений для языка F# (в порядке возрастания приоритета). Также, когда это возможно, указана ассоциативность.

|Оператор|Ассоциативность|
|--------|-------------|
|`as`|Справа|
|`when`|Правый|
|<code>&#124;</code> (вертикальная черта)|Слева|
|`;`|Правый|
|`let`|Неассоциативный|
|`function`, `fun`, `match`, `try`|Неассоциативный|
|`if`|Неассоциативный|
|`not`|Правый|
|`->`|Правый|
|`:=`|Правый|
|`,`|Неассоциативный|
|`or`, <code>&#124;&#124;</code>|По левому краю|
|`&`, `&&`|По левому краю|
|`:>`, `:?>`|Правый|
|`<`*OP*, `>` *op*, `=`, <code>&#124;</code> *op*, `&` *op*, `&`<br /><br />(включая `<<<`, `>>>`, <code>&#124;&#124;&#124;</code>, `&&&`)|Слева|
|`^`*op*<br /><br />(включая `^^^`)|Правый|
|`::`|Правый|
|`:?`|Не ассоциативен|
|`-`*op*, `+`*op*|Применяется к инфиксному использованию этих символов|
|`*`*op*, `/`*op*, `%`*op*|Левый|
|`**`*op*|Правый|
|`f x` (применение функции)|Слева|
|<code>&#124;</code> (соответствие шаблону)|Правый|
|Префиксные операторы (`+`*op*, `-`*op*, `%`, `%%`, `&`, `&&`, `!`*op*, `~`*op*)|Слева|
|`.`|Слева|
|`f(x)`|Слева|
|`f<`*типы*`>`|Слева|

F# поддерживает перегрузку пользовательских операторов. Это значит, что пользователь может определять собственные операторы. В предыдущей таблице *op* может быть любой допустимой (возможно, пустой) последовательностью символов операторов, встроенных или пользовательских. Таким образом, этой таблицей можно пользоваться, чтобы определить, какую последовательность символов использовать для пользовательского оператора с целью достижения нужного уровня приоритета. Начальные символы `.` игнорируются, когда компилятор определяет приоритет.

## <a name="see-also"></a>См. также

- [Справочник по языку F#](../index.md)
- [Перегрузка операторов](../operator-overloading.md)
