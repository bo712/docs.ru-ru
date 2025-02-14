---
title: Копирование и обновление выражений записей
description: Вы можете научиться писать «копировать и обновить выражение», копирует существующую запись или записи в анонимные и обновления поля и возвращает обновленной записи или анонимные записи.
author: ChrSteinert
ms.date: 06/12/2019
ms.openlocfilehash: d16f5ca337047ab2eecc8828b21d8a423bf39a1f
ms.sourcegitcommit: c4dfe37032c64a1fba2cc3d5947550d79f95e3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041739"
---
# <a name="copy-and-update-record-expressions"></a>Копирование и обновление выражений записей

Объект *копирование и обновление выражений записей* выражение, которое копирует существующую запись, затем обновляет указанные поля и возвращает обновленной записи.

## <a name="syntax"></a>Синтаксис

```fsharp
{ record-name with
    updated-labels }

{| anonymous-record-name with
    updated-labels |}
```

## <a name="remarks"></a>Примечания

Записи и анонимный записи являются неизменяемыми по умолчанию, таким образом, возможна по существующей записи не обновляются. Для создания обновленной записи все поля записи придется задать снова. Для упрощения этой задачи *копирование и обновление выражений* может использоваться. Это выражение принимает существующую запись, создает новый того же типа, используя указанные поля из выражения и отсутствует поле, указанных с помощью выражения.

Это может быть полезно, если необходимо скопировать существующую запись и при необходимости измените некоторые значения поля.

Возьмем например созданной записи.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

Если пришлось обновлять только в поле этой записи можно использовать *копирование и обновление выражений записей* следующим образом:

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

## <a name="see-also"></a>См. также

- [Записи](records.md)
- [Анонимные записей](anonymous-records.md)
- [Справочник по языку F#](index.md)
