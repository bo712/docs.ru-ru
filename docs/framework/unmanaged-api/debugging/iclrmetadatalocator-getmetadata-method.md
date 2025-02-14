---
title: Метод ICLRMetadataLocator::GetMetadata
ms.date: 03/30/2017
api_name:
- ICLRMetadataLocator.GetMetadata
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRMetadataLocator::GetMetadata
helpviewer_keywords:
- GetMetadata method, ICLRMetadataLocator interface [.NET Framework debugging]
- ICLRMetadataLocator::GetMetadata method [.NET Framework debugging]
ms.assetid: 704a8893-ac56-43b4-90ea-715f38ccb40e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e677aefd5420f71867c1f11a2c9408c77d305c45
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61697840"
---
# <a name="iclrmetadatalocatorgetmetadata-method"></a>Метод ICLRMetadataLocator::GetMetadata
Вызывается службами доступа к данным среды выполнения (CLR) для получения метаданных изображения.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetMetadata(  
    [in]  LPCWSTR         imagePath,  
    [in]  ULONG32         imageTimestamp,  
    [in]  ULONG32         imageSize,  
    [in]  GUID*           mvid,  
    [in]  ULONG32         mdRva,  
    [in]  ULONG32         flags,  
    [in]  ULONG32         bufferSize,  
    [out, size_is(bufferSize), length_is(*dataSize)]  
          BYTE*           buffer,  
    [out] ULONG32*        dataSize  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `imagePath`  
 [in] Строка, указывающая путь к файлу изображения.  
  
 `imageTimestamp`  
 [in] Метка времени файла изображения.  
  
 `imageSize`  
 [in] Размер файла изображения.  
  
 `mvid`  
 [in] Глобальный уникальный идентификатор изображения.  
  
 `mdRva`  
 [in] Относительный виртуальный адрес (RVA) метаданных. Адрес задается относительно базового адреса образа.  
  
 `flags`  
 [in] Зарезервировано для будущего использования.  
  
 `bufferSize`  
 [in] Размер буфера для размещения метаданных.  
  
 `buffer`  
 [out] Буфер, в котором следует разместить метаданные.  
  
 `dataSize`  
 [out] Размер метаданных, который возвращается.  
  
## <a name="remarks"></a>Примечания  
 Этот метод реализуется модулем записи отладчика.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** ClrData.idl, ClrData.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICLRMetadataLocator](../../../../docs/framework/unmanaged-api/debugging/iclrmetadatalocator-interface.md)
