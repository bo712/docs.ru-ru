---
title: Метод SetManifestFile
ms.date: 03/30/2017
api_name:
- IALink3.SetManifestFile
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- SetManifestFile
helpviewer_keywords:
- SetManifestFile method
ms.assetid: 1b33de4c-19cb-4a36-a93f-8675b2a36d58
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8307960166cfc668a577431d688c439f0f794be2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61949047"
---
# <a name="setmanifestfile-method"></a>Метод SetManifestFile
Позволяет задать или сбросить файл манифеста, компоновщик использует при создании сборки.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT SetManifestFile(  
    LPCWSTR pszFile  
) PURE;  
```  
  
## <a name="parameters"></a>Параметры  
 `pszFile`  
  
 Имя файла манифеста, содержимое которого помещаются в большой двоичный объект ресурсов Win32.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Возвращает S_OK, если метод выполнен успешно.  
  
## <a name="remarks"></a>Примечания  
 Вызовите это перед запросом Win32ResBlob. Значение `pszFile` параметр является имя файла манифеста, содержимое которого считывается и помещается в ресурсы Win32 с Идентификатором RT_MANIFEST. При вызове с помощью параметра значение NULL, все ранее считанного манифест очищается. Это позволяет сбросить состояние компоновщика, чтобы во время инициализации.  
  
## <a name="requirements"></a>Требования  
 Требуется aLink.h  
  
## <a name="see-also"></a>См. также

- [Интерфейс IALink3](../../../../docs/framework/unmanaged-api/alink/ialink3-interface.md)
- [API ALink](../../../../docs/framework/unmanaged-api/alink/index.md)
- [Интерфейс IALink](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [Al.exe (компоновщик сборок)](../../../../docs/framework/tools/al-exe-assembly-linker.md)
