---
title: Практическое руководство. Создание предварительно вычисленных задач
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, creating pre-computed
ms.assetid: a73eafa2-1f49-4106-a19e-997186029b58
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5e68465b6fae39089600457414e7f2a2328f725b
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593122"
---
# <a name="how-to-create-pre-computed-tasks"></a>Практическое руководство. Создание предварительно вычисленных задач
В этом документе описывается способ использования метода <xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=nameWithType> для получения результатов асинхронных операций загрузки, удерживаемых в кэше. Метод <xref:System.Threading.Tasks.Task.FromResult%2A> возвращает завершенный объект <xref:System.Threading.Tasks.Task%601>, содержащий предоставленное значение как свойство <xref:System.Threading.Tasks.Task%601.Result%2A>. Этот метод полезен тогда, когда выполняется асинхронная операция, возвращающая объект <xref:System.Threading.Tasks.Task%601>, и результат этого объекта <xref:System.Threading.Tasks.Task%601> уже вычислен.  
  
## <a name="example"></a>Пример  
 В следующем примере загружаются строки из Интернета. Здесь определяется метод `DownloadStringAsync`. Этот метод загружает строки из Интернета асинхронным образом. В этом примере также используется объект <xref:System.Collections.Concurrent.ConcurrentDictionary%602> для кэширования результатов предыдущих операций. Если введенный адрес хранится в этом кэше, `DownloadStringAsync` использует метод <xref:System.Threading.Tasks.Task.FromResult%2A> для создания объекта <xref:System.Threading.Tasks.Task%601>, содержащего содержимое этого адреса. В противном случае `DownloadStringAsync` загружает файл из Интернета и добавляет результат в кэш.  
  
 [!code-csharp[TPL_CachedDownloads#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cacheddownloads/cs/cacheddownloads.cs#1)]
 [!code-vb[TPL_CachedDownloads#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cacheddownloads/vb/cacheddownloads.vb#1)]  
  
 В этом примере вычисляется время, необходимое для загрузки нескольких строк дважды. Второй набор операций загрузки должен занимать меньше времени, чем первый набор, поскольку результаты хранятся в кэше. Метод <xref:System.Threading.Tasks.Task.FromResult%2A> позволяет методу `DownloadStringAsync` создавать объекты <xref:System.Threading.Tasks.Task%601>, которые содержат эти предварительно вычисленные результаты.  
  
## <a name="see-also"></a>См. также

- [Асинхронное программирование на основе задач](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
