---
title: Исключение комментария XML должно иметь атрибут cref
ms.date: 07/20/2015
f1_keywords:
- bc42319
- vbc42319
helpviewer_keywords:
- BC42319
ms.assetid: 62eeeba3-6811-48be-b1ef-c2e4feda3177
ms.openlocfilehash: 91bde92e2184c90b14838a09a89a6d261447f139
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662611"
---
# <a name="xml-comment-exception-must-have-a-cref-attribute"></a>Исключение комментария XML должно иметь атрибут cref
\<Исключение > тег предоставляет способ для документирования исключений, которые могут быть созданы с помощью метода. Необходимая `cref` атрибут назначает имя элемента, которое проверяется генератором документации. Если элемент существует, он преобразуется в каноническое имя элемента в файле документации.  
  
 **Идентификатор ошибки:** BC42319  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
- Добавление `cref` атрибут исключение следующим образом:  
  
    ```  
    '''<exception cref="member">description</exception>  
    ```  
  
## <a name="see-also"></a>См. также

- [\<exception>](../../../visual-basic/language-reference/xmldoc/exception.md)
- [Практическое руководство. Создание XML-документации](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
- [XML-теги для комментариев](../../../visual-basic/language-reference/xmldoc/index.md)
