---
title: Структура OSINFO
ms.date: 03/30/2017
api_name:
- OSINFO
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- OSINFO
helpviewer_keywords:
- OSINFO structure [.NET Framework metadata]
ms.assetid: fac7b480-7adb-4450-a5e9-690fed81ffae
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0aba49fb4a60b2e471c541a8d8531a1cbc8627f9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61775204"
---
# <a name="osinfo-structure"></a>Структура OSINFO
Содержит сведения об операционной системе для сборки или модуля.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
typedef struct {  
    DWORD   dwOSPlatformId;  
    DWORD   dwOSMajorVersion;   
    DWORD   dwOSMinorVersion;   
} OSINFO;  
```  
  
## <a name="members"></a>Участники  
  
|Член|Описание|  
|------------|-----------------|  
|`dwOSPlatformId`|Одно из значений идентификатора, определенных с помощью функции платформы Microsoft Windows `GetVersionEx`. Поддерживаются следующие значения:<br /><br /> -VER_PLATFORM_WIN32s, или 0x0000, чтобы указать Microsoft Windows 3.1.<br />-VER_PLATFORM_WIN32_WINDOWS, или 0x0001, чтобы указать Windows 95, Windows 98 или операционных систем, происходящий из них.<br />-VER_PLATFORM_WIN32_NT, или 0x0010, чтобы указать Windows NT или операционных систем, производных от него.|  
|`dwOSMajorVersion`|Основной номер версии операционной системы, или значение NULL для указания любой версии.|  
|`dwOSMinorVersion`|Дополнительный номер версии операционной системы, или значение NULL для указания любой версии.|  
  
## <a name="remarks"></a>Примечания  
 `OSINFO` на основе `OSVERSIONINFOEX` структура и используется в вызовах функции платформы Microsoft Windows `GetVersionEx`. Эта структура используется структура ASSEMBLYMETADATA для указания поддержки операционной системы.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** Cor.h  
  
 **Библиотека:** Используется как ресурс в MsCorEE.dll  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Структуры метаданных](../../../../docs/framework/unmanaged-api/metadata/metadata-structures.md)
- [Интерфейс IMetaDataAssemblyEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
