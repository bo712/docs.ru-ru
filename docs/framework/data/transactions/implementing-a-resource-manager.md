---
title: Реализация диспетчера ресурсов
ms.date: 03/30/2017
ms.assetid: d5c153f6-4419-49e3-a5f1-a50ae4c81bf3
ms.openlocfilehash: f3e29dae095fbe56181cf7b67787c1044efa07ae
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61793709"
---
# <a name="implementing-a-resource-manager"></a>Реализация диспетчера ресурсов
Каждым используемым в транзакции ресурсом управляет диспетчер ресурсов, действия которого координируются диспетчером транзакций. Диспетчеры ресурсов работают совместно с диспетчером транзакций для предоставления приложения, гарантирующего атомарность и изоляцию. Примерами диспетчеров ресурсов являются Microsoft SQL Server, устойчивые очереди сообщений и расположенные в оперативной памяти хэш-таблицы.  
  
 Диспетчер ресурсов управляет либо устойчивыми, либо неустойчивыми данными. Устойчивость (или наоборот, неустойчивость) диспетчера ресурсов определяет, поддерживает ли он восстановление после сбоя. Если диспетчер ресурсов поддерживает восстановление после сбоя, он сохраняет данные в устойчивом хранилище во время фазы 1 (подготовка); таким образом, если диспетчер ресурсов выходит из строя, он может повторно зачислиться в транзакцию после восстановления и выполнить соответствующие действия на основе уведомлений, полученных от диспетчера транзакций. В основном, диспетчеры неустойчивых ресурсов управляют неустойчивыми ресурсами, такими как структура данных, расположенная в оперативной памяти (например транзакционная хэш-таблица), а диспетчеры устойчивых ресурсов управляют устойчивыми ресурсами, которые имеют более устойчивое резервное хранилище (например, базой данных, резервным хранилищем которой является диск).  
  
 Для участия в транзакции ресурс должен зачислиться в нее. <xref:System.Transactions.Transaction> Класс определяет набор методов, имена которых начинаются с **Enlist** , предоставляет такой возможности. Различные **Enlist** методы соответствуют к различным типам зачисления, которые могут использоваться диспетчером ресурсов. В частности, методы <xref:System.Transactions.Transaction.EnlistVolatile%2A> используются для неустойчивых ресурсов, а метод <xref:System.Transactions.Transaction.EnlistDurable%2A> - для устойчивых ресурсов. После выбора используемого метода (<xref:System.Transactions.Transaction.EnlistDurable%2A> или <xref:System.Transactions.Transaction.EnlistVolatile%2A>) в зависимости от поддержки ресурсом восстановления после сбоя необходимо зачислить ресурс для участия в двухфазной фиксации путем реализации интерфейса <xref:System.Transactions.IEnlistmentNotification> для диспетчера ресурсов. Дополнительные сведения о 2PC, см. в разделе [Фиксация транзакции однофазная и Многофазная](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md).  
  
 Зачисление гарантирует получение диспетчером ресурсов обратных вызовов от диспетчера транзакций при фиксации или прерывании транзакции. Для каждого зачисления существует один экземпляр класса <xref:System.Transactions.IEnlistmentNotification>. Как правило, для каждой транзакции существует одно зачисление, однако диспетчер ресурсов может зачислиться в одну транзакцию несколько раз.  
  
 После зачисления диспетчер ресурсов отвечает на запросы транзакции. Диспетчер устойчивых ресурсов сохраняет достаточное количество данных, чтобы отменить или повторить операции транзакции над ресурсами, которыми он управляет. Существует множество способов сохранения этих данных; двумя наиболее распространенными из них являются сохранение версий данных и ведение журнала изменений.  
  
 Когда приложение запрашивает фиксацию транзакции, диспетчер транзакций инициирует протокол двухфазной фиксации. Сначала диспетчер транзакций опрашивает все зачисленные диспетчеры ресурсов, чтобы выяснить, готовы ли они к фиксации транзакции. Диспетчер ресурсов должен подготовиться к фиксации или прерыванию транзакции.  
  
 В фазе подготовки диспетчер устойчивых ресурсов записывает старые и новые данные в устойчивое хранилище, чтобы иметь возможность их восстановления в случае сбоя системы. Если диспетчер ресурсов способен выполнить подготовку, он передает диспетчеру транзакции свой голос за фиксацию или прерывание транзакции. Если хотя бы от одного диспетчера ресурсов получено сообщение о том, что подготовку выполнить не удалось, диспетчер транзакций передает команду отката каждому диспетчеру ресурсов и сообщает приложению о сбое фиксации.  
  
 После подготовки диспетчер ресурсов должен ожидать получения обратного вызова фиксации или прекращения от диспетчера транзакций на второй фазе. Обычно весь протокол подготовки и фиксации выполняется за долю секунды. В случае системного сбоя или отказа канала связи уведомление о фиксации или прерывании может прийти по прошествии нескольких минут или часов. В течение этого времени диспетчеру ресурсов не известен результат транзакции. Он не знает, была ли транзакция зафиксирована или прервана. Пока результат транзакции неизвестен, диспетчер ресурсов сохраняет измененные данные посредством сохранения блокировки транзакции, изолируя эти изменения от всех остальных транзакций.  
  
 При сбое диспетчера ресурсов прерываются все его транзакции, за исключением транзакций, которые были подготовлены или зафиксированы до сбоя. После перезапуска диспетчер устойчивых ресурсов воссоздает фиксированное состояние управляемых им ресурсов путем извлечения данных подготовки, записанных в фазе подготовки, и соответственно фиксирует или прерывает эти транзакции.  
  
 Протокол двухфазной фиксации и диспетчеры ресурсов вместе обеспечивают атомарность и устойчивость транзакций.  
  
 Класс <xref:System.Transactions.Transaction> также предоставляет метод <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> для PSPE-зачисления. Это позволяет диспетчеру устойчивых ресурсов "владеть" и управлять транзакцией, которая затем при необходимости может быть повышена до транзакции MSDTC. Дополнительные сведения об этом см. в разделе [оптимизация производительности с помощью однофазной фиксации и повышаемого однофазного уведомления](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md).  
  
## <a name="in-this-section"></a>В этом разделе  
 Действия, обычно выполняемые диспетчером ресурсов, описываются в следующих разделах.  
  
 [Зачисление ресурсов в транзакцию в качестве участников](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md)  
  
 Описывает порядок зачисления устойчивого или неустойчивого ресурса в транзакцию.  
  
 [Однофазная и многофазная фиксация транзакции](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md)  
  
 Описывает, как диспетчер ресурсов отвечает на уведомление о фиксации и подготавливает фиксацию.  
  
 [Выполнение восстановления](../../../../docs/framework/data/transactions/performing-recovery.md)  
  
 Описывает порядок восстановления диспетчера устойчивых ресурсов после сбоя.  
  
 [Уровни доверия, используемые при доступе к ресурсам](../../../../docs/framework/data/transactions/security-trust-levels-in-accessing-resources.md)  
  
 Описывает, как три уровня доверия для System.Transactions ограничивают доступ к ресурсам различных типов, используемым инфраструктурой <xref:System.Transactions>.  
  
 [Оптимизация производительности с помощью механизмов уведомления об однофазной фиксации и повышаемого однофазного присоединения](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md)  
  
 Описывает способы оптимизации, доступные реализациям диспетчеров ресурсов.
