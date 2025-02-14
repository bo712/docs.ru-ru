---
title: Рекомендации по частичному доверию
ms.date: 03/30/2017
ms.assetid: 0d052bc0-5b98-4c50-8bb5-270cc8a8b145
ms.openlocfilehash: 6c01824ef3d86600fd946e7f510b854b5138ec00
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64603886"
---
# <a name="partial-trust-best-practices"></a>Рекомендации по частичному доверию
В этом разделе описываются рекомендации при запуске Windows Communication Foundation (WCF) в среде с частичным доверием.  
  
## <a name="serialization"></a>Сериализация  
 При использовании <xref:System.Runtime.Serialization.DataContractSerializer> в частично доверенном приложении следуйте указанным ниже рекомендациям.  
  
- Все сериализуемые типы должны быть явно отмечены атрибутом `[DataContract]`. В среде с частичным доверием следующие методы не поддерживаются:  
  
- маркирование сериализуемых классов атрибутом <xref:System.SerializableAttribute>;  
  
- реализация интерфейса <xref:System.Runtime.Serialization.ISerializable>, чтобы класс мог управлять своим процессом сериализации.  
  
### <a name="using-datacontractserializer"></a>Использование DataContractSerializer  
  
- Все типы, отмеченные атрибутом `[DataContract]`, должны быть открытыми. Сериализация неоткрытых типов в среде с частичным доверием невозможна.  
  
- Все члены `[DataContract]` в сериализуемом типе `[DataContract]` должны быть открытыми. Сериализация типа с неоткрытым членом `[DataMember]` в среде с частичным доверием невозможна.  
  
- Методы, обрабатывающие события сериализации (например, `OnSerializing`, `OnSerialized`, `OnDeserializing` и `OnDeserialized`) должны быть объявлены как открытые. Однако поддерживаются явные и неявные реализации <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization%28System.Object%29>.  
  
- Типы `[DataContract]`, реализованные в сборках, отмеченных атрибутом <xref:System.Security.AllowPartiallyTrustedCallersAttribute>, не должны выполнять в конструкторе типа действия, связанные с безопасностью, так как <xref:System.Runtime.Serialization.DataContractSerializer> не вызывает конструктор вновь созданного объекта во время десериализации. В частности, для типов `[DataContract]` следует избегать использования указанных ниже общих методов обеспечения безопасности:  
  
- попытка ограничить доступ с частичным доверием, делая конструктор типа внутренним или закрытым;  
  
- ограничение доступа к типу путем добавления `[LinkDemand]` в конструктор типа;  
  
- предположение об успешном прохождении любых принудительно выполняемых конструктором проверок правильности в случае успешного создания объекта.  
  
### <a name="using-ixmlserializable"></a>Использование IXmlSerializable  
 Ниже приведены рекомендации для типов, которые реализуют интерфейс <xref:System.Xml.Serialization.IXmlSerializable> и сериализуются с помощью <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
- Реализации статического метода <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> должны быть `public`.  
  
- Методы экземпляров, которые реализуют интерфейс <xref:System.Xml.Serialization.IXmlSerializable>, должны быть `public`.  
  
## <a name="using-wcf-from-fully-trusted-platform-code-that-allows-calls-from-partially-trusted-callers"></a>Использование WCF из кода полностью доверенной платформы, который разрешает вызовы от частично доверенных вызывающих  
 Модель безопасности частичного доверия WCF предполагает, что любой вызывающий объект WCF открытого метода или свойства выполняется в контексте разграничения доступа кода ведущего приложения. WCF также предполагается, что только один контекст безопасности приложения для каждого <xref:System.AppDomain>, и что этот контекст будет установлен на <xref:System.AppDomain> время создания доверенным узлом (например, путем вызова <xref:System.AppDomain.CreateDomain%2A> или диспетчером приложения ASP.NET).  
  
 Эта модель безопасности применяется для написанных пользователем приложений, которые не могут утвердить дополнительные разрешения на управление доступом для кода. Примером такого приложения является пользовательский код, выполняющийся в приложении ASP.NET со средним уровнем доверия. Однако кода полностью доверенной платформы (например, сторонние сборки, устанавливается в глобальный кэш сборок и принимающей вызовы от частично доверенного кода) должны принимать предосторожности при вызове в WCF от имени частично доверенного приложения для Избегайте уязвимости системы безопасности на уровне приложения.  
  
 Код с полным доверием следует избегать изменения набора разрешений CAS для текущего потока (путем вызова <xref:System.Security.PermissionSet.Assert%2A>, <xref:System.Security.PermissionSet.PermitOnly%2A>, или <xref:System.Security.PermissionSet.Deny%2A>) перед вызовом API-интерфейсы WCF от имени частично доверенного кода. Утверждение, отклонение или создание контекста разрешений потока, который не зависит от контекста безопасности уровня приложения, может привести к непредвиденному поведению. В зависимости от приложения такое поведение может стать причиной появления уязвимых с точки зрения безопасности мест на уровне приложения.  
  
 Код, который вызывает WCF, используя контекст разрешений потока должны быть готовы обрабатывать следующие ситуации, которые могут возникнуть.  
  
- Контекст безопасности потока может не поддерживаться в ходе выполнения операции, что приводит к потенциальным исключениям, связанным с безопасностью.  
  
- Внутренний код WCF, а также любых пользовательских обратных вызовов могут выполняться в контексте безопасности, чем та, в котором был первоначально инициирован вызов. К таким контекстам относятся следующие.  
  
    - Контекст разрешений приложения.  
  
    - Любой контекст разрешений потока, ранее созданным другими пользовательскими потоками, используемыми для вызова WCF в течение времени существования выполняющейся в данный момент <xref:System.AppDomain>.  
  
 WCF гарантирует, что частично доверенный код не удается получить разрешения полного доверия, если такие разрешения утверждены полностью доверенным компонентом до обращения общедоступных интерфейсов API WCF. Однако она не гарантирует, что результаты утверждения полного доверия изолируются для конкретного потока, операции или действия пользователя.  
  
 Рекомендуется избегать создания контекста разрешений потока посредством вызова <xref:System.Security.PermissionSet.Assert%2A>, <xref:System.Security.PermissionSet.PermitOnly%2A> или <xref:System.Security.PermissionSet.Deny%2A>. Вместо этого предоставьте привилегию самому приложению или отклоните ее, чтобы вызывать <xref:System.Security.PermissionSet.Assert%2A>, <xref:System.Security.PermissionSet.Deny%2A> или <xref:System.Security.PermissionSet.PermitOnly%2A> не требовалось.  
  
## <a name="see-also"></a>См. также

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.Serialization.IXmlSerializable>
