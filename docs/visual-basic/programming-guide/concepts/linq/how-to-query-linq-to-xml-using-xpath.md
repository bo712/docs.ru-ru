---
title: Практическое руководство. Запрос LINQ to XML с использованием XPath (Visual Basic)
ms.date: 07/20/2015
ms.assetid: e1f69a20-1efa-452d-9089-c472fa84b3d5
ms.openlocfilehash: cff0b5f6e4bb3c64522dc13a44dd79d7c172c1b5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62008893"
---
# <a name="how-to-query-linq-to-xml-using-xpath-visual-basic"></a>Практическое руководство. Запрос LINQ to XML с использованием XPath (Visual Basic)
В этом разделе описываются методы расширения, обеспечивающие запрос XML-дерева с помощью XPath. Подробные сведения об использовании данных методов расширения см. в разделе <xref:System.Xml.XPath.Extensions?displayProperty=nameWithType>.  
  
 Рекомендуется использовать XPath с LINQ to XML, только если есть основательная причина для применения запросов на основе XPath, такая как широкое использование кода прежних версий. Запросы XPath не действуют столь эффективно, как запросы [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].  
  
## <a name="example"></a>Пример  
 В следующем примере создается небольшое XML-дерево и для получения набора элементов используется запрос <xref:System.Xml.XPath.Extensions.XPathSelectElements%2A>.  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <Child1>1</Child1>  
        <Child1>2</Child1>  
        <Child1>3</Child1>  
        <Child2>4</Child2>  
        <Child2>5</Child2>  
        <Child2>6</Child2>  
    </Root>  
  
Dim list As IEnumerable(Of XElement) = root.XPathSelectElements("./Child2")  
For Each el As XElement In list  
    Console.WriteLine(el)  
Next  
```  
  
 В этом примере выводятся следующие данные:  
  
```xml  
<Child2>4</Child2>  
<Child2>5</Child2>  
<Child2>6</Child2>  
```  
  
## <a name="see-also"></a>См. также

- [Дополнительные способы создания запросов (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
