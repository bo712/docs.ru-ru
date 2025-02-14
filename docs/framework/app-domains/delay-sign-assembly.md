---
title: Отложенная подпись сборки
ms.date: 07/31/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- deferring assembly signing
- signing assemblies
- assemblies [.NET Framework], signing
- strong-named assemblies, delaying assembly signing
- partial assembly signing
ms.assetid: 9d300e17-5bf1-4360-97da-2aa55efd9070
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 31c43607a710316696a9765feb6f36b7676f906f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593642"
---
# <a name="delay-signing-an-assembly"></a>Отложенная подпись сборки
Организация может располагать тщательно оберегаемой парой ключей, повседневный доступ к которой разработчикам не предоставляется. Открытый ключ часто является доступным, но доступ к закрытому ключу предоставляется лишь отдельным лицам. При разработке сборок со строгими именами каждая сборка, в которой имеется ссылка на другую сборку со строгим именем, должна содержать маркер открытого ключа, использованного для присвоения строгого имени второй сборке. Данный подход требует, чтобы открытый ключ был доступен во время процесса разработки.  
  
 Во время компоновки сборки можно использовать отложенную или частичную подпись для того, чтобы зарезервировать в переносимом исполняемом файле (PE-файле) место для подписи строгого имени, а применение полноценной подписи отложить и выполнить на следующем этапе (обычно непосредственно перед поставкой сборки).  
  
 В приведенной ниже последовательности шагов отражены основные этапы отложенного подписания сборки.  
  
1. Получите открытый ключ, входящий в состав пары ключей, у организации, отвечающей за окончательную подпись. Обычно этот ключ предоставляется в форме SNK-файла, который может быть создан с помощью [программы строгих имен (Sn.exe)](../../../docs/framework/tools/sn-exe-strong-name-tool.md), входящей в состав [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
2. Включите в исходный код сборки два указанных ниже настраиваемых атрибута из пространства имен <xref:System.Reflection>.  
  
    - Атрибут <xref:System.Reflection.AssemblyKeyFileAttribute>, который передает имя файла, содержащего открытый ключ, своему конструктору в качестве параметра.  
  
    - Атрибут<xref:System.Reflection.AssemblyDelaySignAttribute>, который указывает, что используется отложенная подпись, передавая значение **true** своему конструктору в качестве параметра. Пример:  
  
         [!code-cpp[AssemblyDelaySignAttribute#4](../../../samples/snippets/cpp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cpp/source2.cpp#4)]
         [!code-csharp[AssemblyDelaySignAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AssemblyDelaySignAttribute/cs/source2.cs#4)]
         [!code-vb[AssemblyDelaySignAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AssemblyDelaySignAttribute/vb/source2.vb#4)]  
  
3. Компилятор вставляет открытый ключ в манифест сборки и резервирует в PE-файле место для полной подписи строгого имени. При компоновке сборки должен использоваться подлинный открытый ключ, чтобы другие сборки, ссылающиеся на данную сборку, могли получить этот ключ и сохранить его в своих ссылках на сборку.  
  
4. Так как подпись строгого имени сборки пока некорректна, необходимо отключить проверку этой подписи. Это можно сделать с помощью программы строгих имен, используя параметр **–Vr**.  
  
     В следующем примере производится отключение проверки сборки с именем `myAssembly.dll`.  
  
    ```  
    sn –Vr myAssembly.dll  
    ```  
  
     Чтобы отключить проверку на платформах, где нельзя запустить средства для работы со строгими именами, такими как микропроцессоры Advanced RISC Machine (ARM), используйте параметр **–Vk** для создания файла реестра. Импортируйте файл реестра в реестр на компьютере, где нужно отключить проверку. В следующем примере создается файл реестра для `myAssembly.dll`.  
  
    ```  
    sn –Vk myRegFile.reg myAssembly.dll  
    ```  
  
     С помощью параметра **–Vr** или **–Vk** можно дополнительно включить SNK-файл для подписывания ключа теста.  
  
    > [!WARNING]
    > Строгие имена не являются средством обеспечения безопасности. Они служат только для однозначной идентификации.
  
    > [!NOTE]
    >  Если во время разработки с помощью Visual Studio на компьютере с 64-разрядной архитектурой используется отложенная подпись и сборка компилируется для конфигурации **Любой ЦП**, возможно, параметр **-Vr** потребуется применить дважды. (В Visual Studio конфигурация **Любой ЦП** является значением свойства сборки **Целевая платформа**; при компиляции из командной строки это параметр по умолчанию.) Чтобы запустить приложение из командной строки или в проводнике, используйте 64-разрядную версию [Sn.exe (средство строгих имен)](../../../docs/framework/tools/sn-exe-strong-name-tool.md) для применения к сборке параметра **-Vr**. Чтобы загрузить сборку в Visual Studio во время разработки (например, если сборка содержит компоненты, используемые другими сборками в приложении), необходимо использовать 32-разрядную версию средства работы со строгими именами. Причина заключается в том, что JIT-компилятор компилирует сборки в 64-разрядный машинный код, когда сборка запускается из командной строки, и в 32-разрядный машинный код, когда сборка загружается в среду во время разработки.  
  
5. Позже, обычно сразу перед поставкой, необходимо отправить сборку в подписывающий центр организации для подписания действующим строгим именем с помощью параметра программы строгих имен **–R**.  
  
     В следующем примере сборка с именем `myAssembly.dll` подписывается строгим именем с помощью пары ключей `sgKey.snk`.  
  
    ```  
    sn -R myAssembly.dll sgKey.snk  
    ```  
  
## <a name="see-also"></a>См. также

- [Создание сборок](../../../docs/framework/app-domains/create-assemblies.md)
- [Практическое руководство. Создание пары открытого и закрытого ключей](../../../docs/framework/app-domains/how-to-create-a-public-private-key-pair.md)
- [Sn.exe (средство строгих имен)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)
- [Программирование с использованием сборок](../../../docs/framework/app-domains/programming-with-assemblies.md)
