---
title: Метод ICorDebugStepper::Step
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.Step
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::Step
helpviewer_keywords:
- Step method, ICorDebugStepper interface [.NET Framework debugging]
- ICorDebugStepper::Step method [.NET Framework debugging]
ms.assetid: 38c1940b-ada1-40ba-8295-4c0833744e1e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 444390622ca68244661b91dc85814b05556b12a2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61994322"
---
# <a name="icordebugstepperstep-method"></a>Метод ICorDebugStepper::Step
Принуждает ICorDebugStepper выполнить один шаг через содержащую и при необходимости, чтобы продолжить, при пошаговом выполнении функций, которые вызываются в потоке.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT Step (  
    [in] BOOL   bStepIn  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `bStepIn`  
 [in] Значение `true` на шаг с заходом в функцию, которая вызывается в потоке. Значение `false` на шаг с обходом функции.  
  
## <a name="remarks"></a>Примечания  
 Когда среда CLR выполняет следующую инструкцию управляемого кода в кадре средства пошагового завершения этого шага. Если `Step` является вызывается для средства пошагового, который не находится в управляемом коде, шаг будет выполнен при выполнении следующей инструкции управляемого кода в потоке.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
