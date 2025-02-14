---
title: Идентификация и проверка подлинности службы
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- authentication [WCF], specifying the identity of a service
ms.assetid: a4c8f52c-5b30-45c4-a545-63244aba82be
ms.openlocfilehash: 834829d8eee95a8a62363a05b4af9430c435753b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64586228"
---
# <a name="service-identity-and-authentication"></a>Идентификация и проверка подлинности службы
Это служба *удостоверение конечной точки* представляет собой значение, созданный из службы языка описания служб (WSDL). Это значение распространяется по всем клиентам и используется для проверки подлинности службы. После того как клиент инициирует связь с конечной точкой и служба пройдет проверку подлинности на клиенте, клиент сравнивает значение удостоверения конечной точки с действительным значением, возвращенным процессом проверки подлинности конечной точки. Если значения совпадают, значит клиент связался с ожидаемой конечной точкой службы. Это работает как защиту от *фишинг* , предотвращая клиента осуществляется перенаправление в конечную точку, размещенную на вредоносной службы.  
  
 Образец приложения, демонстрирующий настройку удостоверения, см. в разделе [образец идентификации службы](../../../../docs/framework/wcf/samples/service-identity-sample.md). Дополнительные сведения о конечных точках и адреса конечных точек см. в разделе [адреса](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md).  
  
> [!NOTE]
>  При использовании NT LanMan (NTLM) для проверки подлинности удостоверение службы не проверяется, так как в NTLM проверка подлинности сервера клиентом не поддерживается. NTLM используется, когда компьютеры входят в рабочую группу Windows или при работе в старых версиях Windows, не поддерживающих проверку подлинности Kerberos.  
  
 Когда клиент инициирует защищенный канал для отправки сообщения в службу над ней, инфраструктуре Windows Communication Foundation (WCF) проверяет подлинность службы и отправляет сообщение, только если удостоверение службы соответствует удостоверению, указанному в конечной точке адрес, который клиент использует.  
  
 Обработка удостоверений включает следующие этапы.  
  
- Во время проектирования разработчик клиента определяет удостоверение службы на основе метаданных конечной точки (передаваемых через WSDL).  
  
- Во время выполнения клиентское приложение проверяет утверждения учетных данных безопасности службы, прежде чем пересылать ей какие-либо сообщения.  
  
 Обработка идентификаций на клиенте аналогична проверке подлинности клиента в службе. Защищенная служба не выполняет код до тех пор, пока не будет проведена проверка подлинности учетных данных клиента. Аналогично, клиент не отправляет сообщения службе до тех пор, пока не будет проведена проверка подлинности учетных данных службы, исходя из заранее известной информации на основе метаданных службы.  
  
 Свойство <xref:System.ServiceModel.EndpointAddress.Identity%2A> класса <xref:System.ServiceModel.EndpointAddress> представляет удостоверение службы, вызываемой клиентом. Служба публикует свойство <xref:System.ServiceModel.EndpointAddress.Identity%2A> в своих метаданных. Когда разработчик клиента запускает [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) для конечной точки службы, созданное удостоверение содержит значение службы <xref:System.ServiceModel.EndpointAddress.Identity%2A> свойство. Инфраструктура WCF (если настроено с безопасностью) проверяет, что служба обрабатывает удостоверение, указанное.  
  
> [!IMPORTANT]
>  Метаданные содержат ожидаемое удостоверение службы, поэтому рекомендуется передавать метаданные службы через защищенные средства, например путем создания конечной точки HTTPS для службы. Дополнительные сведения см. в разделе [Как Защита конечных точек метаданных](../../../../docs/framework/wcf/feature-details/how-to-secure-metadata-endpoints.md).  
  
## <a name="identity-types"></a>Типы удостоверений  
 Служба может предоставлять шесть типов удостоверений. Каждый тип удостоверения соответствует элементу, который может содержаться в элементе `<identity>` в конфигурации. Используемый тип зависит от сценария и требований службы к безопасности. Типы удостоверений описаны в приведенной ниже таблице.  
  
|Тип удостоверения|Описание|Типичный сценарий|  
|-------------------|-----------------|----------------------|  
|Служба доменных имен (DNS)|Этот элемент следует использовать с сертификатами X.509 или учетными записями Windows. Он сравнивает DNS-имя, указанное в учетных данных, со значением, указанным в этом элементе.|Проверка DNS позволяет использовать сертификаты с DNS-именами или именами субъектов. Если сертификат повторно выдан с тем же DNS-именем или именем субъекта, тогда проверка удостоверения по-прежнему действительна. При повторной выдаче сертификата он получает новый ключ RSA, однако при этом сохраняется то же DNS-имя или имя субъекта. Это означает, что клиентам не нужно обновлять в удостоверении информацию о службе.|  
|Сертификат. Используется по умолчанию, если параметру `ClientCredentialType` присвоено значение "Certificate".|Этот элемент задает значение сертификата X.509 в кодировке Base64 для сравнения с клиентом.<br /><br /> Этот элемент также следует применять при использовании [!INCLUDE[infocard](../../../../includes/infocard-md.md)] в качестве учетных данных для проверки подлинности службы.|Этот элемент ограничивает проверку подлинности одним сертификатом на основе значения отпечатка. Это обеспечивает более строгую проверку подлинности, поскольку значения отпечатков уникальны. Эта проблема исходит за одним исключением: Если сертификат повторно выдан с тем же именем субъекта, также имеет новый отпечаток. Следовательно, клиенты могут проверить службу только в том случае, когда известен новый отпечаток. Дополнительные сведения о поиске отпечатка сертификата, см. в разделе [как: Извлечение отпечатка сертификата](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md).|  
|Ссылка на сертификат|Идентичен описанному выше типу "Сертификат". Однако этот элемент позволяет задавать имя сертификата и сохранять расположение, из которого нужно получать сертификат.|Аналогичен описанному выше сценарию для типа "Сертификат".<br /><br /> Преимущество в том, что есть возможность изменить расположение хранилища сертификатов.|  
|RSA|Этот элемент задает значение ключа RSA для сравнения с клиентом. Он аналогичен типу "Сертификат", однако вместо использования отпечатка сертификата используется ключ RSA сертификата.|Проверка RSA позволяет ограничить проверку подлинности одним сертификатом с использованием его ключа RSA. Это позволяет выполнять более строгую проверку подлинности определенного ключа RSA, однако если значение ключа RSA будет изменено, служба больше не будет работать с существующими клиентами.|  
|Имя участника-пользователя. Используется по умолчанию, если параметру `ClientCredentialType` присвоено значение "Windows" и процесс службы выполняется не под одной из системных учетных записей.|Этот элемент задает имя участника-пользователя, под которым выполняется служба. См. в разделе протокол Kerberos и удостоверение [переопределение идентификатора службы для проверки подлинности](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md).|Это обеспечивает выполнение службы под определенной учетной записью пользователя Windows. В качестве учетной записи может использоваться либо учетная запись текущего пользователя, либо служба, запущенная под учетной записью определенного пользователя.<br /><br /> Для этого параметра используется безопасность Windows Kerberos, если служба выполняется под учетной записью домена в среде Active Directory.|  
|Имя участника-службы. Используется по умолчанию, если параметру `ClientCredentialType` присвоено значение "Windows" и процесс службы выполняется под одной из системных учетных записей: LocalService, LocalSystem или NetworkService.|Этот элемент задает имя участника-службы, связанное с учетной записью службы. См. в разделе протокол Kerberos и удостоверение [переопределение идентификатора службы для проверки подлинности](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md).|Это обеспечивает идентификацию службы с помощью имени участника-службы и определенной учетной записи Windows, связанной с этим именем.<br /><br /> Для связывания учетной записи компьютера для учетной записи пользователя службы можно воспользоваться средством Setspn.exe.<br /><br /> Этот параметр использует безопасность Windows Kerberos, если служба выполняется под одной из системных учетных записей или под учетной записью домена, с которой связано имя участника-службы, при условии что компьютер входит в домен в среде Active Directory.|  
  
## <a name="specifying-identity-at-the-service"></a>Задание удостоверения в службе  
 Как правило, нет необходимости задавать удостоверение в службе, поскольку выбор типа учетных данных клиента определяет тип удостоверения, предоставляемого в метаданных службы. Дополнительные сведения о том, как переопределить или указать удостоверение службы, см. в разделе [переопределение идентификатора службы для проверки подлинности](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md).  
  
## <a name="using-the-identity-element-in-configuration"></a>С помощью \<удостоверений > элемент в конфигурации  
 Если изменить тип учетных данных клиента в привязке, ранее показанной сертификату `Certificate,` созданный WSDL будет содержать сериализованный сертификат X.509 в кодировке Base64, соответствующий значению удостоверения, как показано в следующем примере кода. Используется по умолчанию для всех типов учетных данных клиентов, за исключением Windows.  

 Можно изменить значение по умолчанию удостоверения службы или измените тип удостоверения с помощью `<identity>` в конфигурации или задав удостоверение в коде. В следующем коде конфигурации задается идентификатор DNS со значением `contoso.com`.  

## <a name="setting-identity-programmatically"></a>Задание удостоверения программным способом  
 Службе не требуется явно задавать удостоверение, поскольку WCF определяет его автоматически. Тем не менее WCF позволяет указать удостоверение для конечной точки, если это необходимо. В приведенном ниже примере кода добавляется новая конечная точка службы с определенным идентификатором DNS.  
  
 [!code-csharp[C_Identity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_identity/cs/source.cs#5)]
 [!code-vb[C_Identity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_identity/vb/source.vb#5)]  
  
## <a name="specifying-identity-at-the-client"></a>Назначение удостоверения в клиенте  
 Во время разработки разработчик клиента обычно использует [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) для создания конфигурации клиента. Созданный файл конфигурации (предназначенный для использования клиентом) содержит удостоверение сервера. Например, приведенный ниже код создан на основе службы, в которой задан идентификатор DNS, как показано в предыдущем примере. Обратите внимание, что значение удостоверения конечной точки клиента совпадает с соответствующим значением службы. В этом случае, когда клиент получает учетные данные Windows (Kerberos) для службы, он ожидает значение `contoso.com`.  

 Если вместо Windows сертификат в службе задан в качестве клиентского типа учетных данных, тогда ожидается, что свойство DNS будет иметь значение `contoso.com`. (Если же свойство DNS имеет значение `null`, имя субъекта сертификата должно иметь значение `contoso.com`.)  
  
#### <a name="using-a-specific-value-for-identity"></a>Использование определенного значения для удостоверения  
 В приведенном ниже файле конфигурации клиента показано, каким образом в качестве удостоверения службы может ожидаться использование определенного значения. В приведенном ниже примере клиент может связываться с двумя конечными точками. Первая конечная точка определяется отпечатком сертификата, а вторая – ключом RSA сертификата. Другими словами, сертификатом, содержащим только пару открытого и закрытого ключей, который не был издан доверенным центром.  

## <a name="identity-checking-at-run-time"></a>Проверка удостоверения во время выполнения  
 Во время проектирования разработчик клиента определяет удостоверение сервера с помощью его метаданных. Во время выполнения проверка удостоверения выполняется перед вызовом конечных точек в службе.  
  
 Значение удостоверения привязано к типу проверки подлинности, указанному в метаданных; другими словами, к типу учетных данных, используемому в службе.  
  
 Если в канале настроена проверка подлинности с использованием протокола SSL на уровне сообщений или транспортном уровне с сертификатами X.509, действительны следующие значения удостоверения.  
  
- DNS. WCF гарантирует, что сертификат, предоставленный во время подтверждения SSL содержит DNS или `CommonName` атрибут (CN), равным значению, заданному в идентификаторе DNS на клиенте. Обратите внимание, что эти проверки выполняются в дополнение к определению действительности сертификата сервера. По умолчанию WCF проверяет, что сертификат сервера выдан доверенным корневым центром.  
  
- Сертификат. Во время подтверждения SSL WCF гарантирует, что Удаленная конечная точка предоставляет значение именно тот сертификат, заданному в идентификаторе.  
  
- Ссылка на сертификат. Аналогичен значению "Сертификат".  
  
- RSA. Во время подтверждения SSL WCF гарантирует, что Удаленная конечная точка предоставляет точный ключ RSA, заданному в идентификаторе.  
  
 Если служба выполняет проверку подлинности с использованием протокола SSL на уровне сообщений или транспортном уровне с учетными данными Windows и согласует учетные данные, следующие значения удостоверения являются действительными.  
  
- DNS. Согласование проходит имя участника-службы, так что DNS-имя может быть проверено. Имя участника-службы указывается в формате `host/<dns name>`.  
  
- Имя участника-службы. Возвращается явное имя участника-службы, например `host/myservice`.  
  
- Имя участника-пользователя. Имя участника-пользователя учетной записи службы. Имя участника-пользователя указывается в формате `username` @ `domain`. Например, при выполнении службы под учетной записью пользователя может использоваться такое имя участника-пользователя, как `username@contoso.com`.  
  
 Назначать удостоверение программным путем (с использованием свойства <xref:System.ServiceModel.EndpointAddress.Identity%2A>) не обязательно. Если удостоверение не задано и используется тип учетных данных клиента Windows, по умолчанию имени участника-службы назначается значение, соответствующее имени узла в адресе конечной точки службы с префиксом "host/". Если удостоверение задано и в качестве типа учетных данных клиента применяется сертификат, по умолчанию используется значение `Certificate`. Это относится к безопасности как на уровне сообщений, так и на транспортном уровне.  
  
## <a name="identity-and-custom-bindings"></a>Удостоверение и пользовательские привязки  
 Поскольку удостоверение службы зависит от используемого типа привязки, при создании пользовательской привязки убедитесь, что передается требуемое удостоверение. Например, в приведенном ниже примере кода передаваемое удостоверение несовместимо с типом безопасности, поскольку удостоверение для привязки начальной загрузки защищенного диалога не соответствует удостоверению для привязки на конечной точке. Привязка защищенного диалога назначает идентификатор DNS, тогда как <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement> назначает удостоверение имени участника-пользователя или участника-службы.  
  
 [!code-csharp[C_Identity#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_identity/cs/source.cs#8)]
 [!code-vb[C_Identity#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_identity/vb/source.vb#8)]  
  
 Дополнительные сведения о том, как стека привязки элементов правильно для пользовательской привязки, см. в разделе [параметрах привязок](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md). Дополнительные сведения о создании пользовательской привязки с <xref:System.ServiceModel.Channels.SecurityBindingElement>, см. в разделе [как: Создание SecurityBindingElement для заданного режима проверки подлинности](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md).  
  
## <a name="see-also"></a>См. также

- [Практическое руководство. Создание пользовательской привязки с использованием элемента SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [Практическое руководство. Создание SecurityBindingElement для заданного режима проверки подлинности](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
- [Практическое руководство. Создание средства проверки идентификации настраиваемого клиента](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md)
- [Выбор типа учетных данных](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)
- [Работа с сертификатами](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
- [Служебная программа для метаданных ServiceModel (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
- [Создание пользовательских привязок](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)
- [Практическое руководство. Извлечение отпечатка сертификата](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)
