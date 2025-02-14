---
title: Практическое руководство. Настройка политики кэша на основе времени
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time-based cache policies
- customizing time-based cache policies
- cache [.NET Framework], time-based policies
ms.assetid: 8d84f936-2376-4356-9264-03162e0f9279
ms.openlocfilehash: 457de16337fd2a37dad9042c770680ba5ad27a0d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64624609"
---
# <a name="how-to-customize-a-time-based-cache-policy"></a>Практическое руководство. Настройка политики кэша на основе времени
При создании политики кэша на основе времени можно настроить поведение кэширования, устанавливая значения максимального возраста, минимальной актуальности или даты синхронизации кэша. Объект <xref:System.Net.Cache.HttpRequestCachePolicy> предоставляет несколько конструкторов, позволяющих определять допустимые сочетания этих значений.  
  
### <a name="to-create-a-time-based-cache-policy-that-uses-a-cache-synchronization-date"></a>Создание политики кэша на основе времени с использованием даты синхронизации кэша  
  
- Создание политики кэша на основе времени с использованием даты синхронизации кэша осуществляется за счет передачи объекта <xref:System.DateTime> в конструктор <xref:System.Net.Cache.HttpRequestCachePolicy>.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateLastSyncPolicy(DateTime when)  
    {  
        HttpRequestCachePolicy policy =   
            new HttpRequestCachePolicy(when);  
        Console.WriteLine("When: {0}", when);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateLastSyncPolicy([when] As DateTime) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy([when])  
        Console.WriteLine("When: {0}", [when])  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 Выходные данные будут иметь примерно следующий вид:  
  
```  
When: 1/14/2004 8:07:30 AM  
Level:Default CacheSyncDate:1/14/2004 8:07:30 AM  
```  
  
### <a name="to-create-a-time-based-cache-policy-that-is-based-on-minimum-freshness"></a>Создание политики кэша на основе времени с использованием минимальной актуальности  
  
- Чтобы создать политику кэша на основе времени с использованием минимальной актуальности, укажите <xref:System.Net.Cache.HttpCacheAgeControl.MinFresh> в качестве значения параметра `cacheAgeControl` и передайте объект <xref:System.TimeSpan> в конструктор <xref:System.Net.Cache.HttpRequestCachePolicy>.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateMinFreshPolicy(TimeSpan span)  
    {  
        HttpRequestCachePolicy policy =   
            new HttpRequestCachePolicy(HttpCacheAgeControl.MinFresh, span);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateMinFreshPolicy(span As TimeSpan) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy(HttpCacheAgeControl.MinFresh, span)  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 Для следующего вызова:  
  
```  
CreateMinFreshPolicy(new TimeSpan(1,0,0));  
```  
  
```  
Level:Default MinFresh:3600  
```  
  
### <a name="to-create-a-time-based-cache-policy-that-is-based-on-minimum-freshness-and-maximum-age"></a>Создание политики кэша на основе времени с использованием минимальной актуальности и максимального возраста  
  
- Чтобы создать политику кэша на основе времени с использованием минимальной актуальности и максимального возраста, укажите <xref:System.Net.Cache.HttpCacheAgeControl.MaxAgeAndMinFresh> в качестве значения параметра `cacheAgeControl` и передайте два объекта <xref:System.TimeSpan> в конструктор <xref:System.Net.Cache.HttpRequestCachePolicy>. Один из этих объектов задает максимальный возраст ресурсов, а второй — минимально допустимую актуальность объекта, возвращаемого из кэша.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateFreshAndAgePolicy(TimeSpan freshMinimum, TimeSpan ageMaximum)  
    {  
        HttpRequestCachePolicy policy =   
        new HttpRequestCachePolicy(HttpCacheAgeControl.MaxAgeAndMinFresh, ageMaximum, freshMinimum);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateFreshAndAgePolicy(freshMinimum As TimeSpan, ageMaximum As TimeSpan) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy(HttpCacheAgeControl.MaxAgeAndMinFresh, ageMaximum, freshMinimum)  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 Для следующего вызова:  
  
```  
CreateFreshAndAgePolicy(new TimeSpan(5,0,0), new TimeSpan(10,0,0));  
```  
  
```  
Level:Default MaxAge:36000 MinFresh:18000  
```  
  
## <a name="see-also"></a>См. также

- [Управление кэшем для сетевых приложений](../../../docs/framework/network-programming/cache-management-for-network-applications.md)
- [Политика кэша](../../../docs/framework/network-programming/cache-policy.md)
- [Политики кэша на основе расположения](../../../docs/framework/network-programming/location-based-cache-policies.md)
- [Политики кэша на основе времени](../../../docs/framework/network-programming/time-based-cache-policies.md)
- [Элемент \<requestCaching> (сетевые параметры)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)
