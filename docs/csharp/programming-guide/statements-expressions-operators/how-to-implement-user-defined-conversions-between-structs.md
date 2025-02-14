---
title: Практическое руководство. Реализация пользовательских преобразований между структурами (Руководство по программированию на C#)
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- user-defined conversions [C#]
ms.assetid: 97839aef-8fbc-40d5-9769-6b569bc2710b
ms.openlocfilehash: f33d8791791543704c8a49a44167b94c0f0c86b8
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64608177"
---
# <a name="how-to-implement-user-defined-conversions-between-structs-c-programming-guide"></a>Практическое руководство. Реализация пользовательских преобразований между структурами (Руководство по программированию на C#)
В этом примере определяются две структуры (`RomanNumeral` и `BinaryNumeral`) и демонстрируются преобразования между ними.  
  
## <a name="example"></a>Пример  
 [!code-csharp[csProgGuideStatements#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#13)]  
  
## <a name="robust-programming"></a>Отказоустойчивость  
  
- В предыдущем примере инструкция:  
  
     [!code-csharp[csProgGuideStatements#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#14)]  
  
     выполняет преобразование из `RomanNumeral` в `BinaryNumeral`. Поскольку прямого преобразования из `RomanNumeral` в `BinaryNumeral` не существует, используется приведение для преобразования из `RomanNumeral` в `int` и еще одно приведение для преобразования из `int` в `BinaryNumeral`.  
  
- Кроме того, инструкция  
  
     [!code-csharp[csProgGuideStatements#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#15)]  
  
     выполняет преобразование из `BinaryNumeral` в `RomanNumeral`. Поскольку `RomanNumeral` определяет неявное преобразование из `BinaryNumeral`, приведение не требуется.  
  
## <a name="see-also"></a>См. также

- [Справочник по C#](../../../csharp/language-reference/index.md)
- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)
- [Операторы преобразования](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)
