---
title: Руководство по программированию на C#. Общие сведения о взаимодействии
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop
- C# language, interoperability
- C++ Interop
- interoperability, about interoperability
- platform invoke
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
ms.openlocfilehash: 589bb205b10a5b7b0c4480393b8937e0df36022f
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66052399"
---
# <a name="interoperability-overview-c-programming-guide"></a>Общие сведения о взаимодействии. (Руководство по программированию в C#)
В этом разделе описываются способы включения взаимодействия между управляемым кодом C# и неуправляемым кодом.  
  
## <a name="platform-invoke"></a>Вызов неуправляемого кода  
 *Вызов неуправляемого кода* — это служба, позволяющая управляемому коду вызывать неуправляемые функции, реализованные в библиотеках динамической компоновки (DLL), например функции библиотек Microsoft Windows API. Он обнаруживает и вызывает экспортированную функцию и при необходимости маршалирует ее аргументы (целые числа, строки, массивы, структуры и так далее) через границы взаимодействия.  
  
 Дополнительные сведения см. в статьях [Использование неуправляемых функций DLL](../../../framework/interop/consuming-unmanaged-dll-functions.md) и [Руководство по программированию на C#. Использование вызова неуправляемого кода для воспроизведения звукового файла](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md).  
  
> [!NOTE]
>  [Среда CLR](../../../standard/clr.md) управляет доступом к системным ресурсам. Вызов неуправляемого кода, который находится вне среды CLR, обходит этот механизм защиты и таким образом представляет угрозу безопасности. Например, неуправляемый код может обращаться к ресурсам в неуправляемом коде напрямую, минуя механизмы обеспечения безопасности среды CLR. Дополнительные сведения см. в разделе [Безопасность в .NET](../../../standard/security/index.md).  
  
## <a name="c-interop"></a>взаимодействие C++  
 Взаимодействие C++, также известное как IJW, можно использовать для создания оболочки для собственного класса C++ для использования в коде, созданном на C# или другом языке .NET Framework. Для этого необходимо написать код C++, создающий оболочку для собственного DLL- или COM-компонента. В отличие от других языков .NET Framework, Visual C++ включает поддержку взаимодействия, что позволяет размещать управляемый и неуправляемый код в одном приложении и даже в одном файле. Затем вы выполняете сборку кода C++ с помощью параметра компилятора **/clr** для создания управляемой сборки. И, наконец, необходимо добавить ссылку на сборку в проекте C# и использовать объекты с оболочкой так же, как другие управляемые классы.  
  
## <a name="exposing-com-components-to-c"></a>Предоставление доступа к COM-компонентам кода C\#
 Вы можете использовать COM-компоненты в проекте C#. Общая процедура следующая.  
  
1. Найдите нужный COM-компонент и зарегистрируйте его. Используйте regsvr32.exe для регистрации или отмены регистрации библиотеки DLL модели COM.  
  
2. Добавьте в проект ссылку на COM-компонент или библиотеку типов.  
  
     При добавлении ссылки Visual Studio использует [Tlbimp.exe (программу импорта библиотек типов)](../../../../docs/framework/tools/tlbimp-exe-type-library-importer.md), которая принимает на вход библиотеку типов и выдает на выходе сборку взаимодействия .NET Framework. Сборка, также называемая вызываемой оболочкой времени выполнения (RCW), содержит управляемые классы и интерфейсы, которые служат оболочкой для классов и интерфейсов COM в библиотеке типов. Visual Studio добавляет в проект ссылку на созданную сборку.  
  
3. Создайте экземпляр класса, определенного в вызываемой оболочке времени выполнения. Он, в свою очередь, создает экземпляр COM-объекта.  
  
4. Используйте объект так же, как другие управляемые объекты. Когда объект удаляется сборщиком мусора, экземпляр COM-объекта также удаляется из памяти.  
  
 Дополнительные сведения см. в статье [Предоставление клиентам .NET Framework доступа к COM-компонентам](../../../../docs/framework/interop/exposing-com-components.md).  
  
## <a name="exposing-c-to-com"></a>Предоставление C# клиентам COM  
 Клиенты COM могут потреблять типы C#, которые были правильно предоставлены. Ниже приведены основные шаги для предоставления типов C#.  
  
1. Добавьте атрибуты взаимодействия в проект C#.  
  
     Сборку COM можно сделать видимой, изменив свойства проекта Visual C#. Дополнительные сведения см. в разделе [Диалоговое окно "Сведения о сборке"](/visualstudio/ide/reference/assembly-information-dialog-box).  
  
2. Создайте библиотеку типов COM и зарегистрируйте ее для использования моделью COM.  
  
     Можно изменить свойства проекта Visual C# для автоматической регистрации сборки C# для COM-взаимодействия. Visual Studio использует [Regasm.exe (средство регистрации сборок)](../../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md) с параметром командной строки `/tlb`. Средство принимает на вход управляемую сборку и создает библиотеку типов. Эта библиотека типов описывает типы `public` в сборке и добавляет записи реестра, чтобы клиенты COM могли создавать управляемые классы.  
  
 Дополнительные сведения см. в разделе [Предоставление COM-клиентам доступа к компонентам .NET Framework](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md) и [Пример COM-класса](../../../csharp/programming-guide/interop/example-com-class.md).  
  
## <a name="see-also"></a>См. также

- [Улучшение производительности взаимодействия](https://docs.microsoft.com/previous-versions/msp-n-p/ff647812%28v=pandp.10%29)
- [Общие сведения о взаимодействии между COM и .NET](/office/client-developer/outlook/pia/introduction-to-interoperability-between-com-and-net)
- [Общие сведения о взаимодействии между COM и Visual Basic](../../../../docs/visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)
- [Marshaling between Managed and Unmanaged Code (Маршалинг между управляемым и неуправляемым кодом)](../../../../docs/framework/interop/interop-marshaling.md)
- [Взаимодействие с неуправляемым кодом](../../../../docs/framework/interop/index.md)
- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)
