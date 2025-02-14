---
title: Процесс корпоративных закупок
ms.date: 03/30/2017
ms.assetid: a5e57336-4290-41ea-936d-435593d97055
ms.openlocfilehash: 83290245dd203d4bb63c96e94ca6bdafee4ecffb
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2019
ms.locfileid: "65876172"
---
# <a name="corporate-purchase-process"></a>Процесс корпоративных закупок
Этот образец показывает, как создать очень простой запрос предложений на основе процесса покупки с автоматическим выбором наилучшего предложения. В нем совместно применяются операторы <xref:System.Activities.Statements.Parallel>, <xref:System.Activities.Statements.ParallelForEach%601> и <xref:System.Activities.Statements.ForEach%601>, а также пользовательское действие для создания рабочего потока, который представляет процесс.

 Этот пример содержит клиентского приложения ASP.NET, которое обеспечивает взаимодействие с процессом в качестве различных участников (исходной запрашивающей стороны или конкретного поставщика).

## <a name="requirements"></a>Требования

- Visual Studio 2012.

- [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].

## <a name="demonstrates"></a>Демонстрации

- Настраиваемые действия.

- Сочетание действий.

- Закладки.

- Сохраняемость.

- Схематизированная сохраняемость.

- Трассировка.

- Отслеживание.

- Размещение [!INCLUDE[wf1](../../../../includes/wf1-md.md)] в различных клиентах (веб-приложений ASP.NET и приложения WinForms).

> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) для загрузки всех Windows Communication Foundation (WCF) и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] примеры. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Application\PurchaseProcess`  
  
## <a name="description-of-the-process"></a>Описание процесса  
 В этом образце показана реализация программы Windows Workflow Foundation (WF) для сбора предложений от поставщиков для универсального компании.  
  
1. Сотрудник компании X создает запрос предложений.  
  
    1. Сотрудник вводит название и описание запроса предложений.  
  
    2. Сотрудник выбирает поставщиков, которых он желает пригласить для передачи предложений.  
  
2. Сотрудник передает предложение.  
  
    1. Создается экземпляр рабочего процесса.  
  
    2. Рабочий процесс ожидает, чтобы все поставщики передали свои предложения.  
  
3. После получения всех предложений рабочий процесс обрабатывает в цикле все полученные предложения и выбирает наилучшее.  
  
    1. Каждый поставщик имеет репутацию (в этом образце список репутаций сохраняется в VendorRepository.cs).  
  
    2. Общая стоимость предложения определяется по формуле (Стоимость, предложенная поставщиком)*(Зарегистрированный показатель репутации поставщика) / 100.  
  
4. Исходная запрашивающая сторона может видеть все переданные предложения. Наилучшее предложение представлено в специальном разделе отчета.  
  
## <a name="process-definition"></a>Определение процесса  
 В основной логике образца используется действие <xref:System.Activities.Statements.ParallelForEach%601>, которое ожидает предложения от каждого поставщика (с применением пользовательского действия, которое создает закладку) и регистрирует предложение поставщика как запрос предложений (с применением действия <xref:System.Activities.Statements.InvokeMethod>).  
  
 Затем в образце выполняется обработка в цикле всех полученных предложений, сохраненных в `RfpRepository`, вычисление откорректированного значения (с использованием действия <xref:System.Activities.Statements.Assign> и действий <xref:System.Activities.Expressions>), и если откорректированное значение оказывается лучше по сравнению с предыдущим наилучшим предложением, присваивание нового значения как наилучшего предложения (с использованием действий <xref:System.Activities.Statements.If> и <xref:System.Activities.Statements.Assign>).  
  
## <a name="projects-in-this-sample"></a>Проекты в этом образце  
 Этот образец содержит следующие проекты.  
  
|Проект|Описание|  
|-------------|-----------------|  
|Общие|Объекты сущности, используемые в процессе («Запрос предложения», «Поставщик» и «Предложение поставщика»).|  
|WfDefinition|Определение процесса (как программы [!INCLUDE[wf1](../../../../includes/wf1-md.md)]) и узел (`PurchaseProcessHost`), используемый клиентскими приложениями для создания и использования экземпляров рабочего потока процесса покупки.|  
|WebClient|ASP.NET клиентского приложения, позволяет пользователям создавать и участвовать в работе экземпляров процесса покупки. Для взаимодействия с подсистемой рабочих процессов используется настраиваемый сервер.|  
|WinFormsClient|Клиентское приложение Windows Forms, которое позволяет пользователям создавать и участвовать в работе экземпляров процесса покупки. Для взаимодействия с подсистемой рабочих процессов используется настраиваемый сервер.|  
  
### <a name="wfdefinition"></a>WfDefinition  
 В следующей таблице содержится описание наиболее важных файлов в проекте WfDefinition.  
  
|Файл|Описание|  
|----------|-----------------|  
|IPurchaseProcessHost.cs|Интерфейс для узла рабочего процесса.|  
|PurchaseProcessHost.cs|Реализация узла для рабочего процесса. Узел позволяет абстрагироваться от подробных сведений о среде выполнения рабочего процесса и используется во всех клиентских приложениях для загрузки, запуска и взаимодействия с экземплярами рабочего процесса `PurchaseProcess`.|  
|PurchaseProcessWorkflow.cs|Действие, которое содержит определение рабочего процесса покупки (происходит от <xref:System.Activities.Activity>).<br /><br /> Действия, которые происходят от <xref:System.Activities.Activity>, формируют функциональные возможности, выполняя сборку существующих пользовательских действий и действий из библиотеки действий [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]. Сборка этих действий является наиболее простым способом создания пользовательских функциональных возможностей.|  
|WaitForVendorProposal.cs|Это пользовательское действие происходит от <xref:System.Activities.NativeActivity> и создает именованную закладку, которая должна быть возобновлена в дальнейшем поставщиком путем передачи предложения.<br /><br /> Действия, которые являются производными от <xref:System.Activities.NativeActivity> аналогично производным действиям от <xref:System.Activities.CodeActivity>, создают императивные функции путем переопределения <xref:System.Activities.NativeActivity.Execute%2A>, но также имеют доступ ко всем функциям среды выполнения рабочего процесса благодаря <xref:System.Activities.ActivityContext>, который передается методу `Execute`. Этот контекст поддерживает планирование и отмену дочерних действий, подготовку к работе зон, не обеспечивающих сохраняемость (блоков выполнения, в ходе работы которых среда выполнения не сохраняет данные рабочего потока, как при неразрывных транзакциях), и объекты <xref:System.Activities.Bookmark> (маркеры возобновления приостановленных рабочих процессов).|  
|TrackingParticipant.cs|Участник <xref:System.Activities.Tracking.TrackingParticipant>, который получает все события отслеживания и сохраняет их в текстовом файле.<br /><br /> Участники отслеживания добавляются к экземпляру рабочего процесса как расширения.|  
|XmlWorkflowInstanceStore.cs|Пользовательское хранилище <xref:System.Runtime.DurableInstancing.InstanceStore>, которое сохраняет приложения рабочего процесса в XML-файлах.|  
|XmlPersistenceParticipant.cs|Пользовательское хранилище <xref:System.Activities.Persistence.PersistenceParticipant>, которое сохраняет экземпляр запроса предложения в XML-файле.|  
|AsyncResult.cs / CompletedAsyncResult.cs|Вспомогательные классы для реализации асинхронной технологии в компонентах сохраняемости.|  
  
### <a name="common"></a>Общие  
 В следующей таблице содержится описание наиболее важных классов в проекте Common.  
  
|Класс|Описание|  
|-----------|-----------------|  
|Vendor|Поставщик, который передает предложения в запросе предложений.|  
|RequestForProposal|Запрос предложений представляет собой приглашение для поставщиков, согласно которому они должны передать предложения по конкретному товару или услуге.|  
|VendorProposal|Предложение, переданное поставщиком в ответ на конкретный запрос предложений.|  
|VendorRepository|Репозиторий поставщиков. Эта реализация содержит в оперативной памяти коллекцию экземпляров поставщиков и методов доступа к этим экземплярам.|  
|RfpRepository|Репозиторий запросов предложений. Эта реализация содержит примеры использования Linq to XML для запроса XML-файла запросов предложений, созданного схематизированными средствами обеспечения сохраняемости. |  
|IOHelper|Этот класс разрешает все проблемы, связанные с вводом-выводом (которые касаются папок, путей и т. д.).|  
  
### <a name="web-client"></a>Веб-клиент  
 В следующей таблице содержится описание наиболее важных веб-страниц в проекте веб-клиента.  
  
|Файл|Описание|  
|-|-|  
|CreateRfp.aspx|Создает и отправляет новый запрос предложений.|  
|Default.aspx|Показывает все активные и завершенные запросы предложений.|  
|GetVendorProposal.aspx|Возвращает предложение от поставщика в конкретном запросе предложений. Эта страница используется только поставщиками.|  
|ShowRfp.aspx|Выводит все сведения о запросе предложений (полученные предложения, даты, стоимость и другие данные). Эта страница используется только создателем запроса предложений.|  
  
### <a name="winforms-client"></a>Клиент WinForms  
 В следующей таблице содержится описание наиболее важных форм в проекте WinForms.  
  
|Form|Описание|  
|-|-|  
|NewRfp|Создает и отправляет новый запрос предложений.|  
|ShowProposals|Показывает все активные и завершенные запросы предложений. **Примечание.**  Может потребоваться щелкните **обновить** кнопку в пользовательском Интерфейсе для просмотра изменений на этом экране после создания или изменения запроса предложений.|  
|SubmitProposal|Возвращает предложение от поставщика в конкретном запросе предложений. Это окно используется только поставщиками.|  
|ViewRfp|Выводит все сведения о запросе предложений (полученные предложения, даты, стоимость и другие данные). Это окно используется только создателем запроса предложений.|  
  
### <a name="persistence-files"></a>Файлы сохраняемости  
 В следующей таблице показаны файлы, созданные поставщиком сохраняемости (`XmlPersistenceProvider`), которые находятся в пути к временной папке текущей системы (использующей <xref:System.IO.Path.GetTempPath%2A>). Файл трассировки создается в текущем пути выполнения.  
  
|Имя файла|Описание|Путь|  
|-|-|-|  
|rfps.xml|XML-файл со всеми активными и завершенными запросами предложений.|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceid]|Этот файл содержит все сведения об экземпляре рабочего процесса.<br /><br /> Этот файл создается схематизированной реализацией сохраняемости (PersistenceParticipant в XmlPersistenceProvider).|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceId].tracking|Текстовый файл со всеми событиями, которые произошли в конкретном экземпляре.<br /><br /> Этот файл создается объектом TrackingParticipant.|<xref:System.IO.Path.GetTempPath%2A>|  
|PurchaseProcess.Tracing.TraceLog.txt|Файл трассировки, созданный рабочим потоком на основе параметров конфигурации в файлах App.config или Web.config.|Текущий путь выполнения|  
  
#### <a name="to-use-this-sample"></a>Использование этого образца  
  
1. С помощью Visual Studio 2010, откройте решения purchaseprocess.sln.  
  
2. Чтобы выполнить проект веб-клиента, откройте **обозревателе решений** и щелкните правой кнопкой мыши **веб-клиент** проекта. Выберите **Назначить запускаемым проектом**.  
  
3. Чтобы выполнить проект клиента WinForms, откройте **обозревателе решений** и щелкните правой кнопкой мыши **клиента WinForms** проекта. Выберите **Назначить запускаемым проектом**.  
  
4. Для построения решения нажмите CTRL+SHIFT+B.  
  
5. Чтобы запустить решение, нажмите клавиши CTRL+F5.  
  
### <a name="web-client-options"></a>Параметры веб-клиента  
  
- **Создание нового запроса Предложений**: Создает новый запрос для Предложений и запускает рабочий процесс покупки.  
  
- **Обновить**: Обновляет список активных и завершенных запросов предложений в главном окне.  
  
- **Вид**: Показывает содержимое существующего запроса Предложений. Поставщики могут передавать свои предложения (если они приглашены или запрос предложений не завершен).  
  
- Просмотрите как: Пользователь может обращаться к запросу Предложений, используя другие идентификаторы, путем выбора желаемого участника в **в виде** поле со списком в сетке активной таблицы запросов предложений.  
  
### <a name="winforms-client-options"></a>Параметры клиента WinForms  
  
- **Создание запроса Предложений**: Создает новый запрос для Предложений и запускает рабочий процесс покупки.  
  
- **Обновить**: Обновляет список активных и завершенных запросов предложений в главном окне.  
  
- **Просмотр запроса Предложений**: Показывает содержимое существующего запроса Предложений. Поставщики могут передавать свои предложения (если они приглашены или запрос предложений не завершен).  
  
- **Подключиться как**: Пользователь может обращаться к запросу Предложений, используя другие идентификаторы, путем выбора желаемого участника в **в виде** поле со списком в сетке активной таблицы запросов предложений.
