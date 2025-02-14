---
title: Метод ICorDebugProcess::GetHelperThreadID
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetHelperThreadID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetHelperThreadID
helpviewer_keywords:
- GetHelperThreadID method [.NET Framework debugging]
- ICorDebugProcess::GetHelperThreadID method [.NET Framework debugging]
ms.assetid: 84e1e605-37c1-49a5-8e12-35db85654622
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cd5e30d08e667dcd5a8be1f9502462f28290068e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61987744"
---
# <a name="icordebugprocessgethelperthreadid-method"></a>Метод ICorDebugProcess::GetHelperThreadID
Получает идентификатор потока операционной системы (ОС) внутреннего вспомогательного потока отладчика.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetHelperThreadID (  
    [out] DWORD *pThreadID  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `pThreadID`  
 [out] Идентификатор внутреннего вспомогательного потока отладчика потока в указатель на ОС.  
  
## <a name="remarks"></a>Примечания  
 Во время отладки управляемых и неуправляемых отвечает за отладчика убедитесь, что непрерывное выполнение потока с указанным Идентификатором при его попадании в точку останова, размещенную отладчиком. Отладчик может возникнуть необходимость скрыть этот поток от пользователя. Если существует вспомогательного потока в процессе, тем не менее, `GetHelperThreadID` метод возвращает нуль в *`pThreadID`.  
  
 Идентификатор потока вспомогательного потока кэшировать нельзя, поскольку со временем может меняться. Необходимо повторно запрашивать идентификатор потока при каждом событии остановки.  
  
 Идентификатор вспомогательного потока отладчика будет корректироваться при каждой неуправляемой [ICorDebugManagedCallback::CreateThread](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-createthread-method.md) событий, что позволяет отладчику определить идентификатор вспомогательного потока и скрыть его от пользователя. Поток, который указан в качестве вспомогательного потока во время неуправляемую `ICorDebugManagedCallback::CreateThread` событие никогда не будет выполняться управляемый пользовательский код.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug.idl. CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
