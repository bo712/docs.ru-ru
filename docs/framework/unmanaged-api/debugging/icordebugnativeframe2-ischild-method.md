---
title: Метод ICorDebugNativeFrame2::IsChild
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2.IsChild Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2::IsChild
helpviewer_keywords:
- IsChild method [.NET Framework debugging]
- ICorDebugNativeFrame2::IsChild method [.NET Framework debugging]
ms.assetid: 9e2aae09-49cb-4fbd-81e5-e29cd864a88b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9503c12da9e98fbd43f3904aad25c5d10655cec2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61994647"
---
# <a name="icordebugnativeframe2ischild-method"></a>Метод ICorDebugNativeFrame2::IsChild
Определяет, является ли текущий кадр дочерним.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT IsChild([out] BOOL * pIsChild);  
```  
  
## <a name="parameters"></a>Параметры  
 `pIsChild`  
 [out] Логическое значение, указывающее, является ли текущий кадр дочерним.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Этот метод возвращает следующие конкретные результаты HRESULT, а также ошибки HRESULT, которые указывают на сбой метода.  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|S_OK|Состояние дочернего был успешно возвращен.|  
|E_FAIL|Состояние дочернего не могут быть возвращены.|  
|E_INVALIDARG|Параметр `pIsChild` имеет значение null.|  
  
## <a name="exceptions"></a>Исключения  
  
## <a name="remarks"></a>Примечания  
 `IsChild` Возвращает метод `true` Если объект кадра, для которого вызван метод является потомком другого кадра. Если это так, используйте [IsMatchingParentFrame](../../../../docs/framework/unmanaged-api/debugging/icordebugnativeframe2-ismatchingparentframe-method.md) метод для проверки, является ли кадр родительской.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorDebugNativeFrame2](../../../../docs/framework/unmanaged-api/debugging/icordebugnativeframe2-interface.md)
- [Интерфейсы отладки](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [Отладка](../../../../docs/framework/unmanaged-api/debugging/index.md)
