---
title: Разработка современных веб-приложений с помощью ASP.NET Core и Azure
description: Этот документ является полным руководством по созданию монолитных веб-приложений с помощью ASP.NET Core и Azure.
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: 0b29a407ae18f3ce0c7499c75ee3c888296102c2
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65639312"
---
# <a name="architect-modern-web-applications-with-aspnet-core-and-azure"></a>Разработка современных веб-приложений с помощью ASP.NET Core и Azure

![Изображение обложки руководства по архитектуре современных веб-приложений.](./media/index/web-application-guide-cover-image.png)

ИЗДАТЕЛЬ

Подразделение Microsoft Developer Division, команды разработки .NET и Visual Studio

Подразделение корпорации Майкрософт

One Microsoft Way

Redmond, Washington 98052-6399

© Корпорация Майкрософт (Microsoft Corporation), 2019.

Все права защищены. Запрещается полное или частичное воспроизведение или передача настоящей книги в любом виде или любыми средствами без письменного разрешения издателя.

Эта книга предоставляется на условиях "как есть" и выражает взгляды и мнения автора. Взгляды, мнения и сведения, содержащиеся в этой книге, включая URL-адреса и другие ссылки на веб-сайты, могут изменяться без уведомления.

Некоторые приведенные в книге примеры служат только для иллюстрации и являются вымышленными. Все совпадения с реальными наименованиями, людьми и любыми другими предметами являются непреднамеренными и случайными.

Microsoft и товарные знаки, перечисленные на странице "Товарные знаки" на сайте https://www.microsoft.com, являются товарными знаками группы компаний Майкрософт.

Mac и macOS являются товарными знаками Apple Inc.

Логотип Docker с изображением кита является зарегистрированным товарным знаком Docker, Inc. Используется с разрешения.

Все другие наименования и логотипы являются собственностью своих законных владельцев.

Автор:

> **Стив Смит (Steve Smith)**, преподаватель и разработчик программного обеспечения, [Ardalis.com](https://ardalis.com)

Редакторы:

> **Майра Вензел (Maira Wenzel)**

## <a name="introduction"></a>Вступление

.NET Core и ASP.NET Core имеют ряд преимуществ по сравнению с традиционной разработкой .NET. Используйте .NET Core для серверных приложений, если для их успешной работы вам важны некоторые или все приведенные далее аспекты:

- Поддержка разных платформ.

- Использование микрослужб.

- Использование контейнеров Docker.

- Требования к обеспечению высокой производительности и масштабируемости.

- Параллельное управление версиями приложения .NET на одном сервере.

Эти требования поддерживаются многими стандартными приложениями .NET, но оптимизированные платформы ASP.NET Core и .NET Core обеспечивают расширенную поддержку указанных выше сценариев.

Все больше организаций предпочитают размещать свои веб-приложения в облаке с помощью таких служб, как Microsoft Azure. Рекомендуется рассмотреть возможность размещения приложения в облаке, если для приложения или организации важны следующие моменты:

- Сокращение инвестиций в центр обработки данных (оборудование, программное обеспечение, помещения, коммунальные услуги, управление серверами и т. д.)

- Гибкие цены (оплата за фактически используемые, а не простаивающие ресурсы).

- Исключительная надежность.

- Улучшенная мобильность приложений, простота изменения места и способа их развертывания.

- Гибкая емкость, масштабирование в соответствии с фактическими потребностями.

Создание веб-приложений с помощью ASP.NET Core, размещенных в Azure, имеет множество конкурентных преимуществ по сравнению с традиционными альтернативами. Платформа ASP.NET Core оптимизирована для современных методик разработки веб-приложений и сценариев размещения в облаке. В этом руководстве вы узнаете, как спроектировать приложения ASP.NET Core, чтобы максимально эффективно воспользоваться этими возможностями.

## <a name="purpose"></a>Цель

Этот документ является полным руководством по созданию *монолитных* веб-приложений с помощью ASP.NET Core и Azure. В этом контексте монолитность означает то, что эти приложения развертываются как единое целое, а не как коллекция интерактивных служб и приложений.

Это руководство представляет собой дополнение к микрослужбам ["_.NET. Архитектура для упакованных в контейнеры приложений .NET_"](../microservices-architecture/index.md) с акцентом на Docker, микрослужбах и развертывании контейнеров для размещения корпоративных приложений.

### <a name="net-microservices-architecture-for-containerized-net-applications"></a>Микрослужбы .NET. Архитектура контейнерных приложений .NET

- **электронная книга**  
  <https://aka.ms/MicroservicesEbook>
- **Пример приложения**  
  <https://aka.ms/microservicesarchitecture>

## <a name="who-should-use-this-guide"></a>Кому необходимо это руководство

Это руководство предназначено главным образом для разработчиков, руководителей отделов разработки и архитекторов, заинтересованных в создании современных веб-приложений с помощью технологий и служб Майкрософт в облаке.

Вторичной аудиторией являются лица, ответственные за принятие технических решений, которые уже знакомы с ASP.NET или Azure и которым требуются сведения о целесообразности обновления до ASP.NET Core для разработки новых и поддержки существующих проектов.

## <a name="how-you-can-use-this-guide"></a>Как использовать это руководство

Это руководство было сведено в относительно небольшой документ, в котором основное внимание уделяется созданию веб-приложений с помощью современных технологий .NET и Windows Azure. Поэтому, чтобы получить базовое представление о таких приложениях и разобраться в соответствующих технических рекомендациях, изучите документ полностью. Это руководство вместе с примером приложения может быть хорошей отправной точкой или полезным справочным документом. Используйте приведенный пример приложения в качестве шаблона для собственных приложений, или чтобы увидеть, каким образом можно организовать составные части приложения. Принимая решение о применении этих вариантов к своему приложению, вы всегда можете обратиться к описанным в руководстве принципам и направлениям архитектуры и технологическим возможностям.

При необходимости вы можете порекомендовать это руководство членам своей команды, чтобы и они были в курсе всех важных аспектов. Если все заинтересованные лица будут использовать общий набор терминологии и придерживаться основополагающих принципов, архитектурные модели и практики будут применяться более последовательно.

## <a name="references"></a>Ссылки

- **Выбор между .NET Core и .NET Framework для серверных приложений**  
  [https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server](../choosing-core-framework-server.md)

>[!div class="step-by-step"]
>[Вперед](modern-web-applications-characteristics.md)
