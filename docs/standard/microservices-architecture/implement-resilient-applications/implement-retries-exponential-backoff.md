---
title: Реализация повторных попыток с экспоненциальной выдержкой
description: Узнайте, как реализовать метод повторных попыток с экспоненциальной задержкой.
ms.date: 10/16/2018
ms.openlocfilehash: 1b948e399495eeb12016006442ac08d2b04f2e69
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644215"
---
# <a name="implement-retries-with-exponential-backoff"></a>Реализация повторных попыток с экспоненциальной выдержкой

[*Повторные попытки с экспоненциальной задержкой*](/azure/architecture/patterns/retry) — это метод, который пытается повторить операцию с экспоненциально растущим временем ожидания, пока не будет достигнуто максимальное число повторных попыток ([экспоненциальная задержка](https://en.wikipedia.org/wiki/Exponential_backoff)). Этот метод учитывает тот факт, что облачные ресурсы могут быть периодически недоступны в течение нескольких секунд по различным причинам. Например, оркестратор может перемещать контейнер на другой узел в кластере для балансировки нагрузки. В течение этого времени некоторые запросы могут завершиться с ошибкой. Другой пример — база данных, например база данных SQL Azure. В этом случае база данных может перемещаться на другой сервер для балансировки нагрузки. Во время этого перемещения она может быть недоступна в течение нескольких секунд.

Существует множество подходов для реализации логики повторных попыток с экспоненциальной выдержкой.

>[!div class="step-by-step"]
>[Назад](partial-failure-strategies.md)
>[Вперед](implement-resilient-entity-framework-core-sql-connections.md)
