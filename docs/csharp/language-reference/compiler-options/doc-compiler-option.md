---
title: -doc (параметры компилятора C#)
ms.date: 07/20/2015
f1_keywords:
- FileProperties.BuildAction
- /doc
helpviewer_keywords:
- comments, C# code
- XML documentation [C#], comments in source files
- doc compiler option [C#]
- Visual C#, XML documentation for
- -doc compiler option [C#]
- /doc compiler option [C#]
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
ms.openlocfilehash: 7c8fc11c8799912ea6340940ccd254ae82519591
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591694"
---
# <a name="-doc-c-compiler-options"></a>-doc (параметры компилятора C#)
Параметр **-doc** позволяет поместить комментарии документации в XML-файл.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-doc:file  
```  
  
## <a name="arguments"></a>Аргументы  
 `file`  
 Выходной XML-файл, который заполняется комментариями из файлов исходного кода, участвующих в компиляции.  
  
## <a name="remarks"></a>Примечания  
 Комментарии документации могут быть обработаны и добавлены в XML-файл, если они предшествуют объектам файлов исходного кода, перечисленным ниже.  
  
- Такие определяемые пользователем типы, как [класс](../../../csharp/language-reference/keywords/class.md), [делегат](../../../csharp/language-reference/keywords/delegate.md) или [интерфейс](../../../csharp/language-reference/keywords/interface.md).  
  
- Такие члены, как поле, [событие](../../../csharp/language-reference/keywords/event.md), [свойство](../../../csharp/programming-guide/classes-and-structs/using-properties.md) или метод.  
  
 Файл исходного кода, содержащий метод "Main", первым выводится в XML-файл.  
  
 Чтобы использовать созданный XML-файл с помощью функции [IntelliSense](/visualstudio/ide/using-intellisense), имя XML-файла должно совпадать с именем сборки, а сам XML-файл должен находиться в одном каталоге со сборкой. Таким образом, если в проект Visual Studio добавляется ссылка на сборку, то XML-файл также будет найден. Дополнительные сведения см. в разделе [Создание XML-примечаний к коду](/visualstudio/ide/supplying-xml-code-comments).  
  
 Если при компиляции не используется параметр [-target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), `file` будет содержать теги \<assembly>\</assembly>, которые указывают имя файла, содержащего манифест сборки для выходного файла компиляции.  
  
> [!NOTE]
>  Параметр -doc применяется ко всем входным файлам или (если он установлен в параметрах проекта) ко всем файлам проекта. Чтобы отключить предупреждения, связанные с комментариями документации для определенного файла или раздела кода, используйте директиву [#pragma warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md).  
  
 Способы создания документации из комментариев в коде описаны в разделе [Рекомендуемые теги для комментариев документации](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio  
  
1. Откройте страницу **Свойства** проекта.  
  
2. Перейдите на вкладку **Сборка**.  
  
3. Измените свойство **XML-файл документации**.  
  
 Сведения об установке этого параметра компилятора программными средствами см. в разделе <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>.  
  
## <a name="see-also"></a>См. также

- [Параметры компилятора C# ](../../../csharp/language-reference/compiler-options/index.md)
- [Управление свойствами проектов и решений](/visualstudio/ide/managing-project-and-solution-properties)
