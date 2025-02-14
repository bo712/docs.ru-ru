---
title: Изолированное хранилище
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- data storage using isolated storage
- stores
- storing data using isolated storage
- isolated storage
- location of isolated storage in file system
- standardizing storage systems
- storing data using isolated storage, when not to use
- code, isolated storage
- isolated storage, options
- data storage using isolated storage, when not to use
- storing data using isolated storage, options
- isolated storage, when not to use
- data storage using isolated storage, options
- isolation
ms.assetid: aff939d7-9e49-46f2-a8cd-938d3020e94e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6f6453b8ef2ef2a1b5e86ae461a626808cff7455
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025512"
---
# <a name="isolated-storage"></a>Изолированное хранилище
<a name="top"></a> Для приложений [!INCLUDE[desktop_appname](../../../includes/desktop-appname-md.md)] изолированное хранилище — это механизм хранения данных, обеспечивающий изоляцию и безопасность данных путем определения стандартизованных способов для сопоставления кода с сохраненными данными. Стандартизация также имеет и другие преимущества. Администраторы могут использовать инструменты управления изолированным хранением для конфигурирования пространства хранения файлов, установки политики безопасности и удаления неиспользуемых данных. При изолированном хранении нет необходимости указывать уникальные пути для безопасного размещения кода в файловой системе, и данные защищены от других приложений, имеющих доступ только к изолированному хранению. Нет необходимости в аппаратно закодированной информации, указывающей место размещения области хранения данных приложения.

> [!IMPORTANT]
> Изолированное хранилище недоступно для приложений Windows [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] . Вместо этого используйте классы данных приложений в пространствах имен `Windows.Storage`, включенных в API среды выполнения Windows для хранения локальных данных и файлов. Дополнительные сведения см. в статье [Доступ к данным приложения](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10)) в Центре разработки для Windows.

В этом разделе содержатся следующие подразделы.

- [Секции данных и хранилища](#data_compartments_and_stores)

- [Квоты для изолированного хранилища](#quotas)

- [Безопасный доступ](#secure_access)

- [Разрешенное использование и угрозы безопасности](#allowed_usage)

- [Расположения изолированных хранилищ](#isolated_storage_locations)

- [Создание, перечисление и удаление изолированного хранилища](#isolated_storage_tasks)

- [Сценарии изолированного хранилища](#scenarios_for_isolated_storage)

- [Связанные разделы](#related_topics)

- [Ссылки](#reference)

<a name="data_compartments_and_stores"></a>

## <a name="data-compartments-and-stores"></a>Секции данных и хранилища

Когда приложение сохраняет данные в файле, выбирать имя файла и место его хранения следует так, чтобы минимизировать вероятность того, что место хранения данных будет доступно другим приложениям и, следовательно, станет уязвимым к повреждению. В отсутствие стандартной системы для решения подобных проблем разработка специальных средств минимизации конфликтов хранения может стать чрезмерно сложной, а ее результаты — ненадежными.

В изолированном хранилище данные всегда изолированы по пользователю или сборке. Сборка идентифицируется учетными данными, такими как источник или строгое имя. Данные также могут быть изолированы по домену приложения при помощи подобных учетных данных.

В изолированном хранилище приложение сохраняет данные в уникальной ячейке данных, привязанной к одному из аспектов, идентифицирующих код, например к издателю или подписи. Ячейка данных — это абстракция, а не определенное место хранения. Она состоит из одного или нескольких файлов для изолированного хранения, называемых хранилищами, которые содержат действительные адреса каталогов, в которых хранятся данные. Например, приложение может иметь связанную с ним ячейку данных, а действительное хранение данных для этого приложения может осуществляться в каталоге файловой системы. Данные, сохраняемые в хранилище, могут быть любого типа, от информации о пользовательских настройках до состояния приложения. Для разработчика расположение ячейки данных является прозрачным. Хранилища обычно находятся на клиенте, но серверное приложение может использовать изолированные хранилища для информации путем олицетворения пользователя, от лица которого оно действует. В изолированном хранилище информация также может храниться на сервере с перемещаемым профилем пользователя, что обеспечивает ее перемещение вместе с пользователем.

<a name="quotas"></a>

## <a name="quotas-for-isolated-storage"></a>Квоты для изолированного хранилища

Квота — это ограничение доступного для использования объема изолированного хранилища. Квота учитывает байты файлового пространства, а также служебные данные, связанные с каталогом и другой информацией в хранилище. Изолированное хранилище использует квоты разрешения, которые представляют собой допустимые пределы хранения, устанавливаемые посредством объектов <xref:System.Security.Permissions.IsolatedStoragePermission> . При попытке записать данные в превышение квоты возникает исключение <xref:System.IO.IsolatedStorage.IsolatedStorageException> .  Какие разрешения даются коду, определяет политика безопасности, которую можно менять с помощью средства настройки .NET Framework (Mscorcfg.msc). Для кода, которому предоставлено разрешение <xref:System.Security.Permissions.IsolatedStoragePermission> , выделяется хранилище, максимальный размер которого определяется свойством <xref:System.Security.Permissions.IsolatedStoragePermission.UserQuota%2A> . Тем не менее, поскольку код может обходить квоты разрешения, используя различные удостоверения пользователя, эти квоты в большей степени имеют характер рекомендаций по работе кода, нежели выступают в роли строгих ограничений.

К перемещаемым хранилищам квоты не применяются. По этой причине для их использования код должен располагать разрешениями несколько более высокого уровня. Значения перечисления <xref:System.Security.Permissions.IsolatedStorageContainment.AssemblyIsolationByRoamingUser> и <xref:System.Security.Permissions.IsolatedStorageContainment.DomainIsolationByRoamingUser> определяют разрешение на использование изолированного хранилища для перемещаемого профиля пользователя.

<a name="secure_access"></a>

## <a name="secure-access"></a>Безопасный доступ

Использование изолированного хранения позволяет частично доверенным приложениям сохранять данные под контролем политики безопасности компьютера. Это особенно удобно при работе с загружаемыми компонентами, которые не вызывают у пользователя полного доверия. Политика безопасности редко предоставляет такому коду право доступа к файловой системе с использованием стандартных механизмов ввода-вывода. Однако по умолчанию код, запускаемый с локального компьютера, из локальной или глобальной сети получает право на использование изолированного хранилища.

Администраторы могут ограничивать размеры изолированного хранилища, доступного приложению или пользователю, в зависимости от соответствующего уровня доверия. Кроме того, администраторы могут удалить все хранящиеся данные. Чтобы создать изолированное хранилище или получить доступ к нему, коду необходимо предоставить соответствующее разрешение <xref:System.Security.Permissions.IsolatedStorageFilePermission> .

Для доступа к изолированному хранилищу коду должны быть назначены все необходимые права операционной системы собственной платформы. Должны быть выполнены требования списков управления доступом, которые определяют, какие пользователи имеют права на пользование файловой системой. Приложения платформы .NET Framework по умолчанию имеют права доступа к изолированному хранилищу на уровне операционной системы, если только они не выполняют олицетворение (специфическое для платформы). В таком случае ответственность за обеспечение наличия у олицетворяемого пользователя прав, необходимых для доступа к изолированному хранилищу, несет приложение. Такой доступ позволяет коду, запускаемому или загружаемому через Интернет, выполнять чтение и запись в области хранения, относящейся к конкретному пользователю.

Для управления доступом к изолированному хранилищу среда CLR использует объекты <xref:System.Security.Permissions.IsolatedStorageFilePermission> . Каждый объект имеет свойства, которые определяют следующие значения:

- Разрешенное использование, которое указывает тип разрешенного доступа. Значения являются членами перечисления <xref:System.Security.Permissions.IsolatedStorageContainment> . Дополнительные сведения об этих значениях см. в таблице в следующем разделе.

- Квота хранилища, описанная в предыдущем разделе.

Среда выполнения требует разрешения <xref:System.Security.Permissions.IsolatedStorageFilePermission> при первой попытке открыть хранилище. Решение о предоставлении этого разрешения определяется с учетом надежности кода. Если разрешение выдается, значения квоты использования и хранилища определяются политикой безопасности и запросом кода на получение разрешения <xref:System.Security.Permissions.IsolatedStorageFilePermission>. Политика безопасности задается с помощью средства настройки .NET Framework (Mscorcfg.msc). Все вызывающие программы в стеке вызовов проверяются на наличие по меньшей мере одного соответствующего разрешения на использования. Среда выполнения также проверяет наличие квоты у кода, открывшего или создавшего хранилище, в которое записывается файл. Если все эти условия выполнены, то выдается разрешение. Квота проверяется каждый раз при записи файла в хранилище.

Коду приложения не нужно запрашивать разрешение, поскольку среда CLR выдаст соответствующее разрешение <xref:System.Security.Permissions.IsolatedStorageFilePermission> , исходя из политики безопасности. Однако имеет смысл запрашивать определенные разрешения для своего приложения, включая <xref:System.Security.Permissions.IsolatedStorageFilePermission>.

<a name="allowed_usage"></a>

## <a name="allowed-usage-and-security-risks"></a>Разрешенное использование и угрозы безопасности

Разрешенное использование, заданное при помощи <xref:System.Security.Permissions.IsolatedStorageFilePermission> , определяет степень, в которой коду разрешено создавать и использовать изолированное хранилище. В следующей таблице приведено соответствие между разрешенным использованием и типами изоляции, а также кратко описаны риски безопасности, связанные с каждым из видов разрешенного использования.

|Разрешенное использование|Типы изоляции|Риски безопасности|
|-------------------|---------------------|---------------------|
|<xref:System.Security.Permissions.IsolatedStorageContainment.None>|Нет разрешения на изолированное хранилище.|Влияния на безопасность нет.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.DomainIsolationByUser>|Изоляция по пользователям, доменам и сборкам. Каждая сборка имеет отдельное вложенное хранилище внутри домена. Хранилища, использующие это разрешение, также неявно изолируются компьютером.|Этот уровень разрешения оставляет возможность несанкционированного чрезмерного использования ресурсов, хотя применение квот делает это затруднительным. Этот процесс называется атакой типа "отказ в обслуживании".|
|<xref:System.Security.Permissions.IsolatedStorageContainment.DomainIsolationByRoamingUser>|То же, что и `DomainIsolationByUser`, однако хранилище сохраняется в перемещаемое расположение, если применяются перемещаемые профили пользователей и не применяются квоты.|Поскольку квоты приходится отключать, то ресурсы хранения более уязвимы к атаке типа "отказ в обслуживании".|
|<xref:System.Security.Permissions.IsolatedStorageContainment.AssemblyIsolationByUser>|Изоляция по пользователям и сборкам. Хранилища, использующие это разрешение, также неявно изолируются компьютером.|На этом уровне применяются квоты для предотвращения атак типа "отказ в обслуживании". Та же сборка в другом домене может иметь доступ к хранилищу, что может привести к утечке информации между приложениями.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.AssemblyIsolationByRoamingUser>|То же, что и `AssemblyIsolationByUser`, однако хранилище сохраняется в перемещаемое расположение, если применяются перемещаемые профили пользователей и не применяются квоты.|То же, что и `AssemblyIsolationByUser`, но без квот; риск атак типа "отказ в обслуживании" возрастает.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.AdministerIsolatedStorageByUser>|Изоляция по пользователям. Обычно этот уровень разрешения используют только средства администрирования или отладки.|Доступ с этим уровнем разрешения позволяет коду просматривать или удалять любые файлы и каталоги изолированного хранилища пользователя (независимо от изоляции сборки). Риски, помимо прочего, включают утечку информации и потерю данных.|
|<xref:System.Security.Permissions.IsolatedStorageContainment.UnrestrictedIsolatedStorage>|Изоляция по всем пользователям, доменам и сборкам. Обычно этот уровень разрешения используют только средства администрирования или отладки.|Это разрешение может привести к потере защищенной информации всех изолированных хранилищ для всех пользователей.|

<a name="isolated_storage_locations"></a>

## <a name="isolated-storage-locations"></a>Расположения изолированных хранилищ

В некоторых случаях рекомендуется проверять изменения в изолированном хранилище, используя файловую систему операционной системы. Могут потребоваться сведения о размещении файлов изолированного хранилища. Место их размещения зависит от операционной системы. Ниже в таблице приведены корневые адреса файлов изолированного хранилища для некоторых распространенных операционных систем. В корневых адресах см. каталоги Microsoft\IsolatedStorage. Для того чтобы отобразить изолированное хранилище в файловой системе, нужно изменить настройки папки, установив для нее отображение скрытых файлов и папок.

|Операционная система|Местоположение в файловой системе|
|----------------------|-----------------------------|
|Windows 2000, Windows XP, Windows Server 2003 (обновление Windows NT 4.0)|Перемещаемые хранилища =<br /><br /> \<КОРНЕВОЙ КАТАЛОГ СИСТЕМЫ>\Profiles\\<имя пользователя\>\Application Data<br /><br /> Неперемещаемые хранилища =<br /><br /> \<КОРНЕВОЙ КАТАЛОГ СИСТЕМЫ>\Profiles\\<имя пользователя\>\Local Settings\Application Data|
|Windows 2000 — чистая установка (и обновление с Windows 98 и Windows NT 3.51)|Перемещаемые хранилища =<br /><br /> \<СИСТЕМНЫЙ ДИСК>\Documents and Settings\\<имя пользователя\>\Application Data<br /><br /> Неперемещаемые хранилища =<br /><br /> \<СИСТЕМНЫЙ ДИСК>\Documents and Settings\\<имя пользователя\>\Local Settings\Application Data|
|Windows XP, Windows Server 2003 — чистая установка (или обновление с Windows 2000 и Windows 98)|Перемещаемые хранилища =<br /><br /> \<СИСТЕМНЫЙ ДИСК>\Documents and Settings\\<имя пользователя\>\Application Data<br /><br /> Неперемещаемые хранилища =<br /><br /> \<СИСТЕМНЫЙ ДИСК>\Documents and Settings\\<имя пользователя\>\Local Settings\Application Data|
|[!INCLUDE[win8](../../../includes/win8-md.md)], Windows 7, Windows Server 2008, Windows Vista|Перемещаемые хранилища =<br /><br /> \<СИСТЕМНЫЙ ДИСК>\Users\\<имя пользователя\>\AppData\Roaming<br /><br /> Неперемещаемые хранилища =<br /><br /> \<СИСТЕМНЫЙ ДИСК>\Users\\<имя пользователя\>\AppData\Local|

<a name="isolated_storage_tasks"></a>

## <a name="creating-enumerating-and-deleting-isolated-storage"></a>Создание, перечисление и удаление изолированного хранилища

В составе платформы .NET Framework есть три класса в пространстве имен <xref:System.IO.IsolatedStorage> , которые помогают выполнять задачи, включающие изолированное хранилище:

- Класс<xref:System.IO.IsolatedStorage.IsolatedStorageFile>, производный от класса <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=nameWithType> , обеспечивает базовую функциональность для управления хранимыми сборками и файлами приложений. Экземпляр класса <xref:System.IO.IsolatedStorage.IsolatedStorageFile> служит для представления единичного хранилища, расположенного в файловой системе.

- Класс<xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> , производный от класса <xref:System.IO.FileStream?displayProperty=nameWithType> , предоставляет доступ к файлам, расположенным в хранилище.

- Класс<xref:System.IO.IsolatedStorage.IsolatedStorageScope> — это перечисление, позволяющее создавать и выбирать хранилища с необходимым типом изоляции.

Классы, предназначенные для работы с изолированными хранилищами, позволяют создавать, перечислять и удалять изолированные хранилища. Доступ к методам, используемым для выполнения этих действий, осуществляется с помощью объекта <xref:System.IO.IsolatedStorage.IsolatedStorageFile> . Для выполнения некоторых операций необходимо разрешение <xref:System.Security.Permissions.IsolatedStorageFilePermission> , обеспечивающее право администрирования изолированного хранилища. Для доступа к некоторым файлам и каталогам также могут потребоваться права операционной системы.

Несколько примеров, демонстрирующих часто встречающиеся задачи изолированного хранения см. в практических руководствах, перечисленных в разделе [Связанные разделы](#related_topics).

<a name="scenarios_for_isolated_storage"></a>

## <a name="scenarios-for-isolated-storage"></a>Сценарии изолированного хранилища

Изолированное хранилище может оказаться полезным во многих случаях, в том числе в следующих четырех ситуациях:

- Загружаемые элементы управления. Элементам управления, загружаемым через Интернет, не разрешено записывать данные на жесткий диск посредством обычных классов ввода-вывода, но они могут использовать изолированное хранилище для хранения параметров пользователя и состояний приложения.

- Хранение общих компонентов. Компоненты, общие для нескольких приложений, могут использовать изолированное хранилище для обеспечения управляемого доступа к хранилищам данных.

- Хранение на сервере. Серверные приложения могут использовать изолированные хранилища для представления отдельных хранилищ большому числу пользователей, обращающихся с запросами к приложению. Так как изолированное хранилище всегда выделяется пользователем, сервер должен выполнять роль пользователя, создающего запрос. В этом случае данные изолируются на основе идентификатора субъекта, который является тем же идентификатором, который используется приложением для того, чтобы различать пользователей.

- Перемещение. Приложения могут также использовать изолированное хранилище с перемещаемыми профилями пользователей. Это позволяет изолированным данным пользователя перемещаться вслед за его профилем.

Изолированное хранилище не следует использовать в следующих ситуациях:

- Для хранения важных конфиденциальных данных, таких как незашифрованные ключи или пароли, поскольку изолированное хранилище не защищено от высоконадежного кода, от неуправляемого кода и от доверенных пользователей компьютера.

- Для хранения кода.

- Для хранения параметров конфигурации и развертывания, которые контролируются администраторами. (настройки пользователя не считаются параметрами конфигурации, т.к. они не управляются администраторами).

Многие приложения используют базы данных для хранения и изолирования данных, в которых одна или несколько строк могут представлять хранилище для определенного пользователя. Применение изолированное хранилища вместо базы данных как правило выбирается в тех случаях, когда число пользователей невелико, когда использование базы данных влечет значительные потери производительности или когда отсутствуют средства для поддержания баз данных. Изолированное хранилище также представляет вполне реальную альтернативу в тех случаях, когда приложению требуется более гибкое и сложное хранилище, чем строка в базе данных.

<a name="related_topics"></a>

## <a name="related-topics"></a>См. также

|Заголовок|Описание|
|-----------|-----------------|
|[Типы изоляции](../../../docs/standard/io/types-of-isolation.md)|Описание различных типов изоляции.|
|[Практическое руководство. Получение хранилищ для изолированного хранения](../../../docs/standard/io/how-to-obtain-stores-for-isolated-storage.md)|Пример использования класса <xref:System.IO.IsolatedStorage.IsolatedStorageFile> для получения хранилища, изолированного по пользователю и сборке.|
|[Практическое руководство. Перечисление хранилищ для изолированного хранилища](../../../docs/standard/io/how-to-enumerate-stores-for-isolated-storage.md)|Пример использования метода <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=nameWithType> для вычисления общего размера всех изолированных хранилищ пользователя.|
|[Практическое руководство. Удаление хранилищ из области изолированного хранения](../../../docs/standard/io/how-to-delete-stores-in-isolated-storage.md)|Пример использования метода <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%2A?displayProperty=nameWithType> для удаления изолированных хранилищ двумя разными способами.|
|[Практическое руководство. Предупреждение о нехватке места при изолированном хранении](../../../docs/standard/io/how-to-anticipate-out-of-space-conditions-with-isolated-storage.md)|Пример измерения оставшегося свободного места в изолированном хранилище.|
|[Практическое руководство. Создание файлов и каталогов в изолированном хранилище](../../../docs/standard/io/how-to-create-files-and-directories-in-isolated-storage.md)|Ряд примеров создания файлов и каталогов в изолированном хранилище.|
|[Практическое руководство. Поиск существующих файлов и каталогов в изолированном хранилище](../../../docs/standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md)|Пример считывания структуры каталогов и файлов в изолированном хранилище.|
|[Практическое руководство. Считывание из файлов и запись в файлы в изолированном хранилище](../../../docs/standard/io/how-to-read-and-write-to-files-in-isolated-storage.md)|Содержит пример записи строки в файл изолированного хранилища и его чтения.|
|[Практическое руководство. Удаление файлов и каталогов из изолированного хранилища](../../../docs/standard/io/how-to-delete-files-and-directories-in-isolated-storage.md)|Пример удаления файлов и каталогов в изолированном хранилище.|
|[Файловый и потоковый ввод-вывод](../../../docs/standard/io/index.md)|Описание способов выполнения синхронного и асинхронного доступа к файлам и доступа к данным потока.|

<a name="reference"></a>

## <a name="reference"></a>Ссылки

- <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=nameWithType>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream?displayProperty=nameWithType>

- <xref:System.IO.IsolatedStorage.IsolatedStorageScope?displayProperty=nameWithType>
