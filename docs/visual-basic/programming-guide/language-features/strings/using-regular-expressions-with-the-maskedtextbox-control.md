---
title: Использование регулярных выражений в элементе управления MaskedTextBox в Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], regular expressions
- strings [Visual Basic], masked edit
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
ms.openlocfilehash: e0165fb8d573878ae19378b2656d89627680b804
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024512"
---
# <a name="using-regular-expressions-with-the-maskedtextbox-control-in-visual-basic"></a>Использование регулярных выражений в элементе управления MaskedTextBox в Visual Basic
В этом примере показано, как преобразовать простой регулярных выражений для работы с <xref:System.Windows.Forms.MaskedTextBox> элемента управления.  
  
## <a name="description-of-the-masking-language"></a>Описание языка маски  
 Стандартный <xref:System.Windows.Forms.MaskedTextBox> маскирования язык основан на, используемая `Masked Edit` управления в Visual Basic 6.0 и должны быть знакомы пользователи, переходящие с данной платформы.  
  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> Свойство <xref:System.Windows.Forms.MaskedTextBox> элемент управления указывает маски ввода для использования. Маска должна быть строкой, состоящей из одного или нескольких элементов маски из следующей таблицы.  
  
|Элемент маски|Описание|Элемент регулярного выражения|  
|---------------------|-----------------|--------------------------------|  
|0|Любой цифре от 0 до 9. Требуется объект.|\\d|  
|9|Цифра или пробел. Необязательный.|[\d]?|  
|#|Цифра или пробел. Необязательный. Если эта позиция указывается в маске, он будет отображаться как пробел. Плюс (+) и минус (-) допускаются знаки.|[ \d+-]?|  
|L|Буквой ASCII. Требуется объект.|[a-zA-Z]|  
|?|Буквой ASCII. Необязательный.|[a-zA-Z]?|  
|&|Символ. Требуется объект.|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]|  
|В|Символ. Необязательный.|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]?|  
|А|Буквенно-цифровых. Необязательный.|\W|  
|.|Десятичный разделитель, соответствующий язык и региональные параметры.|Недоступно.|  
|,|Соответствующий язык и региональные параметры тысяч разделитель.|Недоступно.|  
|:|Разделитель компонентов времени соответствующего языка и региональных параметров.|Недоступно.|  
|/|Разделитель компонентов даты для соответствующего языка и региональных параметров.|Недоступно.|  
|$|Язык и региональные параметры стандарту символа валюты.|Недоступно.|  
|\<|Преобразует все последующие символы в нижний регистр.|Недоступно.|  
|>|Преобразует все последующие символы в верхнем регистре.|Недоступно.|  
|&#124;|Отмена предыдущего изменения вверх или выполнить сдвиг.|Недоступно.|  
|&#92;|Escape-последовательности символов маски литерал. "\\\\" — escape-последовательность для обратной косой черты.|&#92;|  
|Все остальные символы.|Литералы. Все элементы без маски отображаются в <xref:System.Windows.Forms.MaskedTextBox>.|Все остальные символы.|  
  
 Decimal (.), разделитель тысяч (,), времени (:), дата (/) и символы валют ($) по умолчанию отображаются в соответствии с определением языка и региональных параметров приложения. Можно принудительно отображать символы для другого языка и региональных параметров с помощью <xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A> свойство.  
  
## <a name="regular-expressions-and-masks"></a>Регулярные выражения и маски  
 Несмотря на то, что можно использовать регулярные выражения и маски для проверки ввода пользователя, они не являются полностью эквивалентны. Регулярные выражения можно выразить более сложные шаблоны, чем маски, но маски можно выразить те же сведения, более четко и языку и региональным параметрам соответствующий формат.  
  
 В следующей таблице сравниваются четыре регулярных выражений и эквивалентные маску для каждого.  
  
|Регулярное выражение|Маска|Примечания|  
|------------------------|----------|-----------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|`/` Символ в маске является логическим разделителем даты, и он будет отображаться для пользователя как разделитель компонентов даты, подходящие для текущего языка и региональных параметров приложения.|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|Дата (день, сокращенное обозначение месяца и год) в формате США, в котором отображается сокращенное название месяца с начальным прописными буквами следуют две буквы нижнего регистра.|  
|`(\(\d{3}\)-)?\d{3}-d{4}`|`(999)-000-0000`|Номер телефона в США, код города необязательно. Если пользователь не хочет вводить дополнительные символы, она можно ввести пробелы или наведите указатель мыши непосредственно в позиции в маске, представленную первым 0.|  
|`$\d{6}.00`|`$999,999.00`|Значение валюты в диапазоне от 0 до 999999. Валюты, разделителя и десятичные символы будут заменяться во время выполнения их их эквиваленты для данного языка и региональных параметров.|  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>
- <xref:System.Windows.Forms.MaskedTextBox>
- [Проверка строк в Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)
- [Элемент управления MaskedTextBox](../../../../framework/winforms/controls/maskedtextbox-control-windows-forms.md)
