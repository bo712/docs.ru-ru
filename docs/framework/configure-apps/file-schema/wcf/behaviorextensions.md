---
title: <behaviorExtensions>
ms.date: 03/30/2017
ms.assetid: 59f2791a-c78f-40d7-aa80-0d9cd10135d9
ms.openlocfilehash: 81ce9bb0e55fe4570f8a21187d9df80ea22393fe
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61673463"
---
# <a name="behaviorextensions"></a>\<behaviorExtensions>
Расширения поведений позволяют пользователям создавать пользовательские элементы поведений. Эти элементы могут использоваться вместе со стандартными элементами поведений Windows Communication Foundation (WCF). В разделе `behaviorExtensions` определяется элемент, который может использоваться в конфигурации. Далее приведен пример типичного расширения поведения.  
  
```xml  
<system.serviceModel>
  <extensions>
    <behaviorExtensions>
      <add name="myBehavior"
           type="Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </behaviorExtensions>
  </extensions>
</system.serviceModel>
```  
  
 Чтобы добавить в элемент возможности конфигурации, нужно записать и зарегистрировать элемент конфигурации. Дополнительные сведения об этом см. в документации по <xref:System.Configuration>.  
  
 После определения элемента и его типа конфигурации поведение можно использовать, как показано в следующем примере.  
  
```xml  
<behaviors>
  <behavior configurationName="testChannelBehavior">
    <myBehavior />
    <channelSecurity cacheCookies="false"
                     detectReplays="false"
                     maxCachedNonces="9"
                     maxClockSkew="00:00:03"
                     maxCookieCachingTime="00:07:24"
                     replayWindow="00:07:22.2190000" />
  </behavior>
</behaviors>
```  
  
## <a name="security"></a>Безопасность  
 Настоятельно рекомендуется использовать полные имена сборок при регистрации типов в файлах `machine.config` и `app.config`. Если тип определен неоднозначно, загрузчик типов среды CLR ищет его в следующих местоположениях в заданном порядке:  
  
 Если сборка типа известна, загрузчик ищет в местах перенаправления файла конфигурации, в глобальном кэше сборок, в текущей сборке, используя данные конфигурации, и в базовой папке приложения. Если сборка неизвестна, загрузчик ищет в текущей сборке, в библиотеке mscorlib и в месте, возвращаемом обработчиком событий `TypeResolve`. Порядок поиска в среде CLR может быть изменен с помощью таких средств, как механизм пересылки типа и событие AppDomain.TypeResolve.  
  
 Злоумышленник может использовать порядок поиска в среде CLR и выполнить неавторизованный код. Использование полных (строгих) имен однозначно идентифицирует тип и еще больше повышает безопасность системы.  
  
 Дополнительные сведения см. в разделе [Обнаружение сборок в среде выполнения](https://go.microsoft.com/fwlink/?LinkId=95336) и <xref:System.AppDomain.TypeResolve>.  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>
- [Настройка и расширение среды выполнения с помощью поведений](../../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)
