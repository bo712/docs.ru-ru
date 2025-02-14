---
title: Размещение в службах IIS
ms.date: 03/30/2017
helpviewer_keywords:
- hosting services [WCF], IIS
ms.assetid: ddae14e8-143c-442d-b660-2046809b2d43
ms.openlocfilehash: 8563662a4408d0425e92b960301311ce5d423f9d
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025747"
---
# <a name="hosting-in-internet-information-services"></a>Размещение в службах IIS
Один из вариантов размещения служб Windows Communication Foundation (WCF) — внутри приложения Internet Information Services (IIS). Эта модель размещения похожа на модель, используемые ASP.NET и веб-служб ASP.NET Web services (ASMX).  
  
## <a name="versions-of-iis"></a>Версии IIS  
 WCF можно размещать в следующих версиях IIS в следующих операционных системах:  
  
- IIS 5.1 в [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)]. Эта среда хорошо подходит для проектирования и разработки размещаемых в IIS приложений, которые впоследствии будут развертываться на серверных операционных системах, например на [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)].  
  
- [!INCLUDE[iis601](../../../../includes/iis601-md.md)] в [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]. В службах [!INCLUDE[iis601](../../../../includes/iis601-md.md)] реализована расширенная модель процессов, которая обеспечивает лучшую масштабируемость, надежность и изоляцию приложений. Эта среда подходит для рабочего развертывания служб WCF, использующих только транспорт HTTP.  
  
- IIS 7.0 в [!INCLUDE[wv](../../../../includes/wv-md.md)] и [!INCLUDE[lserver](../../../../includes/lserver-md.md)]. Службы IIS 7.0 реализуют такую же расширенную модель процессов, как и [!INCLUDE[iis601](../../../../includes/iis601-md.md)], но используют службу активации Windows (WAS) для обеспечения поддержки активации и сетевого взаимодействия с помощью протоколов, отличных от HTTP. Эта среда подходит для разработки служб WCF, которые взаимодействуют через все сетевые протоколы, поддерживаемые платформой WCF (включая HTTP, net.tcp, net.pipe и net.msmq). Дополнительные сведения о WAS, см. в разделе [размещение в службе активации процессов Windows](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md).  
  
- [Windows Server AppFabric](https://go.microsoft.com/fwlink/?LinkId=196496) работает с [!INCLUDE[iisver](../../../../includes/iisver-md.md)] и Windows активации Service (WAS), обеспечивая среду для служб NET4 WCF и WF для размещения многофункциональных приложений. К ее преимуществам относятся управление жизненным циклом, перезапуск процессов, совместное размещение, быстрая защита от сбоев, обработка потерянных процессов, активация по запросу и наблюдение за работоспособностью. Подробные сведения см. в разделе [AppFabric Hosting Features](https://go.microsoft.com/fwlink/?LinkId=196494) и [основы размещения AppFabric](https://go.microsoft.com/fwlink/?LinkId=196495).  
  
## <a name="benefits-of-iis-hosting"></a>Преимущества размещения в IIS  
 Размещение служб WCF в IIS имеет несколько преимуществ:  
  
- Службы WCF, размещенные в IIS развертываются и управляются как любой другой тип приложения IIS, включая приложения ASP.NET и ASMX.  
  
- службы IIS предоставляют функции активации процессов, управления работоспособностью и перезапуска процессов, что позволяет повысить надежность приложений;  
  
- Как ASP.NET службы WCF, размещенные в ASP.NET использовать преимущества модели совместного размещения ASP.NET когда несколько приложений располагаются в одном рабочем процессе для плотности и масштабируемости сервера улучшенные.  
  
- Службы WCF, размещенные в IIS используют одну и ту же модель динамической компиляции как ASP.NET 2.0, которая упрощает разработку и развертывание размещенных служб.  
  
 При принятии решения о размещении служб WCF в IIS, важно помнить, что в версиях IIS 5.1 и [!INCLUDE[iis601](../../../../includes/iis601-md.md)] ограничены только подключения по протоколу HTTP. Дополнительные сведения о выборе среды размещения см. в разделе [размещение служб](../../../../docs/framework/wcf/hosting-services.md).  
  
## <a name="deploying-an-iis-hosted-wcf-service"></a>Развертывание службы WCF, размещаемой в IIS  
 Разработка и развертывание службы WCF, размещенных в IIS состоит из следующих задач:  
  
- Убедитесь, что службы IIS, ASP.NET, WCF и компонента активации WCF HTTP службы правильно установлен и зарегистрирован.  
  
- Создание нового приложения IIS или повторно использовать существующее приложение ASP.NET.  
  
- Создание SVC-файла для службы WCF.  
  
- Развертывание реализации службы в приложение IIS.  
  
- Настройка службы WCF.  
  
 Описание каждого из этих задач, см. в разделе [развертывание службы WCF, Internet Information Services-Hosted](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md).  
  
## <a name="wcf-services-and-aspnet"></a>Службы WCF и ASP.NET  
 Службы WCF могут быть размещенного либо side-by-side с ASP.NET или в режиме совместимости ASP.NET, в котором службы могут воспользоваться всеми преимуществами функций, предоставляемых платформой ASP.NET Web application. Описание этих возможностей, см. в разделе [службы WCF и ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md).  
  
## <a name="see-also"></a>См. также

- [Расширение размещения с использованием ServiceHostFactory](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md)
- [Развертывание службы WCF, размещенной в IIS](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)
- [Службы WCF и ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)
- [Рекомендации по размещению в службах IIS](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)
- [Настройка IIS 7.0 для Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/configuring-iis-for-wcf.md)
- [Функции размещения Windows Server App Fabric](https://go.microsoft.com/fwlink/?LinkId=201276)
