---
title: Директива x:Members
ms.date: 03/30/2017
ms.assetid: 155b393d-3b49-4c5a-8c9e-b3d9893af4e4
ms.openlocfilehash: d23e6b459af932e0a6f69309f26a1cce70a9d256
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938896"
---
# <a name="xmembers-directive"></a>Директива x:Members
Содержит набор элементов, которые определены в разметке, которые применяются к x: Class родительского элемента.  
  
## <a name="xaml-attribute-usage"></a>Использование атрибута XAML  
  
```  
<object x:Class="className">  
  <x:Members>  
    oneOrMoreMembers  
  </x:Members  
</object>  
```  
  
## <a name="xaml-values"></a>Значения XAML  
  
|||  
|-|-|  
|`className`|Имя класса резервирования или разделяемого класса для рабочей среды XAML. См. заметки.|  
|`oneOrMoreMembers`|Один или несколько элементов объектов, представляющих определения элементов. Как правило, это `x:Property` объектных элемента. См. заметки.|  
  
## <a name="remarks"></a>Примечания  
 В реализации служб XAML .NET Framework нет резервного класса или базового реализацию члена для `x:Members`. `x:Members` является членом специальные XAML, который может существовать как член с любым типом. В потоке узлов XAML `x:Members` представляется как элемент с именем `Members`, из пространства имен XAML языка XAML. Элемент `Members` содержит только для чтения список параметров `Member` объектов. В разметке типичных отдельные элементы указываются как `x:Property` свойств элементов. `x:Property` — Это более точный тип, специально для свойств типов и может быть назначен `x:Member`. Дополнительные сведения см. в разделе [директива x: Property](x-property-directive.md).  
  
 Для поддержки практического использования `x:Members` как средства указания определений членов в разметке эти члены должны быть связаны с классом, который может быть изменен. Предполагаемая модель состоит в том, что `x:Members` существует в качестве члена типа, указывающего `x:Class`. Однако механизм для сопоставления типов и членов или для создания определений динамических членов не поддерживается на уровне служб XAML .NET Framework. Это отводится отдельным платформам, имеющим модели приложений, поддерживающие определения членов из XAML. Как правило, для поддержки этой функции требуются действия MSBUILD при построении, которые компилируют разметку XAML и либо интегрируют его с выделенным кодом, либо создают чистые сборки из XAML.  
  
## <a name="xmembers-for-windows-workflow-foundation"></a>x: Members для Windows Workflow Foundation  
 Для Windows Workflow Foundation `x:Members` входят члены пользовательского действия, составленного полностью в XAML или XAML – определенные динамические члены для конструктора действий с выделенным кодом. `x:Class` также должен быть указан в корневом элементе рабочей среды XAML. Это не является обязательным на уровне служб XAML .NET Framework, но становится обязательным при загрузке рабочей среды XAML с помощью действий MSBUILD при построении, которые поддерживают пользовательские действия и Windows Workflow Foundation XAML в целом. `x:Members` должен быть первый дочерний элемент в разметке элемента объекта, который объявляет `x:Class`.
