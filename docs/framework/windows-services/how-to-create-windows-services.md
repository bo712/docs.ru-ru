---
title: Практическое руководство. Создание служб Windows
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, creating
- templates, Windows Service
ms.assetid: 0f5e2cbb-d95d-477c-b2b5-4b990e6b86ff
author: ghogen
ms.openlocfilehash: 124e8a0dff18f02c178b56167cd12faa1fc97992
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649403"
---
# <a name="how-to-create-windows-services"></a>Практическое руководство. Создание служб Windows
При создании службы можно использовать шаблон проекта Visual Studio, который называется **Служба Windows**. Этот шаблон автоматически выполняет основную часть работы, ссылаясь на необходимые классы и пространства имен, устанавливая наследование от базового класса для служб и переопределяя некоторые методы, которые вы обычно хотите переопределять.  
  
> [!WARNING]
>  Шаблон проекта "Службы Windows" в экспресс-выпуске Visual Studio отсутствует.  
  
 Для создания функциональной службы необходимо выполнить, как минимум, следующее:  
  
- Задайте свойство <xref:System.ServiceProcess.ServiceBase.ServiceName%2A>.  
  
- Создайте установщики, необходимые для приложения службы.  
  
- Переопределите и задайте код для методов <xref:System.ServiceProcess.ServiceBase.OnStart%2A> и <xref:System.ServiceProcess.ServiceBase.OnStop%2A> для настройки режимов поведения службы.  
  
### <a name="to-create-a-windows-service-application"></a>Создание приложения службы Windows  
  
1. Создайте проект **Служба Windows**.  
  
    > [!NOTE]
    >  Инструкции по созданию службы без использования шаблона см. в разделе [Практический пример. Создание служб программным способом](../../../docs/framework/windows-services/how-to-write-services-programmatically.md).  
  
2. В окне **Свойства** задайте для своей службы свойство <xref:System.ServiceProcess.ServiceBase.ServiceName%2A>.  
  
     ![Задание свойства ServiceName](../../../docs/framework/windows-services/media/windowsservice-servicename.PNG "WindowsService_ServiceName")  
  
    > [!NOTE]
    >  Значение <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> свойства всегда должно соответствовать имени, указанному в классах установщика. При изменении этого свойства необходимо также обновить свойство <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> классов установщика.  
  
3. Установите любые из следующих свойств для определения режима работы службы.  
  
    |Свойство.|Параметр|  
    |--------------|-------------|  
    |<xref:System.ServiceProcess.ServiceBase.CanStop%2A>|`True`, чтобы указать, что служба может принимать запросы на останов работы; `false` для предотвращения останова службы.|  
    |<xref:System.ServiceProcess.ServiceBase.CanShutdown%2A>|`True`, чтобы указать, что служба хочет принимать уведомления о выключении компьютера, на котором она работает, позволяя ему вызывать процедуру <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A>.|  
    |<xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A>|`True`, чтобы указать, что служба может принимать запросы на приостановку или возобновление выполнения; `false` для предотвращения приостановки и возобновления работы службы.|  
    |<xref:System.ServiceProcess.ServiceBase.CanHandlePowerEvent%2A>|`True`, чтобы указать, что служба может обрабатывать уведомления об изменениях состояния питания компьютера; `false`, чтобы не сообщать службе об этих изменениях.|  
    |<xref:System.ServiceProcess.ServiceBase.AutoLog%2A>|`True` для внесения информационных записей в журнал событий приложения, когда служба выполняет некоторое действие; `false` для отключения этой функции. Дополнительные сведения см. в разделе [Практическое руководство. Запись сведений о службах в журнал](../../../docs/framework/windows-services/how-to-log-information-about-services.md). **Примечание.**  По умолчанию свойство <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> имеет значение `true`.|  
  
    > [!NOTE]
    >  Когда <xref:System.ServiceProcess.ServiceBase.CanStop%2A> или <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> имеют значение `false`, **диспетчер служб** будет отключать пункты меню, отвечающие за остановку, приостановку или возобновление работы службы.  
  
4. Откройте редактор кода и введите данные для выполнения операций для процедур <xref:System.ServiceProcess.ServiceBase.OnStart%2A> и <xref:System.ServiceProcess.ServiceBase.OnStop%2A>.  
  
5. Переопределите все прочие методы, для которых необходимо определить функциональные возможности.  
  
6. Добавить установщики, необходимые для приложения службы. Дополнительные сведения см. в разделе [Практическое руководство. Добавление установщиков в приложение-службу](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
7. Скомпилируйте проект, выбрав в меню **Сборка** пункт **Собрать решение**.  
  
    > [!NOTE]
    >  Не нажимайте клавишу F5 для запуска проекта — таким способом нельзя запустить проект службы.  
  
8. Установите службу. Дополнительные сведения см. в разделе [Практическое руководство. Установка и удаление служб](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md).  
  
## <a name="see-also"></a>См. также

- [Знакомство с приложениями служб Windows](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)
- [Практическое руководство. Создание служб программным способом](../../../docs/framework/windows-services/how-to-write-services-programmatically.md)
- [Практическое руководство. Добавление установщиков в приложение-службу](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)
- [Практическое руководство. Запись сведений о службах в журнал](../../../docs/framework/windows-services/how-to-log-information-about-services.md)
- [Практическое руководство. Запуск служб](../../../docs/framework/windows-services/how-to-start-services.md)
- [Практическое руководство. Назначение службам контекста безопасности](../../../docs/framework/windows-services/how-to-specify-the-security-context-for-services.md)
- [Практическое руководство. Установка и удаление служб](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)
- [Пошаговое руководство: Создание приложения служб Windows в конструкторе компонентов](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)
