---
title: Руководство по программированию на C#. Объекты
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- objects [C#], about objects
- variables [C#]
ms.assetid: af4a5230-fbf3-4eea-95e1-8b883c2f845c
ms.openlocfilehash: de44f0c416de798fb42fba93e30ec6aa6ed0208d
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65585975"
---
# <a name="objects-c-programming-guide"></a>Объекты (Руководство по программированию на C#)
Определение класса или структуры подобно чертежу, на котором указаны действия, выполняемые типом. В сущности, объект является блоком памяти, выделенной и настроенной в соответствии с чертежом. Программа может создать множество объектов одного класса. Объекты также называют экземплярами. Они могут храниться либо в именованной переменной, либо в массиве или коллекции. Клиентский код — это код, использующий эти переменные для вызова методов и доступа к открытым свойствам объекта. В объектно-ориентированном языке, таком как C#, стандартная программа состоит из нескольких динамически взаимодействующих объектов.  
  
> [!NOTE]
>  Поведение статических типов отличается от описанного здесь поведения. Дополнительные сведения см. в статье [Статические классы и члены статических классов](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
## <a name="struct-instances-vs-class-instances"></a>Экземпляры структуры и Экземпляры классов  
 Так как классы являются ссылочными типами, в переменной объекта класса хранится ссылка на адрес объекта в управляемой куче. Если первому объекту назначен второй объект того же типа, обе переменные ссылаются на объект, расположенный по данному адресу. Эта особенность обсуждается более подробно далее в этом разделе.  
  
 Экземпляры классов создаются с помощью [оператора new](../../../csharp/language-reference/keywords/new-operator.md). В приведенном ниже примере `Person` является типом, а `person1` и `person 2` — экземплярами или объектами этого типа.  
  
 [!code-csharp[csProgGuideStatements#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#30)]  
  
 Так как структуры являются типами значений, в переменной объекта структуры хранится копия всего объекта. Экземпляры структур также можно создавать с помощью оператора `new`, однако он не является обязательным, как показано в следующем примере:  
  
 [!code-csharp[csProgGuideStatements#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#31)]  
  
 Память для `p1` и `p2` выделена в стеке потока. Эта память освобождается вместе с типом или методом, в котором она объявляется. Эта одна из причин того, почему структуры копируются при присваивании. Напротив, при выходе всех ссылок на объект из области действия среда CLR автоматически освобождает память (выполняет сборку мусора), выделенную для экземпляра класса. Возможность детерминированного уничтожения объекта класса, имеющаяся в C++, в данном случае отсутствует. Дополнительные сведения о сборке мусора в .NET Framework см. в разделе [Сборка мусора](../../../standard/garbage-collection/index.md).  
  
> [!NOTE]
>  В среде CLR процесс выделения и освобождения памяти в управляемой куче значительно оптимизирован. В большинстве случаев нет существенной разницы в затратах производительности на выделение экземпляра класса в куче и выделение экземпляра структуры в стеке.  
  
## <a name="object-identity-vs-value-equality"></a>Идентификация объектов и равенство значений  
 Сравнивая два объекта на предмет равенства, сначала необходимо определить, нужно ли узнать, представляют ли две переменные один объект в памяти или значения одного или нескольких их полей являются равными. Если вы планируете сравнить значения, следует решить, являются ли объекты экземплярами типов значений (структурами) или ссылочными типами (классами, делегатами, массивами).  
  
- Чтобы определить, ссылаются ли два экземпляра класса на одно расположение в памяти (то есть имеют одинаковый *идентификатор*), воспользуйтесь статическим методом <xref:System.Object.Equals%2A>. (<xref:System.Object?displayProperty=nameWithType> является неявным базовым классом для всех типов значений и ссылочных типов, включая структуры и классы, определенные пользователем.)  
  
- Чтобы определить, имеют ли поля экземпляра в двух экземплярах структуры одинаковые значения, воспользуйтесь методом <xref:System.ValueType.Equals%2A?displayProperty=nameWithType>. Так как все структуры неявно наследуются от <xref:System.ValueType?displayProperty=nameWithType>, метод можно вызвать непосредственно в объекте, как показано в следующем примере:  
  
 [!code-csharp[csProgGuideStatements#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#32)]  
  
 В реализации <xref:System.ValueType?displayProperty=nameWithType> `Equals` используется отражение, так как необходимо определить поля, имеющиеся в любой структуре. При создании собственных структур переопределите метод `Equals` для предоставления эффективного алгоритма равенства, соответствующего вашему типу.  
  
- Чтобы определить, равны ли значения полей в двух экземплярах класса, можно воспользоваться методом <xref:System.Object.Equals%2A> или [оператором ==](../../../csharp/language-reference/operators/equality-operators.md#equality-operator-). Однако их следует использовать, только если они переопределены или перегружены классом с целью предоставления пользовательского определение равенства для объектов этого типа. Класс может также реализовывать интерфейс <xref:System.IEquatable%601> или интерфейс <xref:System.Collections.Generic.IEqualityComparer%601>. Оба интерфейса предоставляют методы, которые можно использовать для проверки равенства значений. При создании собственных классов, переопределяющих `Equals`, следуйте рекомендациям из [практического руководства по определению равенства значений для типа](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md) и раздела <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType>.  
  
## <a name="related-sections"></a>Связанные разделы  
 Дополнительные сведения:  
  
- [Классы](../../../csharp/programming-guide/classes-and-structs/classes.md)  
  
- [Структуры](../../../csharp/programming-guide/classes-and-structs/structs.md)  
  
- [Конструкторы](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
  
- [Методы завершения](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
  
- [События](../../../csharp/programming-guide/events/index.md)  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)
- [object](../../../csharp/language-reference/keywords/object.md)
- [Наследование](../../../csharp/programming-guide/classes-and-structs/inheritance.md)
- [class](../../../csharp/language-reference/keywords/class.md)
- [struct](../../../csharp/language-reference/keywords/struct.md)
- [Оператор new](../../../csharp/language-reference/keywords/new-operator.md)
- [Система общих типов CTS](../../../standard/base-types/common-type-system.md)
