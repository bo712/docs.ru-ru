---
title: Выполнение команды
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
ms.openlocfilehash: c3ed424aff3cd485a78d26a7f27bc5b1eac66448
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61879415"
---
# <a name="executing-a-command"></a>Выполнение команды
Каждый поставщик данных .NET Framework, включенный в состав .NET Framework, имеет собственный объект команды, наследуемый от <xref:System.Data.Common.DbCommand>. Поставщик данных .NET Framework для OLE DB содержит объект <xref:System.Data.OleDb.OleDbCommand>, поставщик данных .NET Framework для SQL Server - объект <xref:System.Data.SqlClient.SqlCommand>, поставщик данных .NET Framework для ODBC - объект <xref:System.Data.Odbc.OdbcCommand>, а поставщик данных .NET Framework для Oracle - объект <xref:System.Data.OracleClient.OracleCommand>. Каждый из этих объектов предоставляет методы выполнения команд с учетом типа команды и требуемого возвращаемого значения, как описано в следующей таблице.  
  
|Команда|Возвращаемое значение|  
|-------------|------------------|  
|`ExecuteReader`|Возвращает объект `DataReader`.|  
|`ExecuteScalar`|Возвращает одно скалярное значение.|  
|`ExecuteNonQuery`|Выполняет команду, которая не возвращает строк.|  
|`ExecuteXMLReader`|Возвращает значение типа <xref:System.Xml.XmlReader>. Этот метод предусмотрен только для объекта `SqlCommand`.|  
  
 Каждый строго типизированный объект команды поддерживает также перечисление <xref:System.Data.CommandType>, которое указывает способ интерпретации строки команды, как описано в следующей таблице.  
  
|CommandType|Описание|  
|-----------------|-----------------|  
|`Text`|Команда SQL, определяющая инструкции, которые выполняются применительно к источнику данных.|  
|`StoredProcedure`|Имя хранимой процедуры. Свойство команды `Parameters` может использоваться для доступа к входным и выходным параметрам и возвращаемым значениям независимо от вызываемого метода `Execute`. При использовании `ExecuteReader` возвращаемые значения и выходные параметры будут недоступными, пока не будет закрыт `DataReader`.|  
|`TableDirect`|Имя таблицы.|  
  
## <a name="example"></a>Пример  
 Следующий пример кода демонстрирует способ создания объекта <xref:System.Data.SqlClient.SqlCommand> для выполнения хранимой процедуры путем установки его свойств. Объект <xref:System.Data.SqlClient.SqlParameter> используется для задания входных параметров хранимой процедуры. Команда выполняется с помощью метода <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A>, и выходное значение из <xref:System.Data.SqlClient.SqlDataReader> отображается в окне консоли.  
  
 [!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]  
  
### <a name="troubleshooting-commands"></a>Команды устранения неполадок  
 Поставщик данных .NET Framework для SQL Server добавляет счетчики производительности, позволяя обнаруживать периодически возникающие проблемы, связанные со сбоями команд. Дополнительные сведения см. в разделе [счетчики производительности](../../../../docs/framework/data/adonet/performance-counters.md).  
  
## <a name="see-also"></a>См. также

- [Команды и параметры](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [Объекты DataAdapter и DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [Общие сведения об ADO.NET](ado-net-overview.md)
