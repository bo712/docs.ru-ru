---
title: Практическое руководство. Как представить столбцы в виде членов класса
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7ab28021-4d15-4d9c-bf2e-6ccc0daa7d1a
ms.openlocfilehash: 009da2579a6fe15cea3913ae5844fc886da2586c
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910744"
---
# <a name="how-to-represent-columns-as-class-members"></a>Практическое руководство. Как представить столбцы в виде членов класса
Используйте [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Mapping.ColumnAttribute> атрибут для связи поля или свойства со столбцом базы данных.  
  
### <a name="to-map-a-field-or-property-to-a-database-column"></a>Сопоставление поля или свойства со столбцом база данных  
  
- Добавьте атрибут <xref:System.Data.Linq.Mapping.ColumnAttribute> в объявление свойства или поля.  
  
## <a name="example"></a>Пример  
 В следующем коде поле `CustomerID` в классе `Customer` сопоставляется со столбцом `CustomerID` в таблице базы данных `Customers`.  
  
 [!code-csharp[DLinqCustomize#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#2)]
 [!code-vb[DLinqCustomize#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#2)]  
  
 Если можно определить имя, указывать свойство <xref:System.Data.Linq.Mapping.DataAttribute.Name%2A> нет необходимости. Если имя не указано, оно будет считаться совпадающим с именем свойства или поля.  
  
## <a name="see-also"></a>См. также

- [Модель объектов LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)
- [Практическое руководство. Настройка классов сущностей с помощью редактора кода](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)
