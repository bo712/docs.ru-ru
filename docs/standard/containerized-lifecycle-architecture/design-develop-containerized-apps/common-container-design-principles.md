---
title: Общие принципы проектирования контейнеров
description: Сведения о фундаментальном принципе проектирования контейнеров, который заключается в том, что в контейнере должен размещаться только один процесс.
ms.date: 02/15/2019
ms.openlocfilehash: 69f3ff6c9303f0c4082695d861a8c90031295b6a
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/13/2019
ms.locfileid: "65644798"
---
# <a name="common-container-design-principles"></a>Общие принципы проектирования контейнеров

Прежде чем погрузиться в процесс разработки, следует рассмотреть несколько основных понятий, касающихся использования контейнеров.

## <a name="container-equals-a-process"></a>Равноценность контейнера процессу

Контейнер в модели на основе контейнеров представляет отдельный процесс. Определив контейнер как границу процесса, вы можете создавать примитивы, позволяющие масштабировать процессы или помещать их в пакет. Когда вы запускаете контейнер Docker, отображается определение [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint). Оно определяет процесс и время существования контейнера. По завершении процесса время существования контейнера истекает. Существуют как длительные процессы, например веб-серверы, так и кратковременные, например пакетные задания, которые могли реализовываться как [веб-задания](https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/) Microsoft Azure. В случае сбоя процесса работа контейнера завершается и оркестратор принимает управление. Если оркестратору указано поддерживать пять выполняющихся экземпляров, то в случае сбоя одного из них оркестратор создаст ему на замену еще один контейнер. В пакетном задании процесс запускается с параметрами. По завершении выполнения процесса работа считается выполненной.

Возможны ситуации, когда в одном контейнере желательно выполнять несколько процессов. В любом документе по архитектуре никогда не используется понятие "никогда", а также не используется всеохватывающее понятие "всегда". Распространенным шаблоном для сценариев, требующих несколько процессов, является [Контролер](http://supervisord.org/).

>[!div class="step-by-step"]
>[Назад](design-docker-applications.md)
>[Вперед](monolithic-applications.md)
