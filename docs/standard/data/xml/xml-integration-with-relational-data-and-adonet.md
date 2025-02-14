---
title: Интеграция XML с реляционными данными и ADO.NET
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: f6ebb1a1-f2ca-49b9-92c9-0150940cf6e6
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 93b414eea5849ed020b521fcd5e5d5f5d194c35f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64589805"
---
# <a name="xml-integration-with-relational-data-and-adonet"></a>Интеграция XML с реляционными данными и ADO.NET
Класс **XmlDataDocument** является производным от класса **XmlDocument** и содержит XML-данные. Класс **XmlDataDocument** полезен тем, что он организует связь между реляционными и иерархическими данными. Этот класс **XmlDocument** можно привязать к объекту **DataSet**, после чего любые изменения их данных будут одновременно отображаться в обоих классах. Класс **XmlDocument**, привязанный к объекту **DataSet**, позволяет интегрировать XML-данные с реляционными данными, не преобразуя все данные в формат XML или в реляционный формат. Можно использовать оба формата, не ограничиваясь единым способом представления данных.  
  
 Доступность двух представлений данных дает следующие преимущества.  
  
- Структурированную часть XML-документа можно сопоставить с набором данных и эффективным образом хранить, индексировать и использовать в поиске.  
  
- В XML-данных, хранимых в реляционном формате, можно эффективно выполнять преобразования, проверку и навигацию с помощью модели курсора. Иногда в реляционных структурах эти операции выполняются более эффективно, чем для XML-данных, хранящихся в модели **XmlDocument**.  
  
- Объект **DataSet** может хранить часть XML-документа. Это значит, что с помощью **XPath** или **XslTransform** можно сохранять в объекте **DataSet** только нужные элементы и атрибуты. Это позволяет внести изменения в отфильтрованный набор данных меньшего размера, а затем передать изменения в более крупный набор данных **XmlDataDocument**.  
  
 Также вы можете преобразовать данные, загруженные в объект **DataSet** из SQL Server. Есть и еще один вариант: привязать элементы управления WinForm и WebForm, управляемые классами платформы .NET Framework, к объекту **DataSet**, который заполнен из потока входных XML-данных.  
  
 Помимо поддержки класса **XslTransform**, класс **XmlDataDocument** предоставляет доступ к реляционным данным для запросов **XPath** и проверки.  Для реляционных данных, в основном, доступны все XML-службы, а реляционные средства, такие как привязка элементов управления, CodeGen и т. д., доступны с помощью структурированной проекции XML-данных без нарушения их точности.  
  
 Так как класс **XmlDataDocument** наследуется от класса **XmlDocument**, он содержит реализацию модели W3C DOM. Тот факт, что класс **XmlDataDocument** связан с объектом **DataSet** и хранит в нем часть своих данных, ни в коей мере не ограничивает и не изменяет его использование в качестве класса **XmlDocument**. Код, написанный для обработки событий класса **XmlDocument**, работает с классом **XmlDataDocument** без изменений. Объект **DataSet** обеспечивает реляционное представление тех же данных, определяя таблицы, столбцы, связи и ограничения, и является изолированным хранилищем пользовательских данных в памяти.  
  
 На рисунке ниже показаны различные связи между XML-данными, объектом **DataSet** и классом **XmlDataDocument**. 
  
 ![Схема, иллюстрирующая разные связи с объектом XML DataSet.](./media/xml-integration-with-relational-data-and-adonet/xml-integration-relational-data-adodotnet.gif)  
  
 На рисунке вы видите, что XML-данные можно загрузить непосредственно в объект **DataSet**, что позволяет использовать реляционные методы для работы с ними. Также XML-данные можно загрузить в класс **XmlDataDocument**, производный от модели DOM, а затем загрузить в объект **DataSet** и синхронизировать. Поскольку объект **DataSet** и класс **XmlDataDocument** синхронизируются по одному набору данных, то все изменения в любом из этих хранилищ отражаются и в другом хранилище.  
  
 Класс **XmlDataDocument** наследует все возможности редактирования и навигации из класса **XmlDocument**. Бывают случаи, когда использование класса **XmlDataDocument** с его наследуемыми возможностями и синхронизация с объектом **DataSet** оказываются более предпочтительным вариантом, чем загрузка XML-данных непосредственно в объект **DataSet**. В следующей таблице перечислены аспекты, которые нужно учитывать при выборе метода загрузки для объекта **DataSet**.  
  
|Причины для загрузки XML-данных непосредственно в объект DataSet|Причины для синхронизации класса XmlDataDocument с объектом DataSet|  
|----------------------------------------------|-----------------------------------------------------------|  
|Запросы к данным в объекте **DataSet** проще выполнять через SQL, чем через XPath.|Необходимо использовать запросы XPath к данным в объекте **DataSet**.|  
|Не обязательно сохранять порядок элементов в исходном XML-коде.|Важно сохранять порядок элементов в исходном XML-коде.|  
|Не нужно сохранять пробелы между элементами и форматированием в исходном XML-коде.|Важно сохранять пробелы и форматирование в исходном XML-коде.|  
  
 Если непосредственная загрузка XML-данных в объект и из объекта **DataSet** соответствует поставленным задачам, изучите документацию о [загрузке DataSet из XML](../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md) и [записи DataSet в виде XML](../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md).  
  
 Если нужно загружать данные в объект **DataSet** из класса **XmlDataDocument**, переходите к документу [о синхронизации объекта DataSet с XML-документом](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md).  
  
## <a name="see-also"></a>См. также

- [Использование XML в наборах данных](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)
