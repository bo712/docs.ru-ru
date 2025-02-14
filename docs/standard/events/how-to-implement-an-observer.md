---
title: Как выполнить Реализация наблюдателя
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- observers [.NET Framework], observer design pattern
- observer design pattern [.NET Framework], implementing observers
ms.assetid: 8ecfa9f5-b500-473d-bcf0-5652ffb1e53d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b410b9381246cef2e61086e333c4c5b07646a575
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59301065"
---
# <a name="how-to-implement-an-observer"></a>Как выполнить Реализация наблюдателя
Шаблон разработки наблюдателя подразумевает разделение ролей наблюдателя, который регистрируется для получения уведомлений, и поставщика, который отслеживает данные и отправляет уведомления одному или нескольким наблюдателям. В этой статье объясняется, как создать наблюдатель. Создание поставщика рассматривается в связанной статье [Практическое руководство. Реализация поставщика](../../../docs/standard/events/how-to-implement-a-provider.md).  
  
### <a name="to-create-an-observer"></a>Создание наблюдателя  
  
1. Определите наблюдатель в виде типа, реализующего интерфейс <xref:System.IObserver%601?displayProperty=nameWithType>. Например, в следующем примере кода определяется тип с именем `TemperatureReporter`, представляющий собой реализацию <xref:System.IObserver%601?displayProperty=nameWithType> с аргументом универсального типа `Temperature`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#8)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#8)]  
  
2. Если наблюдатель может прекратить получение уведомлений до вызова поставщиком его реализации <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>, определите частную переменную, которая будет содержать реализацию <xref:System.IDisposable>, полученную из метода <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> поставщика. Также следует определить метод подписки, который вызывает метод <xref:System.IObservable%601.Subscribe%2A> поставщика и сохраняет возвращенный объект <xref:System.IDisposable>. Например, следующий код определяет закрытую переменную с именем `unsubscriber` и определяет метод `Subscribe`, который вызывает метод <xref:System.IObservable%601.Subscribe%2A> поставщика и назначает возвращенный объект переменной `unsubscriber`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#9)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#9)]  
  
3. Определите метод, позволяющий наблюдателю прекратить получение уведомлений до вызова поставщиком его реализации <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>, если вам нужна такая функциональность. В следующем примере определяется метод `Unsubscribe`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#10)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#10)]  
  
4. Предоставьте реализацию трех методов, определяемых интерфейсом <xref:System.IObserver%601>: <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>, <xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType> и <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>. В зависимости от поставщика и задач приложения, для методов <xref:System.IObserver%601.OnError%2A> и <xref:System.IObserver%601.OnCompleted%2A> можно использовать заглушки. Обратите внимание, что метод <xref:System.IObserver%601.OnError%2A> не должен обрабатывать переданный объект <xref:System.Exception> как исключение, а метод <xref:System.IObserver%601.OnCompleted%2A> может вызывать реализацию <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> поставщика. В приведенном ниже примере показана реализация <xref:System.IObserver%601> для класса `TemperatureReporter`.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#11)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#11)]  
  
## <a name="example"></a>Пример  
 Ниже представлен полный пример исходного кода для класса `TemperatureReporter`, который предоставляет реализацию <xref:System.IObserver%601> для приложения мониторинга температуры.  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#12)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#12)]  
  
## <a name="see-also"></a>См. также

- <xref:System.IObserver%601>
- [Шаблон разработки наблюдателя](../../../docs/standard/events/observer-design-pattern.md)
- [Практическое руководство. Реализация поставщика](../../../docs/standard/events/how-to-implement-a-provider.md)
- [Рекомендации по шаблону разработки Observer](../../../docs/standard/events/observer-design-pattern-best-practices.md)
