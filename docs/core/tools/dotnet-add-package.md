---
title: Команда dotnet add package
description: Команду dotnet add package удобно использовать для добавления ссылки на пакет NuGet в проект.
ms.date: 04/24/2019
ms.openlocfilehash: 82f178026b46eb0237243b8ae49d17fbcc1af6ec
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959251"
---
# <a name="dotnet-add-package"></a>dotnet add package

**Эта статья относится к ✓** SDK для .NET Core 1.x и более поздних версий

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>name

`dotnet add package` — добавляет ссылку на пакет в файл проекта.

## <a name="synopsis"></a>Краткий обзор

`dotnet add [<PROJECT>] package <PACKAGE_NAME> [-h|--help] [-f|--framework] [--interactive] [-n|--no-restore] [--package-directory] [-s|--source] [-v|--version]`

## <a name="description"></a>Описание

Команда `dotnet add package` предоставляет удобный способ для добавления ссылки на пакет в файл проекта. После запуска этой команды выполняется проверка совместимости, чтобы убедиться, что пакет совместим со всеми платформами в проекте. Если проверка проходит успешно, в файл проекта добавляется элемент `<PackageReference>` и выполняется команда [dotnet restore](dotnet-restore.md).

[!INCLUDE[DotNet Restore Note](../../../includes/dotnet-restore-note.md)]

Например, при добавлении `Newtonsoft.Json` в *ToDo.csproj* создаются выходные данные примерно следующего вида:

```console
  Writing C:\Users\mairaw\AppData\Local\Temp\tmp95A8.tmp
info : Adding PackageReference for package 'Newtonsoft.Json' into project 'C:\projects\ToDo\ToDo.csproj'.
log  : Restoring packages for C:\Temp\projects\consoleproj\consoleproj.csproj...
info :   GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/newtonsoft.json/index.json 79ms
info :   GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/12.0.1/newtonsoft.json.12.0.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/newtonsoft.json/12.0.1/newtonsoft.json.12.0.1.nupkg 232ms
log  : Installing Newtonsoft.Json 12.0.1.
info : Package 'Newtonsoft.Json' is compatible with all the specified frameworks in project 'C:\projects\ToDo\ToDo.csproj'.
info : PackageReference for package 'Newtonsoft.Json' version '12.0.1' added to file 'C:\projects\ToDo\ToDo.csproj'.
```

Файл *ToDo.csproj* теперь содержит элемент [`<PackageReference>`](/nuget/consume-packages/package-references-in-project-files) для пакета, на который указывает ссылка.

```xml
<PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
```

## <a name="arguments"></a>Аргументы

* **`PROJECT`**

  Указывает файл проекта. Если он не указан, команда ищет текущий каталог для него.

* **`PACKAGE_NAME`**

  Добавляемая ссылка на пакет.

## <a name="options"></a>Параметры

* **`-f|--framework <FRAMEWORK>`**

  Добавляет ссылку на пакет только при ориентации на конкретную [платформу](../../standard/frameworks.md).

* **`-h|--help`**

  Выводит краткую справку по команде.

* **`--interactive`**

  Позволяет остановить команду и дождаться, пока пользователь введет данные или выполнит действие (например, завершит проверку подлинности). Доступно с версии пакета SDK 2.1 для .NET Core версии 2.1.400 или более поздней версии.

* **`-n|--no-restore`**

  Добавляет ссылку на пакет без предварительного просмотра восстановления и проверки совместимости.

* **`--package-directory <PACKAGE_DIRECTORY>`**

  Каталог, в который нужно восстановить пакеты.

* **`-s|--source <SOURCE>`**

  Источник пакета NuGet для использования в ходе операции восстановления.

* **`-v|--version <VERSION>`**

  Версия пакета. См. статью [Package versioning](https://docs.microsoft.com/nuget/reference/package-versioning) (Управление версиями пакета).

## <a name="examples"></a>Примеры

* Добавление пакета NuGet `Newtonsoft.Json` в проект:

  ```console
  dotnet add package Newtonsoft.Json
  ```

* Добавление определенной версии пакета в проект:

  ```console
  dotnet add ToDo.csproj package Microsoft.Azure.DocumentDB.Core -v 1.0.0
  ```

* Добавление пакета с помощью определенного источника NuGet:

  ```console
  dotnet add package Microsoft.AspNetCore.StaticFiles -s https://dotnet.myget.org/F/dotnet-core/api/v3/index.json
  ```
