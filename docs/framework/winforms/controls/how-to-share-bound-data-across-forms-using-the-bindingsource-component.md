---
title: Практическое руководство. Совместное использование одних и тех же данных в нескольких формах посредством компонента BindingSource
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- examples [Windows Forms], BindingSource component
- data binding [Windows Forms], sharing data across forms
- BindingSource component [Windows Forms], examples
- BindingSource [Windows Forms], using with multiple forms
ms.assetid: a1a49630-db9c-4485-b888-1f62a373a4f7
ms.openlocfilehash: 28eceaec72053d70885d54bc09179cff743ff71c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591436"
---
# <a name="how-to-share-bound-data-across-forms-using-the-bindingsource-component"></a>Практическое руководство. Совместное использование одних и тех же данных в нескольких формах посредством компонента BindingSource
С помощью компонента <xref:System.Windows.Forms.BindingSource> одни и те же данные можно легко использовать в нескольких формах. Например, может потребоваться отобразить одну форму только для чтения со сводкой данных и другую редактируемую форму с подробными сведениями о выбранном в данный момент элементе в источнике данных. В этом примере демонстрируется такая возможность.  
  
## <a name="example"></a>Пример  
 В примере кода ниже показано, как совместно использовать источник <xref:System.Windows.Forms.BindingSource> и связанные с ним данные в разных формах. В этом примере общий источник <xref:System.Windows.Forms.BindingSource> передается в конструктор дочерней формы. Дочерняя форма позволяет пользователю изменять данные элемента, выбранного в настоящий момент в главной форме.  
  
> [!NOTE]
>  В этом примере обрабатывается событие <xref:System.Windows.Forms.BindingSource.BindingComplete> для компонента <xref:System.Windows.Forms.BindingSource>, обеспечивая синхронизацию двух форм. Дополнительные сведения о том, почему это делать, см. в разделе [как: Элементов управления с привязкой к тому же источнику данных будут синхронизированы](../multiple-controls-bound-to-data-source-synchronized.md).  
  
 [!code-csharp[System.Windows.Forms.BindingSourceMultipleForms#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleForms/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingSourceMultipleForms#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleForms/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Для этого примера требуются:  
  
- Ссылки на сборки System, System.Windows.Forms, System.Drawing, System.Data и System.Xml.  
  
## <a name="see-also"></a>См. также

- [Компонент BindingSource](bindingsource-component.md)
- [Привязка данных Windows Forms](../windows-forms-data-binding.md)
- [Практическое руководство. Обработка ошибок и исключений, происходящих при выполнении привязки данных](how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)
