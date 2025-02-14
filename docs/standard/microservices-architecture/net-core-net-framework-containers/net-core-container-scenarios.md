---
title: Выбор .NET Core для контейнеров Docker
description: Архитектура микрослужб .NET для упакованных в контейнеры приложений .NET | Выбор .NET Core для контейнеров Docker
ms.date: 09/11/2018
ms.openlocfilehash: 54ed1b4bbb16352b8c99204383f85ffb25d62be7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644375"
---
# <a name="when-to-choose-net-core-for-docker-containers"></a>Выбор .NET Core для контейнеров Docker

Благодаря модульности и упрощенному характеру .NET Core идеально подходит для контейнеров. При развертывании и запуске контейнера размер его образа гораздо меньше в среде .NET Core. Напротив, при использовании .NET Framework для контейнера необходимо использовать Windows Server Core в качестве базового образа, который занимает гораздо больше места, чем образ Nano Windows Server или Linux, которые используются для .NET Core.

Кроме того, платформа .NET Core является кроссплатформенной, поэтому вы можете разворачивать серверные приложения в Linux и Windows контейнерах. Однако при использовании традиционной .NET Framework можно развернуть только образ, основанный на Windows Server Core.

Ниже более подробно описаны преимущества .NET Core.

## <a name="developing-and-deploying-cross-platform"></a>Разработка и развертывание на различных платформах

Очевидно, что если ваша цель — приложение (веб-приложение или служба), которое можно запускать на нескольких платформах, поддерживаемых в Docker (Linux и Windows), целесообразно выбрать .NET Core, так как платформа .NET Framework поддерживает только Windows.

.NET Core также поддерживает macOS в качестве платформы разработки. Тем не менее при развертывании контейнеров на узле Docker этот узел должен (в настоящее время) базироваться на Windows или Linux. Например, в среде разработки можно использовать виртуальную машину с Linux, запущенную на компьютере с Mac.

[Visual Studio](https://www.visualstudio.com/vs/) предоставляет интегрированную среду разработки (IDE) для Windows и поддерживает разработку с использованием Docker.

[Visual Studio для Mac](https://www.visualstudio.com/vs/visual-studio-mac/) — это интегрированная среда разработки, которая является эволюцией Xamarin Studio, выполняется в macOS и поддерживает разработку приложений на основе Docker. Она должна быть предпочтительным вариантом для разработчиков, работающих на компьютерах Mac и стремящихся использовать мощную интегрированную среду разработки.

Можно также использовать редактор [Visual Studio Code](https://code.visualstudio.com/) (VS Code) на платформах macOS, Linux и Windows. VS Code поддерживает .NET Core, включая технологию IntelliSense и отладку. Поскольку VS Code является упрощенным редактором, то для разработки контейнерных приложений на компьютере Mac его можно использовать в сочетании с Docker CLI и [.NET Core CLI](../../../core/tools/index.md). Для разработки на платформе .NET Core также можно использовать большинство сторонних редакторов, например Sublime, Emacs, vi и проект с открытым кодом OmniSharp, который также поддерживает технологию IntelliSense.

Помимо интегрированных сред разработки и редакторов для всех поддерживаемых платформ можно использовать средства [.NET Core CLI](../../../core/tools/index.md).

## <a name="using-containers-for-new-green-field-projects"></a>Использование контейнеров для новых ("с нуля") проектов

Контейнеры обычно используются в сочетании с архитектурой микрослужб, хотя их также можно использовать для упаковки веб-приложений или служб, созданных на базе любого архитектурного шаблона. Среду .NET Framework можно использовать для контейнеров Windows, но упрощенный характер и модульный принцип среды .NET Core делают ее оптимальной для контейнеров и архитектуры микрослужб. При создании и развертывании контейнера размер его образа гораздо меньше в среде .NET Core, чем в .NET Framework.

## <a name="creating-and-deploying-microservices-on-containers"></a>Создание и развертывание микрослужб в контейнерах

Традиционный .NET Framework можно использовать для создания приложений на основе микрослужб (без контейнеров) с помощью простых процессов. Платформа .NET Framework уже установлена и совместно используется процессами, поэтому в этом случае процессы небольшие по размеру и быстро выполняются. Но при использовании контейнеров образы для традиционного .NET Framework основаны на Windows Server Core, что делает их слишком большими для подхода "микрослужбы в контейнерах".

В противоположность этому .NET Core благодаря упрощенному характеру является наилучшим выбором, если вы используете ориентированную на микрослужбы систему, которая основана на контейнерах. Кроме того, связанные с NET Core образы, как Linux, так и Windows Nano, являются компактными и небольшими по размеру, что обеспечивает их быстрый запуск.

Термин "микрослужба" означает, что она должна быть настолько маленькой, насколько это возможно, чтобы обеспечивать быстрое развертывание, занимать мало места в памяти (см. статью о [проблемно-ориентированном проектировании](https://en.wikipedia.org/wiki/Domain-driven_design)), решать небольшую часть задачи и быть способной к быстрому запуску и остановке. Для выполнения этих требований необходимо использовать небольшой и быстро создаваемый образ контейнера, такой как образ контейнера .NET Core.

Архитектура микрослужб также позволяет использовать сочетание технологий за пределами службы. Благодаря этому возможна постепенная миграция на технологию .NET Core новых служб, которые работают совместно с другими микрослужбами или со службами, разработанными с помощью Node.js, Python, Java, GoLang и других технологий.

## <a name="deploying-high-density-in-scalable-systems"></a>Развертывание с высокой плотностью в масштабируемых системах

Если для вашей системы, основанной на контейнерах, требуется максимально возможная плотность, детализация и производительность, то мы рекомендуем использовать .NET Core и ASP.NET Core. Среда ASP.NET Core в 10 раз быстрее, чем ASP.NET в традиционном .NET Framework, и поддерживает другие популярные отраслевые технологии микрослужб, такие как сервлеты Java, Go и Node.js.

Это особенно важно для архитектур микрослужб, где могут выполняться сотни микрослужб (контейнеров). Образы ASP.NET Core (основанные на среде выполнения .NET Core) на Windows Nano или Linux позволяют запустить систему с гораздо меньшим количеством серверов или виртуальных машин и, в конечном счете, снизить затраты на инфраструктуру и размещение.

>[!div class="step-by-step"]
>[Назад](general-guidance.md)
>[Вперед](net-framework-container-scenarios.md)
