---
title: Экспорт и импорт метаданных
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WCF], exporting and importing
ms.assetid: 614a75bb-e0b0-4c95-b6d8-02cb5e5ddb38
ms.openlocfilehash: 39b964584cde42e6569da35f8653042f6d7432cb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61856470"
---
# <a name="exporting-and-importing-metadata"></a>Экспорт и импорт метаданных
В Windows Communication Foundation (WCF), экспорт метаданных — это процесс описания конечных точек службы и проецирования их в параллельное, стандартизованное представление, клиенты могут использовать, чтобы понять, как использовать службу. Импорт метаданных службы - это процесс создания экземпляров <xref:System.ServiceModel.Description.ServiceEndpoint> или частей из метаданных службы.  
  
## <a name="exporting-metadata"></a>Экспорт метаданных  
 Для экспорта метаданных из экземпляров <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType> используется реализация абстрактного класса <xref:System.ServiceModel.Description.MetadataExporter>. <xref:System.ServiceModel.Description.WsdlExporter> Тип представляет собой реализацию <xref:System.ServiceModel.Description.MetadataExporter> абстрактный класс, в состав WCF.  
  
 Тип <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=nameWithType> создает метаданные языка описания веб-служб (WSDL) с присоединенными выражениями политики в экземпляре <xref:System.ServiceModel.Description.MetadataSet>. Экземпляр <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=nameWithType> можно использовать для итерационного экспорта метаданных для объектов <xref:System.ServiceModel.Description.ContractDescription> и объектов <xref:System.ServiceModel.Description.ServiceEndpoint>. Можно также экспортировать коллекцию объектов <xref:System.ServiceModel.Description.ServiceEndpoint> и связать их с определенным именем службы.  
  
> [!NOTE]
>  `WsdlExporter` может использоваться только для экспорта метаданных из экземпляров `ContractDescription`, в которых содержатся сведения о типе среды CLR, например, экземпляр `ContractDescription`, созданный с помощью метода `ContractDescription.GetContract` или созданный как часть `ServiceDescription` для экземпляра `ServiceHost`. Нельзя использовать `WsdlExporter` для экспорта метаданных из экземпляров `ContractDescription`, импортированных из метаданных службы или созданных без сведений о типе.  
  
## <a name="importing-metadata"></a>Импорт метаданных  
  
### <a name="importing-wsdl-documents"></a>Импорт документов WSDL  
 Чтобы импортировать метаданные службы в WCF, используется реализация <xref:System.ServiceModel.Description.MetadataImporter> абстрактного класса. <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> Тип представляет собой реализацию <xref:System.ServiceModel.Description.MetadataImporter> абстрактный класс, в состав WCF. Тип <xref:System.ServiceModel.Description.WsdlImporter> импортирует метаданные языка WSDL с прикрепленными политиками, объединенными в объекте <xref:System.ServiceModel.Description.MetadataSet>.  
  
 Тип <xref:System.ServiceModel.Description.WsdlImporter> позволяет контролировать способ импорта метаданных. Можно импортировать все конечные точки, все привязки или все контракты. Можно импортировать все конечные точки, связанные с определенной службой, привязкой или типом порта WSDL. Можно также импортировать конечную точку для определенного порта WSDL, привязку для определенной привязки WSDL или контракт для определенного типа порта WSDL.  
  
 <xref:System.ServiceModel.Description.WsdlImporter> также предоставляет свойство <xref:System.ServiceModel.Description.MetadataImporter.KnownContracts%2A>, позволяющее задать набор контрактов, которые не требуется импортировать. <xref:System.ServiceModel.Description.WsdlImporter> использует контракты из свойства <xref:System.ServiceModel.Description.MetadataImporter.KnownContracts%2A>, вместо того, чтобы импортировать контракты с тем же полным именем из метаданных.  
  
### <a name="importing-policies"></a>Импорт политик  
 Тип <xref:System.ServiceModel.Description.WsdlImporter> собирает выражения политики, присоединенные к субъектам политики сообщения, операции и конечной точки, а затем использует реализации <xref:System.ServiceModel.Description.IPolicyImportExtension> в коллекции <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> для импорта выражений политики.  
  
 Логика импорта политики автоматически обрабатывает ссылки политики на выражения политики в этом же документе WSDL и указывается атрибутом `wsu:Id` или `xml:id`. Логика импорта политики защищает приложения от циклических ссылок политики, ограничивая размер выражения политики 4096 узлами, где узлом является один из следующих элементов: `wsp:Policy`, `wsp:All`, `wsp:ExactlyOne`, `wsp:policyReference`.  
  
 Логика импорта политики также автоматически нормализует выражения политики. Вложенные выражения политики и атрибут `wsp:Optional` не нормализуются. Объем обработки для нормализации ограничен 4096 шагами, где каждый шаг дает утверждение политики или дочерний элемент элемента `wsp:ExactlyOne`.  
  
 Тип <xref:System.ServiceModel.Description.WsdlImporter> пробует до 32 комбинацией альтернативных политик, присоединенных к различным субъектам политики WSDL. Если ни одну из этих комбинацией не удается импортировать без ошибок, первая комбинация используется для создания частичной пользовательской привязки.  
  
## <a name="error-handling"></a>Обработка ошибок  
 Типы <xref:System.ServiceModel.Description.MetadataExporter> и <xref:System.ServiceModel.Description.MetadataImporter> предоставляют свойство `Errors`, которое может содержать коллекцию сообщений об ошибках и предупреждениях, возникших во время экспорта и импорта соответственно, и которую можно использовать при реализации средств.  
  
 Тип <xref:System.ServiceModel.Description.WsdlImporter> обычно создает исключение для исключения, перехваченного в процессе импорта, и добавляет соответствующую ошибку в свое свойство `Errors`. Однако методы <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>, <xref:System.ServiceModel.Description.WsdlImporter.ImportAllBindings%2A>, <xref:System.ServiceModel.Description.WsdlImporter.ImportAllEndpoints%2A> и <xref:System.ServiceModel.Description.WsdlImporter.ImportEndpoints%2A> не создают такие исключения, поэтому необходимо проверять свойство `Errors`, чтобы определить, не было ли каких-либо проблем при вызове этих методов.  
  
 Тип <xref:System.ServiceModel.Description.WsdlExporter> заново создает все исключения, перехваченные во время процесса экспорта. Эти исключения не записываются в виде ошибок в свойство `Errors`. После того, как <xref:System.ServiceModel.Description.WsdlExporter> создал исключение, он находится в состоянии ошибки и не может использоваться повторно. <xref:System.ServiceModel.Description.WsdlExporter> не добавляет предупреждения в свое свойство `Errors`, если экспорт операции невозможен из-за использования подстановочных действий или если обнаружены одинаковые имена привязок.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Практическое руководство. Импорт метаданных в конечные точки службы](../../../../docs/framework/wcf/feature-details/how-to-import-metadata-into-service-endpoints.md)  
 Описание порядка импорта загруженных метаданных в объекты описания.  
  
 [Практическое руководство. Экспорт метаданных из конечных точек службы](../../../../docs/framework/wcf/feature-details/how-to-export-metadata-from-service-endpoints.md)  
 Описание порядка экспорта объектов описания в метаданные.  
  
 [ServiceDescription и справочная информация о WSDL](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md)  
 Описание сопоставления объектов описания и языка WSDL.  
  
 [Практическое руководство. Использование Svcutil.exe для экспорта метаданных из скомпилированного кода службы](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)  
 Описание использования средства Svcutil.exe для экспорта метаданных служб, контрактов и типов данных в скомпилированных сборках.  
  
 [Справочник по схеме контрактов данных](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)  
 Описание подмножества схемы XML (XSD), используемого <xref:System.Runtime.Serialization.DataContractSerializer> для описания типов среды CLR, применяемых для сериализации XML.  
  
## <a name="reference"></a>Ссылка  
 <xref:System.ServiceModel.Description.WsdlExporter>  
  
 <xref:System.ServiceModel.Description.WsdlImporter>  
  
## <a name="see-also"></a>См. также

- [Экспорт пользовательских метаданных для расширения WCF](../../../../docs/framework/wcf/extending/exporting-custom-metadata-for-a-wcf-extension.md)
- [Импорт пользовательских метаданных для расширения WCF](../../../../docs/framework/wcf/extending/importing-custom-metadata-for-a-wcf-extension.md)
