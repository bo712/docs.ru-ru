---
title: Руководство по программированию на C#. Аргументы командной строки
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- command-line arguments [C#]
ms.assetid: 0e597e0d-ea7a-41ba-a38a-0198122f3c26
ms.openlocfilehash: 8216e144dfcaeaf9b480d681ae91ce59832ae9e3
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2019
ms.locfileid: "65877535"
---
# <a name="command-line-arguments-c-programming-guide"></a>Аргументы командной строки (Руководство по программированию на C#)
Вы можете передавать аргументы в метод `Main`, определив метод одним из следующих способов:  
  
 [!code-csharp[csProgGuideMain#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#2)]  
  
 [!code-csharp[csProgGuideMain#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#3)]  
  
> [!NOTE]
>  Чтобы включить аргументы командной строки в методе `Main` в приложении Windows Forms, необходимо вручную изменить сигнатуру `Main` в файле program.cs. Код, созданный с помощью конструктора Windows Forms, создает `Main` без входного параметра. Также можно использовать <xref:System.Environment.CommandLine%2A?displayProperty=nameWithType> или <xref:System.Environment.GetCommandLineArgs%2A?displayProperty=nameWithType> для доступа к аргументам командной строки из любой точки в консоли или приложении Windows.  
  
 Параметр метода `Main` — это массив <xref:System.String>, представляющий аргументы командной строки. Как правило, определить, существуют ли аргументы, можно, проверив свойство `Length`, например:  
  
 [!code-csharp[csProgGuideMain#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#4)]  
  
 Строковые аргументы также можно преобразовать в числовые типы с помощью класса <xref:System.Convert> или метода `Parse`. Например, следующая инструкция преобразует `string` в число `long` с помощью метода <xref:System.Int64.Parse%2A>:  
  
```  
long num = Int64.Parse(args[0]);  
```  
  
 Можно также использовать тип C# `long`, который является псевдонимом `Int64`:  
  
```  
long num = long.Parse(args[0]);  
```  
  
 Кроме того, можно использовать метод класса `Convert`, `ToInt64`:  
  
```  
long num = Convert.ToInt64(s);  
```  
  
 Дополнительные сведения см. в разделах <xref:System.Int64.Parse%2A> и <xref:System.Convert>.  
  
## <a name="example"></a>Пример  
 В следующем примере показано использование аргументов командной строки в консольном приложении. Приложение принимает один аргумент времени выполнения, преобразует аргумент в целое число и вычисляет факториал числа. Если не указано никаких аргументов, приложение выдает сообщение, поясняющее правильное использование программы.  
  
 Чтобы скомпилировать и запустить приложение из командной строки, выполните следующие действия.  
  
1. Вставьте следующий код в любой текстовый редактор и сохраните файл как текстовый файл с именем `Factorial.cs`.  
  
     [!code-csharp[csProgGuideMain#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class1.cs#16)]  
  
2. На **начальном** экране или в меню **Пуск** откройте окно **командной строки разработчика** Visual Studio и перейдите к папке, содержащей файл, который вы только что создали.  
  
3. Введите следующую команду для компиляции приложения.  
  
     `csc Factorial.cs`  
  
     Если для приложения не выдаются ошибки компиляции, создается исполняемый файл с именем `Factorial.exe`.  
  
4. Введите приведенную ниже команду для вычисления факториала числа 3:  
  
     `Factorial 3`  
  
5. Код создает следующие выходные данные: `The factorial of 3 is 6.`  
  
> [!NOTE]
>  При выполнении приложения в Visual Studio аргументы командной строки можно указать на [странице "Отладка" в конструкторе проектов](/visualstudio/ide/reference/debug-page-project-designer).  
  
 Дополнительные примеры использования аргументов командной строки см. в статье [Практическое руководство. Создание и использование сборок с помощью командной строки](../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-and-use-assemblies-using-the-command-line.md).  
  
## <a name="see-also"></a>См. также

- <xref:System.Environment?displayProperty=nameWithType>
- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)
- [Main() и аргументы командной строки](../../../csharp/programming-guide/main-and-command-args/index.md)
- [Практическое руководство. Отображение аргументов командной строки](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)
- [Значения, возвращаемые методом main()](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)
- [Классы](../../../csharp/programming-guide/classes-and-structs/classes.md)
