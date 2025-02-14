---
title: Тестовый клиент WCF (WcfTestClient.exe)
ms.date: 03/30/2017
ms.assetid: d4302855-677f-4640-aa90-c5d785d72fb7
ms.openlocfilehash: ee40ca7a07729cac284ef8c634d63d673be3fbd0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64613079"
---
# <a name="wcf-test-client-wcftestclientexe"></a>Тестовый клиент WCF (WcfTestClient.exe)
Тестовый клиент Windows Communication Foundation (WCF) (WcfTestClient.exe) — это средство с графическим Интерфейсом, позволяющий пользователю вводить тестовые параметры, отправлять их в службу и просматривать ответную службы. Он предоставляет удобный способ тестирования в сочетании с узла службы WCF служб.  
  
 Тестовый клиент WCF (WcfTestClient.exe) обычно можно найти в следующем расположении: `C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE` - сообщества может принимать одно из «Корпоративный», «Professional» или «Сообщество» в зависимости от того, какой уровень Visual Studio установлен.
  
## <a name="scenarios-for-using-test-client"></a>Сценарии использования тестового клиента  
 В следующих разделах рассматриваются наиболее распространенные сценарии, в которых можно использовать тестовый клиент WCF для упрощения процесса разработки.  
  
### <a name="inside-visual-studio"></a>В Visual Studio  
  
#### <a name="wcf-service-host-starts-wcf-test-client-with-a-single-service"></a>Узел службы WCF запускает тестового клиента WCF с одной службой  
 После создания нового проекта службы WCF, и нажмите клавишу F5 для запуска отладчика узел службы WCF становится местом размещения службы в проекте. Затем тестовый клиент WCF открывает и отображает список конечных точек службы, определенные в файле конфигурации. Можно протестировать эти параметры и запустить службу, и повторять этот процесс для последовательного тестирования и проверки службы.  
  
#### <a name="wcf-service-host-starts-wcf-test-client-with-multiple-services"></a>Узел службы WCF запускает тестового клиента WCF с несколькими службами  
 Можно также использовать тестовый клиент WCF для отладки проекта, содержащего несколько служб. При открытии тестового клиента WCF, он автоматически выполняет итерацию списка служб в проект и открывает их для тестирования.  
  
### <a name="outside-visual-studio"></a>Вне Visual Studio  
 Клиент тестирования WCF (WcfTestClient.exe) также можно вызвать вне Visual Studio для проверки произвольной службы в Интернете. Инструмент расположен в следующей папке:  
  
 `C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE` (где сообщества может принимать одно из «Корпоративный», «Professional» или «Сообщество», в зависимости от уровня Visual Studio установлена на компьютере)
  
 Для использования средства дважды щелкните кнопкой мыши имя файла, чтобы открыть его, или запустите его из командной строки.  
  
 Тестовый клиент WCF принимает произвольное число идентификаторы URI в качестве аргументов командной строки.  Это универсальные коды ресурса служб, которые могут быть проверены.  
  
 `wcfTestClient.exe URI1 URI2 …`  
  
 После открытия окна тестового клиента WCF, нажмите кнопку **файл**->**добавить службу**и введите адрес конечной точки службы, которую требуется открыть.  
  
## <a name="wcf-test-client-user-interface"></a>Пользовательский интерфейс тестового клиента WCF  
 Тестовый клиент WCF можно использовать с одной или нескольких служб.  
  
### <a name="service-operations"></a>Операции служб  
 На левой панели, главного окна тестового клиента WCF перечисляются все доступные службы, а также их конечных точек и операций.  
  
 Если дважды щелкнуть операцию, в правой области внутри новой вкладки с именем операции отображается ее содержимое.  
  
 В левой области также отображается список файлов конфигурации. Дважды щелкните любой элемент, чтобы открыть в правой области содержимое этого файла в виде нового окна с вкладками.  
  
### <a name="entering-test-parameters"></a>Ввод тестовых параметров  
 Для просмотра тестовых параметров дважды щелкните операцию, чтобы открыть ее в правой области. Параметры показаны в **форматированный** представление по умолчанию, где можно ввести произвольные значения параметров для тестирования службы.  
  
 Для просмотра текста XML сообщения щелкните **XML**. Чтобы отправить их в службу, нажмите кнопку **Invoke**.  
  
 Для параметра набора данных, нажмите кнопку **...** рядом с пунктом **изменить...** Чтобы изменить его в новом окне в DataGrid. Обратите внимание, что внешний вид **Копировать DataSet** и **вставить DataSet** кнопки. Если схема объекта DataSet неизвестна при первом изменении, то DataGrid будет пустым. Необходимо вставить в текущий объект в DataGrid объект DataSet с такой же схемой. (Учтите, что перед операцией вставки потребуется скопировать схему из другого места.) Также можно скопировать объект Dataset для использования в дальнейшем, нажав кнопку **Копировать DataSet** кнопки.  
  
 Ответ службы отображается под тестовыми параметрами.  
  
> [!NOTE]
>  Если ожидаемое возвращаемое значение является строкой, результат отображается в виде строки в кавычках, хотя входные значения вводятся без кавычек.  
  
 Если при создании контракта для службы некоторая операция была указана как односторонняя, реакция службы не отображается. Как только сообщение поступает в очередь на доставку, появляется диалоговое окно с уведомлением, что сообщение успешно отравлено.  
  
### <a name="session-support"></a>Поддержка сеансов  
 **Запустить новый прокси** флажок на вкладке операции службы позволяет включить поддержку сеансов. По умолчанию этот флажок снят.  
  
 После ввода параметров проверки для конкретной операции (или другой операции этой же конечной точки службы) и нажмите кнопку **Invoke** несколько раз с этот флажок снят, эти операции совместно используют один прокси и служба находится в состоянии сохраняются между несколькими операциями.  
  
 Если **запустить новый прокси** флажок установлен, то запускается новый прокси, для каждого **Invoke**, предыдущий сценарий сеанса завершается и сбрасывается состояние службы.  
  
### <a name="editing-client-configuration"></a>Изменение конфигурации клиента  
 На левой панели, главного окна тестового клиента WCF перечисляются файлы конфигурации клиента. Дважды щелкните любой из этих элементов, чтобы отобразить содержимое файла в правой области.  
  
#### <a name="edit-with-service-configuration-editor"></a>Изменение с помощью редактора конфигурации служб  
 Щелкните правой кнопкой мыши **файл конфигурации** в левой панели и выберите в контекстном меню **изменить с помощью редактора SvcConfigEditor**. Открывается редактор конфигурации служб, в который загружено содержимое конфигурации клиента. В этом средстве конфигурацию можно изменить и сохранить.  
  
 После сохранения файла в редакторе конфигурации службы, тестовый клиент WCF выводит предупреждающее сообщение о том, что файл был изменен вне и запрашивает, следует ли перезагрузить его.  
  
 При выборе **Да**, то содержимое конфигурации на вкладке «Client.dll.config» отражает изменения, внесенные в редакторе.  
  
 При выборе **нет**, то содержимое конфигурации на вкладке «Client.dll.config» остается неизменным, и измененное содержимое автоматически сохраняется в исходном файле.  
  
#### <a name="restore-to-default-configuration"></a>Восстановление конфигурации по умолчанию  
 Если вы хотите отменить все изменения и восстановить в конфигурации клиента по умолчанию, щелкните правой кнопкой мыши **файл конфигурации** в левой панели и выберите в контекстном меню **восстановить конфигурацию по умолчанию**. Загружаются значения конфигурации по умолчанию и восстанавливается содержимое на вкладке «Client.dll.config».  
  
#### <a name="validate-changes"></a>Проверка изменений  
 Когда сохраненные изменения загружаются в тестовом клиенте WCF, конфигурация проверяется на допустимость по схеме WCF. При нахождении ошибок отображается диалоговое окно со сведениями об ошибке.  
  
 При создании прокси, двоичной компиляции или вызове службы команды пункты меню, которые поддерживают изменение (то есть «Изменение...», «Восстановление...» и т. д.) отключены. Вызов службы также отключается при загрузке обновленной конфигурации в тестовый клиент WCF.  
  
#### <a name="persist-client-configuration"></a>Сохранение конфигурация клиента  
 **Средства**->**параметры**->**конфигурация клиента** вкладка содержит **всегда повторно создавать конфигурации при запуске Службы** параметр, который включен по умолчанию. Этот параметр указывает, что каждый раз, чтобы тестовый клиент WCF загружает службы, он повторно создает файл конфигурации, в зависимости от последней контракта службы и файла App.config.  
  
 Если изменения конфигурации клиента для службы WCF и необходимо всегда использовать этот обновленный файл для отладки службы, можно снять **повторно создать** параметр. Таким образом, даже в том случае, если обновить службу и снова откройте тестовый клиент WCF, файл Client.dll.config является то, что вы обновили ранее, а не повторно созданным один на основе обновленной службы.  
  
 Однако может потребоваться изменение файла конфигурации, чтобы сделать его совместимым с повторно созданным прокси. Если повторно созданный прокси и файл конфигурации не соответствуют из-за обновленной службы, то произойдет ошибка при вызове службы.  
  
> [!CAUTION]
>  Если файл конфигурации клиента был изменен и выбран для повторного использования его в будущем, то файл находится в следующем расположении:  
>   
>  \Documents and Settings\\[учетной записи пользователя] \My Documents\Test клиентских проектов.  
>   
>  Все обновленные учетные данные, сохраненные в файле конфигурации клиента, защищены списком управления доступа (ACL) этой папки.  
  
### <a name="adding-removing-and-refreshing-services"></a>Добавление, удаление и обновление служб  
  
#### <a name="add-service"></a>Добавление службы  
 Нажмите кнопку **файл**->**добавить службу** добавить службу в тестовом клиенте WCF. Далее требуется ввести универсальный код ресурса (адрес конечной точки) добавляемой службы. Адрес службы может быть адресом обмена метаданными (MEX) или адресом языка описания веб-служб (WSDL).  
  
 Также можно найти список 10 последних добавленных конечных точек служб в **последние службы** подменю. Если выбрать один из них, указанная служба добавляется тестовый клиент WCF.  
  
 Щелкните правой кнопкой мыши корень дерева службы **Мои проекты служб**и выберите **добавить службу** для достижения такого же результата.  
  
 При создании прокси, двоичной компиляции или вызове службы, команды меню, которые поддерживают добавление службы отключены. Вызов службы также отключен.  
  
#### <a name="remove-service"></a>Удаление службы  
 Щелкните правой кнопкой мыши корень службы, службы, которую необходимо удалить и выберите **удалить службу** для удаления службы из тестового клиента WCF.  
  
 При создании прокси, двоичной компиляции или вызове службы, команды меню, которые поддерживают удаление службы отключены. Вызов службы также отключен.  
  
#### <a name="refresh-service"></a>Обновление службы  
 При внесении изменений в службу тестовый клиент WCF работает и вы хотите убедиться, что реализация тестового клиента WCF для этой службы не требует обновления, щелкните правой кнопкой мыши корень службы удаляемой службы и выберите **обновить службу**. Обратите внимание, что после обновления состояние службы сброшено.  
  
 При создании прокси, двоичной компиляции или вызове службы, команды меню, которые поддерживают обновление службы отключены. Вызов службы также отключен.  
  
## <a name="location-of-files-generated-by-the-test-client"></a>Расположение файлов, созданных тестовым клиентом.  
 По умолчанию тестовый клиент WCF сохраняет созданный клиентом код и файлы конфигурации в папке «%appdata%\Local\temp\Test Client Projects». Эта папка удаляется после выхода тестового клиента WCF. При изменении файла конфигурации в тестовом клиенте WCF и **всегда повторно создавать конфигурацию при запуске служб** недоступен, измененный файл копируется в папку «CachedConfig» в группе «My Documents\Test клиентские проекты» с помощью файла сопоставления XML (метаданные адрес к файла) как индекс.  
  
 Тестовый клиент WCF также можно запустить в командной строке, используйте `/ProjectPath` указание в качестве указателя пути сохранения создаваемых файлов, либо используйте `/RestoreProjectPath` переключиться в режим восстановления расположение по умолчанию. Синтаксис выглядит следующим образом:  
  
 `wcfTestClient.exe /ProjectPath [desired location]`  
  
 Выполнение этой команды не открывает тестовый клиент WCF. Изменяется только расположение папок. Эту команду можно выполнить ли тестовый клиент WCF выполняется или нет. Новое расположение применяется при перезапуске тестовый клиент WCF. Сведения о расположении можно сохранить в реестре или в файле WcfTestClient.exe.option в папке «%appdata%\Local\temp\Test Client Projects».  
  
## <a name="features-supported-by-wcf-test-client"></a>Возможности, поддерживаемые тестовым клиентом WCF  
 Ниже приведен список функций, поддерживаемых тестовым клиентом WCF:  
  
- Вызов службы: Запрос-ответ и одностороннее сообщение.  
  
- Привязки: все привязки, поддерживаемые программой Svcutil.exe.  
  
- Управление сеансом.  
  
- Контракт сообщения.  
  
- XML-сериализация.  
  
 Ниже приведен список компонентов, не поддерживается в тестовом клиенте WCF:  
  
- Типы: <xref:System.IO.Stream>, <xref:System.ServiceModel.Channels.Message>, <xref:System.Xml.XmlElement>, <xref:System.Xml.XmlAttribute>, <xref:System.Xml.XmlNode>, типы, в которых реализован интерфейс <xref:System.Xml.Serialization.IXmlSerializable>, включая связанный атрибут <xref:System.Xml.Serialization.XmlSchemaProviderAttribute>, а также типы <xref:System.Xml.Linq.XDocument> и <xref:System.Xml.Linq.XElement> и тип ADO.NET <xref:System.Data.DataTable>.  
  
- Дуплексный контракт.  
  
- Транзакция.  
  
- Безопасность: [!INCLUDE[infocard](../../../includes/infocard-md.md)], сертификат, имя пользователя/пароль.  
  
- Привязки: WSFederationbinding, любые контекстные привязки и привязка Https, WebHttpbinding (поддержка ответных сообщений Json).  
  
## <a name="closing-wcf-test-client"></a>Закрытие тестового клиента WCF  
 Тестовый клиент WCF можно закрыть следующими способами:  
  
- На **файл** меню, щелкните **выхода**. Кроме того, в главном окне тестового клиента WCF, нажмите кнопку **закрыть**. Эти действия также завершить работу WCF Service Auto Host и остановить процесс отладки Visual Studio, если был запущен тестовый клиент WCF в Visual Studio.  
  
- Щелкните правой кнопкой мыши **узел службы WCF** значок в области уведомлений и нажмите кнопку **выхода.** Это завершает работу WCF Service Auto Host и тестовый клиент WCF и останавливается процесс отладки Visual Studio.  
  
## <a name="see-also"></a>См. также

- [Узел службы WCF (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
