---
title: Метод ICorProfilerInfo2::DoStackSnapshot
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.DoStackSnapshot
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::DoStackSnapshot
helpviewer_keywords:
- ICorProfilerInfo2::DoStackSnapshot method [.NET Framework profiling]
- DoStackSnapshot method [.NET Framework profiling]
ms.assetid: 287b11e9-7c52-4a13-ba97-751203fa97f4
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 386e15ba3b1b392efccae159d7131bb2c69b0267
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64607195"
---
# <a name="icorprofilerinfo2dostacksnapshot-method"></a>Метод ICorProfilerInfo2::DoStackSnapshot
Пошаговое описание управляемые фреймы в стеке для указанного потока и отправляет сведения профилировщику посредством обратного вызова.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT DoStackSnapshot(  
    [in] ThreadID thread,  
    [in] StackSnapshotCallback *callback,  
    [in] ULONG32 infoFlags,  
    [in] void *clientData,  
    [in, size_is(contextSize), length_is(contextSize)] BYTE context[],  
    [in] ULONG32 contextSize);  
```  
  
## <a name="parameters"></a>Параметры  
 `thread`  
 [in] Идентификатор целевой поток.  
  
 Передача значения null в `thread` создается моментальный снимок текущего потока. Если `ThreadID` из другого потока, передается, общеязыковой среды выполнения (CLR) приостанавливает работу потока, делает моментальный снимок и возобновляет работу.  
  
 `callback`  
 [in] Указатель на реализацию [StackSnapshotCallback](../../../../docs/framework/unmanaged-api/profiling/stacksnapshotcallback-function.md) метод, который вызывается средой CLR для предоставления информации для каждого управляемого кадра и каждом запуске неуправляемых фреймов профилировщика.  
  
 `StackSnapshotCallback` Метод реализуется разработчиком профилировщика.  
  
 `infoFlags`  
 [in] Значение [COR_PRF_SNAPSHOT_INFO](../../../../docs/framework/unmanaged-api/profiling/cor-prf-snapshot-info-enumeration.md) перечисления, который определяет объем данных будет передан обратно для каждого кадра с `StackSnapshotCallback`.  
  
 `clientData`  
 [in] Указатель на данные клиента, который передается напрямую через `StackSnapshotCallback` функцию обратного вызова.  
  
 `context`  
 [in] Указатель на Win32 `CONTEXT` структуру, которая используется для задания начального значения стека. Win32 `CONTEXT` структура содержит значения для регистров ЦП и отражает состояние ЦП в определенный момент времени.  
  
 Начальное значение позволяет среде CLR определить, откуда следует начинать анализ стека, в верхней части стека в случае вспомогательный неуправляемый код; в противном случае — значение начального заполнения игнорируется. Для асинхронного прохода необходимо указать начальное значение. Если вы выполняете синхронный анализ стека, начальное значение не требуется.  
  
 `context` Параметр допустим только в том случае, если был передан флаг COR_PRF_SNAPSHOT_CONTEXT `infoFlags` параметра.  
  
 `contextSize`  
 [in] Размер `CONTEXT` структуру, которая ссылается `context` параметра.  
  
## <a name="remarks"></a>Примечания  
 Передача значения null для `thread` создается моментальный снимок текущего потока. Моментальные снимки могут быть взяты из других потоков, только в том случае, если целевой поток приостановлен во время.  
  
 Когда профилировщик хочет пройти по стеку, он вызывает `DoStackSnapshot`. Прежде чем среда CLR возвращает из этого вызова, он вызывает ваш `StackSnapshotCallback` несколько раз, один раз для каждого управляемого фрейма (или неуправляемых фреймов) в стеке. При возникновении неуправляемых фреймов, вы должны пройти их самостоятельно.  
  
 Порядок, в котором выполняется обход стека является обратной по отношению как кадры были переданы в стек: последнего конечные (отправить в последней) во-первых, основной (первый переданный) фрейма.  
  
 Дополнительные сведения о программировании профилировщика для обхода управляемых стеков см. в разделе [Profiler, анализ стека в .NET Framework 2.0: Основы и за его пределами](https://go.microsoft.com/fwlink/?LinkId=73638).  
  
 Обход стека может быть синхронным или асинхронным, как описано в следующих разделах.  
  
## <a name="synchronous-stack-walk"></a>Синхронные стека  
 Синхронные стека включает в себя анализ стека текущего потока в ответ на обратный вызов. Он не требует заполнения или приостановить действие.  
  
 Внесенные синхронной вызывается, когда, в ответ на CLR, вызвав один из вашего профилировщика [ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) (или [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)) методы, вызов `DoStackSnapshot` для анализа стека текущий поток. Это полезно, если вы хотите увидеть стек как выглядят на уведомление о таких как [ICorProfilerCallback::ObjectAllocated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectallocated-method.md). Нужно просто вызвать `DoStackSnapshot` изнутри вашей `ICorProfilerCallback` , передавая значение null в `context` и `thread` параметров.  
  
## <a name="asynchronous-stack-walk"></a>Асинхронный проход стека  
 Влечет за собой Асинхронный проход стека, анализ стека другого потока или анализ стека текущего потока не в ответ на обратный вызов, а также путем перехвата указателя инструкций для текущего потока. Для асинхронного прохода требуется исходное значение, если неуправляемый код, который не является частью платформы находится вверху стека вызова (PInvoke) или вызов COM, а вспомогательным кодом самой CLR. Например код, который собирает just-in-time (JIT) компиляцию или сбор мусора является вспомогательным кодом.  
  
 Получить начальное значение, непосредственно приостановки анализируемого потока и пройти по стеку самостоятельно, пока не найдете самый верхний управляемый фрейм. После целевой поток приостанавливается и получите текущий контекст регистра анализируемого потока. Проверьте, указывает ли регистров на неуправляемый код, вызвав [ICorProfilerInfo::GetFunctionFromIP](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromip-method.md) , если он возвращает `FunctionID` равен нулю, кадр является неуправляемым кодом. Теперь обход стека, пока не достигнете первого управляемого фрейма, а затем вычислить контекст начального значения, исходя из контекста регистра для этого кадра.  
  
 Вызовите `DoStackSnapshot` с контекстом направления, чтобы начать Асинхронный проход стека. Если не указать начальное значение, `DoStackSnapshot` может пропустить управляемые фреймы на вершине стека и, следовательно, предоставит неполный проход стека. Если указать начальное значение, оно должно указывать на JIT-компиляции или собственного генератором образов (Ngen.exe)-сформированного кода; в противном случае `DoStackSnapshot` возвращает код ошибки, CORPROF_E_STACKSNAPSHOT_UNMANAGED_CTX.  
  
 Стека может легко привести к возникновению взаимоблокировки или нарушение прав доступа, если не следовать рекомендациям:  
  
- При приостановке непосредственно потоков, помните, что только поток, ни никогда не выполняет управляемый код может приостановить другой поток.  
  
- Всегда блока в вашей [ICorProfilerCallback::ThreadDestroyed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threaddestroyed-method.md) обратного вызова до завершения анализа стека данного потока.  
  
- Не блокируйте период обращения вашего профилировщика к функции CLR, способной запустить сбор мусора. То есть не удерживать блокировку, если собственный поток может осуществить вызов, который запускает сборку мусора.  
  
 Есть также риск взаимоблокировки при вызове метода `DoStackSnapshot` из потока, который создал ваш профилировщик, таким образом, чтобы вы для прохода по стеку анализируемого потока. Первый раз вы создали поток входит в определенных `ICorProfilerInfo*` методы (включая `DoStackSnapshot`), среда CLR будет выполнять на уровне потока, инициализации среды CLR в этом потоке. Если профилировщик приостановил анализируемый поток, стек которого вы пытаетесь получить пошаговые инструкции, и если этот целевой поток является владельцем блокировки, необходимой для выполнения инициализации каждого потока, произойдет взаимоблокировка. Чтобы избежать этой взаимоблокировки, выполните исходный вызов в `DoStackSnapshot` из вашего потока, созданного профилировщика для обхода предназначены потока отдельно, но не приостанавливаете анализируемый поток сначала. Исходный вызов гарантирует, что инициализация отдельных потоков может быть завершена без взаимоблокировки. Если `DoStackSnapshot` выполняется успешно, а также отчеты по крайней мере один кадр после этой точки, будут иметь безопасный для этого потока, созданный профилировщиком приостановить любой целевой поток и вызов `DoStackSnapshot` для анализа стека данного целевого потока.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** См. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок.** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [Интерфейс ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
