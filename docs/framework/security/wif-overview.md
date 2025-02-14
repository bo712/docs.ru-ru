---
title: Обзор Windows Identity Foundation 4.5
ms.date: 03/30/2017
ms.assetid: 5f723345-7270-49e2-b638-b3a34bd40517
author: BrucePerlerMS
ms.openlocfilehash: d3076bbda47ac4aac0c8f0b9f9c69d17f370e765
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592403"
---
# <a name="windows-identity-foundation-45-overview"></a>Обзор Windows Identity Foundation 4.5
Windows Identity Foundation 4.5 — это набор классов .NET Framework для реализации в приложениях удостоверений на основе утверждений. С его помощью вам будет гораздо проще воспользоваться преимуществами приложений и служб, поддерживающих утверждения. WIF 4.5 можно использовать в любом веб-приложении или в любой веб-службе, использующей NET Framework 4.5 или более поздней версии. WIF — один из компонентов семейства ПО Microsoft Federated Identity, реализующего общую отраслевую концепцию на основе открытых стандартов. Федеративная Идентификация состоит из трех компонентов: [Службы федерации Active Directory®](https://go.microsoft.com/fwlink/?LinkID=247516) (AD FS) 2.0, [службы управления Windows Azure доступ](https://go.microsoft.com/fwlink/?LinkID=247517) (ACS) и WIF. В совокупности эти 3 компонента формируют основу новой облачной платформы удостоверений и доступа на основе утверждений.  
  
 Дополнительные сведения о WIF см. в разделе [Windows Identity Foundation, веб-сайт](https://go.microsoft.com/fwlink/?LinkId=149009) в центре разработчиков безопасности на сайте MSDN. Введение в создание приложений с помощью WIF, см. в разделе [Programming Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=210158) , Витторио Берточчи (опубликованных издательством Microsoft Press).  
  
## <a name="wif-45-features"></a>Возможности WIF 4.5  
 WIF 4.5 — это платформа для создания приложений, поддерживающих удостоверения. Данная платформа абстрагирует протоколы WS-Trust и WS-Federation и предоставляет разработчикам API-интерфейсы для создания приложений, поддерживающих утверждения, а также, при необходимости, служб токенов безопасности (STS). Приложения могут использовать WIF для обработки токенов, выданных службой STS (например, AD FS 2.0 или ACS), и принимать решения на основе удостоверения на уровне веб-приложения или веб-службы.  
  
 Основные возможности WIF 4.5:  
  
- Создание приложения, поддерживающего удостоверения (приложения проверяющей стороны). WIF помогает разработчикам создавать приложения, поддерживающие удостоверения. Помимо модели утверждений, данное семейство предоставляет разработчикам приложений набор разнообразных API-интерфейсов, помогающих принимать решения о предоставлении пользователю доступа на основе утверждений.  WIF также предоставляет разработчикам согласованный интерфейс программирования с возможностью выбрать для создания приложений среду ASP.NET или WCF.  
  
- Добавление поддержки делегирования удостоверений в приложения, поддерживающие утверждения.  WIF предлагает возможность сохранять удостоверения исходных источников запросов в средах нескольких служб. Эта возможность достигается с помощью функций "ActAs"или "OnBehalfOf", представленных в платформе, и позволяет разработчикам добавлять в приложения, поддерживающие утверждения, функцию поддержки делегирования удостоверений.  
  
- Создание настраиваемых служб STS.  WIF значительно упрощает процесс создания настраиваемой службы STS, поддерживающей протокол WS-Trust. Такая служба STS также именуется "активной".  
  
     Кроме того, данная платформа также обеспечивает возможность создания службы STS с поддержкой WS-Federation для клиентов на основе веб-браузера. Такая служба STS также именуется "пассивной".  
  
- Новое средство удостоверения и доступа для Visual Studio 11, предоставляющее возможность защитить приложение с помощью удостоверений на основе утверждений и принять пользователей от различных поставщиков удостоверений. Это средство STS можно загрузить со следующего URL: <https://go.microsoft.com/fwlink/?LinkID=245849> или непосредственно из Visual Studio 11, выполнив поиск «identity» в диспетчере расширений. Дополнительные сведения см. в разделе [Средство Identity and Access Tool для Visual Studio 2012](../../../docs/framework/security/identity-and-access-tool-for-vs.md).  
  
 STS поддерживает следующие основные сценарии:  
  
- Федерация.  WIF дает возможность включить федерацию между двумя или несколькими партнерами. Возможность создания приложений, поддерживающих утверждения (приложения проверяющей стороны) и настраиваемые службы STS помогает разработчикам реализовать такой сценарий.  
  
- Делегирование удостоверения.  WIF упрощает поддержку удостоверений за пределами службы, благодаря чему разработчики могут реализовать сценарий делегирования удостоверений.  
  
- Расширенная аутентификация. Требования к аутентификации могут быть различными для разных ресурсов в пределах одного приложения. WIF предоставляет разработчикам возможность создания приложений, предъявляющих различные требования к аутентификации на разных этапах (например, первоначальный вход в систему будет выполняться с аутентификацией по имени пользователя или паролю, а затем будет применяться аутентификация по смарт-карте).  
  
 С помощью WIF вам будет гораздо проще реализовать преимущества модели удостоверений, основанных на утверждениях. Дополнительные сведения см. в [техническом документе по Windows Identity Foundation для разработчиков](https://download.microsoft.com/download/7/d/0/7d0b5166-6a8a-418a-addd-95ee9b046994/windowsidentityfoundationwhitepaperfordevelopers-rtw.pdf).
