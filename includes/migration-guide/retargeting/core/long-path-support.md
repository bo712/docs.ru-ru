---
ms.openlocfilehash: 506218195417548880a9d8d10508a570a7769682
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804878"
---
### <a name="long-path-support"></a>Поддержка длинных путей

|   |   |
|---|---|
|Подробные сведения|Начиная с приложений, ориентированных на .NET Framework 4.6.2, поддерживаются длинные пути (до 32 тыс. символов), а ограничение длины пути в 260 символов (или <code>MAX_PATH</code>) было удалено. Для приложений, которые перекомпилируются для использования в .NET Framework 4.6.2, кодовые пути, ранее вызывавшие исключение <xref:System.IO.PathTooLongException?displayProperty=name>, когда путь превышал 260 символов, теперь будут вызывать исключение <xref:System.IO.PathTooLongException?displayProperty=name> только при следующих условиях:<ul><li>длина пути превышает <xref:System.Int16.MaxValue> (32 767) символов;</li><li>операционная система возвращает <code>COR_E_PATHTOOLONG</code> или его эквивалент;</li></ul>Для приложений, предназначенных для .NET Framework 4.6.1 и более ранних версий, среда выполнения автоматически создает исключение <xref:System.IO.PathTooLongException?displayProperty=name>, когда длина пути превышает 260 символов.|
|Предложение|Для приложений, предназначенных для .NET Framework 4.6.2, можно отказаться от поддержки длинного пути, добавив следующую строку в раздел <code>&lt;runtime&gt;</code> файла <code>app.config</code>:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>Для приложений, которые предназначены для более ранних версий .NET Framework, но выполняются в .NET Framework 4.6.2 или более поздней версии, можно включить поддержку длинного пути, добавив следующую строку в раздел <code>&lt;runtime&gt;</code> файла <code>app.config</code>:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Область|Дополнительный номер|
|Версия|4.6.2|
|Тип|Изменение целевой платформы|
