---
title: Метод ICorDebugController::HasQueuedCallbacks
ms.date: 03/30/2017
api_name:
- ICorDebugController.HasQueuedCallbacks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::HasQueuedCallbacks
helpviewer_keywords:
- HasQueuedCallbacks method [.NET Framework debugging]
- ICorDebugController::HasQueuedCallbacks method [.NET Framework debugging]
ms.assetid: 0d6a1cd9-370b-4462-adbf-e3980e897ea7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ce6ad24e5e670db21d3a6942ab4650a68ae44568
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61749559"
---
# <a name="icordebugcontrollerhasqueuedcallbacks-method"></a>Метод ICorDebugController::HasQueuedCallbacks
Получает значение, указывающее ли любой управляемый оно для указанного потока.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT HasQueuedCallbacks (  
    [in] ICorDebugThread *pThread,  
    [out] BOOL           *pbQueued  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `pThread`  
 [in] Указатель на объект «ICorDebugThread», представляющий поток.  
  
 `pbQueued`  
 [out] Указатель на значение, являющееся `true` в случае любого управляемого обратные вызовы в настоящее время в очереди для указанного потока, в противном случае — `false`.  
  
 Если указано значение null для `pThread` параметра `HasQueuedCallbacks` вернет `true` Если в настоящий момент управляемый обратные вызовы в очередь для любого потока.  
  
## <a name="remarks"></a>Примечания  
 Обратные вызовы будут отправляемой поочередно, каждый раз [ICorDebugController::Continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) вызывается. Отладчик может установить этот флаг, если он хочет получить отчет несколько отладочных событий, которые выполняются одновременно.  
  
 При отладке события находятся в очереди, они уже произошли, поэтому отладчик должен обработать всю очередь, чтобы о состоянии отлаживаемой программы. (Вызов `ICorDebugController::Continue` для очистки очереди.) Например, если очередь содержит два события отладки потока *X*, и отладчик приостанавливает поток *X* после первого события отладки, а затем вызывает `ICorDebugController::Continue`, второе событие отладки для поток *X* несмотря на то, что поток был приостановлен, будут переданы.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также
