---
title: Безопасность и ввод данных пользователем
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- security [.NET Framework], user input
- user input, security
- secure coding, user input
- code security, user input
ms.assetid: 9141076a-96c9-4b01-93de-366bb1d858bc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ce6dd2fcf913c16e4da68dec35ea3ccd8e90a948
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665785"
---
# <a name="security-and-user-input"></a>Безопасность и ввод данных пользователем
Пользовательские данные, представляющие собой любой вид входных данных (данные из веб-запроса или URL-адрес, входные данные в элементы управления приложения Microsoft Windows Forms и так далее), могут отрицательно влиять на код, поскольку такие данные часто используются непосредственно как параметры для вызова другого кода. Такое поведение аналогично поведению вредоносного кода, вызывающего ваш код со странными параметрами, поэтому следует предпринимать такие же меры предосторожности. Ввод данных пользователем на самом деле защитить несколько труднее, поскольку нет кадра стека, с помощью которого можно отслеживать наличие потенциально недоверенных данных.  
  
 Это одна из ошибок безопасности, которые наиболее сложно найти, поскольку несмотря на то, что они находятся в коде, на первый взгляд не связанном с безопасностью, такие данные играют роль шлюза для передачи неверных данных в другой код. В процессе поиска подобных ошибок проанализируйте все входные данные, все возможные диапазоны значений и определите, может ли код в случае обнаружения таких данных корректно их обработать. Такие ошибки можно устранить посредством проверки диапазонов и отбрасывания любых входных данных, которые не могут быть обработаны кодом.  
  
 Ниже приведены некоторые важные аспекты, связанные с данными пользователя.  
  
- Все данные пользователя в ответе сервера выполняются в контексте узла сервера на клиенте. Если веб-сервер принимает пользовательские данные и вставляет их в возвращаемую веб-страницу, можно, например, включить тег **\<script>** и запустить выполнение как с сервера.  
  
- Помните, что клиент может запросить любой URL-адрес.  
  
- Рассмотрим сложные и некорректные пути:  
  
    - ..\ , пути очень большой длины;  
  
    - Использование подстановочных знаков (*).  
  
    - Расширение токена (%token%).  
  
    - Необычные пути, имеющие специальное значение.  
  
    - Альтернативные имена потоков файловой системы, например `filename::$DATA`.  
  
    - Короткие имена файлов, такие как `longfi~1` для `longfilename`.  
  
- Помните, что Eval(userdata) может выполнять любые операции.  
  
- Будьте осторожны при позднем связывании с именем, которое содержит какие-либо пользовательские данные.  
  
- Если вы имеете дело с веб-данными, проверьте на допустимость различные формы escape-последовательностей, включая:  
  
    - Шестнадцатеричные escape-последовательности (%nn).  
  
    - escape-последовательности Юникода (%nnn).  
  
    - Специальные символы увеличенной длины в UTF-8 (%nn%nn).  
  
    - Двойные escape-последовательности (%nn становится %mmnn, где %mm — escape-последовательность для "%").  
  
- Будьте осторожны с именами пользователей, которые могут иметь несколько канонических форматов. Например, часто можно использовать либо формат ДОМЕН\\*имя_пользователя*, либо формат *имя_пользователя* @mydomain.example.com.  
  
## <a name="see-also"></a>См. также

- [Правила написания безопасного кода](../../../docs/standard/security/secure-coding-guidelines.md)
