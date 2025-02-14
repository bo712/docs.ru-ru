---
title: Участники
description: Дополнительные сведения об элементах объекта в F# языка программирования.
ms.date: 05/16/2016
ms.openlocfilehash: 0da704b637a9421aa150aa8d8de504bec858e252
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645157"
---
# <a name="members"></a>Участники

Эта статья описывает элементы типов объектов F#.

## <a name="remarks"></a>Примечания

*Элементы* являются компонентами, которые входят в состав определения типа и объявляются с помощью ключевого слова `member`. Типы объектов F#, такие как записи, классы, размеченные объединения, интерфейсы и структуры, поддерживают элементы. Дополнительные сведения см. в статьях [Записи](../records.md), [Классы](../classes.md), [Размеченные объединения](../discriminated-Unions.md), [Интерфейсы](../interfaces.md) и [Структуры](../structures.md).

Обычно элементы составляют открытый интерфейс для типа, поэтому они считаются открытыми, если не указано иное. Элементы также можно объявлять как закрытые или внутренние. Дополнительные сведения см. в статье [Управление доступом](../access-Control.md). Сигнатуры для типов также можно использовать, чтобы предоставлять или не предоставлять определенные элементы типа. Дополнительные сведения см. в статье [Сигнатуры](../signatures.md).

Частные поля и привязки `do`, которые используются только с классами, не являются подлинными элементами, так как они никогда входят в состав открытого интерфейса типа и не объявляются с помощью ключевого слова `member`, но они также описаны в этой статье.

## <a name="related-topics"></a>См. также

|Раздел|Описание|
|-----|-----------|
|[Привязки `let` в классах](let-bindings-in-classes.md)|Описывает определение частных полей и функций в классах.|
|[Привязки `do` в классах](do-bindings-in-classes.md)|Описывает указание кода инициализации объекта.|
|[Свойства](properties.md)|Описывает элементы свойств в классах и других типах.|
|[Индексированные свойства](indexed-properties.md)|Описывает массивоподобные свойства в классах и других типах.|
|[Методы](methods.md)|Описывает функции, являющиеся элементами типа.|
|[Конструкторы](constructors.md)|Описывает специальные функции, инициализирующие объекты типа.|
|[Перегрузка операторов](../operator-overloading.md)|Описывает определение настраиваемых операторов для типов.|
|[События](events.md)|Описывается определение событий и поддержку обработки событий в F#.|
|[Явные поля. Ключевое слово `val`](explicit-fields-the-val-keyword.md)|Описывает определение неинициализированных полей в типе.|
