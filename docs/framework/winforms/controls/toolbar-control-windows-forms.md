---
title: Элемент управления ToolBar (Windows Forms)
ms.date: 03/30/2017
helpviewer_keywords:
- toolbars [Windows Forms]
- ToolBar control [Windows Forms]
ms.assetid: 6b40e9ce-6a7a-4784-bfc9-7f1d36b7462e
ms.openlocfilehash: 3f0a1b6a7f83753ccae1a129528ed320a2613122
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009556"
---
# <a name="toolbar-control-windows-forms"></a>Элемент управления ToolBar (Windows Forms)
> [!NOTE]
>  Элемент управления <xref:System.Windows.Forms.ToolStrip> заменяет элемент управления `ToolBar` и расширяет его функциональные возможности; однако при необходимости элемент управления `ToolBar` можно сохранить для обратной совместимости и использования в будущем.  
  
 Элемент управления Windows Forms `ToolBar` используется в формах в качестве панели управления, на которой выводится ряд раскрывающихся меню и кнопок с растровыми изображениями, активирующих команды. То есть щелчок по кнопке на панели инструментов эквивалентен выбору команды в меню. Для кнопок можно настроить режим поведения кнопок, раскрывающихся меню или разделителей. Обычно на панели инструментов содержатся кнопки и меню, соответствующие элементам в структуре меню приложения, которые предоставляют быстрый доступ к наиболее часто используемым в приложении функциям и командам.  
  
> [!NOTE]
>  Свойство <xref:System.Windows.Forms.ToolBarButton.DropDownMenu%2A> элемента управления `ToolBar` принимает в качестве ссылки экземпляр класса <xref:System.Windows.Forms.ContextMenu>. При использовании подобных кнопок на панели инструментов приложения будьте внимательны в выборе передаваемой ссылки, так как это свойство принимает любой объект, наследуемый от класса <xref:System.Windows.Forms.Menu>.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Общие сведения об элементе управления ToolBar](toolbar-control-overview-windows-forms.md)  
 Общие понятия, связанные с элементом управления `ToolBar`, который позволяет разрабатывать пользовательские панели инструментов.  
  
 [Практическое руководство. Добавление кнопок в элемент управления ToolBar](how-to-add-buttons-to-a-toolbar-control.md)  
 Описываются способы добавления кнопок в элемент управления `ToolBar`.  
  
 [Практическое руководство. Определение значка для кнопки панели инструментов](how-to-define-an-icon-for-a-toolbar-button.md)  
 Описываются способы отображения значков на кнопках элемента управления `ToolBar`.  
  
 [Практическое руководство. Триггер событий меню для кнопок панели инструментов](how-to-trigger-menu-events-for-toolbar-buttons.md)  
 Инструкции по написанию кода для определения нажатой пользователем кнопки элемента управления `ToolBar`.  
  
 Также см. раздел [Как Определение значка для кнопки панели инструментов, с помощью конструктора](how-to-define-an-icon-for-a-toolbar-button-using-the-designer.md), [как: Добавление кнопок в элемент управления ToolBar с помощью конструктора](how-to-add-buttons-to-a-toolbar-control-using-the-designer.md).  
  
## <a name="reference"></a>Ссылка  
 Класс <xref:System.Windows.Forms.ToolBar>  
 Справочная информация о классе и его членах.  
  
## <a name="related-sections"></a>Связанные разделы  
 [Элементы управления для использования в Windows Forms](controls-to-use-on-windows-forms.md)  
 Полный список элементов управления Windows Forms со ссылками на информацию об их применении.  
  
 [Элемент управления ToolStrip](toolstrip-control-windows-forms.md)  
 Описываются панели инструментов, на которых можно разместить меню, элементы управления и пользовательские элементы управления в приложениях Windows Forms.
