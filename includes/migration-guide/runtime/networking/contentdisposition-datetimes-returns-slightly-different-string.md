---
ms.openlocfilehash: 705bbd0e0bf80e0726d41898685a5e166e039f99
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774157"
---
### <a name="contentdisposition-datetimes-returns-slightly-different-string"></a>ContentDisposition DateTime возвращает немного другую строку

|   |   |
|---|---|
|Подробные сведения|Строковые представления <xref:System.Net.Mime.ContentDisposition?displayProperty=name> были обновлены, начиная с версии 4.6, чтобы всегда представлять компонент часа <xref:System.DateTime?displayProperty=name> с использованием двух цифр. Это сделано в соответствии с [RFC822](https://www.ietf.org/rfc/rfc0822.txt) и [RFC2822](https://www.ietf.org/rfc/rfc2822.txt). В результате <xref:System.Net.Mime.ContentDisposition.ToString> возвращает немного другую строку в 4.6 в сценариях, где один из элементов времени расположения имел значение, предшествующее 10:00. Обратите внимание, что ContentDispositions иногда сериализуются посредством преобразования в строки, поэтому следует проверить все операции <xref:System.Net.Mime.ContentDisposition.ToString>, сериализации или вызовы GetHashCode.|
|Предложение|Не ожидается, что строковые представления ContentDispositions из разных версий .NET Framework будут правильно сравниваться друг с другом. Если возможно, перед сравнением преобразуйте строки обратно в ContentDispositions.|
|Область|Дополнительный номер|
|Версия|4.6|
|Тип|Среда выполнения|
|Затронутые API|<ul><li><xref:System.Net.Mime.ContentDisposition.ToString?displayProperty=nameWithType></li><li><xref:System.Net.Mime.ContentDisposition.GetHashCode?displayProperty=nameWithType></li></ul>|
