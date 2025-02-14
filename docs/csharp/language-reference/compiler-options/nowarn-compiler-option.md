---
title: -nowarn (параметры компилятора C#)
ms.date: 07/20/2015
f1_keywords:
- /nowarn
helpviewer_keywords:
- nowarn compiler option [C#]
- /nowarn compiler option [C#]
- -nowarn compiler option [C#]
ms.assetid: 6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4
ms.openlocfilehash: b455a2f719e7350c51cf4a1f095d4669529d0e5e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592809"
---
# <a name="-nowarn-c-compiler-options"></a>-nowarn (параметры компилятора C#)
Параметр **-nowarn** позволяет предотвратить отображение одного или нескольких предупреждений компилятором. Разделяйте предупреждения запятыми.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-nowarn:number1[,number2,...]  
```  
  
## <a name="arguments"></a>Аргументы  
 `number1`, `number2`  
 Номер (номера) предупреждений, которые требуется отключить в компиляторе.  
  
## <a name="remarks"></a>Примечания  
 Необходимо указать только числовую часть идентификатора предупреждения. Например, если требуется отключить CS0028, можно указать `-nowarn:28`.  
  
 Компилятор просто пропустит номера предупреждений, переданные `-nowarn`, которые использовались в предыдущих версиях, но были удалены из компилятора. Например, предупреждение CS0679 использовалось в компиляторе Visual Studio .NET 2002, но было удалено в последующих версиях.  
  
 Параметр `-nowarn` позволяет отключить следующие предупреждения:  
  
- Предупреждение компилятора (уровень 1) CS2002  
  
- Предупреждение компилятора (уровень 1) CS2023  
  
- Предупреждение компилятора (уровень 1) CS2029  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio  
  
1. Откройте страницу **свойств** для проекта. Дополнительные сведения см. в разделе [Страница "Сборка", конструктор проектов (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp).  
  
2. Щелкните страницу свойств **Сборка**.  
  
3. Измените свойство **Отключить предупреждения**.  
  
 Дополнительные сведения об установке этого параметра компилятора программным путем см. в разделе <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.  
  
## <a name="see-also"></a>См. также

- [Параметры компилятора C# ](../../../csharp/language-reference/compiler-options/index.md)
- [Управление свойствами проектов и решений](/visualstudio/ide/managing-project-and-solution-properties)
- [Ошибки компилятора C#](../../../csharp/language-reference/compiler-messages/index.md)
