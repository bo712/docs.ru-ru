---
ms.openlocfilehash: 3cff9bfbb1adb6004921903276d75f641c7e703c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774192"
---
### <a name="contractinvariant-or-contractrequirestexception-do-not-consider-stringisnullorempty-to-be-pure"></a>Contract.Invariant или Contract.Requires\<TException> не учитывает необходимость чистоты String.IsNullOrEmpty

|   |   |
|---|---|
|Подробные сведения|В приложениях, предназначенных для .NET Framework 4.6.1, если контракт инвариантности для <xref:System.Diagnostics.Contracts.Contract.Invariant%2A?displayProperty=nameWithType> или контракт предусловия для <xref:System.Diagnostics.Contracts.Contract.Requires%2A?displayProperty=nameWithType)> вызывает метод <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType>, средство перезаписи выдает предупреждение компилятора CC1036: &quot;Обнаружен вызов метода <xref:System.String.IsNullOrWhiteSpace%2A?displayProperty=nameWithType> без [Pure] в методе.&quot; Это предупреждение, а не ошибка компилятора.|
|Предложение|Проблема была устранена в [билете 339 на сайте GitHub](https://github.com/Microsoft/CodeContracts/issues/339). Чтобы устранить это предупреждение, можно скачать и скомпилировать обновленную версию исходного кода для инструментов контрактов кода с сайта [GitHub](https://github.com/Microsoft/CodeContracts/blob/master/README.md). Сведения о скачивании находятся в нижней части страницы.|
|Область|Дополнительный номер|
|Версия|4.6.1|
|Тип|Среда выполнения|
|Затронутые API|<ul><li><xref:System.Diagnostics.Contracts.Contract.Invariant(System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Contracts.Contract.Requires(System.Boolean)?displayProperty=nameWithType></li></ul>|
