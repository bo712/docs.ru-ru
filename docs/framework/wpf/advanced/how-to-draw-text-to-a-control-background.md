---
title: Практическое руководство. Рисование текста для фона элемента управления
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], drawing text to backgrounds
- text [WPF], drawing to control backgrounds
- drawing [WPF], text to control backgrounds
- backgrounds [WPF], drawing text to
- typography [WPF], drawing text to control backgrounds
ms.assetid: 686d8fba-f61c-4974-a871-c635d67a7f69
ms.openlocfilehash: 76449c88f9a720741c8ed61255e04a40e6a8613f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776213"
---
# <a name="how-to-draw-text-to-a-controls-background"></a>Практическое руководство. Рисование текста для фона элемента управления
Можно рисовать текст непосредственно на фоне элемента управления, преобразовав строку текста в <xref:System.Windows.Media.FormattedText> объекта, а затем рисуя объект элемента управления <xref:System.Windows.Media.DrawingContext>. Этот метод также можно использовать для рисования на фоне объектов, производных от <xref:System.Windows.Controls.Panel>, такие как <xref:System.Windows.Controls.Canvas> и <xref:System.Windows.Controls.StackPanel>.  
  
 ![Элементы управления, отображающие текст в качестве фона](./media/drawtext2background01.png "DrawText2Background01")  
Пример элементов управления с фоном из пользовательского текста  
  
## <a name="example"></a>Пример  
 Для рисования фона элемента управления, создайте новый <xref:System.Windows.Media.DrawingBrush> объекта и нарисуйте преобразованный текст объекта <xref:System.Windows.Media.DrawingContext>. Затем назначьте новый <xref:System.Windows.Media.DrawingBrush> свойству фона элемента управления.  
  
 В следующем примере кода показано, как создать <xref:System.Windows.Media.FormattedText> и рисовать фон <xref:System.Windows.Controls.Label> и <xref:System.Windows.Controls.Button> объекта.  
  
 [!code-csharp[DrawTextToControlBackground#DrawTextToControlBackground1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawTextToControlBackground/CSHARP/Window1.xaml.cs#drawtexttocontrolbackground1)]  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Media.FormattedText>
- [Рисование форматированного текста](drawing-formatted-text.md)
