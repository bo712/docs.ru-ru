---
title: Выбор версии языка C#. Руководство по C#
description: Настройка компилятора для выполнения проверки синтаксиса с помощью конкретной версии компилятора
ms.date: 02/28/2019
ms.openlocfilehash: feb3e51a107f9830071b55c7985f202edc842f4a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59770884"
---
# <a name="select-the-c-language-version"></a>Выбор версии языка C#

Компилятор C# определяет версию языка по умолчанию на основе целевой платформы или платформ проекта. Если проект предназначен для платформы в предварительной версии с поддержкой соответствующего языка в предварительной версии, будет использоваться язык, поддерживаемый в предварительной версии. Если же проект не предназначен для платформы в предварительной версии, используется последняя дополнительная версия.

Например, в период действия предварительной версии .NET Core 3.0 в любом проекте, предназначенном для `netcoreapp3.0` или `netstandard2.1` (поддерживаются в предварительной версии), будет использоваться язык C# 8.0 (также в предварительной версии). В проектах, предназначенных для любой выпущенной версии, будет использоваться C# 7.3 (последняя выпущенная версия). Это означает, что в любом проекте, предназначенном для .NET Framework будет использоваться последняя версия (C# 7.3). 

Эта возможность разделяет установку новых версий пакета SDK и средств в среде разработки и включение новых возможностей языка в проект. Вы можете установить последнюю версию пакета SDK и средств на компьютер сборки. В каждом проекте можно настроить использование определенной версии языка для сборки. По умолчанию любые функции языка, основанные на новых типах или новом поведении среды CLR, будут включены, только если проекты предназначены для этих платформ.

Поведение по умолчанию можно переопределить, указав версию языка. Существует несколько способов задания языковой версии:

- использование [быстрого действия Visual Studio](#visual-studio-quick-action);
- установка версии языка в [пользовательском интерфейсе Visual Studio](#set-the-language-version-in-visual-studio);
- ручное редактирование [**CSPROJ**-файла](#edit-the-csproj-file);
- задание языковой версии [для нескольких проектов в подкаталоге](#configure-multiple-projects);
- настройка [параметра компилятора `-langversion`](#set-the-langversion-compiler-option).

## <a name="visual-studio-quick-action"></a>Быстрое действие Visual Studio

Visual Studio позволяет определить требуемую версию языка. При использовании функции языка, которая недоступна для текущей выбранной версии, Visual Studio отображает возможное решение для изменения версии языка для проекта.

## <a name="set-the-language-version-in-visual-studio"></a>Установка версии языка в Visual Studio

Вы можете задать версию в Visual Studio. В обозревателе решений щелкните узел проекта правой кнопкой мыши и выберите пункт **Свойства**. Откройте вкладку **Сборка** и нажмите на кнопку **Дополнительно**. В раскрывающемся списке выберите версию. На следующем рисунке показаны "последние" параметры:

![Снимок экрана: дополнительные параметры сборки, в которых можно указать версию языка](./media/configure-language-version/advanced-build-settings.png)

> [!NOTE]
> Если вы используете интегрированную среду разработки Visual Studio для обновления CSPROJ-файлов, IDE создает отдельные узлы для каждой конфигурации сборки. Как правило, вы устанавливаете одинаковое значение во всех конфигурациях сборки, но необходимо задать его явным образом для каждой конфигурации сборки или выбрать "Все конфигурации" при изменении этого параметра. В CSPROJ-файле вы увидите следующий код:
>
>```xml
> <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
>  <LangVersion>latest</LangVersion>
></PropertyGroup>
>
> <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|AnyCPU'">
>  <LangVersion>latest</LangVersion>
> </PropertyGroup>
> ```
>

## <a name="edit-the-csproj-file"></a>Редактирование CSPROJ-файла

Версию языка можно задать в **CSPROJ**-файле. Добавьте элемент следующим образом:

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

Значение параметра `latest` использует последнюю дополнительную версию языка C#. Допустимые значения:

|Значение|Значение|
|------------|-------------|
|preview|Компилятор допускает использование любого допустимого синтаксиса языка из последней предварительной версии.|
|latest|Компилятор принимает синтаксис из последней выпущенной версии компилятора (включая дополнительный номер версии).|
|latestMajor|Компилятор принимает синтаксис из последней основной версии компилятора.|
|8.0|Компилятор принимает только синтаксис, включенный в спецификацию C# 8.0 или более ранней версии.|
|7.3|Компилятор принимает только синтаксис, включенный в спецификацию C# 7.3 или более ранней версии.|
|7.2|Компилятор принимает только синтаксис, включенный в спецификацию C# 7.2 или более ранней версии.|
|7.1|Компилятор принимает только синтаксис, включенный в спецификацию C# 7.1 или более ранней версии.|
|7|Компилятор принимает только синтаксис, включенный в спецификацию C# 7.0 или более ранней версии.|
|6|Компилятор принимает только синтаксис, включенный в спецификацию C# 6.0 или более ранней версии.|
|5|Компилятор принимает только синтаксис, включенный в спецификацию C# 5.0 или более ранней версии.|
|4|Компилятор принимает только синтаксис, включенный в спецификацию C# 4.0 или более ранней версии.|
|3|Компилятор принимает только синтаксис, включенный в спецификацию C# 3.0 или более ранней версии.|
|ISO-2|Компилятор принимает только синтаксис, включенный в спецификацию ISO/IEC 23270:2006 C# (2.0) |
|ISO-1|Компилятор принимает только синтаксис, включенный в спецификацию ISO/IEC 23270:2003 C# (1.0/1.2) |

## <a name="configure-multiple-projects"></a>Настройка нескольких проектов

Можно создать файл **Directory.Build.props**, содержащий элемент `<LangVersion>`, чтобы настроить несколько каталогов. Обычно это делается в каталоге решения. Добавьте следующий код в файл **Directory.Build.props** в каталоге решения:

```xml
<Project>
 <PropertyGroup>
   <LangVersion>7.3</LangVersion>
 </PropertyGroup>
</Project>
```

Теперь сборки в каждом подкаталоге каталога, который содержит этот файл, будут использовать синтаксис C# версии 7.3. Дополнительные сведения см. в статье о [настройке сборки](/visualstudio/msbuild/customize-your-build).

## <a name="set-the-langversion-compiler-option"></a>Задание параметра компилятора langversion

Вы можете использовать параметр командной строки `-langversion`. Дополнительные сведения см. в статье, посвященной параметру компилятора [-langversion](../language-reference/compiler-options/langversion-compiler-option.md). Чтобы просмотреть список допустимых значений, введите `csc -langversion:?`.
