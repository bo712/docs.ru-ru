---
title: Функция BeginMethodEnumeration (Справочник по неуправляемым API)
description: Функция BeginMethodEnumeration начинается перечисление методы объекта
ms.date: 11/06/2017
api_name:
- BeginMethodEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BeginMethodEnumeration
helpviewer_keywords:
- BeginMethodEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2d6de2a5ff4d2743c7aca2e46b3af848138c15fb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61917362"
---
# <a name="beginenumeration-function"></a>Функция BeginEnumeration
Начинает перечисление методы, доступные для объекта.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a>Синтаксис  
  
``` 
HRESULT BeginMethodEnumeration (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LONG              lEnumFlags
); 
```  

## <a name="parameters"></a>Параметры

`vFunc`  
[in] Этот параметр не используется.

`ptr`  
[in] Указатель на [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) экземпляра.

`lEnumFlags`  
[in] Ноль (0) для всех методов, или флаг, указывающий область видимости перечисления. Далее перечислены флаги определяются в *WbemCli.h* файл заголовка, или их можно определить как константы в коде:

Константа  |Значение  |Описание  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | Ограничения перечисления к методам, которые определены в самом классе. |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | Ограничения перечисления для свойства, наследуемые от базовых классов. |

## <a name="return-value"></a>Возвращаемое значение

Следующие значения, возвращаемые этой функцией, определяются в *WbemCli.h* файл заголовка, или их можно определить как константы в коде:

|Константа  |Значение  |Описание  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | `lEnnumFlags` не равно нулю и не является одним из указанных флагов. |
|`WBEM_S_NO_ERROR` | 0 | Вызов функции был успешным.  |
  
## <a name="remarks"></a>Примечания

Эта функция создает оболочку для вызова [IWbemClassObject::BeginMethodEnumeration](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-beginmethodenumeration) метод.

Вызов этого метода поддерживается только в том случае, если текущий объект является определение класса. Метод манипуляции не доступен из [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) указатели, которые указывают на экземпляры. Порядок, в котором перечисляются методы обязательно является инвариантным для заданного экземпляра [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject).

## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** WMINet_Utils.idl  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>См. также

- [WMI и счетчики производительности (Справочник по неуправляемым API)](index.md)
