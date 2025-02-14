---
title: Не удается преобразовать анонимный тип в дерево выражений, поскольку он содержит поле, которое было использовано в инициализации другого поля
ms.date: 07/20/2015
f1_keywords:
- bc36548
- vbc36548
helpviewer_keywords:
- BC36548
ms.assetid: 27de068f-080e-4160-86bf-1ec23fd1925a
ms.openlocfilehash: 045061f403b301d460bc85d161c1d6dee9c7d9f1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64602405"
---
# <a name="cannot-convert-anonymous-type-to-expression-tree-because-it-contains-a-field-that-is-used-in-the-initialization-of-another-field"></a>Не удается преобразовать анонимный тип в дерево выражений, поскольку он содержит поле, которое было использовано в инициализации другого поля
Компилятор не принимает преобразование анонимных в дерево выражения, когда одно свойство анонимного типа используется для инициализации другого свойства анонимного типа. Например, в следующем коде `Prop1` объявлена в списке инициализации, а затем используется в качестве начального значения для `Prop2`.  
  
```vb  
Module M2  
  
    Sub ExpressionExample(Of T)(ByVal x As Expressions.Expression(Of Func(Of T)))  
    End Sub  
  
    Sub Main()  
        ' The following line causes the error.  
        ' ExpressionExample(Function() New With {.Prop1 = 2, .Prop2 = .Prop1})  
  
    End Sub  
End Module  
```  
  
 **Идентификатор ошибки:** BC36548  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
- Назначать начальное значение для `Prop1` локальной переменной. Назначьте этой переменной к обоим `Prop1` и `Prop2`, как показано в следующем коде.  
  
    ```  
    Sub Main()  
  
        Dim temp = 2  
        ExpressionExample(Function() New With {.Prop1 = temp, .Prop2 = temp})  
  
    End Sub  
    ```  
  
## <a name="see-also"></a>См. также

- [Анонимные типы (Visual Basic)](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Expression Trees (Visual Basic)](../../programming-guide/concepts/expression-trees/index.md) (Деревья выражений (Visual Basic))
- [Практическое руководство. Использование деревьев выражений для построения динамических запросов (Visual Basic)](../../programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md)
