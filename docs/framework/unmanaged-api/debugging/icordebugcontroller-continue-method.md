---
title: Метод ICorDebugController::Continue
ms.date: 03/30/2017
api_name:
- ICorDebugController.Continue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Continue
helpviewer_keywords:
- Continue method [.NET Framework debugging]
- ICorDebugController::Continue method [.NET Framework debugging]
ms.assetid: 8684cd06-ad3e-48ef-832e-15320e1f43a2
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7eacffe5769bc77ab626f6adbc99db1137da565f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61749674"
---
# <a name="icordebugcontrollercontinue-method"></a>Метод ICorDebugController::Continue
Возобновляет выполнение управляемых потоков после вызова [метод Stop](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-stop-method.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT Continue (  
    [in] BOOL fIsOutOfBand  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `fIsOutOfBand`  
 [in] Значение `true` в событие каналу; в противном случае значение `false`.  
  
## <a name="remarks"></a>Примечания  
 `Continue` Продолжение процесса после вызова `ICorDebugController::Stop` метод.  
  
 При выполнении отладки в смешанном режиме, не следует вызывать `Continue` на Win32 событий потоков, если не является продолжением-внешнее событие.  
  
 *События внутри диапазона* управляемое событие или обычное неуправляемое событие во время которого отладчик поддерживает взаимодействие с управляемым состоянием процесса. В этом случае отладчик получает [ICorDebugUnmanagedCallback::DebugEvent](../../../../docs/framework/unmanaged-api/debugging/icordebugunmanagedcallback-debugevent-method.md) обратного вызова с его `fOutOfBand` параметру присвоить `false`.  
  
 *-Внешнее событие* — это неуправляемых событий во время которого взаимодействие с управляемым состоянием процесса невозможна, пока процесс будет остановлен из-за события. В этом случае отладчик получает `ICorDebugUnmanagedCallback::DebugEvent` обратного вызова с его `fOutOfBand` параметру присвоить `true`.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также
