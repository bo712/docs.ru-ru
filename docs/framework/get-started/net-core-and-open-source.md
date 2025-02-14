---
title: Ядро .NET и открытый исходный код
ms.date: 03/30/2017
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2c2eecdee3448b59422a8c6c73fc85745b41c52b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64626107"
---
# <a name="net-core-and-open-source"></a>Ядро .NET и открытый исходный код
В этом разделе приводится краткий обзор .NET Core и указываются ресурсы с дополнительными сведениями. Полный список разделов по .NET Core см. в [Руководстве по .NET Core](../../core/index.md).
  
<a name="BKMK_WhatisNETCore"></a>   
## <a name="what-is-net-core"></a>Что такое .NET Core?  
 .NET Core — это универсальная, модульная, кроссплатформенная и открытая версия платформы .NET Standard. Она содержит большую часть тех же интерфейсов API, что и платформа .NET Framework (но .NET Core включает меньший набор API) и включает компоненты среды выполнения, платформы и компилятора, а также инструменты, поддерживающие различные операционные системы и компоненты оборудования. Создание платформы .NET Core было вызвано необходимостью использовать рабочие нагрузки ASP.NET Core, а также необходимостью получить более современную реализацию платформы. Ее можно использовать при работе с устройствами, облаком, а также в сценариях внедрения и Интернета вещей.  
  
 Чтобы приступить к работе с .NET Core, посетите [домашнюю страницу .NET Core](https://www.microsoft.com/net/core).  
  
 Ниже перечислены основные характеристики .NET Core.  
  
- **Кроссплатформенность.** .NET Core предоставляет ключевые возможности для реализации возможностей приложений, необходимых для повторного использования этого кода независимо от целевой платформы. В настоящее время она поддерживает три основные операционные системы (ОС): Windows, Linux и macOS. Можно писать приложения и создавать библиотеки, которые будут выполняться на поддерживаемых операционных системах без изменений. Список поддерживаемых операционных систем см. в [плане развития .NET Core](https://github.com/dotnet/core/blob/master/roadmap.md).
  
- **Открытый исходный код.** .NET Core является одним из многих проектов под управлением [.NET Foundation](https://www.dotnetfoundation.org/) и доступна на сайте [GitHub](https://github.com/).  Наличие .NET Core в виде проекта с открытым исходным кодом обеспечивает более высокий уровень прозрачности процесса разработки и способствует привлечению активных и заинтересованных участников сообщества.  
  
- **Гибкое развертывание.** Существует два способа развертывания приложения: зависящее от платформы и автономное. В рамках зависящего от платформы развертывания устанавливаются только ваши приложения и сторонние зависимости устанавливаются, и ваше приложения зависит от наличия системной версии .NET Core.  При автономном развертывании версия .NET Core, используемая для построения приложения, также развертывается вместе с вашим приложением и сторонними зависимостями и может выполняться параллельно с другими версиями.    Дополнительные сведения см. в разделе [Развертывание приложений .NET Core](../../core/deploying/index.md).

- **Модульность.** Среда .NET Core является модульной, так как она выпускается в NuGet в небольших пакетах сборки. .NET Core предоставляется в виде небольших пакетов с компонентами, а не в одной большой сборке, которая содержит большинство основных возможностей. В этом случае мы имеем более гибкую модель разработки, а вы можете оптимизировать приложение, чтобы включать в него только необходимые пакеты NuGet. За счет небольшого размера контактной зоны приложения доступны такие преимущества, как более высокий уровень безопасности, минимальное обслуживание, улучшенная производительность и сниженные затраты в модели оплаты только используемых ресурсов.  
  
## <a name="the-net-core-platform"></a>Платформа .NET Core  
 Платформа .NET Core состоит из нескольких компонентов, включая управляемые компиляторы, среду выполнения, библиотеки базовых классов и многочисленные модели приложений, такие как ASP.NET Core. Дополнительные сведения о различных компонентов см. в следующих репозиториях [GitHub](https://github.com/).  
  
- [.NET Core](https://github.com/dotnet/core)  
  
- [CoreFX — фундаментальные библиотеки .NET Core](https://github.com/dotnet/corefx)  
  
- [CoreCLR — среда выполнения .NET Core](https://github.com/dotnet/coreclr)  
  
- [CLI — средства интерфейса командной строки .NET Core](https://github.com/dotnet/cli)  
  
- [Roslyn — платформа компилятора .NET](https://github.com/dotnet/roslyn)  
  
- [ASP.NET Core](https://github.com/aspnet/home)  
  
## <a name="see-also"></a>См. также

- [Домашняя страница .NET Core](https://www.microsoft.com/net/core)
- [Руководство по .NET Core](../../core/index.md)
- [Документация по ASP.NET Core](/aspnet/core/)
