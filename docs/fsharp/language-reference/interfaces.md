---
title: интерфейсов,
description: Узнайте, как F# интерфейсы задают наборы связанных элементов, реализуемых другими классами.
ms.date: 05/16/2016
ms.openlocfilehash: 5b57769af6c05b83b3a112635033abf4efaca772
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645375"
---
# <a name="interfaces"></a>интерфейсов,

*Интерфейсы* указать наборы связанных элементов, реализуемых другими классами.

## <a name="syntax"></a>Синтаксис

```fsharp
// Interface declaration:
[ attributes ]
type [accessibility-modifier] interface-name =
    [ interface ]     [ inherit base-interface-name ...]
    abstract member1 : [ argument-types1 -> ] return-type1
    abstract member2 : [ argument-types2 -> ] return-type2
    ...
[ end ]

// Implementing, inside a class type definition:
interface interface-name with
    member self-identifier.member1argument-list = method-body1
    member self-identifier.member2argument-list = method-body2

// Implementing, by using an object expression:
[ attributes ]
let class-name (argument-list) =
    { new interface-name with
        member self-identifier.member1argument-list = method-body1
        member self-identifier.member2argument-list = method-body2
        [ base-interface-definitions ]
    }
    member-list
```

## <a name="remarks"></a>Примечания

Объявления интерфейса похоже на объявление класса за исключением того, что члены не реализуются. Вместо этого все члены являются абстрактными, обозначенный ключевое слово `abstract`. Вы не укажете тела метода для абстрактных методов. Тем не менее, можно добавить реализацию по умолчанию, также указав отдельное определение члена как метода с `default` ключевое слово. Это эквивалентно созданию виртуальный метод в базовом классе в других языках .NET. Виртуальный метод может переопределяться в классах, реализующих интерфейс.

Доступность по умолчанию для интерфейсов `public`.

Можно присвоить каждого параметра метода имя, с помощью обычного F# синтаксис:

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet24032.fs)]

В указанных выше `ISprintable` примере `Print` метод имеет один параметр типа `string` с именем `format`.

Существует два способа реализации интерфейсов: с помощью выражений объектов и с помощью типов классов. В любом случае выражение типа или объекта класса предоставляет тел методов для абстрактных методов интерфейса. Реализации для каждого типа, который реализует интерфейс. Таким образом методы интерфейса на разных типах, может отличаться друг от друга.

Ключевые слова `interface` и `end`, отмечающие начало и конец определения, являются необязательными, если используется упрощенный синтаксис. Если вы не используете эти ключевые слова, компилятор пытается определить, является ли тип классом или интерфейсом, анализируя конструкции, которые можно использовать. Если определение элемента или использовать другой синтаксис класса, тип интерпретируется как класс.

Стиль написания кода .NET является начало интерфейсов с заглавной буквы `I`.

## <a name="implementing-interfaces-by-using-class-types"></a>Реализация интерфейсов с помощью типов классов

Один или несколько интерфейсов можно реализовать в типе класса с помощью `interface` ключевое слово, имя интерфейса и `with` ключевое слово, и определения членов интерфейса, как показано в следующем коде.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2801.fs)]

Реализации интерфейса наследуются, поэтому всем производным классам не нужно повторно реализовать их.

## <a name="calling-interface-methods"></a>Вызов методов интерфейса

Методы интерфейса может вызываться только через интерфейс, не с помощью любого объекта типа, который реализует интерфейс. Таким образом, может потребоваться привести к типу интерфейса с помощью `:>` оператор или `upcast` оператор для вызова этих методов.

Для вызова метода интерфейса, при наличии объекта типа `SomeClass`, необходимо привести объект к типу интерфейса, как показано в следующем коде.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2802.fs)]

Альтернативой является объявление метода для объекта, приводит и вызывает метод интерфейса, как показано в следующем примере.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2803.fs)]

## <a name="implementing-interfaces-by-using-object-expressions"></a>Реализация интерфейсов с помощью выражения объекта

Выражения объектов обеспечивают простой способ реализации интерфейса. Они полезны в тех случаях, когда нет необходимости создавать именованный тип, и вам требуется объект, поддерживающий методов интерфейса, без дополнительных методов. В следующем коде показано выражение объекта.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2804.fs)]

## <a name="interface-inheritance"></a>Наследование интерфейса

Интерфейсы могут наследовать от одного или нескольких базовых интерфейсов.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2805.fs)]

## <a name="see-also"></a>См. также

- [Справочник по языку F#](index.md)
- [Выражения объекта](object-expressions.md)
- [Классы](classes.md)
