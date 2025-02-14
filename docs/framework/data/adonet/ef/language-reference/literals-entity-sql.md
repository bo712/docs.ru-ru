---
title: Литералы (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 092ef693-6e5f-41b4-b868-5b9e82928abf
ms.openlocfilehash: bff9b1907d3424dc2e3df80480b6ab12f5ab9261
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61760666"
---
# <a name="literals-entity-sql"></a>Литералы (Entity SQL)
В этом разделе рассматривается поддержка литералов в [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## <a name="null"></a>Null  
 Литерал null используется для представления значения NULL применительно к любому типу. Литерал null является совместимым с любым типом.  
  
 Типизированные значения null могут быть созданы путем применения операции приведения к типу по отношению к литералу NULL. Дополнительные сведения см. в разделе [ПРИВЕДЕНИЯ](../../../../../../docs/framework/data/adonet/ef/language-reference/cast-entity-sql.md).  
  
 Для правил о том, где бесплатно с плавающей запятой литералы null можно использовать, см. в разделе [литералы Null и вывод типов](../../../../../../docs/framework/data/adonet/ef/language-reference/null-literals-and-type-inference-entity-sql.md).  
  
## <a name="boolean"></a>Boolean  
 Логические литералы могут быть представлены с помощью ключевых слов `true` и `false`.  
  
## <a name="integer"></a>Целое число  
 Целочисленные литералы могут иметь тип <xref:System.Int32> или <xref:System.Int64>. Литерал <xref:System.Int32> представляет собой ряд цифр. Литерал <xref:System.Int64> представляет собой ряд цифр, за которыми следует прописная буква L.  
  
## <a name="decimal"></a>Десятичное число  
 Число с фиксированной запятой (десятичное) представляет собой последовательность цифр, запятую (,) и еще одну последовательность цифр, за которой следует прописная буква «М».  
  
## <a name="float-double"></a>С плавающей запятой  
 Число с плавающей запятой двойной точности представляет собой ряд цифр, запятую (,) и еще один ряд цифр, за которыми может следовать показатель степени. Число с плавающей запятой одинарной точности (или просто число с плавающей запятой) представляет собой число с синтаксисом числа с плавающей запятой двойной точности, за которым следует строчная буква f.  
  
## <a name="string"></a>String  
 Строка - это ряд символов, заключенных в кавычки. Кавычки могут быть либо одинарными (`'`), либо двойными ("). Символьные строковые литералы могут быть представлены либо в Юникоде, либо в кодировке, отличной от Юникода. Чтобы объявить символьный строковый литерал как представленный в Юникоде, необходимо обозначить литерал префиксом в виде прописной буквы «N». По умолчанию символьные строковые литералы рассматриваются как имеющие кодировку, отличную от Юникода. Не должно быть пробелов между буквой N и полезными данными строкового литерала, а буква N должна быть прописной.  
  
```  
'hello' -- non-Unicode character string literal  
N'hello' -- Unicode character string literal  
"x"  
N"This is a string!"  
'so is THIS'  
```  
  
## <a name="datetime"></a>DateTime  
 Литерал даты-времени является не зависимым от языкового стандарта и состоит из части даты и части времени. Обе части - и даты, и времени - являются обязательными, и какие-либо значения по умолчанию не предусмотрены.  
  
 Часть даты должна иметь формат: `YYYY` - `MM` - `DD`, где `YYYY` представляет собой значение года из четырех цифр между 0001 и 9999, `MM` -месяц со значением от 1 до 12 и `DD` — значение дня, действителен в течение данного месяца `MM`.  
  
 Часть времени должна иметь формат: `HH`:`MM`[:`SS`, где `HH` представляет собой значение часа от 0 до 23 включительно, `MM` - значение минут от 0 до 59 включительно, `SS` - значение секунд от 0 до 59 включительно, а fffffff - значение долей секунд от 0 до 9999999 включительно. Все диапазоны значений являются включительными. Часть, содержащая доли секунды, является необязательной. Часть, содержащая секунды, является необязательной, если не была задана часть с долями секунды. В последнем случае часть с секундами обязательна. Если секунды или доли секунд не заданы, то по умолчанию используется значение ноль.  
  
 Между символом DATETIME и полезными данными литерала может быть любое количество пробелов, но не должно быть новых строк.  
  
```  
DATETIME'2006-10-1 23:11'  
DATETIME'2006-12-25 01:01:00.0000000' -- same as DATETIME'2006-12-25 01:01'  
```  
  
## <a name="time"></a>Время  
 Литерал time является независимым от языкового стандарта и состоит только из части времени. Часть времени является обязательной, и для нее не существует значения по умолчанию. Она должна иметь формат HH:MM[:SS[.fffffff]], где HH представляет собой значение часа от 0 до 23 включительно, MM - значение минут от 0 до 59 включительно, SS - значение секунд от 0 до 59 включительно, а fffffff - значение долей секунд от 0 до 9999999 включительно. Все диапазоны значений являются включительными. Часть, содержащая доли секунды, является необязательной. Часть, содержащая секунды, является необязательной, если не была задана часть с долями секунды. В последнем случае часть с секундами обязательна. Если секунды или доли секунды не заданы, то по умолчанию используется значение ноль.  
  
 Между символом TIME и полезными данными литерала может быть любое количество пробелов, но не должно быть новых строк.  
  
```  
TIME‘23:11’  
TIME‘01:01:00.1234567’  
```  
  
## <a name="datetimeoffset"></a>DateTimeOffset  
 Литерал datetimeoffset является независимым от языкового стандарта и состоит из части даты и части времени. Части даты, времени и смещения являются обязательными, и какие-либо значения по умолчанию не предусмотрены. Часть даты должна иметь формат YYYY-MM-DD, где YYYY представляет собой значение года из четырех цифр между 0001 и 9999, MM - месяц со значением от 1 до 12, а DD - значение суток, допустимое для данного месяца. Часть времени должна иметь формат HH:MM[:SS[.fffffff]], где HH представляет собой значение часа от 0 до 23 включительно, MM - значение минут от 0 до 59 включительно, SS - значение секунд от 0 до 59 включительно, а fffffff - значение долей секунды от 0 до 9999999 включительно. Все диапазоны значений являются включительными. Часть, содержащая доли секунды, является необязательной. Часть, содержащая секунды, является необязательной, если не была задана часть с долями секунды. В последнем случае часть с секундами обязательна. Если секунды или доли секунды не заданы, то по умолчанию используется значение ноль. Часть смещения должна иметь формат {+&#124;-} чч: мм, где HH и MM имеют то же значение, и в части времени. Значение смещения, однако, должно находиться в пределах от -14:00 до +14:00  
  
 Между символом DATETIMEOFFSET и полезными данными литерала может быть любое количество пробелов, но не должно быть новых строк.  
  
```  
DATETIMEOFFSET‘2006-10-1 23:11 +02:00’  
DATETIMEOFFSET‘2006-12-25 01:01:00.0000000 -08:30’  
```  
  
> [!NOTE]
>  Допустимое значение литерала Entity SQL может находиться вне допустимого диапазона CLR или источника данных. В этом случае может возникнуть исключение.  
  
## <a name="binary"></a>Бинарный  
 Двоичный строковый литерал представляет собой последовательность шестнадцатеричных цифр, заключенную в одинарные кавычки, следующую за ключевым словом binary или символом сокращения `X` или `x`. Символ сокращения `X` без учета регистра. Допускается наличие нуля и более пробелов между ключевым словом `binary` и двоичным строковым значением.  
  
 Шестнадцатеричные символы также являются нечувствительными к регистру. Если литерал состоит из нечетного количества шестнадцатеричных цифр, то литерал выравнивается вправо к следующей четной шестнадцатеричной цифре путем применения к нему префикса в виде шестнадцатеричной цифры ноль. На размер двоичной строки не распространяются какие-либо ограничения, определяемые форматом.  
  
```  
Binary'00ffaabb'  
X'ABCabc'  
BINARY    '0f0f0f0F0F0F0F0F0F0F'  
X'' –- empty binary string  
```  
  
## <a name="guid"></a>Guid  
 Литерал `GUID` представляет собой идентификатор GUID. Он является последовательностью, сформированной ключевым словом `GUID` следуют шестнадцатеричные цифры в форме, известной как *реестра* формат: цифры 8-4-4-4-12, заключенные в одинарные кавычки. Шестнадцатеричные цифры являются нечувствительными к регистру.  
  
 Между символом GUID и полезными данными литерала может быть любое количество пробелов, но не должно быть новых строк.  
  
```  
Guid'1afc7f5c-ffa0-4741-81cf-f12eAAb822bf'  
GUID  '1AFC7F5C-FFA0-4741-81CF-F12EAAB822BF'  
```  
  
## <a name="see-also"></a>См. также

- [Общие сведения об Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)
