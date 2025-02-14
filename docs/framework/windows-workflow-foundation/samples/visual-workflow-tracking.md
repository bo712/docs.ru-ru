---
title: Визуальное отслеживание рабочего процесса
ms.date: 03/30/2017
ms.assetid: 0143448f-2044-40a0-8a3d-941f6d12468b
ms.openlocfilehash: abd9f294018f6aa1fd2020314688258ac00792f7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637804"
---
# <a name="visual-workflow-tracking"></a>Визуальное отслеживание рабочего процесса
В этом образце показано, как подготовить приложение для визуального отслеживания рабочих процессов с использованием функции отладки, доступной через [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)].

## <a name="sample-details"></a>Подробные сведения об образце
 Приложение запускает простой рабочий процесс блок-схемы (определенной в файле Workflow.xaml) и повторно размещает конструктор рабочих процессов для отображения рабочего процесса, выполняемого в настоящий момент. По мере выполнения рабочего процесса действие, выполняемое в настоящий момент, отображается с желтым контуром и стрелкой отладки. Кроме того, записи отслеживания, создаваемые рабочим процессом, также отображаются в окне приложения. Дополнительные сведения об отслеживании рабочего процесса см. в разделе [отслеживание и трассировка рабочих процессов](../workflow-tracking-and-tracing.md). Дополнительные сведения о повторном размещении конструктора рабочих процессов, см. в разделе [повторное размещение конструктора рабочих процессов](../rehosting-the-workflow-designer.md).

 Симулятор рабочих процессов работает за счет двух словарей. Один из словарей содержит сопоставление между объектом действия, исполняемого в настоящий момент, и номером XAML-строки, в которой запускается действие. Другой словарь содержит сопоставление между идентификатором экземпляра действия и объектом действия. Когда при помощи настраиваемого профиля отслеживания создаются записи отслеживания, приложение определяет идентификатор экземпляра действия, исполняемого в настоящий момент, и сопоставляет его с файлом XAML, который запустил действие. После этого вновь размещенный конструктор рабочих процессов выделяет действие в области конструктора и использует такой же метод, что и отладчик рабочих процессов, при этом вокруг действия появляется желтый контур, а в левой части конструктора - желтая стрелка.

#### <a name="to-use-this-sample"></a>Использование этого образца

1. Откройте файл WorkflowSimulator.sln из папки образцов в Visual Studio 2010.

2. Чтобы построить решение, нажмите CTRL+SHIFT+B.

3. Чтобы запустить образец, нажмите клавиши CTRL+F5. Файл Workflow.xaml будет отображен в окне вновь размещенного конструктора рабочих процессов.

4. Нажмите кнопку **файл** меню и выберите **выполнить рабочий процесс...** .

5. Обратите внимание, что действие, исполняемое в настоящий момент, подсвечивается, как и было указано ранее, а записи отслеживания отображаются с правой стороны окна приложения.

6. После завершения рабочего процесса пользователь может щелкнуть любую запись отслеживания, чтобы посмотреть, к какому действию она относится.

> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) для загрузки всех Windows Communication Foundation (WCF) и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] примеры. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Application\VisualWorkflowTracking`
