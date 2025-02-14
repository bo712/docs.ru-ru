---
title: Встроенный тип XAML x:Code
ms.date: 03/30/2017
f1_keywords:
- Code
- x:Code
- xCode
helpviewer_keywords:
- Code directive in XAML [XAML Services]
- x:Code XAML directive element [XAML Services]
- XAML [XAML Services], x:Code directive element
ms.assetid: 87986b13-1a2e-4830-ae36-15f9dc5629e8
ms.openlocfilehash: f6898008fa3e3e7e385a2bc77c5b2eac7eeda2ec
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64617157"
---
# <a name="xcode-intrinsic-xaml-type"></a>Встроенный тип XAML x:Code
Позволяет помещать код в рабочем XAML. Такой код может компилироваться либо с любой реализации обработчика XAML, которая компилирует XAML или влево в рабочей среде XAML для использования более поздней версии, например для интерпретации во время выполнения.  
  
## <a name="xaml-object-element-usage"></a>Использование элемента объекта XAML  
  
```  
<x:Code>  
   // code instructions, usually enclosed by CDATA...  
</x:Code>  
```  
  
## <a name="remarks"></a>Примечания  
 Код внутри `x:Code` элемент директивы XAML является по-прежнему интерпретируется в общее пространство имен XML и пространства имен XAML, предоставляемые. Таким образом, это обычно потребует вложить код, используемый для `x:Code` внутри `CDATA` сегмента.  
  
 `x:Code` не допускается для всех возможных механизмов развертывания рабочей среды XAML. Код должен быть скомпилирован в конкретных платформах (например, WPF). В других платформах `x:Code` использования обычно может быть запрещено.  
  
 Для платформ, которые разрешают управляемых `x:Code` содержимого правильного компилятора языка для `x:Code` содержимое определяется параметрами и целевыми объектами содержащего проекта, который используется для компиляции приложения.  
  
## <a name="wpf-usage-notes"></a>Примечания об использовании WPF  
 Код объявлены внутри `x:Code` для WPF, имеет несколько существенных ограничений:  
  
- `x:Code` Элемент директивы должен быть непосредственным дочерним элементом корневого элемента XAML производства.  
  
- [Директива x: Class](x-class-directive.md) должен быть предоставлен в родительском корневом элементе.  
  
- Код помещен в `x:Code` будет рассматриваться при компиляции в пределах разделяемый класс, который уже создан для этой страницы XAML. Поэтому весь код вами необходимо членам или переменным этого разделяемого класса.  
  
- Невозможно определить дополнительные классы, кроме вложенного класса внутри разделяемого класса (допускается вложенность, но он не является типичным, поскольку вложенные классы не могут ссылаться на XAML). Пространства имен CLR, отличном от пространства имен, который используется для существующего разделяемого класса не определены или добавлен.  
  
- Ссылки на сущности кода за пределами пространства имен CLR разделяемого класса должен иметь полное имя. Члены объявленные переопределения, чтобы переопределяемые члены разделяемого класса, необходимо указать с помощью ключевого слова переопределения для конкретного языка. Если члены, объявленные в `x:Code` область конфликтуют с членами разделяемого класса, могут быть созданы из XAML, таким образом, что компилятор сообщает конфликт, файл XAML не удается скомпилировать или загрузить.  
  
## <a name="see-also"></a>См. также

- [Директива x:Class](x-class-directive.md)
- [Код программной части и XAML в WPF](../wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [Общие сведения о языке XAML (WPF)](../wpf/advanced/xaml-overview-wpf.md)
