---
title: Справочник по API отражения для машинного кода .NET
ms.date: 03/30/2017
ms.assetid: 0429c049-22a3-4ba1-9cc8-f6ee91e31d9c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 833d31c48220e2d2b5d07ee482325df090714329
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66052424"
---
# <a name="net-native-reflection-api-reference"></a>Справочник по API отражения для машинного кода .NET
.NET native включает три новых типа исключений: [System.Runtime.CompilerServices.MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md), [System.Reflection.MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md), и [System.Reflection.MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) . Все эти типы исключений имеют указанные ниже особенности:  
  
 Эти типы предназначены только для внутреннего использования.  
 Эти три типа исключений предназначены для использования цепочки инструментов .NET Native только. Исключения возникают, когда цепочка инструментов .NET Native обнаруживает отсутствие данных, который не позволяет продолжить выполнение программы.  
  
 Не обрабатывайте эти исключения в своем коде.  
 Эти исключения указывают на отсутствие метаданных (исключения [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md) и [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) ) или кода реализации (исключение [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) ), которые необходимы вашему приложению. Чтобы устранить причины этих исключений, измените файл директив среды выполнения (RD.XML) так, чтобы необходимые метаданные или код реализации были доступны во время выполнения. Дополнительные сведения см. в разделе [Runtime Directives (rd.xml) Configuration File Reference](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md). Доступны два средства устранения неполадок, которые предоставляют соответствующие записи для файла директив времени выполнения, устраняющие исключения [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) и [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) .  
  
- [Средство устранения неполадок MissingMetadataException](https://dotnet.github.io/native/troubleshooter/type.html) для типов.  
  
- [Средство устранения неполадок MissingMetadataException](https://dotnet.github.io/native/troubleshooter/method.html) для методов.  
  
> [!NOTE]
>  Этот справочник документирует три типа исключений, которые уникальны для машинного кода .NET. Справочная документация по API-интерфейса отражения .NET Framework core, см. в разделе <xref:System.Reflection>, <xref:System.Reflection.Context> и <xref:System.Reflection.Emit> пространства имен. Справочную документацию по основному API взаимодействия для .NET Framework см. в разделе <xref:System.Runtime.InteropServices>.  
  
## <a name="systemreflection-namespace"></a>Пространства имен System.Reflection  
 Пространство имен <xref:System.Reflection> содержит базовые типы, используемые для отражения в платформе .NET Framework. Для машинного кода .NET он также включает два новых типа исключений:  
  
|Класс|Описание|  
|-----------|-----------------|  
|[MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md)|Исключение, возникающее при использовании отражения для извлечения метаданных, которые не существуют.|  
|[MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md)|Исключение возникает, когда метаданные для типа или члена типа доступны, но его реализация была удалена.|  
  
 Для получения сведений о других типов из этого пространства имен см. страницы справочника <xref:System.Reflection> в наборе документации платформы .NET Framework.  
  
## <a name="systemruntimecompilerservices-namespace"></a>Пространство имен System.Runtime.CompilerServices  
 Пространство имен <xref:System.Runtime.CompilerServices> содержит типы, создаваемые для пользователя компиляторами языка. Для машинного кода .NET он также включает новый тип исключения:  
  
|Класс|Описание|  
|-----------|-----------------|  
|[MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)|Исключение, которое возникает, когда вызывается ручной метод маршалинга, но не найдены метаданные для типа в ходе статического анализа или в файле директив среды выполнения.|  
  
 Для получения сведений о других типов из этого пространства имен см. страницы справочника <xref:System.Runtime.CompilerServices> в наборе документации платформы .NET Framework.  
  
## <a name="see-also"></a>См. также

- [Класс MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)
- [Класс MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md)
- [Класс MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md)
- [Начало работы](../../../docs/framework/net-native/getting-started-with-net-native.md)
