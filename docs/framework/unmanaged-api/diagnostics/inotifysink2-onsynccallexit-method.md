---
title: Метод INotifySink2::OnSyncCallExit
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallExit
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallExit
helpviewer_keywords:
- INotifySink2::OnSyncCallExit method [.NET Framework debugging]
- OnSyncCallExit method [.NET Framework debugging]
ms.assetid: d9d7600e-a8f5-443a-96de-67d26e130f2d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9144ab7fc74bdb5b980b4ff1e1a903653bd056f6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61940378"
---
# <a name="inotifysink2onsynccallexit-method"></a>Метод INotifySink2::OnSyncCallExit
Вызывается при выходе из вызова.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT OnSyncCallExit  
(  
    [in]  CALL_ID   in_CallID,  
    [out, size_is(, *out_pBufferSize)] BYTE**  out_ppBuffer,  
    [out] DWORD*    out_pBufferSize  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `in_CallID`  
 [in] Идентификатор вызова завершил работу. См. в разделе [структура CALL_ID](../../../../docs/framework/unmanaged-api/diagnostics/call-id-structure.md).  
  
 `out_ppBuffer`  
 [out] Буфер для вызова.  
  
 `out_pBufferSize`  
 [out] Размер буфера вызова в байтах.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Значение S_OK, если метод выполнен успешно.  
  
## <a name="requirements"></a>Требования  
 **Заголовок.** ProtocolNotify2.idl  
  
## <a name="see-also"></a>См. также

- [Интерфейс INotifySink2](../../../../docs/framework/unmanaged-api/diagnostics/inotifysink2-interface.md)
- [Интерфейс INotifySource2](../../../../docs/framework/unmanaged-api/diagnostics/inotifysource2-interface.md)
- [Интерфейс INotifyConnection2](../../../../docs/framework/unmanaged-api/diagnostics/inotifyconnection2-interface.md)
