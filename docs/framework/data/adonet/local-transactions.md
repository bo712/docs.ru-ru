---
title: Локальные транзакции
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ae3712f-ef5e-41a1-9ea9-b3d0399439f1
ms.openlocfilehash: f686c20a9afd981405e32854fcc594abac78c85c
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2019
ms.locfileid: "65882029"
---
# <a name="local-transactions"></a>Локальные транзакции
Транзакции в ADO.NET используются в том случае, если вы хотите объединить несколько задач, чтобы они выполнялись как одно целое. Например, пусть приложение выполняет две задачи. Во-первых, оно заносит в таблицу сведения о заказе. Во-вторых, обновляет таблицу, содержащую список товаров на складе, списывая заказанные элементы. При сбое любой задачи, затем оба обновления откатываются.  
  
## <a name="determining-the-transaction-type"></a>Определение типа транзакции  
 Транзакция считается локальной транзакции при состоит из одной фазы и обрабатывается непосредственно базой данных. Транзакция считается распределенной транзакции при координируется монитором транзакций и используется для разрешения транзакций резервные механизмы (например, двухфазную фиксацию).  
  
 Каждый из поставщиков данных .NET Framework имеет свой собственный `Transaction` объект для выполнения локальных транзакций. Если требуется выполнить транзакцию в базе данных SQL Server, выбирается транзакция <xref:System.Data.SqlClient>. Для транзакции Oracle используйте поставщик <xref:System.Data.OracleClient>. Кроме того, <xref:System.Data.Common.DbTransaction> класс, который доступен для написания независимого от поставщика кода, который требуется транзакций.  
  
> [!NOTE]
> Транзакции наиболее эффективны, если они выполняются на сервере. При работе с базой данных SQL Server, интенсивно использующей явные транзакции, следует рассмотреть возможность их записи в виде хранимых процедур при помощи инструкции Transact-SQL BEGIN TRANSACTION.
  
## <a name="performing-a-transaction-using-a-single-connection"></a>Выполнение транзакций с использованием одного соединения  
 В ADO.NET, вы управляете транзакции с `Connection` объекта. Инициировать транзакцию можно с помощью метода `BeginTransaction`. После начала транзакции при помощи свойства `Transaction` объекта `Command` к ней можно прикрепить команду. Затем в зависимости от успеха или ошибки компонентов транзакции можно зафиксировать или откатить изменения, сделанные в источнике данных.  
  
> [!NOTE]
>  Метод `EnlistDistributedTransaction` не должен использоваться для локальной транзакции.  
  
 Область действия транзакции ограничена соединением. В следующем примере выполняется явная транзакция, состоящая из двух отдельных команд в блоке `try`. Команды выполняют инструкции INSERT для таблицы Production.ScrapReason в образце базы данных AdventureWorks в SQL Server, которые будут зафиксированы при отсутствии исключений. При возникновении исключения код в блоке `catch` произведет откат транзакции. При отмене транзакции или обрыве соединения до выполнения транзакции она откатывается автоматически.  
  
## <a name="example"></a>Пример  
 Чтобы осуществить транзакцию, выполните указанные ниже действия.  
  
1. Вызовите метод <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> объекта <xref:System.Data.SqlClient.SqlConnection> для отметки начала транзакции. Метод <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A> возвращает ссылку на транзакцию. Эта ссылка назначается объектам <xref:System.Data.SqlClient.SqlCommand>, прикрепленным к транзакции.  
  
2. Присвойте объект `Transaction` свойству <xref:System.Data.SqlClient.SqlCommand.Transaction%2A> объекта <xref:System.Data.SqlClient.SqlCommand>. Исключение вызывается, если команда выполняется при соединении с активной транзакцией, а объект `Transaction` не был назначен свойству `Transaction` объекта `Command`.  
  
3. Выполните требуемые команды.  
  
4. Для выполнения транзакции вызовите метод <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> объекта <xref:System.Data.SqlClient.SqlTransaction>, для завершения транзакции вызовите метод <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A>. Транзакция откатывается, если соединение закрывается или пропадает до выполнения метода <xref:System.Data.SqlClient.SqlTransaction.Commit%2A> либо <xref:System.Data.SqlClient.SqlTransaction.Rollback%2A>.  
  
 В следующем примере кода демонстрирует транзакционную логику, с помощью ADO.NET с Microsoft SQL Server.  
  
 [!code-csharp[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTransaction.Local#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTransaction.Local/VB/source.vb#1)]  
  
## <a name="see-also"></a>См. также

- [Транзакции и параллельность](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)
- [Распределенные транзакции](../../../../docs/framework/data/adonet/distributed-transactions.md)
- [Интеграция System.Transactions с SQL Server](../../../../docs/framework/data/adonet/system-transactions-integration-with-sql-server.md)
- [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](https://go.microsoft.com/fwlink/?LinkId=217917)
