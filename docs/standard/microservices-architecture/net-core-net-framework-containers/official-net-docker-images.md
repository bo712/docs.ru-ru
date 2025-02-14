---
title: Официальные .NET-образы Docker
description: Архитектура микрослужб .NET для упакованных в контейнеры приложений .NET | Официальные .NET-образы Docker
ms.date: 01/07/2019
ms.openlocfilehash: b184e8f3606da8448a06a1cad90688958ecbce3a
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644347"
---
# <a name="official-net-docker-images"></a>Официальные .NET-образы Docker

Официальные .NET-образы Docker — это образы Docker, оптимизированные Майкрософт. Они доступны для всех в репозиториях Майкрософт в [Центре Docker](https://hub.docker.com/u/microsoft/). Каждый репозиторий может содержать несколько образов, в зависимости от версии платформы .NET и операционной системы (Linux Debian, Linux Alpine, Windows Nano Server, Windows Server Core и т. д.).

Начиная с версии .NET Core 2.1, все образы .NET Core, в том числе для ASP.NET Core, можно найти в репозитории образов .NET Core на сайте Docker Hub: https://hub.docker.com/_/microsoft-dotnet-core/

Большинство репозиториев образов предоставляют широкие возможности по использованию тегов, чтобы облегчить выбор не только конкретной версии платформы, но и ОС (дистрибутива Linux или версии Windows).

## <a name="net-core-and-docker-image-optimizations-for-development-versus-production"></a>Оптимизация образов .NET Core и Docker для разработки и производства

При создании образов Docker для разработчиков Майкрософт сосредотачивается на следующих основных сценариях:

- образы, используемые для *разработки* и сборки приложений .NET Core;

- образы, используемые для *выполнения* приложений .NET Core.

Зачем использовать несколько образов? При разработке, сборке и выполнении приложений в контейнерах приоритеты будут разными. Предоставляя различные образы для каждой из задач, Майкрософт помогает оптимизировать отдельные процессы разработки, сборки и развертывания приложений.

### <a name="during-development-and-build"></a>Во время разработки и сборки

Во время разработки важна скорость выполнения итераций для изменений и возможность отлаживать изменения. Размер образа не так важен, как возможность быстро вносить изменения в код и просматривать их. Некоторые средства и "контейнеры агентов сборки" на стадии разработки и сборки используют образ .NET Core для разработки (*mcr.microsoft.com/dotnet/core/sdk:2.2*). При сборке внутри контейнера Docker надо учитывать, какие элементы необходимы для компиляции приложения. Сюда входят зависимости компилятора и другие зависимости .NET.

Почему так важен этот тип образа сборки? Этот образ не развертывается в рабочую среду. Это образ, который вы используете для сборки содержимого, помещаемого в рабочий образ. Если вы используете многоэтапную сборку Docker, этот образ будет применяться в среде непрерывной интеграции (CI) или в среде сборки.

### <a name="in-production"></a>Производство

При производстве важно быстро развернуть и запустить контейнеры на основе рабочего образа .NET Core. Поэтому образ только для среды выполнения на базе *mcr.microsoft.com/dotnet/core/aspnet:2.2* имеет малый размер и может быстро перемещаться по сети из реестра Docker к узлам Docker. Содержимое готово к запуску, поэтому период времени от запуска контейнера до обработки результатов минимален. В модели Docker не нужна компиляция кода C\#, поскольку вы выполняете команду dotnet build или dotnet publish при использовании контейнера сборки.

В этот оптимизированный образ вы помещаете только двоичные файлы и другое содержимое, необходимое для выполнения приложения. Например, в содержимое, создаваемое командой dotnet publish, входят только скомпилированные двоичные файлы .NET, образы, файлы .js и .css. Со временем появятся образы, которые содержат пакеты, предварительно скомпилированные JIT-компилятором (компиляция из промежуточного языка в машинный код во время выполнения).

Хотя существует несколько версий образов .NET Core и ASP.NET Core, они все имеют один или несколько общих уровней, включая базовый уровень. Поэтому образ занимает мало места на диске, ведь он содержит лишь различия между вашим образом и базовым образом. В результате можно быстро извлекать образы из реестра.

При просмотре репозиториев .NET-образов в центре Docker вы найдете несколько версий, классифицированных или помеченных тегами. Эти теги помогают определить, какую версию использовать, как показано в таблице:

| Изображение                                       | Комментарии                                                                                          |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| mcr.microsoft.com/dotnet/core/aspnet:**2.2** | ASP.NET Core только со средой выполнения и оптимизацией ASP.NET Core в Linux и Windows (для разных архитектур) |
| mcr.microsoft.com/dotnet/core/sdk:**2.2**    | .NET Core с пакетами SDK в Linux и Windows (для разных архитектур)                                  |

> [!div class="step-by-step"]
> [Назад](net-container-os-targets.md)
> [Вперед](../architect-microservice-container-applications/index.md)
