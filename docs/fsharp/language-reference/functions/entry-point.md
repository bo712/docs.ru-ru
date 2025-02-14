---
title: Точка входа
description: Узнайте, как установить точку входа F# программы, который компилируется как исполняемого файла, где формально начинается выполнение.
ms.date: 05/16/2016
ms.openlocfilehash: c7aedda5834fb224507bfcecd4688978efa26547
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645454"
---
# <a name="entry-point"></a>Точка входа

В этом разделе описывается метод, который используется для задания точки входа F# программы.

## <a name="syntax"></a>Синтаксис

```fsharp
[<EntryPoint>]
let-function-binding
```

## <a name="remarks"></a>Примечания

В приведенном выше синтаксисе *привязку функция let* является определением функции в `let` привязки.

Точка входа в программу, которая компилируется как исполняемый файл является формально начала выполнения. Укажите точку входа для F# приложения путем применения `EntryPoint` атрибут в программу `main` функции. Эта функция (созданные с помощью `let` привязки) должна быть последней функцией в последнем скомпилированном файле. Последний скомпилированного файла является последний файл проекта или последнего файла, который передается в командную строку.

Функция точки входа имеет тип `string array -> int`. Аргументы, предоставленные в командной строке передаются `main` функции в массив строк. Первый элемент массива является первым аргументом; Имя исполняемого файла не включается в массиве, как в некоторых других языков. Возвращаемое значение используется как код выхода для процесса. Ноль обычно указывает на успешное завершение; ненулевые значения указывают на ошибку. Имеют каких-либо конкретных значений ненулевое коды возврата. значения кодов возврата относятся к конкретным приложениям.

В следующем примере показан простой `main` функции.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/entry-point/snippet501.fs)]

При выполнении этого кода с помощью командной строки `EntryPoint.exe 1 2 3`, результат выглядит следующим образом.

```console
Arguments passed to function : [|"1"; "2"; "3"|]
```

## <a name="implicit-entry-point"></a>Неявная точка входа

Если в программе нет **EntryPoint** атрибут, который явно указывает точку входа, привязки верхнего уровня в последнем файле компилируемом используются в качестве точки входа.

## <a name="see-also"></a>См. также

- [Функции](index.md)
- [Привязки let](let-bindings.md)
