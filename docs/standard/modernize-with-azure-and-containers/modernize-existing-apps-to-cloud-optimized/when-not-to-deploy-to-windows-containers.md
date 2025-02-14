---
title: Технологии, не поддерживающие развертывание в контейнерах Windows
description: Модернизация существующих приложений .NET с помощью облака Azure и Windows контейнерах | Когда не следует развертывать контейнеры Windows в
ms.date: 04/28/2018
ms.openlocfilehash: 65e793b846b495e9a1be6db9ddfa38bbf0d49445
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65638901"
---
# <a name="when-not-to-deploy-to-windows-containers"></a>Технологии, не поддерживающие развертывание в контейнерах Windows

Некоторые технологии Windows не поддерживаются в контейнерах Windows. В таком случае необходимо перенести на виртуальные машины стандартов, обычно с помощью только Windows и IIS.

Случаи, не поддерживается в контейнерах Windows, по состоянию на май 2018 г.:

- Очереди сообщений (Майкрософт) в настоящее время доступна только в зависимости от версии Windows Server v1803 контейнерах Windows, но не в предыдущих выпусках.

  - [Запрос на форуме UserVoice](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/15719031-create-base-container-image-with-msmq-server)

  - [Дискуссионный форум](https://social.msdn.microsoft.com/Forums/bce99a7d-aa60-44fa-a348-450855650810/msmqserver-is-it-supported?forum=windowscontainers)

- Координатор распределенных транзакций (MSDTC) в настоящее время не поддерживается в контейнерах Windows.

  - [На сайте github](https://github.com/MicrosoftDocs/Virtualization-Documentation/issues/494)

- В настоящее время Microsoft Office не поддерживает контейнеры.

  - [Запрос на форуме UserVoice](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/19686220-provide-office-support-for-containers)

- Пользовательский Интерфейс приложений (клиентских приложений с интерфейсом пользователя visual) не описаны поддерживаемые сценарии.

- Инфраструктурные роли Windows (DNS, DHCP, Округ Колумбия, NTP, печати, файловый сервер, IAM и т.д.), не поддерживаемые сценарии.

Дополнительные сценарии не поддерживаются и запросы от сообщества, см. на форуме UserVoice для контейнеров Windows: <https://windowsserver.uservoice.com/forums/304624-containers>.

### <a name="additional-resources"></a>Дополнительные ресурсы

- **Виртуальные машины и контейнеры в Azure**

    <https://azure.microsoft.com/overview/containers/>

> [!div class="step-by-step"]
> [Назад](deploy-existing-net-apps-as-windows-containers.md)
> [Вперед](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)
