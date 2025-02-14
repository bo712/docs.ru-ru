---
title: disconnectedContext MDA
ms.date: 03/30/2017
helpviewer_keywords:
- DisconnectedContext MDA
- MDAs (managed debugging assistants), disconnected context
- dead context
- transitioning disconnected apartment or context
- context disconnections
- managed debugging assistants (MDAs), disconnected context
ms.assetid: 1887d31d-7006-4491-93b3-68fd5b05f71d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: cb42c04df6e02ff43421b7af6bf2d51b53aa3e69
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61755133"
---
# <a name="disconnectedcontext-mda"></a>disconnectedContext MDA
Помощник отладки управляемого кода `disconnectedContext` (MDA) активируется, когда среда CLR пытается перейти в отключенное подразделение или контекст во время обслуживания запроса, связанного с COM-объектом.  
  
## <a name="symptoms"></a>Симптомы  
 Вызовы, выполняемые для [вызываемой оболочки времени выполнения](../../../docs/framework/interop/runtime-callable-wrapper.md) (RCW), направляются в базовый компонент COM в текущем подразделении или контексте вместо того, где они существуют. Это может привести к повреждению или потере данных, если компонент COM не является многопоточным, как в случае с компонентами однопотокового подразделения (STA). Кроме того, если сама вызываемая оболочка времени выполнения является прокси-сервером, вызов может привести к возникновению исключения <xref:System.Runtime.InteropServices.COMException> с HRESULT RPC_E_WRONG_THREAD.  
  
## <a name="cause"></a>Причина  
 Работа контекста или подразделения OLE была завершена, когда среда CLR попыталась перейти в них. Чаще всего это вызвано завершением работы однопотоковых подразделений до полного освобождения всех компонентов COM, принадлежащих этому подразделению. Это может произойти в результате явного вызова из пользовательского кода в вызываемой оболочке времени выполнения либо во время работы среды CLR с этим компонентом COM, например, когда среда CLR освобождает компонент COM после сборки мусора для соответствующей вызываемой оболочки времени выполнения.  
  
## <a name="resolution"></a>Решение  
 Чтобы избежать этой проблемы, убедитесь, что поток, которому принадлежит однопотоковое подразделение, не завершает работу до тех пор, пока приложение не завершит обработку всех объектов, находящихся в подразделении. То же самое касается и контекстов — убедитесь, что контексты не завершают работу до тех пор, пока приложение не завершит обработку всех COM-объектов, находящихся в этом контексте.  
  
## <a name="effect-on-the-runtime"></a>Влияние на среду выполнения  
 Этот помощник отладки управляемого кода не оказывает никакого влияния на среду CLR. Он только выводит данные об отключенном контексте.  
  
## <a name="output"></a>Вывод  
 Указание файла cookie контекста для отключенного подразделения или контекста.  
  
## <a name="configuration"></a>Параметр Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <disconnectedContext />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>См. также

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Диагностика ошибок посредством помощников по отладке управляемого кода](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [Маршалинг взаимодействия](../../../docs/framework/interop/interop-marshaling.md)
