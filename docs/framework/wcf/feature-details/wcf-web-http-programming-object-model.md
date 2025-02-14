---
title: Объектная модель программирования WCF Web HTTP
ms.date: 03/30/2017
ms.assetid: ed96b5fc-ca2c-4b0d-bdba-d06b77c3cb2a
ms.openlocfilehash: f8bda6292506b64057dee006fa59b7723fa406b2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648411"
---
# <a name="wcf-web-http-programming-object-model"></a>Объектная модель программирования WCF Web HTTP
Модель программирования HTTP WCF WEB позволяет разработчикам предоставлять веб-службы Windows Communication Foundation (WCF) службам через базовые HTTP-запросы, не требуя использования SOAP. WCF модель программирования WEB HTTP построена на основе существующей модели расширяемости WCF. Она определяет следующие классы.  
  
 **Модель программирования:**  
  
- <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>  
  
- <xref:System.ServiceModel.Web.WebGetAttribute>  
  
- <xref:System.ServiceModel.Web.WebInvokeAttribute>  
  
- <xref:System.ServiceModel.Web.WebServiceHost>  
  
 **Инфраструктура каналов и диспетчера:**  
  
- <xref:System.ServiceModel.WebHttpBinding>  
  
- <xref:System.ServiceModel.Description.WebHttpBehavior>  
  
 **Служебные классы и точек расширения:**  
  
- <xref:System.UriTemplate>  
  
- <xref:System.UriTemplateTable>  
  
- <xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
- <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>  
  
## <a name="aspnetcacheprofileattribute"></a>AspNetCacheProfileAttribute  
 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> при применении к операции службы указывает профиль кэша вывода ASP.NET в файле конфигурации, который следует использовать в кэшировании ответов для операции в кэше вывода ASP .NET. Это свойство принимает только один параметр, имя профиля кэша, указывающее настройки кэша в файле конфигурации.  
  
## <a name="webgetattribute"></a>WebGetAttribute  
 Атрибут <xref:System.ServiceModel.Web.WebGetAttribute> служит для пометки операций служб, отвечающих на HTTP-запросы GET. Это пассивное поведение операции (методы <xref:System.ServiceModel.Description.IOperationBehavior> не выполняют никаких действий), добавляющее метаданные в описание операции. Применение атрибута <xref:System.ServiceModel.Web.WebGetAttribute> не имеет последствий, если в коллекцию поведения службы не добавлено поведение, выполняющее поиск метаданных в описании операции (например, <xref:System.ServiceModel.Description.WebHttpBehavior>). Атрибут <xref:System.ServiceModel.Web.WebGetAttribute> принимает необязательные параметры, показанные в следующей таблице.  
  
|Параметр|Описание|  
|---------------|-----------------|  
|`BodyStyle`|Определяет, нужно ли заключать в оболочку запросы и ответы операции службы, к которой относится атрибут.|  
|`RequestFormat`|Определяет, каким образом форматируются сообщения запросов.|  
|`ResponseFormat`|Определяет, каким образом форматируются сообщения ответов.|  
|`UriTemplate`|Задает шаблон универсального кода ресурса (URI), который определяет, какие запросы HTTP сопоставляются с операцией службы, к которой относится атрибут.|  
  
## <a name="webhttpbinding"></a>WebHttpBinding  
 Класс <xref:System.ServiceModel.WebHttpBinding> включает поддержку форматов XML, JSON и необработанных двоичных данных, используя для этого элемент <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>. Он состоит из элементов <xref:System.ServiceModel.Channels.HttpsTransportBindingElement> и <xref:System.ServiceModel.Channels.HttpTransportBindingElement>, а также объекта <xref:System.ServiceModel.WebHttpSecurity>. Привязка <xref:System.ServiceModel.WebHttpBinding> предназначена для использования с поведением <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
## <a name="webinvokeattribute"></a>WebInvokeAttribute  
 Атрибут <xref:System.ServiceModel.Web.WebInvokeAttribute> похож на атрибут <xref:System.ServiceModel.Web.WebGetAttribute>, но он служит для пометки операций служб, которые отвечают на HTTP-запросы, отличные от GET. Это пассивное поведение операции (методы <xref:System.ServiceModel.Description.IOperationBehavior> не выполняют никаких действий), добавляющее метаданные в описание операции. Применение атрибута <xref:System.ServiceModel.Web.WebInvokeAttribute> не имеет последствий, если в коллекцию поведения службы не добавлено поведение, выполняющее поиск метаданных в описании операции (например, <xref:System.ServiceModel.Description.WebHttpBehavior>).  
  
 Атрибут <xref:System.ServiceModel.Web.WebInvokeAttribute> принимает необязательные параметры, показанные в следующей таблице.  
  
|Параметр|Описание|  
|---------------|-----------------|  
|`BodyStyle`|Определяет, нужно ли заключать в оболочку запросы и ответы операции службы, к которой относится атрибут.|  
|`Method`|Задает метод HTTP, которому сопоставлена операция службы.|  
|`RequestFormat`|Определяет, каким образом форматируются сообщения запросов.|  
|`ResponseFormat`|Определяет, каким образом форматируются сообщения ответов.|  
|`UriTemplate`|Задает шаблон универсального кода ресурса (URI), который определяет, какие запросы GET сопоставляются с операцией службы, к которой относится атрибут.|  
  
## <a name="uritemplate"></a>UriTemplate  
 Класс <xref:System.UriTemplate> позволяет определить набор кодов URI с одинаковой структурой. Шаблоны состоят из двух частей: путь и запрос. Путь состоит из серии сегментов, разделенных косой чертой (/). Каждый сегмент имеет литеральное значение, значение переменной (написанного в фигурных скобках [{}], ограничен в соответствии с содержимым ровно один сегмент) или подстановочный знак (звездочка [\*], который соответствует «оставшуюся часть пути»), который должен отображаться в в конец пути. Выражение запроса можно полностью опустить. Если оно указано, оно задает неупорядоченную серию пар «имя-значение». Элементами выражения запроса могут быть либо литеральные пары (? x = 2) либо пары переменных (? x = {*значение*}). Непарные значения не допускаются. <xref:System.UriTemplate> используется внутренне классом модели программирования HTTP WCF WEB для сопоставления отдельных URI или их групп с операциями службы.  
  
## <a name="uritemplatetable"></a>UriTemplateTable  
 Класс <xref:System.UriTemplateTable> представляет собой ассоциативный набор объектов <xref:System.UriTemplate>, привязанных к объекту, выбранному разработчиком. Он позволяет сопоставлять потенциальные универсальные идентификаторы ресурсов (URI) с содержащимися в наборе шаблонами и извлекать данные, связанные с шаблонами, для которых обнаружено соответствие. <xref:System.UriTemplateTable> используется внутренне классом модели программирования HTTP WCF WEB для сопоставления отдельных URI или их групп с операциями службы.  
  
## <a name="webservicehost"></a>WebServiceHost  
 <xref:System.ServiceModel.Web.WebServiceHost> расширяет <xref:System.ServiceModel.ServiceHost>, чтобы было проще размещать веб-службы, не использующие протокол SOAP. Если объект <xref:System.ServiceModel.Web.WebServiceHost> не обнаруживает конечные точки в описании службы, он автоматически создает конечную точку по умолчанию по базовому адресу службы. При создании конечной точки HTTP по умолчанию <xref:System.ServiceModel.Web.WebServiceHost> также отключает страницу справки HTTP и функцию GET языка WSDL, чтобы конечная точка метаданных не мешала конечной точке HTTP по умолчанию. <xref:System.ServiceModel.Web.WebServiceHost> также гарантирует, что все конечные точки, использующие <xref:System.ServiceModel.WebHttpBinding>, имеют требуемое вложение <xref:System.ServiceModel.Description.WebHttpBehavior>. Наконец <xref:System.ServiceModel.Web.WebServiceHost> автоматически настраивает привязку конечной точки для работы со связанными параметрами безопасности IIS при использовании в защищенном виртуальном каталоге.  
  
## <a name="webservicehostfactory"></a>WebServiceHostFactory  
 Класс <xref:System.ServiceModel.Activation.WebServiceHostFactory> служит для динамического создания объектов <xref:System.ServiceModel.Web.WebServiceHost>, когда служба размещается в службах IIS или в службе активации Windows (WAS). В отличие от служб с резидентным размещением, когда экземпляры <xref:System.ServiceModel.Web.WebServiceHost> создаются размещающим приложением, службы, размещенные в IIS или WAS, используют для создания объектов <xref:System.ServiceModel.Web.WebServiceHost> этот класс. Метод <xref:System.ServiceModel.Activation.WebServiceHostFactory.CreateServiceHost%28System.Type%2CSystem.Uri%5B%5D%29> вызывается при получении входящего запроса к службе.  
  
## <a name="webhttpbehavior"></a>WebHttpBehavior  
 Класс <xref:System.ServiceModel.Description.WebHttpBehavior> предоставляет необходимые модули форматирования, селекторы операций и другие объекты, необходимые для поддержки веб-служб на уровне модели службы. Все это реализуется в форме поведения конечной точки (используется совместно с <xref:System.ServiceModel.WebHttpBinding>) и позволяет задавать модули форматирования и селекторы для каждой конкретной точки, в результате чего одна реализация службы может быть представлена конечными точками SOAP и POX одновременно.  
  
### <a name="extending-webhttpbehavior"></a>Расширение WebHttpBehavior  
 Класс <xref:System.ServiceModel.Description.WebHttpBehavior> можно расширить с помощью нескольких виртуальных методов: <xref:System.ServiceModel.Description.WebHttpBehavior.GetOperationSelector%28System.ServiceModel.Description.ServiceEndpoint%29>, <xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>, <xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>, <xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29> и <xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29>. Разработчики могут создать производный класс для <xref:System.ServiceModel.Description.WebHttpBehavior> и переопределить эти методы, чтобы изменить поведение по умолчанию.  
  
 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> - пример расширения <xref:System.ServiceModel.Description.WebHttpBehavior>. <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> позволяет конечным точкам Windows Communication Foundation (WCF) получать HTTP-запросы от клиента ASP.NET AJAX на основе веб-обозревателя. [Служба AJAX с помощью HTTP POST](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md) является примером использования этой точки расширяемости.  
  
> [!WARNING]
>  При использовании <xref:System.ServiceModel.Description.WebScriptEnablingBehavior><xref:System.UriTemplate> не поддерживаются внутри атрибутов <xref:System.ServiceModel.Web.WebGetAttribute> или <xref:System.ServiceModel.Web.WebInvokeAttribute>.  
  
## <a name="webhttpdispatchoperationselector"></a>WebHttpDispatchOperationSelector  
 Класс <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector> использует классы <xref:System.UriTemplate> и <xref:System.UriTemplateTable> для распределения вызовов по операциям службы.  
  
## <a name="compatibility"></a>Совместимость  
 Модель программирования HTTP WCF WEB не использует сообщения SOAP и поэтому не поддерживает WS-* протоколы. Тем не менее один контракт можно представить двумя различными конечными точками, одна из которых будет использовать протокол SOAP, а другая не будет. См. практическое руководство по [ Предоставление контрактов SOAP и веб-клиентам](../../../../docs/framework/wcf/feature-details/how-to-expose-a-contract-to-soap-and-web-clients.md) пример.  
  
## <a name="security"></a>Безопасность  
 Поскольку модель программирования HTTP WCF WEB не поддерживает WS-* протоколы, единственным способом защиты веб-службы, построенных на основе модели программирования WCF WEB HTTP является предоставление доступа к ней с помощью протокола SSL. Дополнительные сведения о настройке SSL с [!INCLUDE[iisver](../../../../includes/iisver-md.md)] см. в разделе [реализация SSL-сертификата в IIS](https://go.microsoft.com/fwlink/?LinkId=131613)  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>
- [Общие сведения о модели веб-программирования HTTP WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)
