---
title: Привязка данных и LINQ to DataSet
ms.date: 03/30/2017
ms.assetid: 310bff4a-32dd-4f20-a271-6dbd82912631
ms.openlocfilehash: b081a648023aa21eea3a20ec409600d3bcbe9878
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61607405"
---
# <a name="data-binding-and-linq-to-dataset"></a>Привязка данных и LINQ to DataSet
*Привязка данных* — это процесс, который устанавливает связь между Интерфейсом приложения и бизнес-логики. Если для привязки заданы правильные настройки, а изменения значений данных сопровождаются правильными уведомлениями, привязанные к данным элементы автоматически отражают изменения. Объект <xref:System.Data.DataSet> - это находящееся в памяти представление данных, обеспечивающее согласованную реляционную программную модель, независимо от источника содержащихся в нем данных. Объект <xref:System.Data.DataView> в ADO.NET 2.0 позволяет сортировать и фильтровать данные, хранящиеся в таблице <xref:System.Data.DataTable>. Эта функциональность часто используется в приложениях привязки данных. С помощью объекта <xref:System.Data.DataView> можно представлять данные в таблице с различными порядками сортировки, а также фильтровать данные по состоянию строки или на основе критерия фильтра. Дополнительные сведения о <xref:System.Data.DataView> объекта, см. в разделе [объекты DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md).  
  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] позволяет разработчикам создавать сложные и мощные запросы через <xref:System.Data.DataSet> с помощью [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)]. Тем не менее [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] запрос возвращает перечисление <xref:System.Data.DataRow> объекты, которые легко не используется в сценарии привязки. Для упрощения привязки можно создать <xref:System.Data.DataView> из [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] запроса. Это <xref:System.Data.DataView> использует параметры фильтрации и сортировки, указанные в запросе, но лучше подходит для привязки данных. [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] расширяет функциональность <xref:System.Data.DataView> , предоставляя [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] основано на выражении фильтрации и сортировки, что обеспечивает гораздо более сложные и мощные операции фильтрации и сортировки, чем строковые фильтрации и сортировки.  
  
 Обратите внимание, что объект <xref:System.Data.DataView> представляет непосредственно запрос, а не представление на основе запроса. Объект <xref:System.Data.DataView> привязывается к элементу управления в пользовательском интерфейсе, так же как и <xref:System.Windows.Forms.DataGrid> или <xref:System.Windows.Forms.DataGridView>, обеспечивая простую модель привязки данных. Объект <xref:System.Data.DataView> можно также создать на основе объекта <xref:System.Data.DataTable>, задав представление таблицы по умолчанию.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Создание объекта DataView](../../../../docs/framework/data/adonet/creating-a-dataview-object-linq-to-dataset.md)  
 Содержит сведения о создании объекта <xref:System.Data.DataView>.  
  
 [Фильтрация с использованием объекта DataView](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md)  
 Описывает фильтрацию с помощью объекта <xref:System.Data.DataView>.  
  
 [Сортировка с использованием объекта DataView](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md)  
 Описывает сортировку с помощью объекта <xref:System.Data.DataView>.  
  
 [Запрос к коллекции DataRowView в объекте DataView](../../../../docs/framework/data/adonet/querying-the-datarowview-collection-in-a-dataview.md)  
 Содержит сведения о запросах к коллекции <xref:System.Data.DataRowView>, предоставляемой объектом <xref:System.Data.DataView>.  
  
 [Производительность объекта DataView](../../../../docs/framework/data/adonet/dataview-performance.md)  
 Содержит сведения об объекте <xref:System.Data.DataView> и производительности.  
  
 [Практическое руководство. Связывание объекта DataView в элемент управления DataGridView Windows Forms](../../../../docs/framework/data/adonet/how-to-bind-a-dataview-object-to-a-winforms-datagridview-control.md)  
 Содержит описание процесса привязки объекта <xref:System.Data.DataView> к элементу управления <xref:System.Windows.Forms.DataGridView>.  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)
