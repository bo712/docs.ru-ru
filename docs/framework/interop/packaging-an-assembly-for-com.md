---
title: Упаковка сборки для модели COM
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET Framework components to COM
- COM interop, packaging assemblies
- packaging assemblies for COM
- Tlbexp.exe
- TypeLibConverter class
- .NET Services Installation tool
- Assembly Registration tool
- Type Library Exporter
- Reqsvcs.exe
- interoperation with unmanaged code, exposing .NET Framework components
- interoperation with unmanaged code, packaging assemblies
- COM interop, exposing COM components
- Reqasm.exe
ms.assetid: 39dc55aa-f2a1-4093-87bb-f1c0edb6e761
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dc02178223e48c7c578d10ba92123d9436d4f439
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59097269"
---
# <a name="packaging-an-assembly-for-com"></a>Упаковка сборки для модели COM
Разработчики приложений на основе модели COM могут использовать следующую информацию об управляемых типах, которые они планируют включать в свои приложения:  
  
-   Список типов, которые можно использовать в приложениях на основе модели COM  
  
     Некоторые управляемые типы невидимы в модели COM, другие видны, но недоступны для создания, однако третьи можно как видеть, так и создавать. В сборку можно включать типы любого вида в любом сочетании. Для полноты информации определите типы в сборке, которые будут предоставлены модели COM. Особое внимание уделите типам, входящим в подмножество типов, предоставляемых платформе .NET Framework.  
  
     Дополнительные сведения см. в разделе [Уточнение типов .NET для взаимодействия](qualifying-net-types-for-interoperation.md).  
  
-   Инструкции по управлению версиями  
  
     В отношении управления версиями управляемых классов, которые реализуют интерфейс класса (создаваемые в результате COM-взаимодействия класс), действуют определенные ограничения.  
  
     Рекомендации по использованию интерфейса класса см. в разделе [Introducing the class interface](com-callable-wrapper.md#introducing-the-class-interface) (Введение в интерфейс класса).  
  
-   Инструкции по развертыванию  
  
     Сборки со строгими именами, подписанные издателем, могут устанавливаться в глобальный кэш сборок. Неподписанные сборки необходимо устанавливать на компьютер пользователя в виде частных сборок.  
  
     Дополнительные сведения см. в разделе [Вопросы безопасности сборок](../app-domains/assembly-security-considerations.md).  
  
-   Включение библиотеки типов  
  
     Для использования большинства типов в COM-приложении требуется библиотека типов. Вы можете создать библиотеку типов самостоятельно или поручить эту задачу разработчикам COM-приложений. [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] предоставляет следующие возможности для создания библиотеки типов:  
  
    -   [Программа экспорта библиотек типов](#cpconpackagingassemblyforcomanchor1)  
  
    -   [Класс TypeLibConverter](#cpconpackagingassemblyforcomanchor2)  
  
    -   [Средство регистрации сборок](#cpconpackagingassemblyforcomanchor3)  
  
    -   [Средство установки служб .NET](#cpconpackagingassemblyforcomanchor4)  
  
     Независимо от выбранного механизма, в созданную библиотеку типов включаются только открытые типы, определенные в предоставленной сборке.  
  
     Библиотеку типов можно упаковать в отдельный файл или внедрить в виде файла ресурсов Win32 в приложение на основе платформе .NET. В Microsoft Visual Basic 6.0 эта задача выполняется автоматически, однако при использовании [!INCLUDE[vbprvbext](../../../includes/vbprvbext-md.md)] внедрение библиотеки типов осуществляется вручную. Инструкции см. в разделе [Практическое руководство. Встраивание библиотек типов как ресурсов Win32 в приложения на основе платформы .NET](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ww9a897z(v=vs.100)).  
  
<a name="cpconpackagingassemblyforcomanchor1"></a>   
## <a name="type-library-exporter"></a>программа экспорта библиотек типов  
 [Программа экспорта библиотек типов (Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md) — это средство командной строки, которое преобразует классы и интерфейсы, содержащиеся в сборке, в библиотеку типов COM. После получения информации о типе класса COM-клиенты могут создать экземпляр класса .NET и вызывать его методы так, как если бы он был COM-объектом. Программа Tlbexp.exe преобразует всю сборку за одну операцию. Программу Tlbexp.exe нельзя использовать с целью генерации сведений о типах для подмножества типов, определенных в сборке.  
  
<a name="cpconpackagingassemblyforcomanchor2"></a>   
## <a name="typelibconverter-class"></a>Класс TypeLibConverter  
 Класс <xref:System.Runtime.InteropServices.TypeLibConverter> располагается в пространстве имен **System.Runtime.Interop** и преобразует классы и интерфейсы, содержащиеся в сборке, в библиотеку типов COM. Этот API предоставляет те же сведения, что и программа экспорта библиотек типов, которая описывается в предыдущем разделе.  
  
 Класс **TypeLibConverter** реализует <xref:System.Runtime.InteropServices.ITypeLibConverter>.  
  
<a name="cpconpackagingassemblyforcomanchor3"></a>   
## <a name="assembly-registration-tool"></a>Средство регистрации сборок  
 [Средство регистрации сборок (Regasm.exe)](../tools/regasm-exe-assembly-registration-tool.md) позволяет создавать и регистрировать библиотеку типов с использованием параметров **/tlb:**. COM-клиентам требуется установка библиотек типов в реестр Windows. Без этого параметра программа Regasm.exe регистрирует только типы в сборке, а не библиотеку типов. Регистрация типов сборки и регистрация библиотеки типов — это разные операции.  
  
<a name="cpconpackagingassemblyforcomanchor4"></a>   
## <a name="net-services-installation-tool"></a>Средство установки служб .NET  
 [Средство установки служб .NET (Regsvcs.exe)](../tools/regsvcs-exe-net-services-installation-tool.md) добавляет управляемые классы в службы компонентов Windows 2000 и реализует одновременно несколько задач. Помимо загрузки и регистрации сборки программа Regsvcs.exe может создавать, регистрировать и устанавливать библиотеку типов в существующее приложение COM+ 1.0.  
  
## <a name="see-also"></a>См. также

- <xref:System.Runtime.InteropServices.TypeLibConverter>
- <xref:System.Runtime.InteropServices.ITypeLibConverter>
- [Предоставление компонентов .NET Framework клиентам COM](exposing-dotnet-components-to-com.md)
- [Oпределение типов .NET для взаимодействия](qualifying-net-types-for-interoperation.md)
- [Introducing the class interface](com-callable-wrapper.md#introducing-the-class-interface) (Введение в интерфейс класса)
- [Вопросы безопасности сборок](../app-domains/assembly-security-considerations.md)
- [Tlbexp.exe (программа экспорта библиотек типов)](../tools/tlbexp-exe-type-library-exporter.md)
- [Регистрация сборок в COM](registering-assemblies-with-com.md)
- [Практическое руководство. Встраивание библиотек типов как ресурсов Win32 в приложения](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ww9a897z(v=vs.100))
