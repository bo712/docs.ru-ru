---
title: Возвращаемые ссылочные значения и ссылочные локальные переменные (руководство по языку C#)
description: Сведения о том, как определять и использовать возвращаемые ссылочные значения и ссылочные локальные переменные
author: rpetrusha
ms.author: ronpet
ms.date: 04/04/2018
ms.openlocfilehash: fcac162f63438b6cbe54908383467d4b0f227c39
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59081852"
---
# <a name="ref-returns-and-ref-locals"></a>Возвращаемые ссылочные значения и ссылочные локальные переменные

Начиная с версии 7.0 язык C# поддерживает значения, возвращаемые по ссылке (возвращаемые ссылочные значения). Возвращаемое ссылочное значение позволяет методу вернуть вызывающей стороне ссылку на переменную, а не фиксированное значение. После этого вызывающий может самостоятельно решить, как обрабатывать полученную переменную: по значению или по ссылке. Вызывающий может создать новую переменную и присвоить ей ссылку на полученное значение (локальная ссылочная переменная).

## <a name="what-is-a-reference-return-value"></a>Что представляет собой возвращаемое ссылочное значение?

Большинство разработчиков прекрасно знакомы с передачей аргумента в вызываемый метод *по ссылке*. Список аргументов вызываемого метода включает переменную, переданную по ссылке. Вызывающий может отследить любые изменения этого значения в вызываемом методе. *Возвращаемое ссылочное значение* означает, что метод возвращает *ссылку* на некоторую переменную (или ее псевдоним). В область действия переменной должен входить этот метод. Время существования переменной должно продолжаться после того, как метод возвращает управление. Все изменения, которые вызывающий производит с возвращаемым значением метода, применяются к возвращенной переменной.

Если для метода объявлено *возвращаемое ссылочное значение*, значит он возвращает псевдоним переменной. Чаще всего это нужно для того, чтобы вызывающий код получил псевдоним для доступа к этой переменной, в том числе для ее изменения. Следовательно, методы с возвращаемыми ссылочными значениями не могут иметь тип возвращаемого значения `void`.

Есть несколько ограничений для выражений, которые можно использовать в качестве возвращаемых ссылочных значений метода. К ним относятся указанные ниже ограничения.

- Время существования возвращаемого значения должно превышать период выполнения метода. Другими словами, нельзя возвращать ссылку на локальную переменную вызываемого метода. Это может быть экземпляр статического поля или класса, а также переданный в метод аргумент. При попытке возвратить локальную переменную возникает ошибка компилятора CS8168 "Невозможно вернуть по ссылке локальный "obj", так как это не локальная переменная ref".

- Возвращаемое значение не может быть литералом `null`. При возврате `null` возникает ошибка компилятора CS8156 "Выражение невозможно использовать в данном контексте, так как его невозможно вернуть по ссылке".

   Метод с возвращаемым ссылочным значением может возвращать псевдоним для переменной с текущим значением null (которой не присвоены экземпляры) или [тип, допускающий значение null](../nullable-types/index.md).
 
- Возвращаемое значение не может быть константой, элементом перечисления, полученным по значению, возвращаемым значением свойства, а также методом `class` или `struct`. При нарушении этого правила возникает ошибка компилятора CS8156 "Выражение невозможно использовать в данном контексте, так как его невозможно вернуть по ссылке".

Кроме того, возвращаемые ссылочные значения недопустимы в асинхронных методах. Асинхронный метод может вернуть управление до того, как будет завершено его выполнение и станет известно его возвращаемое значение.
 
## <a name="defining-a-ref-return-value"></a>Определение возвращаемого ссылочного значения

Метод, который возвращает *возвращаемое значение ссылки*, должен удовлетворять следующим двум условиям:

- Сигнатура метода включает ключевое слово [ref](../../language-reference/keywords/ref.md) перед типом возвращаемого значения.
- Каждый оператор [return](../../language-reference/keywords/return.md) в теле метода включает ключевое слово [ref](../../language-reference/keywords/ref.md) перед именем возвращаемого экземпляра.

В следующем примере показан метод, который удовлетворяет указанным условиям и возвращает ссылку на объект `Person` с именем `p`:

```csharp
public ref Person GetContactInformation(string fname, string lname)
{
    // ...method implementation...
    return ref p;
}
```

## <a name="consuming-a-ref-return-value"></a>Использование возвращаемого ссылочного значения

Возвращаемое ссылочное значение является псевдонимом для другой переменной в области вызываемого метода. Любое применение возвращаемого ссылочного значения можно рассматривать как применение псевдонима соответствующей переменной.

- Присваивая новое значение псевдониму, вы присваиваете это значение переменной, на которую он ссылается.
- Считывая значение псевдонима, вы получаете значение переменной, на которую он ссылается.
- Возвращая псевдоним *по ссылке*, вы возвращаете новый псевдоним для той же переменной.
- Передавая псевдоним другому методу *по ссылке*, вы передаете ссылку на переменную, на которую ссылается псевдоним.
- Создавая для псевдонима [локальную ссылочную переменную](#ref-locals), вы создаете новый псевдоним для той же переменной.

## <a name="ref-locals"></a>Ссылочные локальные переменные

Предположим, что для метода `GetContactInformation` объявлено возвращаемое ссылочное значение:

```csharp
public ref Person GetContactInformation(string fname, string lname)
```

При назначении по значению считывается значение переменной и присваивается это значение новой переменной:

```csharp
Person p = contacts.GetContactInformation("Brandie", "Best");
```

В предыдущем назначении `p` объявлена как локальная переменная. Исходное значение копируется из значения, которое возвращает `GetContactInformation`. Все последующие назначения `p` не затронут значения переменной, которую возвращает `GetContactInformation`. Переменная `p` теперь не является псевдонимом для возвращаемой переменной.

Вы объявляете *локальную ссылочную переменную* и сохраняете в ней псевдоним для исходного значения. В следующем назначении `p` является псевдонимом для переменной, возвращаемой из `GetContactInformation`.

```csharp
ref Person p = ref contacts.GetContactInformation("Brandie", "Best");
```

При дальнейшем применении `p` действует так же, как и возвращаемая из `GetContactInformation` переменная, так как `p` является псевдонимом для этой переменной. Любые изменения `p` затрагивают и переменную, возвращаемую из `GetContactInformation`.

Ключевое слово `ref` используется перед объявлением локальной переменной *и* до вызова метода. 

Вы можете таким же образом обратиться к значению по ссылке. В некоторых случаях обращение к значению по ссылке повышает производительность, поскольку позволяет избежать потенциально затратной операции копирования. Например, в следующей инструкции показано, как можно определить локальное ссылочное значение, используемое для ссылки на значение.

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct;
```

Ключевое слово `ref` используется перед объявлением локальной переменной *и* перед значением во втором примере. Если не указать ключевые слова `ref` одновременно в объявлении и присвоении переменной в обоих примерах, возникает ошибка компилятора CS8172 "Невозможно инициализировать значением переменную по ссылке". 

До версии C# 7.3 ссылочные локальные переменные нельзя было переназначить после инициализации так, чтобы они ссылались на другое хранилище. Это ограничение было снято. В следующем примере демонстрируется переназначение:

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct; // initialization
refLocal = ref anotherVeryLargeStruct; // reassigned, refLocal refers to different storage.
```

 Ссылочные локальные переменные по-прежнему необходимо инициализировать во время объявления.

## <a name="ref-returns-and-ref-locals-an-example"></a>Пример использования возвращаемых ссылочных значений и ссылочных локальных переменных

В следующем примере определяется класс `NumberStore`, в котором хранится массив целочисленных значений. Метод `FindNumber` возвращает по ссылке первое число, которое не меньше переданного в аргументе значения. Если такое число не найдено, метод возвращает число с индексом 0. 

[!code-csharp[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/NumberStore.cs#1)]

В следующем примере вызывается метод `NumberStore.FindNumber`, который извлекает первое значение не меньше 16. После этого вызывающий объект удваивает значение, возвращаемое методом. Как видно из выходных данных этого примера, изменение отражается в значении элементов массива в экземпляре `NumberStore`.

[!code-csharp[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/NumberStore.cs#2)]

Без использования возвращаемых ссылочных значений такая операция выполняется путем возврата индекса элемента массива вместе с его значением. После этого вызывающий объект использует индекс для изменения значения в отдельном вызове метода. Тем не менее вызывающий объект также может изменить индекс для доступа к другим значениям массива и их изменения.  

В следующем примере показано, как можно изменить метод `FindNumber` в версии C# 7.3 или более поздней, чтобы использовать переназначение ссылочной локальной переменной:

[!code-csharp[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/NumberStoreUpdated.cs#1)]

Вторая версия более эффективна в случаях, когда искомое число находится ближе к концу большого массива.

## <a name="see-also"></a>См. также

- [Ключевое слово ref](../../language-reference/keywords/ref.md)
- [Написание безопасного и эффективного кода](../../write-safe-efficient-code.md)
