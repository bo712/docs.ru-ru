---
ms.openlocfilehash: 22f8e3bb1ba72379b3f5fc87a077e5fe57f89bf8
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235411"
---
### <a name="null-coalescer-values-are-not-visible-in-debugger-until-one-step-later"></a>Значения NULL операции объединения отображаются в отладчике с запаздыванием на один шаг

|   |   |
|---|---|
|Подробные сведения|Из-за ошибки в .NET Framework 4.5 значения, заданные с использованием операции объединения NULL, не отображаются в отладчике немедленно после выполнения операции присваивания в 64-разрядной версии платформы.|
|Предложение|После выполнения одного дополнительного шага в отладчике локальные значения или значения поля корректно обновляются. Эта проблема также была устранена в .NET Framework 4.6 и может быть решена путем обновления до этой версии платформы.|
|Область|Пограничный случай|
|Версия|4.5|
|Тип|Среда выполнения|
