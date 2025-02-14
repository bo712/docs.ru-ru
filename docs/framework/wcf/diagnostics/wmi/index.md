---
title: Использование Windows Management Instrumentation для диагностики
ms.date: 03/30/2017
ms.assetid: fe48738d-e31b-454d-b5ec-24c85c6bf79a
ms.openlocfilehash: ecc5c754a51a8e1a52797dfd0af0891704eaad1f
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591241"
---
# <a name="using-windows-management-instrumentation-for-diagnostics"></a>Использование Windows Management Instrumentation для диагностики
Windows Communication Foundation (WCF) предоставляет данные проверки службы во время выполнения через поставщика WCF инструментария управления Windows (WMI).  
  
## <a name="enabling-wmi"></a>Реализация WMI  
 Инструментарий WMI - это реализованный корпорацией Майкрософт стандарт управления предприятием через Интернет (WBEM). Дополнительные сведения о пакете WMI SDK см. в разделе [инструментария управления Windows](/windows/desktop/WmiSdk/wmi-start-page). WBEM является отраслевым стандартом предоставления приложениями инструментария управления для внешних средств управления.  
  
 Поставщик инструментария WMI - это компонент, предоставляющий инструментарий в среде выполнения с помощью совместимого с WBEM интерфейса. Он состоит из набора объектов инструментария WMI, имеющих пары атрибут/значение. Пары могут быть нескольких простых типов. Средства управления могут подключаться к службам через интерфейс во время выполнения. WCF предоставляет атрибуты служб, таких как адреса, привязки, поведения и прослушиватели.  
  
 Встроенный поставщик инструментария WMI может быть активирован в файле конфигурации приложения. Это осуществляется посредством `wmiProviderEnabled` атрибут [ \<диагностики >](../../../../../docs/framework/configure-apps/file-schema/wcf/diagnostics.md) в [ \<system.serviceModel >](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) разделе, как показано в следующем примере Конфигурация.  
  
```xml  
<system.serviceModel>  
    …  
    <diagnostics wmiProviderEnabled="true" />  
    …  
</system.serviceModel>  
```  
  
 Эта запись конфигурации предоставляет интерфейс инструментария WMI. Теперь приложения управления могут подключаться через этот интерфейс и обращаться к инструментарию управления приложения.  
  
## <a name="accessing-wmi-data"></a>Доступ к данным WMI  
 Доступ к данным инструментария WMI может осуществляться несколькими различными способами. Microsoft предоставляет программные интерфейсы WMI для скриптов, приложений Visual Basic, C++ приложения и платформы .NET Framework. Дополнительные сведения см. в разделе [использование инструментария WMI](https://go.microsoft.com/fwlink/?LinkId=95183).  
  
> [!CAUTION]
>  При использовании предоставляемых .NET Framework методов для программного доступа к данным WMI следует помнить о том, что при установке подключения эти методы могут вызывать исключения. Подключение устанавливается не во время создания экземпляра <xref:System.Management.ManagementObject>, а при получении первого запроса, при котором происходит реальный обмен данными. Следовательно, следует использовать блок `try..catch` для перехвата возможных исключений.  
  
 Можно изменить уровень ведения журнала сообщений и трассировок, а также параметры журнала сообщений для источника трассировки `System.ServiceModel` в инструментарии WMI. Это можно сделать путем доступа к [AppDomainInfo](../../../../../docs/framework/wcf/diagnostics/wmi/appdomaininfo.md) экземпляр, который предоставляет следующим логическим свойствам: `LogMessagesAtServiceLevel`, `LogMessagesAtTransportLevel`, `LogMalformedMessages`, и `TraceLevel`. Поэтому, если в файле конфигурации прослушиватель трассировки настроен на ведение журнала, но эти параметры имеют значение `false`, можно впоследствии изменить их значения на `true`, когда приложение будет выполняться. В результате ведение журнала будет включено во время выполнения. Аналогично, если ведение журнала было включено в файле конфигурации, его можно отключить во время выполнения с помощью инструментария WMI.  
  
 Необходимо помнить, что если прослушиватели трассировок журнала сообщений для журнала сообщений или прослушиватели трассировок `System.ServiceModel` для трассировок не заданы в файле конфигурации, ни одно из изменений не будет применено, даже если эти изменения принимаются инструментарием WMI. Дополнительные сведения о правильной настройке соответствующих прослушивателей см. в разделе [Настройка ведения журнала сообщений](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md) и [Настройка трассировки](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md). Уровень трассировки всех остальных источников трассировки, заданных конфигурацией, действителен только при запуске приложения и не может быть изменен.  
  
 WCF предоставляет `GetOperationCounterInstanceName` метод для создания сценариев. Если передать этому методу имя операции, он возвращает имя экземпляра счетчика производительности. Однако он не проверяет входные данные. Таким образом, если передать ему неправильное имя операции, возвращается неверное имя счетчика.  
  
 `OutgoingChannel` Свойство `Service` экземпляр не выполняет подсчет каналов, открытых службой для подключения к другой службе, если клиент WCF для целевой службы не создается в `Service` метод.  
  
 **Внимание** WMI поддерживает только <xref:System.TimeSpan> значение до 3 десятичных запятых. Например, если одному из свойств служба присваивает значение <xref:System.TimeSpan.MaxValue>, при просмотре через WMI это значение усекается до 3 знаков после десятичного разделителя.  
  
## <a name="security"></a>Безопасность  
 Так как поставщик инструментария WMI для WCF разрешает обнаружение служб в среде, вы должны быть предельно осторожными для предоставления доступа к нему. При изменении настроек по умолчанию, при которых доступ предоставляется только администратору, третьи лица с более низкой степенью доверия могут получить доступ к конфиденциальным данным в среде. В частности, при расширении разрешений для удаленного доступа к WMI могут возникнуть атаки на переполнение. При переполнении процесса избыточными запросами WMI производительность процесса может снизится.  
  
 Кроме того, при расширении прав доступа к файлу MOF третьи лица с более низкой степенью доверия могут управлять поведением WMI и изменять объекты, находящиеся в схеме WMI. Например, поля могут быть удалены таким образом, что критические данные скрыты от администратора; или поля, которые не заполняются или вызывают исключения, добавляются в файл.  
  
 По умолчанию поставщик инструментария WMI для WCF предоставляет «выполнить метод», «запись поставщика» и «включить учетную запись» Администратор и «включить учетную запись» разрешение для ASP.NET, Local Service и Network Service. В частности, на платформах, отличных от [!INCLUDE[wv](../../../../../includes/wv-md.md)], учетная запись ASP.NET имеет доступ на чтение в пространстве имен ServiceModel инструментария WMI. Если требуется не предоставлять эти привилегии определенной группе пользователей, нужно либо деактивировать поставщика инструментария WMI (по умолчанию он отключен), либо запретить доступ указанной группы пользователей.  
  
 Возможно, поставщик инструментария WMI не удастся включить через конфигурацию по причине недостаточных привилегий пользователя. Однако при возникновении этого сбоя никакой записи в журнале событий не делается.  
  
 Для изменения уровней привилегий пользователя выполните следующие шаги.  
  
1. Нажмите кнопку Пуск и затем запустите введите **compmgmt.msc**.  
  
2. Щелкните правой кнопкой мыши **службы и приложения/управляющий элемент WMI** для выбора **свойства**.  
  
3. Выберите **безопасности** вкладки и перейдите к **Root/ServiceModel** пространства имен. Нажмите кнопку **безопасности** кнопки.  
  
4. Выберите определенную группу или пользователя, который вы хотите управлять доступом и использовать **Разрешить** или **Deny** флажок, чтобы настроить разрешения.  
  
## <a name="granting-wcf-wmi-registration-permissions-to-additional-users"></a>Предоставление дополнительным пользователям разрешений на регистрацию WCF WMI  
 WCF предоставляет доступ к данным управления для WMI. Это достигается путем размещения внутрипроцессного поставщика WMI, иногда называется «несвязанным поставщиком». Для предоставления доступа к данным управления учетная запись, которая регистрирует этот поставщик, должна иметь необходимые разрешения. В Windows регистрация несвязанных поставщиков по умолчанию доступна только небольшому числу привилегированных учетных записей. Это обстоятельство вызывает затруднения, поскольку пользователям обычно нужно предоставлять доступ к данным WMI из службы WCF, которая работает с учетной записью, не входящей в набор по умолчанию.  
  
 Чтобы предоставить такой доступ, администратор должен предоставить дополнительной учетной записи следующие разрешения в указанном порядке:  
  
1. разрешение на доступ к пространству имен WCF WMI;  
  
2. разрешение на регистрацию несвязанного поставщика WMI для WCF.  
  
#### <a name="to-grant-wmi-namespace-access-permission"></a>Предоставление разрешения на доступ к пространству имен WMI  
  
1. Выполните следующий скрипт PowerShell.  
  
    ```powershell  
    write-host ""  
    write-host "Granting Access to root/servicemodel WMI namespace to built in users group"  
    write-host ""  
  
    # Create the binary representation of the permissions to grant in SDDL  
    $newPermissions = "O:BAG:BAD:P(A;CI;CCDCLCSWRPWPRCWD;;;BA)(A;CI;CC;;;NS)(A;CI;CC;;;LS)(A;CI;CC;;;BU)"  
    $converter = new-object system.management.ManagementClass Win32_SecurityDescriptorHelper  
    $binarySD = $converter.SDDLToBinarySD($newPermissions)  
    $convertedPermissions = ,$binarySD.BinarySD  
  
    # Get the object used to set the permissions  
    $security = gwmi -namespace root/servicemodel -class __SystemSecurity  
  
    # Get and output the current settings  
    $binarySD = @($null)  
    $result = $security.PsBase.InvokeMethod("GetSD",$binarySD)  
  
    $outsddl = $converter.BinarySDToSDDL($binarySD[0])  
    write-host "Previous ACL: "$outsddl.SDDL  
  
    # Change the Access Control List (ACL) using SDDL  
    $result = $security.PsBase.InvokeMethod("SetSD",$convertedPermissions)   
  
    # Get and output the current settings  
    $binarySD = @($null)  
    $result = $security.PsBase.InvokeMethod("GetSD",$binarySD)  
  
    $outsddl = $converter.BinarySDToSDDL($binarySD[0])  
    write-host "New ACL:      "$outsddl.SDDL  
    write-host ""  
    ```  
  
     Этот сценарий PowerShell использует язык определения дескрипторов безопасности (SDDL) для предоставления группе встроенные пользователи получают доступ к пространству имен WMI «root/servicemodel». В нем указываются следующие списки управления доступом.  
  
    - Встроенная учетная запись администратора (BA) - уже имеет доступ.  
  
    - Сетевая служба (NS) - уже имеет доступ.  
  
    - Локальная система (LS) - уже имеет доступ.  
  
    - Встроенные пользователи - группа, которой предоставляется доступ.  
  
#### <a name="to-grant-provider-registration-access"></a>Предоставление доступа к регистрации поставщика  
  
1. Выполните следующий скрипт PowerShell.  
  
    ```powershell  
    write-host ""  
    write-host "Granting WCF provider registration access to built in users group"  
    write-host ""  
    # Set security on ServiceModel provider  
    $provider = get-WmiObject -namespace "root\servicemodel" __Win32Provider  
  
    write-host "Previous ACL: "$provider.SecurityDescriptor  
    $result = $provider.SecurityDescriptor = "O:BUG:BUD:(A;;0x1;;;BA)(A;;0x1;;;NS)(A;;0x1;;;LS)(A;;0x1;;;BU)"  
  
    # Commit the changes and display it to the console  
    $result = $provider.Put()  
    write-host "New ACL:      "$provider.SecurityDescriptor  
    write-host ""  
    ```  
  
### <a name="granting-access-to-arbitrary-users-or-groups"></a>Предоставление доступа произвольным пользователям или группам  
 В примере из этого раздела всем локальным пользователям предоставляются права доступа к регистрации поставщика WMI. Если нужно предоставить доступ пользователю или группе, которые не являются встроенными, необходимо получить идентификатор безопасности этого пользователя или группы. Нет общего метода для получения идентификатора безопасности любого пользователя. В качестве одного из решений можно выполнить вход от имени нужного пользователя, а затем выполнить следующую команду в командной оболочке.  
  
```  
Whoami /user  
```  
  
 Это позволит получить идентификатор безопасности текущего пользователя, однако такой метод нельзя использовать, чтобы получить идентификатор безопасности любого пользователя. Другой способ получения идентификатора безопасности является использование [getsid.exe](https://go.microsoft.com/fwlink/?LinkId=186467) средство из [Windows 2000 Resource Kit Tools для выполнения административных задач](https://go.microsoft.com/fwlink/?LinkId=178660). Эта программа сравнивает идентификаторы безопасности двух пользователей (локальных или пользователей домена) и помимо прочего выводит два идентификатора в командную строку. Дополнительные сведения см. в разделе [хорошо известные идентификаторы безопасности](https://go.microsoft.com/fwlink/?LinkId=186468).  
  
## <a name="accessing-remote-wmi-object-instances"></a>Доступ к экземплярам удаленных объектов WMI  
 Если вам нужно получить доступ к экземплярам инструментария WMI для WCF на удаленном компьютере, необходимо разрешить конфиденциальность пакета средств, которые используются для доступа. В следующем разделе описывается, как это можно сделать с помощью WMI CIM Studio, тестера инструментария управления Windows или .NET SDK 2.0.  
  
### <a name="wmi-cim-studio"></a>WMI CIM Studio  
 Если вы установили [Администрирование WMI](https://go.microsoft.com/fwlink/?LinkId=95185), можно использовать WMI CIM Studio, для доступа к экземплярам WMI. Средства расположены в следующей папке:  
  
 **%windir%\Program Files\WMI средства\\**  
  
1. В **подключиться к пространству имен:** введите **root\ServiceModel** и нажмите кнопку **ОК.**  
  
2. В **WMI CIM Studio входа** окно, нажмите кнопку **параметры >>** кнопку, чтобы развернуть окно. Выберите **конфиденциальности пакетов** для **уровень проверки подлинности**и нажмите кнопку **ОК**.  
  
### <a name="windows-management-instrumentation-tester"></a>Тестер инструментария управления Windows  
 Это средство установлено Windows. Чтобы запустить его, запустите консоль командной строки, введя **cmd.exe** в **Пуск/Выполнить** диалоговое окно и нажмите кнопку **ОК**. Введите **wbemtest.exe** в окне командной строки. Запустится средство Тестер инструментария управления Windows.  
  
1. Нажмите кнопку **Connect** кнопки в правом верхнем углу окна.  
  
2. В новом окне введите **root\ServiceModel** для **пространства имен** и выберите **конфиденциальности пакетов** для **уровень проверки подлинности**. Нажмите кнопку **Подключиться**.  
  
### <a name="using-managed-code"></a>Использование управляемого кода  
 Доступ к удаленным экземплярам WMI также может осуществляться программно с помощью классов, предоставляемых пространством имен <xref:System.Management>. В следующем образце кода показано, как это сделать.  
  
```csharp
String wcfNamespace = $@"\\{this.serviceMachineName}\Root\ServiceModel");
  
ConnectionOptions connection = new ConnectionOptions();  
connection.Authentication = AuthenticationLevel.PacketPrivacy;  
ManagementScope scope = new ManagementScope(this.wcfNamespace, connection);  
```
