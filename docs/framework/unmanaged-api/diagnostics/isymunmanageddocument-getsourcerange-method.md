---
title: Метод ISymUnmanagedDocument::GetSourceRange
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetSourceRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetSourceRange
helpviewer_keywords:
- ISymUnmanagedDocument::GetSourceRange method [.NET Framework debugging]
- GetSourceRange method [.NET Framework debugging]
ms.assetid: 20fefee7-1040-41ba-93dc-bd42f68b90c2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 59420cfd29c3228aece9fc5ae02b950db6099ea0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61939864"
---
# <a name="isymunmanageddocumentgetsourcerange-method"></a>Метод ISymUnmanagedDocument::GetSourceRange
Возвращает заданный диапазон внедренного источника в заданный буфер. Буфер должен быть достаточно большой для хранения источника.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetSourceRange(  
    [in]  ULONG32  startLine,  
    [in]  ULONG32  startColumn,  
    [in]  ULONG32  endLine,  
    [in]  ULONG32  endColumn,  
    [in]  ULONG32  cSourceBytes,  
    [out] ULONG32  *pcSourceBytes,  
    [out, size_is(cSourceBytes),  
        length_is(*pcSourceBytes)] BYTE source[]);  
```  
  
## <a name="parameters"></a>Параметры  
 `startLine`  
 [in] Начальная строка текущего документа.  
  
 `startColumn`  
 [in] Начальный столбец текущего документа.  
  
 `endLine`  
 [in] Последняя строка в текущем документе.  
  
 `endColumn`  
 [in] Последний столбец в текущем документе.  
  
 `cSourceBytes`  
 [in] Размер источника, в байтах.  
  
 `pcSourceBytes`  
 [out] Указатель на переменную, которая получает размер источника.  
  
 `source`  
 [out] Размер и длина указанного диапазона исходного документа, в байтах.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Значение S_OK, если метод выполнен успешно.  
  
## <a name="see-also"></a>См. также

- [Интерфейс ISymUnmanagedDocument](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-interface.md)
