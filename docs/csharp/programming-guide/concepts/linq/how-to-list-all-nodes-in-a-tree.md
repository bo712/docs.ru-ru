---
title: Практическое руководство. Перечисление всех узлов в дереве (C#)
ms.date: 07/20/2015
ms.assetid: 3e934371-f4c6-458b-9f6b-f9061b596f5b
ms.openlocfilehash: 16d61e146e3721d8d5110d89e651aeb33ee556cd
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2019
ms.locfileid: "66486677"
---
# <a name="how-to-list-all-nodes-in-a-tree-c"></a>Практическое руководство. Перечисление всех узлов в дереве (C#)
Иногда нужно вывести список всех узлов дерева. Это полезно, если требуется узнать, как метод или свойство повлияли на дерево. Одним из подходов для вывода списка всех узлов в текстовом формате является создание выражения XPath, которое точно определяет каждый конкретный узел дерева.  
  
 Не слишком удобно выполнять выражения XPath с помощью [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]. Выражения XPath имеют более низкую производительность, чем запросы [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], к тому же запросы [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] являются более мощными. Однако для определения узлов в XML-дереве выражения XPath подходят хорошо.  
  
## <a name="example"></a>Пример  
 В этом примере показана функция с именем `GetXPath`, создающая конкретное выражение XPath для каждого узла XML-дерева. Она формирует соответствующие выражения XPath, даже если узлы находятся в пространстве имен. Выражения XPath создаются с помощью префиксов пространства имен.  
  
 Затем пример создает небольшое XML-дерево, содержащее несколько типов узлов. После этого он проходит по узлам-потомкам и выводит выражение XPath для каждого узла.  
  
 Обратите внимание, что XML-декларация не является узлом дерева.  
  
 Следующий XML-файл содержит несколько типов узлов.  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<?target data?>  
<Root AttName="An Attribute" xmlns:aw="http://www.adventure-works.com">  
  <!--This is a comment-->  
  <Child>Text</Child>  
  <Child>Other Text</Child>  
  <ChildWithMixedContent>text<b>BoldText</b>otherText</ChildWithMixedContent>  
  <aw:ElementInNamespace>  
    <aw:ChildInNamespace />  
  </aw:ElementInNamespace>  
</Root>  
```  
  
 Ниже приводится список узлов в XML-дереве, представленном в виде выражений XPath.  
  
```  
/processing-instruction()  
/Root  
/Root/@AttName  
/Root/@xmlns:aw  
/Root/comment()  
/Root/Child[1]  
/Root/Child[1]/text()  
/Root/Child[2]  
/Root/Child[2]/text()  
/Root/ChildWithMixedContent  
/Root/ChildWithMixedContent/text()[1]  
/Root/ChildWithMixedContent/b  
/Root/ChildWithMixedContent/b/text()  
/Root/ChildWithMixedContent/text()[2]  
/Root/aw:ElementInNamespace  
/Root/aw:ElementInNamespace/aw:ChildInNamespace  
```  
  
```csharp  
public static class MyExtensions  
{  
    private static string GetQName(XElement xe)  
    {  
        string prefix = xe.GetPrefixOfNamespace(xe.Name.Namespace);  
        if (xe.Name.Namespace == XNamespace.None || prefix == null)  
            return xe.Name.LocalName.ToString();  
        else  
            return prefix + ":" + xe.Name.LocalName.ToString();  
    }  
  
    private static string GetQName(XAttribute xa)  
    {  
        string prefix =  
            xa.Parent.GetPrefixOfNamespace(xa.Name.Namespace);  
        if (xa.Name.Namespace == XNamespace.None || prefix == null)  
            return xa.Name.ToString();  
        else  
            return prefix + ":" + xa.Name.LocalName;  
    }  
  
    private static string NameWithPredicate(XElement el)  
    {  
        if (el.Parent != null && el.Parent.Elements(el.Name).Count() != 1)  
            return GetQName(el) + "[" +  
                (el.ElementsBeforeSelf(el.Name).Count() + 1) + "]";  
        else  
            return GetQName(el);  
    }  
  
    public static string StrCat<T>(this IEnumerable<T> source,  
        string separator)  
    {  
        return source.Aggregate(new StringBuilder(),  
                   (sb, i) => sb  
                       .Append(i.ToString())  
                       .Append(separator),  
                   s => s.ToString());  
    }  
  
    public static string GetXPath(this XObject xobj)  
    {  
        if (xobj.Parent == null)  
        {  
            XDocument doc = xobj as XDocument;  
            if (doc != null)  
                return ".";  
            XElement el = xobj as XElement;  
            if (el != null)  
                return "/" + NameWithPredicate(el);  
            // the XPath data model does not include white space text nodes  
            // that are children of a document, so this method returns null.  
            XText xt = xobj as XText;  
            if (xt != null)  
                return null;  
            XComment com = xobj as XComment;  
            if (com != null)  
                return  
                    "/" +  
                    (  
                        com  
                        .Document  
                        .Nodes()  
                        .OfType<XComment>()  
                        .Count() != 1 ?  
                        "comment()[" +  
                        (com  
                        .NodesBeforeSelf()  
                        .OfType<XComment>()  
                        .Count() + 1) +  
                        "]" :  
                        "comment()"  
                    );  
            XProcessingInstruction pi = xobj as XProcessingInstruction;  
            if (pi != null)  
                return  
                    "/" +  
                    (  
                        pi.Document.Nodes()  
                        .OfType<XProcessingInstruction>()  
                        .Count() != 1 ?  
                        "processing-instruction()[" +  
                        (pi  
                        .NodesBeforeSelf()  
                        .OfType<XProcessingInstruction>()  
                        .Count() + 1) +  
                        "]" :  
                        "processing-instruction()"  
                    );  
            return null;  
        }  
        else  
        {  
            XElement el = xobj as XElement;  
            if (el != null)  
            {  
                return  
                    "/" +  
                    el  
                    .Ancestors()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    NameWithPredicate(el);  
            }  
            XAttribute at = xobj as XAttribute;  
            if (at != null)  
                return  
                    "/" +  
                    at  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    "@" + GetQName(at);  
            XComment com = xobj as XComment;  
            if (com != null)  
                return  
                    "/" +  
                    com  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        com  
                        .Parent  
                        .Nodes()  
                        .OfType<XComment>()  
                        .Count() != 1 ?  
                        "comment()[" +  
                        (com  
                        .NodesBeforeSelf()  
                        .OfType<XComment>()  
                        .Count() + 1) + "]" :  
                        "comment()"  
                    );  
            XCData cd = xobj as XCData;  
            if (cd != null)  
                return  
                    "/" +  
                    cd  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        cd  
                        .Parent  
                        .Nodes()  
                        .OfType<XText>()  
                        .Count() != 1 ?  
                        "text()[" +  
                        (cd  
                        .NodesBeforeSelf()  
                        .OfType<XText>()  
                        .Count() + 1) + "]" :  
                        "text()"  
                    );  
            XText tx = xobj as XText;  
            if (tx != null)  
                return  
                    "/" +  
                    tx  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        tx  
                        .Parent  
                        .Nodes()  
                        .OfType<XText>()  
                        .Count() != 1 ?  
                        "text()[" +  
                        (tx  
                        .NodesBeforeSelf()  
                        .OfType<XText>()  
                        .Count() + 1) + "]" :  
                        "text()"  
                    );  
            XProcessingInstruction pi = xobj as XProcessingInstruction;  
            if (pi != null)  
                return  
                    "/" +  
                    pi  
                    .Parent  
                    .AncestorsAndSelf()  
                    .InDocumentOrder()  
                    .Select(e => NameWithPredicate(e))  
                    .StrCat("/") +  
                    (  
                        pi  
                        .Parent  
                        .Nodes()  
                        .OfType<XProcessingInstruction>()  
                        .Count() != 1 ?  
                        "processing-instruction()[" +  
                        (pi  
                        .NodesBeforeSelf()  
                        .OfType<XProcessingInstruction>()  
                        .Count() + 1) + "]" :  
                        "processing-instruction()"  
                    );  
            return null;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        XNamespace aw = "http://www.adventure-works.com";  
        XDocument doc = new XDocument(  
            new XDeclaration("1.0", "utf-8", "yes"),  
            new XProcessingInstruction("target", "data"),  
            new XElement("Root",  
                new XAttribute("AttName", "An Attribute"),  
                new XAttribute(XNamespace.Xmlns + "aw", aw.ToString()),  
                new XComment("This is a comment"),  
                new XElement("Child",  
                    new XText("Text")  
                ),  
                new XElement("Child",  
                    new XText("Other Text")  
                ),  
                new XElement("ChildWithMixedContent",  
                    new XText("text"),  
                    new XElement("b", "BoldText"),  
                    new XText("otherText")  
                ),  
                new XElement(aw + "ElementInNamespace",  
                    new XElement(aw + "ChildInNamespace")  
                )  
            )  
        );  
        doc.Save("Test.xml");  
        Console.WriteLine(File.ReadAllText("Test.xml"));  
        Console.WriteLine("------");  
        foreach (XObject obj in doc.DescendantNodes())  
        {  
            Console.WriteLine(obj.GetXPath());  
            XElement el = obj as XElement;  
            if (el != null)  
                foreach (XAttribute at in el.Attributes())  
                    Console.WriteLine(at.GetXPath());  
        }  
    }  
}  
```  
  
 В этом примере выводятся следующие данные:  
  
```  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<?target data?>  
<Root AttName="An Attribute" xmlns:aw="http://www.adventure-works.com">  
  <!--This is a comment-->  
  <Child>Text</Child>  
  <Child>Other Text</Child>  
  <ChildWithMixedContent>text<b>BoldText</b>otherText</ChildWithMixedContent>  
  <aw:ElementInNamespace>  
    <aw:ChildInNamespace />  
  </aw:ElementInNamespace>  
</Root>  
------  
/processing-instruction()  
/Root  
/Root/@AttName  
/Root/@xmlns:aw  
/Root/comment()  
/Root/Child[1]  
/Root/Child[1]/text()  
/Root/Child[2]  
/Root/Child[2]/text()  
/Root/ChildWithMixedContent  
/Root/ChildWithMixedContent/text()[1]  
/Root/ChildWithMixedContent/b  
/Root/ChildWithMixedContent/b/text()  
/Root/ChildWithMixedContent/text()[2]  
/Root/aw:ElementInNamespace  
/Root/aw:ElementInNamespace/aw:ChildInNamespace  
```  
  