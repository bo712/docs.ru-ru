---
title: Работа с LINQ
description: В этом руководстве мы научим вас создавать последовательности с помощью LINQ, создавать методы для использования в запросах LINQ, а также различать упреждающее и отложенное вычисление.
ms.date: 10/29/2018
ms.assetid: 0db12548-82cb-4903-ac88-13103d70aa77
ms.openlocfilehash: e51fb166ccba793f9f2aa9d11a109280bf8eea93
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2019
ms.locfileid: "66486985"
---
# <a name="working-with-linq"></a>Работа с LINQ

## <a name="introduction"></a>Вступление

В этом руководстве описаны возможности .NET Core и C#. Вы узнаете:

- как создать последовательности с помощью LINQ;
- как написать методы, которые можно применять в запросах LINQ;
- как различать упреждающее и отложенное вычисление.

Вы освоите эти методы на примере приложения, которое демонстрирует один из основных навыков любого иллюзиониста: [тасовка по методу фаро](https://en.wikipedia.org/wiki/Faro_shuffle). Так называют метод тасовки, при котором колода делится ровно на две части, а затем собирается заново так, что карты из каждой половины следуют строго поочередно.

Этот метод очень удобен для иллюзионистов, поскольку положение каждой карты после каждой тасовки точно известно, и через несколько циклов порядок карт восстанавливается.

Здесь же он используется в качестве не слишком серьезного примера для процессов управления последовательностями данных. Приложение, которое вы создадите, будет моделировать колоду карт и выполнять для них серию тасовок, выводя новый порядок карт после каждой из них. Вы сможете сравнить новый порядок карт с исходным.

Это руководство описывает несколько шагов. После каждого из них вы сможете запустить приложение и оценить результаты. [Готовый пример](https://github.com/dotnet/samples/blob/master/csharp/getting-started/console-linq) доступен в репозитории dotnet/samples на сайте GitHub. Инструкции по загрузке см. в разделе [Просмотр и скачивание примеров](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

## <a name="prerequisites"></a>Предварительные требования

Компьютер должен быть настроен для выполнения .NET Core. Инструкции по установке см. на странице [.NET Core](https://www.microsoft.com/net/core). Это приложение можно запустить в ОС Windows, Ubuntu Linux, OS X или в контейнере Docker. Вам потребуется редактор кода, но вы можете выбрать любой привычный для вас. В примерах ниже используется кроссплатформенный редактор [Visual Studio Code](https://code.visualstudio.com/) с открытым исходным кодом. Вы можете заменить его на любое другое средство, с которым вам удобно работать.

## <a name="create-the-application"></a>Создание приложения

Первым шагом является создание нового приложения. Откройте командную строку и создайте новый каталог для приложения. Перейдите в этот каталог. В командной строке введите команду `dotnet new console`. Эта команда создает начальный набор файлов для базового приложения Hello World.

Если вы раньше никогда не работали с C#, изучите структуру программы C# по [этому руководству](console-teleprompter.md). Мы рекомендуем сначала ознакомиться с ним, а затем вернуться сюда и продолжить изучение LINQ.

## <a name="creating-the-data-set"></a>Создание набора данных

Перед началом работы убедитесь, что в верхней части файла `Program.cs`, созданного `dotnet new console`, находятся следующие строки:

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using System.Linq;
```

Если эти три строки (инструкции `using`) находятся не в верхней части файла, наша программа не будет компилироваться.

Теперь, когда у вас есть все необходимые ссылки, посмотрите, из чего состоит колода карт. Как правило, в колоде игральных карт четыре масти и в каждой масти по тринадцать значений. Вы можете создать класс `Card` сразу же и заполнить коллекцию объектами `Card` вручную. С помощью LINQ колоду карт можно создать гораздо быстрее, чем обычным способом. Вместо класса `Card` вы можете создать две последовательности, представляющие масти и ранги соответственно. Вы создадите два очень простых [*метода итератора*](../iterators.md#enumeration-sources-with-iterator-methods), которые будут создавать ранги и масти как <xref:System.Collections.Generic.IEnumerable%601> строк:

```csharp
// Program.cs
// The Main() method

static IEnumerable<string> Suits()
{
    yield return "clubs";
    yield return "diamonds";
    yield return "hearts";
    yield return "spades";
}

static IEnumerable<string> Ranks()
{
    yield return "two";
    yield return "three";
    yield return "four";
    yield return "five";
    yield return "six";
    yield return "seven";
    yield return "eight";
    yield return "nine";
    yield return "ten";
    yield return "jack";
    yield return "queen";
    yield return "king";
    yield return "ace";
}
```

Разместите их под методом `Main` в вашем файле `Program.cs`. Оба эти два метода используют синтаксис `yield return`, создавая последовательность по мере выполнения. Компилятор создаст объект, который реализует интерфейс <xref:System.Collections.Generic.IEnumerable%601>, и сохранит в него последовательность строк по мере их получения.

Теперь с помощью этих методов итератора создайте колоду карт. Поместите запрос LINQ в метод `Main`. Это описано ниже:

```csharp
// Program.cs
static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    // Display each card that we've generated and placed in startingDeck in the console
    foreach (var card in startingDeck)
    {
        Console.WriteLine(card);
    }
}
```

Несколько выражений `from` создают запрос <xref:System.Linq.Enumerable.SelectMany%2A>, который формирует одну последовательность из сочетаний каждого элемента первой последовательности с каждым элементом второй последовательности. Для нашего примера важен порядок последовательности. Первый элемент первой последовательности (масти) поочередно сочетается с каждым элементом второй последовательности (ранги). В итоге мы получаем все тринадцать карт первой масти. Этот процесс повторяется для каждого элемента первой последовательности (масти). Конечным результатом является колода карт, упорядоченная сначала по мастям, а затем по достоинствам.

Важно помнить, что независимо от того, будете ли вы записывать LINQ в синтаксисе запросов, показанном выше, или вместо этого будете использовать синтаксис методов, вы всегда можете перейти от одной формы синтаксиса к другой. Приведенный выше запрос, записанный в синтаксисе запросов, можно записать в синтаксис метода следующим образом:

```csharp
var startingDeck = Suits().SelectMany(suit => Ranks().Select(rank => new { Suit = suit, Rank = rank }));
```

Компилятор преобразует инструкции LINQ, написанные с помощью синтаксиса запросов, в эквивалентный синтаксис вызова метода. Таким образом, независимо от выбранного синтаксиса, две версии запроса дают одинаковый результат. Выберите, какой синтаксис лучше всего подходит для вашей ситуации. Например, если вы работаете в команде, в которой у некоторых участников есть сложности с синтаксисом метода, попробуйте использовать синтаксис запроса.

Теперь давайте выполним пример, который вы создали к этому моменту. Он отобразит все 52 карты колоды. Возможно, вам будет интересно выполнить этот пример в отладчике и проследить за выполнением методов `Suits()` и `Ranks()`. Вы сможете заметить, что каждая строка в каждой последовательности создается только по мере необходимости.

![Окно консоли с приложением, которое выводит 52 карты](./media/working-with-linq/console-52-card-application.png)

## <a name="manipulating-the-order"></a>Управление порядком

Теперь рассмотрим, как вы будете тасовать карты в колоде. Чтобы хорошо потасовать, сначала необходимо разделить колоду на две части. Эту возможность вам предоставят методы <xref:System.Linq.Enumerable.Take%2A> и <xref:System.Linq.Enumerable.Skip%2A>, входящие в интерфейсы API LINQ. Поместите их под циклом `foreach`:

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    // 52 cards in a deck, so 52 / 2 = 26
    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
}
```

В стандартной библиотеке нет метода для тасовки, которым можно было бы воспользоваться, поэтому вам нужно написать собственный. Метод для тасовки, который вы создадите, иллюстрирует несколько приемов, которые вы будете использовать в программах на основе LINQ, поэтому каждая часть этого процесса будет описана в действиях.

Чтобы добавить некоторые функции для взаимодействия с <xref:System.Collections.Generic.IEnumerable%601>, который будет возвращен в запросах LINQ, вам потребуется написать особые методы, называемые [методами расширения](../../csharp/programming-guide/classes-and-structs/extension-methods.md). Короче говоря, метод расширения представляет собой специализированный *статический метод*, добавляющий новые функциональные возможности в уже имеющийся тип без изменения исходного типа, в который необходимо добавить функциональные возможности.

Переместите методы расширения в другое расположение, добавив новый файл *статического* класса в программу с именем `Extensions.cs`, а затем приступите к разработке первого метода расширения:

```csharp
// Extensions.cs
using System;
using System.Collections.Generic;
using System.Linq;

namespace LinqFaroShuffle
{
    public static class Extensions
    {
        public static IEnumerable<T> InterleaveSequenceWith<T>(this IEnumerable<T> first, IEnumerable<T> second)
        {
            // Your implementation will go here soon enough
        }
    }
}
```

Обратите внимание на сигнатуру метода, в частности на параметры:

```csharp
public static IEnumerable<T> InterleaveSequenceWith<T> (this IEnumerable<T> first, IEnumerable<T> second)
```

Как вы видите, для первого аргумента этого метода добавлен модификатор `this`. Это означает, что метод вызывается так, как если бы он был методом-членом и имел тип, указанный для первого аргумента. Такое объявление методов соответствует стандартному принципу, по которому для входа и выхода используется тип `IEnumerable<T>`. Такая практика позволяет объединять методы LINQ в цепочку, чтобы создавать более сложные запросы.

Очевидно, что так как вы разделили колоду на две части, их необходимо соединить. В коде это означает, что необходимо перечислить обе последовательности, полученные с помощью <xref:System.Linq.Enumerable.Take%2A> и <xref:System.Linq.Enumerable.Skip%2A> за один раз, применяя команду *`interleaving`* к элементам и создавая одну последовательность: колода карт, которая тасуется сейчас. Чтобы создать метод LINQ, который работает с двумя последовательностями, важно хорошо понимать принципы работы <xref:System.Collections.Generic.IEnumerable%601>.

Интерфейс <xref:System.Collections.Generic.IEnumerable%601> содержит один метод: <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>. Этот метод <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> возвращает объект, у которого есть метод для перехода к следующему элементу и свойство, которое возвращает текущий элемент в последовательности. С помощью этих двух членов вы выполните перебор всей коллекции и получение элементов. Метод Interleave будет реализован как метод итератора, поэтому вы не будете создавать и возвращать коллекцию, а примените описанный выше синтаксис `yield return`.

Так выглядит реализация этого метода:

[!CODE-csharp[InterleaveSequenceWith](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet1)]

Теперь, добавив в проект этот метод, вернитесь к методу `Main` и один раз перетасуйте колоду:

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
    var shuffle = top.InterleaveSequenceWith(bottom);

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }
}
```

## <a name="comparisons"></a>Сравнения

Через сколько тасовок колода снова соберется в исходном порядке? Чтобы узнать это, вам нужно написать метод, который проверяет равенство двух последовательностей. Создав такой метод, вы поместите код тасовки колоды в цикл, в котором будете проверять, расположены ли карты в правильном порядке.

Метод, который сравнивает две последовательности, будет очень простым. По структуре он похож на метод, который мы создали для тасовки колоды. Но теперь вместо команды `yield return`, которая возвращает элементы, вы будете сравнивать элементы каждой последовательности. Если перечисление последовательности завершилось и все элементы попарно совпадают, то последовательности считаются одинаковыми:

[!CODE-csharp[SequenceEquals](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet2)]

Здесь мы видим в действии второй принцип LINQ: терминальные методы. Они принимают последовательность в качестве входных данных (или две последовательности, как в нашем примере) и возвращают скалярное значение. В цепочке методов для запроса LINQ терминальные методы всегда используются последними, отсюда и название "терминальный".

Этот принцип мы применяем при определении того, находится ли колода в исходном порядке. Поместите код тасовки в цикл, который будет останавливаться в том случае, когда порядок последовательности восстановлен. Для проверки примените метод `SequenceEquals()`. Как вы уже поняли, этот метод всегда будет последним в любом запросе, поскольку он возвращает одиночное значение, а не последовательность:

```csharp
// Program.cs
static void Main(string[] args)
{
    // Query for building the deck

    // Shuffling using InterleaveSequenceWith<T>();

    var times = 0;
    // We can re-use the shuffle variable from earlier, or you can make a new one
    shuffle = startingDeck;
    do
    {
        shuffle = shuffle.Take(26).InterleaveSequenceWith(shuffle.Skip(26));

        foreach (var card in shuffle)
        {
            Console.WriteLine(card);
        }
        Console.WriteLine();
        times++;

    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

Выполните код и обратите внимание на то, как выполняется переупорядочивание колоды при каждой тасовке. После 8 тасовок (итераций цикла do-while), колода возвращается к исходной конфигурации, в которой она находилась при создании из начального запроса LINQ.

## <a name="optimizations"></a>Оптимизация

Пример, который вы создали к этому моменту, выполняет *внутреннюю тасовку*, то есть первая и последняя карты колоды сохраняют свои позиции после каждой итерации. Давайте внесем одно изменение: вместо этого мы будем использовать *внешнюю тасовку*, при которой все 52 карты изменяют свои позиции. Для этого колоду нужно собирать так, чтобы первой картой в колоде стала первая карта из нижней половины. Тогда самой нижней картой станет последняя карта из верхней половины колоды. Это простое изменение в одной строке кода. Обновите текущий запрос тасовки, переключив положения <xref:System.Linq.Enumerable.Take%2A> и <xref:System.Linq.Enumerable.Skip%2A>. Это поменяет местами нижнюю и верхнюю половины колоды:

```csharp
shuffle = shuffle.Skip(26).InterleaveSequenceWith(shuffle.Take(26));
```

Снова запустите программу, и вы увидите, что для восстановления исходного порядка теперь требуется 52 итерации. Также вы могли обратить внимание, что по мере выполнения программы она заметным образом замедляется.

Для этого есть сразу несколько причин. Вы можете решить одну из самых существенных причин спада производительности — неэффективное использование [*отложенного вычисления*](../programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).

Короче говоря, отложенное вычисление означает, что вычисление инструкции не выполняется, пока не понадобится ее значение. Запросы LINQ — это инструкции, которые обрабатываются отложенным образом. Последовательности создаются только тогда, когда происходит обращение к их элементам. Обычно это дает LINQ огромное преимущество. Но в некоторых программах, таких как в нашем примере, это приводит к экспоненциальному росту времени выполнения.

Помните, что мы создали исходную колоду с помощью запроса LINQ. Каждая последующая тасовка выполняет три запроса LINQ к колоде, полученной на предыдущем этапе. И все эти запросы выполняются отложенно. В частности, это означает, что запросы выполняются каждый раз при обращении к последовательности. Таким образом, пока вы доберетесь до 52-й итерации, исходная колода будет заново создана очень много раз. Чтобы наглядно это продемонстрировать, давайте создадим журнал выполнения. Затем вы исправите эту проблему.

В вашем файле `Extensions.cs` введите или скопируйте приведенный ниже метод. Этот метод расширения создает файл с именем `debug.log` в каталоге проекта и записывает в файл журнала, какой запрос выполняется в данный момент. Этот метод расширения можно добавить к любому запросу, чтобы зафиксировать его выполнение.

[!CODE-csharp[LogQuery](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet3)]

Теперь давайте дополним определение каждого запроса сообщением для журнала:

```csharp
// Program.cs
public static void Main(string[] args)
{
    var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                        from r in Ranks().LogQuery("Rank Generation")
                        select new { Suit = s, Rank = r }).LogQuery("Starting Deck");

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }

    Console.WriteLine();
    var times = 0;
    var shuffle = startingDeck;

    do
    {
        // Out shuffle
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26)
            .LogQuery("Bottom Half"))
            .LogQuery("Shuffle");
        */

        // In shuffle
        shuffle = shuffle.Skip(26).LogQuery("Bottom Half")
                .InterleaveSequenceWith(shuffle.Take(26).LogQuery("Top Half"))
                .LogQuery("Shuffle");

        foreach (var c in shuffle)
        {
            Console.WriteLine(c);
        }

        times++;
        Console.WriteLine(times);
    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

Обратите внимание, что запись в журнал не нужно выполнять при обращении к запросу. Она выполняется только при создании исходного запроса. Программа по-прежнему работает очень долго, но теперь вы хорошо видите, почему. Если у вас не хватит терпения выполнять внешнюю тасовку с ведением журнала, переключите программу обратно на внутреннюю тасовку. На ней вы также заметите влияние отложенного вычисления. За один запуск программа выполняет 2592 запроса, если учитывать все создания мастей и достоинств.

Вы можете повысить производительность кода, чтобы уменьшить количество выполнений. Простой способ исправить — *кэшировать* результаты исходного запроса LINQ, который создает колоду карт. В настоящее время вы выполняете запросы снова и снова каждый раз, когда цикл do-while проходит через итерацию, повторно создавая и перетасовывая колоду карт. Чтобы кэшировать колоду карт, вы можете использовать методы LINQ <xref:System.Linq.Enumerable.ToArray%2A> и <xref:System.Linq.Enumerable.ToList%2A>. Когда вы добавляете их в запросы, они будут выполнять те действия, которые вы указали, но теперь они будут хранить результаты в массиве или списке в зависимости от того, какой метод вы вызовете. Добавьте метод LINQ <xref:System.Linq.Enumerable.ToArray%2A> в оба запроса и снова запустите программу:

[!CODE-csharp[Main](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet1)]

Теперь при внутренней тасовке выполняется всего 30 запросов. Переключите программу на внешнюю тасовку, и вы заметите аналогичное улучшение: теперь выполняется 162 запроса.

Обратите внимание, что этот пример лишь **демонстрирует** варианты использования, в которых отложенное вычисление приводит к проблемам с производительностью. Хотя очень важно знать, когда отложенное вычисление может повлиять на производительность кода, не менее важно понимать, что не все запросы должны выполняться упреждающе. Если не использовать <xref:System.Linq.Enumerable.ToArray%2A>, производительность снизится. Это связано с тем, что каждое новое расположение карт вычисляется на основе предыдущего расположения. Использование отложенного вычисления означает, что каждое расположение колоды строится с самого начала, из исходной колоды, включая вызов кода для создания `startingDeck`. Это создает огромный объем дополнительной работы.

На практике некоторые алгоритмы хорошо работают с упреждающим вычислением, а другие хорошо выполняются с отложенным вычислением. Для ежедневного использования отложенное вычисление обычно дает более хороший результат, если в качестве источника данных используется отдельный процесс, например база данных. Для баз данных отложенное вычисление позволяет сложным запросам выполнять только один круговой путь к процессу базы данных и обратно к оставшемуся коду. LINQ является гибким, независимо от того, используете ли вы отложенное или упреждающее вычисление, поэтому измерьте процессы и выберите тип вычислений, который обеспечивает наилучшую производительность.

## <a name="conclusion"></a>Заключение

В этом проекте вы изучили:
- использование запросов LINQ для агрегирования данных в осмысленную последовательность;
- запись методов расширения для добавления собственных пользовательских функций в запросы LINQ;
- поиск областей в коде, где могут возникнуть проблемы с производительностью наших запросов LINQ, например снижение скорости;
- упреждающее и отложенное вычисление в отношении запросов LINQ и их влияние на производительность запросов.

Помимо LINQ вы узнали об использовании метода, который иллюзионисты используют для карточных фокусов. Они используют тасовку по методу Фаро, потому что она позволяет хорошо контролировать положение каждой карты в колоде. Теперь, когда вы все это знаете, не рассказывайте это остальным!

Дополнительные сведения о LINQ см. в следующих статьях:
- [LINQ](../programming-guide/concepts/linq/index.md)
  - [Введение в LINQ](../programming-guide/concepts/linq/index.md)
  - [Основные операции запросов LINQ (C#)](../programming-guide/concepts/linq/basic-linq-query-operations.md)
  - [Преобразования данных с помощью LINQ (C#)](../programming-guide/concepts/linq/data-transformations-with-linq.md)
  - [Синтаксис запросов и синтаксис методов в LINQ (C#)](../programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)
  - [Возможности C#, поддерживающие LINQ](../programming-guide/concepts/linq/features-that-support-linq.md)
    