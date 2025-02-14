---
title: Вопросы производительности, связанные с взаимодействием Direct3D9 и WPF
ms.date: 03/30/2017
helpviewer_keywords:
- WPF [WPF], Direct3D9 interop performance
- Direct3D9 [WPF interoperability], performance
ms.assetid: ea8baf91-12fe-4b44-ac4d-477110ab14dd
ms.openlocfilehash: 1371fa901bebc503a0091f3229a8fd7e6ccc2c86
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61772857"
---
# <a name="performance-considerations-for-direct3d9-and-wpf-interoperability"></a>Вопросы производительности, связанные с взаимодействием Direct3D9 и WPF
С помощью можно разместить содержимого Direct3D9 <xref:System.Windows.Interop.D3DImage> класса. Размещение содержимого Direct3D9 может повлиять на производительность приложения. В этом разделе описываются рекомендации по оптимизации производительности при размещении содержимого Direct3D9 в приложении Windows Presentation Foundation (WPF). Эти рекомендации о том, как использовать <xref:System.Windows.Interop.D3DImage> и рекомендации, когда вы используете Windows Vista, Windows XP, и нескольких мониторов.  
  
> [!NOTE]
>  Примеры кода, иллюстрирующие эти рекомендации, см. в разделе [взаимодействие WPF и Direct3D9](wpf-and-direct3d9-interoperation.md).  
  
## <a name="use-d3dimage-sparingly"></a>Как можно реже используйте D3DImage  
 Размещенного содержимого Direct3D9 в <xref:System.Windows.Interop.D3DImage> отображается не так быстро, как чистые приложения Direct3D. Копирование поверхности и очистка буфера команд может быть дорогостоящей операции. Как количество <xref:System.Windows.Interop.D3DImage> экземпляров увеличивается, очистки буфера, а производительность снижается. Таким образом, следует использовать <xref:System.Windows.Interop.D3DImage> только в случае необходимости.  
  
## <a name="best-practices-on-windows-vista"></a>Рекомендации по Windows Vista  
 Для обеспечения максимальной производительности в Windows Vista с отображением, который настроен для использования Windows отображения Driver Model (WDDM), создайте поверхность Direct3D9 на `IDirect3DDevice9Ex` устройства. Это позволит совместно использовать поверхность. Видеоадаптер должен поддерживать `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` и `D3DCAPS2_CANSHARERESOURCE` возможности драйверов Windows Vista. Все остальные параметры привести к рабочей области для копирования посредством программного обеспечения, что значительно снижает производительность.  
  
> [!NOTE]
>  Если Windows Vista используется дисплей, настроен на использование Windows XP отображения драйвер модели (XDDM), в рабочей области всегда копируется программно, независимо от параметров. С помощью правильных настроек и видеоадаптер вы увидите более высокую производительность в Windows Vista при использовании модели WDDM, поскольку выполняется копирование поверхностей оборудования.  
  
## <a name="best-practices-on-windows-xp"></a>Рекомендации по Windows XP  
 Для обеспечения максимальной производительности в Windows XP, которая использует Windows XP отображения драйвер модели (XDDM), создайте блокируемый поверхность, которая работает правильно при `IDirect3DSurface9::GetDC` вызывается метод. На внутреннем уровне `BitBlt` метод переносит поверхность между устройствами. `GetDC` Метод всегда работает на поверхностях XRGB. Тем не менее, если клиентский компьютер работает под управлением Windows XP с SP3 или с пакетом обновления 2 и в клиенте также имеется исправление для функции многоуровневых окон, этот метод работает только на поверхностях ARGB. Видеоадаптер должен поддерживать `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` возможности драйвера.  
  
 Глубина 16-разрядное отображения рабочего стола может значительно снизить производительность. Рекомендуется использовать 32-разрядную глубину.  
  
 Если при разработке для Windows Vista и Windows XP, тестирование производительности в Windows XP. Нехватку памяти в Windows XP является проблемой. Кроме того <xref:System.Windows.Interop.D3DImage> в Windows XP использует больше памяти и пропускной способности, чем Windows Vista WDDM, из-за необходимости копирования дополнительной видеопамяти. Таким образом можно ожидать производительность будет хуже, в Windows XP, чем в Windows Vista для этого же видео оборудования.  
  
> [!NOTE]
>  XDDM можно найти в ОС Windows XP и Windows Vista; Тем не менее WDDM доступна только в Windows Vista.  
  
## <a name="general-best-practices"></a>Общие рекомендации  
 При создании устройства, используйте `D3DCREATE_MULTITHREADED` флаг создания. Это снижает производительность, однако система отрисовки WPF вызывает методы на этом устройстве из другого потока. Не забудьте правильно, выполните протокол блокировки, таким образом, чтобы доступ к устройству двух потоков одновременно.  
  
 Если визуализация выполняется в управляемом потоке WPF, настоятельно рекомендуется создать устройство с помощью `D3DCREATE_FPU_PRESERVE` флаг создания. Без этого параметра визуализации D3D может снизить точность операций WPF двойной точности и вызвать проблемы отрисовки.  
  
 Мозаичное заполнение <xref:System.Windows.Interop.D3DImage> выполняется быстро, за исключением заполнения не pow2 поверхность без поддержки оборудования, либо <xref:System.Windows.Media.DrawingBrush> или <xref:System.Windows.Media.VisualBrush> , содержащий <xref:System.Windows.Interop.D3DImage>.  
  
## <a name="best-practices-for-multi-monitor-displays"></a>Рекомендации при использовании нескольких мониторов  
 Если вы используете компьютер с несколькими мониторами, соблюдайте выше рекомендациям. Кроме того, существуют также некоторые дополнительные рекомендации по производительности для нескольких мониторов.  
  
 При создании задний буфер, он создается для конкретного устройства и адаптера, но WPF может отобразить кадровый буфер на одном адаптере. Копирование через адаптеры для обновления передний буфер может быть очень дорогим. В Windows Vista, настроенный на использование модели WDDM с несколькими видеоадаптерами и `IDirect3DDevice9Ex` устройства, если передний буфер в другой адаптер, но по-прежнему же видеоадаптера, производительность снижается, нет. Однако в Windows XP и XDDM с несколькими видеоадаптерами, есть к значительному снижению производительности при отображении передний буфер в другой адаптер задний буфер. Дополнительные сведения см. в разделе [взаимодействие WPF и Direct3D9](wpf-and-direct3d9-interoperation.md).  
  
## <a name="performance-summary"></a>Отчет о производительности  
 Следующая таблица показывает производительность обновления передний буфер как функция операционной системы, формат пикселей и поверхности. Передний буфер и задний буфер считаются в одном адаптере. В зависимости от конфигурации адаптера обновления оборудования обычно гораздо быстрее, чем обновлений программного обеспечения.  
  
|Формат пикселей поверхности|Windows Vista, WDDM и 9Ex|Другие конфигурации Windows Vista|Windows XP SP3 и SP2 установленным исправлением|Windows XP с пакетом обновления 2 (SP2)|  
|--------------------------|---------------------------------|----------------------------------------|--------------------------------------|--------------------|  
|D3DFMT_X8R8G8B8 (не блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|Обновление программного обеспечения|Обновление программного обеспечения|  
|D3DFMT_X8R8G8B8 (блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|**Обновление оборудования**|**Обновление оборудования**|  
|D3DFMT_A8R8G8B8 (не блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|Обновление программного обеспечения|Обновление программного обеспечения|  
|D3DFMT_A8R8G8B8 (блокируемый)|**Обновление оборудования**|Обновление программного обеспечения|**Обновление оборудования**|Обновление программного обеспечения|  
  
## <a name="see-also"></a>См. также

- <xref:System.Windows.Interop.D3DImage>
- [Взаимодействие WPF и Direct3D9](wpf-and-direct3d9-interoperation.md)
- [Пошаговое руководство: Создание содержимого Direct3D9 для размещения в WPF](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [Пошаговое руководство: Размещение содержимого Direct3D9 в WPF](walkthrough-hosting-direct3d9-content-in-wpf.md)
