---
title: Метод ICorProfilerCallback4::GetReJITParameters
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.GetReJITParameters
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::GetReJITParameters
helpviewer_keywords:
- ICorProfilerCallback4::GetReJITParameters method [.NET Framework profiling]
- GetReJITParameters method, ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 0e9bfe07-9f20-498c-b568-9017c8f6056c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ca176be93b92e44228d9b4063e87a62263e83e04
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61782510"
---
# <a name="icorprofilercallback4getrejitparameters-method"></a>Метод ICorProfilerCallback4::GetReJITParameters
Позволяет задать флаги создания альтернативного кода для нового тела метода перекомпилированной профилировщику кода.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetReJITParameters(     [in] ModuleID moduleId,     [in] mdMethodDef methodId,     [in] ICorProfilerFunctionControl *pFunctionControl);  
```  
  
## <a name="parameters"></a>Параметры  
 `moduleID`  
 [in] Модуль, содержащий метод, для которой среда CLR требуются параметры перекомпиляции JIT.  
  
 `methodId`  
 [in] `MethodDef` Метода, для которой среда CLR требуются параметры перекомпиляции JIT.  
  
 `pFunctionControl`  
 [in] Указатель на [ICorProfilerFunctionControl](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-interface.md) интерфейс, который можно использовать профилировщик для предоставления сведений о перекомпиляции JIT для метода в процессе повторной компиляции.  
  
## <a name="remarks"></a>Примечания  
 Проблемы со средой CLR `GetReJITParameters` обратного вызова, профилировщик можно указать параметры для повторной компиляции указанного метода. `GetReJITParameters` Каждой функцией обратного вызова выдается только один раз; параметрами, предоставленными профилировщик применяются ко всем экземплярам этой функции.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [Интерфейс ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md)
- [Метод JITCompilationStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md)
- [Метод ReJITCompilationStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-rejitcompilationstarted-method.md)
