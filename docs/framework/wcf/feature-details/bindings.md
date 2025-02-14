---
title: Привязки Windows Communication Foundation
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], bindings
- Windows Communication Foundation [WCF], bindings
- bindings [WCF]
ms.assetid: 83639133-89f7-43f0-b4ef-8d9e57c08d25
ms.openlocfilehash: e69cd500c50e9d76824d0e438a1af86f3a722c52
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857692"
---
# <a name="windows-communication-foundation-bindings"></a>Привязки Windows Communication Foundation
Windows Communication Foundation (WCF) отделяет способ записи программное обеспечение для работы приложения от способа его взаимодействия с другим программным обеспечением. Привязки используются для указания транспорта, кодировки и данных протокола, требуемых для связи клиентов и служб. Привязки WCF используются для создания базового описания конечной точки, поэтому большая часть деталей привязки должны быть согласованы взаимодействующих сторон. Самым простым способом является использование клиентами службы той же привязки, которую использует конечная точка службы. Дополнительные сведения о том, как это сделать, см. в разделе [с помощью привязок для настройки служб и клиентов](~/docs/framework/wcf/using-bindings-to-configure-services-and-clients.md).  
  
 Привязка состоит из коллекции элементов привязки. Каждый элемент описывает некоторый аспект взаимодействия конечной точки с клиентами. Привязка должна содержать как минимум один элемент транспорта, как минимум один элемент кодирования сообщений (по умолчанию предоставляемый элементом транспорта привязки) и любое количество других элементов протоколов привязки. Процесс, создающий среду выполнения из этого описания, позволяет добавлять код из каждого элемента привязки в эту среду выполнения.  
  
 WCF предоставляет привязки, содержащие стандартные наборы элементов привязки. Можно использовать их с параметрами по умолчанию либо изменить значения этих параметров согласно потребностям пользователя. Эти предоставляемые системой привязки имеют свойства, обеспечивающие прямое управление элементами привязки и их параметрами. Также можно параллельно работать с несколькими версиями привязки, присвоив отдельное имя каждой из них. Дополнительные сведения см. в разделе [Configuring System-Provided привязки](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md).  
  
 Если потребуется коллекция элементов привязки, не предусмотренная в числе предоставляемых системой, можно создать пользовательскую привязку, содержащую требуемую коллекцию элементов привязки. Создавать эти пользовательские привязки очень просто, и для этого не требуется новый класс, однако в них отсутствуют свойства для управления элементами привязки или их параметрами. Обращаться к элементам привязки и изменять их параметры можно через содержащую их коллекцию. Дополнительные сведения см. в разделе [пользовательские привязки](../../../../docs/framework/wcf/extending/custom-bindings.md).  
  
## <a name="in-this-section"></a>В этом разделе  
 [Настройка привязок, предоставляемых системой](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 Описывает способы использования и изменения привязок, предоставляемых WCF для поддержки стандартных сценариев.  
  
 [Использование привязок для настройки служб и клиентов](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)  
 Описание способов определения привязок Windows Communication Foundation (WCF) для служб и клиентов принудительно в коде или декларативно с помощью конфигурации.  
  
 [Пользовательские привязки](../../../../docs/framework/wcf/extending/custom-bindings.md)  
 Описание элемента <xref:System.ServiceModel.Channels.CustomBinding> и сферы его применения.  
  
## <a name="reference"></a>Ссылка  
 <xref:System.ServiceModel.Channels.Binding>  
  
 <xref:System.ServiceModel.Channels.BindingElement>  
  
 <xref:System.ServiceModel.Channels.CustomBinding>  
  
## <a name="related-sections"></a>Связанные разделы  
 [Расширение привязок](../../../../docs/framework/wcf/extending/extending-bindings.md)
