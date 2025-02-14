---
title: Параметры DataAdapter
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
ms.openlocfilehash: 0cdca872e9e76b7491dc571209292a692a06d8f8
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65583750"
---
# <a name="dataadapter-parameters"></a>Параметры DataAdapter
Класс <xref:System.Data.Common.DbDataAdapter> имеет четыре свойства, которые служат для получения данных из источника данных и обновления данных в нем: свойство <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> возвращает данные из источника данных, а свойства <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>, <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> и <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> используются для управления изменениями в источнике данных. Свойство `SelectCommand` должно быть установлено до вызова метода `Fill` объекта `DataAdapter`. Свойства `InsertCommand`, `UpdateCommand` или `DeleteCommand` должны быть установлены до вызова метода `Update` объекта `DataAdapter` в зависимости от того, какие изменения были сделаны в данных в <xref:System.Data.DataTable>. Например, если добавлены строки, свойство `InsertCommand` должно быть установлено перед вызовом метода `Update`. Если метод `Update` обрабатывает вставленную, обновленную или удаленную строку, `DataAdapter` использует соответствующее свойство `Command` для обработки действия. Текущие данные об измененной строке передаются в объект `Command` через коллекцию `Parameters`.  
  
 При обновлении строки в источнике данных вызывается инструкция UPDATE, которая использует уникальный идентификатор для идентификации строки в таблице, чтобы обновить. Уникальным идентификатором обычно является значение поля первичного ключа. Инструкция UPDATE использует параметры, содержащие и уникальный идентификатор, и столбцы и обновляемые значения, как показано в следующей инструкции Transact-SQL.  
  
```sql
UPDATE Customers SET CompanyName = @CompanyName   
  WHERE CustomerID = @CustomerID  
```  
  
> [!NOTE]
>  Синтаксис местозаполнителей параметров зависит от источника данных. В этом примере показаны местозаполнители для источника данных SQL Server. Для параметров <xref:System.Data.OleDb> и <xref:System.Data.Odbc> в качестве местозаполнителей используйте вопросительный знак (?).  
  
 В этом примере Visual Basic `CompanyName` обновляется значение `@CompanyName` для строки где `CustomerID` равен значению `@CustomerID` параметра. Параметры получают данные из измененной строки, используя <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A> свойство <xref:System.Data.SqlClient.SqlParameter> объекта. Далее представлены параметры для предыдущего образца инструкции UPDATE. В коде предполагается, что переменная `adapter` представляет действительный объект <xref:System.Data.SqlClient.SqlDataAdapter>.  
  
```vb
adapter.Parameters.Add( _  
  "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
Dim parameter As SqlParameter = _  
  adapter.UpdateCommand.Parameters.Add("@CustomerID", _  
  SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
```  
  
 Метод `Add` коллекции `Parameters` принимает имя параметра, тип данных, размер (если он применим к типу) и имя <xref:System.Data.Common.DbParameter.SourceColumn%2A> из `DataTable`. Обратите внимание, что <xref:System.Data.Common.DbParameter.SourceVersion%2A> параметра `@CustomerID` установлена в `Original`. Это гарантирует, что существующая строка в источнике данных обновляется, если значение идентифицирующих столбцов изменилось в измененном <xref:System.Data.DataRow>. В этом случае значение строки `Original` будет соответствовать текущему значению в источнике данных и значение строки `Current` будет содержать обновленное значение. `SourceVersion` для параметра `@CompanyName` не установлена и использует значение по умолчанию строки `Current`.  
  
> [!NOTE]
>  Для обоих `Fill` операций `DataAdapter` и `Get` методы `DataReader`, тип .NET Framework выводится из типа, возвращаемого из поставщика данных .NET Framework. Выводимые типы .NET Framework и методы доступа для типов данных Microsoft SQL Server, OLE DB и ODBC описываются в [сопоставления типов данных в ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md).  
  
## <a name="parametersourcecolumn-parametersourceversion"></a>Parameter.SourceColumn, Parameter.SourceVersion  
 `SourceColumn` и `SourceVersion` могут быть посланы как аргументы в конструктор `Parameter` или установлены как свойства существующих `Parameter`. `SourceColumn` является именем <xref:System.Data.DataColumn> из <xref:System.Data.DataRow>, где значение `Parameter` будет получено. `SourceVersion` задает версию `DataRow`, которую `DataAdapter` использует для получения значения.  
  
 В следующей таблице показаны значения перечисления <xref:System.Data.DataRowVersion>, доступные для использования с `SourceVersion`.  
  
|Перечисление DataRowVersion|Описание|  
|--------------------------------|-----------------|  
|`Current`|Параметр использует текущее значение столбца. Это значение по умолчанию.|  
|`Default`|Параметр использует `DefaultValue` столбца.|  
|`Original`|Параметр использует исходное значение столбца.|  
|`Proposed`|Параметр использует предложенное значение.|  
  
 В примере кода для `SqlClient` в следующем разделе определяется параметр для <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A>, в котором столбец `CustomerID` используется как `SourceColumn` для двух параметров: `@CustomerID` (`SET CustomerID = @CustomerID`) и `@OldCustomerID` (`WHERE CustomerID = @OldCustomerID`). `@CustomerID` Параметр используется для обновления **CustomerID** текущее значение в столбце `DataRow`. В результате `CustomerID` `SourceColumn` с `SourceVersion` из `Current` используется. `@OldCustomerID` Параметр используется для идентификации текущей строки в источнике данных. Так как в версии `Original` строки найдено значение, совпадающее со значением столбца, используется тот же `SourceColumn` (`CustomerID`) с `SourceVersion` для `Original`.  
  
## <a name="working-with-sqlclient-parameters"></a>Работа с параметрами SqlClient  
 Следующий пример демонстрирует, как создать <xref:System.Data.SqlClient.SqlDataAdapter> и установить <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> в <xref:System.Data.MissingSchemaAction.AddWithKey>, чтобы получить из базы данных дополнительные сведения о схеме. Устанавливаются свойства <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> и <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A>, и соответствующие им объекты <xref:System.Data.SqlClient.SqlParameter> добавляются в коллекцию <xref:System.Data.SqlClient.SqlCommand.Parameters%2A>. Метод возвращает объект `SqlDataAdapter`.  
  
 [!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/CS/source.cs#1)]
 [!code-vb[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/VB/source.vb#1)]  
  
## <a name="oledb-parameter-placeholders"></a>Местозаполнители параметров OleDb  
 Для объектов <xref:System.Data.OleDb.OleDbDataAdapter> и <xref:System.Data.Odbc.OdbcDataAdapter> для идентификации параметров необходимо использовать в качестве местозаполнителей вопросительные знаки (?).  
  
```vb  
Dim selectSQL As String = _  
  "SELECT CustomerID, CompanyName FROM Customers " & _  
  "WHERE CountryRegion = ? AND City = ?"  
Dim insertSQL AS String = _  
  "INSERT INTO Customers (CustomerID, CompanyName) VALUES (?, ?)"  
Dim updateSQL AS String = _  
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " & _  
  WHERE CustomerID = ?"  
Dim deleteSQL As String = "DELETE FROM Customers WHERE CustomerID = ?"  
```  
  
```csharp  
string selectSQL =   
  "SELECT CustomerID, CompanyName FROM Customers " +  
  "WHERE CountryRegion = ? AND City = ?";  
string insertSQL =   
  "INSERT INTO Customers (CustomerID, CompanyName) " +  
  "VALUES (?, ?)";  
string updateSQL =   
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " +  
  "WHERE CustomerID = ? ";  
string deleteSQL = "DELETE FROM Customers WHERE CustomerID = ?";  
```  
  
 Инструкции параметризованных запросов определяют, какие входные и выходные параметры должны создаваться. Для создания параметра используйте метод `Parameters.Add` или конструктор `Parameter` для задания имени столбца, типа и размера данных. Для внутренних типов данных, таких как `Integer`, нет необходимости включать размер, либо можно указать размер по умолчанию.  
  
 В следующем примере кода создаются параметры для инструкции SQL, а затем заполняется `DataSet`.  
  
## <a name="oledb-example"></a>Пример OleDb  
  
```vb  
' Assumes that connection is a valid OleDbConnection object.  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter   
  
Dim selectCMD AS OleDbCommand = New OleDbCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add parameters and set values.  
selectCMD.Parameters.Add( _  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add( _  
  "@City", OleDbType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid OleDbConnection object.  
OleDbDataAdapter adapter = new OleDbDataAdapter();  
  
OleDbCommand selectCMD = new OleDbCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
// Add parameters and set values.  
selectCMD.Parameters.Add(  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add(  
  "@City", OleDbType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
## <a name="odbc-parameters"></a>Параметры Odbc  
  
```vb  
' Assumes that connection is a valid OdbcConnection object.  
Dim adapter As OdbcDataAdapter = New OdbcDataAdapter  
  
Dim selectCMD AS OdbcCommand = New OdbcCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid OdbcConnection object.  
OdbcDataAdapter adapter = new OdbcDataAdapter();  
  
OdbcCommand selectCMD = new OdbcCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
//Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
>  Если для параметра не указано имя параметра, параметр присваивается предусмотренное по умолчанию имя параметра*N* *,* начиная с имени «Parameter1». Рекомендуется избегать использования параметра*N* соглашение об именовании при указании имени параметра, поскольку такое имя может конфликтовать с именем существующего параметра по умолчанию в `ParameterCollection`. Если указанное имя уже существует, вызывается исключение.  
  
## <a name="see-also"></a>См. также

- [Объекты DataAdapter и DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [Команды и параметры](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [Обновление источников данных с объектами DataAdapter](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)
- [Изменение данных с помощью хранимых процедур](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)
- [Сопоставления типов данных в ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)
- [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](https://go.microsoft.com/fwlink/?LinkId=217917)
