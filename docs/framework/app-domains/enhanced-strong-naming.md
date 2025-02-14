---
title: Усовершенствованное строгое именование
ms.date: 03/30/2017
helpviewer_keywords:
- strong-named assemblies
- strong naming [.NET Framework], enhanced
ms.assetid: 6cf17a82-62a1-4f6d-8d5a-d7d06dec2bb5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 882b1de4b1fd3b013b6b2825aec5e607a387531b
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2019
ms.locfileid: "66377994"
---
# <a name="enhanced-strong-naming"></a>Усовершенствованное строгое именование
Подпись строгого имени — это механизм идентификации сборок в .NET Framework. Это цифровая подпись с открытым ключом, которая обычно используется для проверки целостности данных, передаваемых от инициатора (подписывающего) к получателю (проверяющему). Эта подпись используется в виде уникального идентификатора сборки и гарантирует, что ссылки на сборку не являются неоднозначными. Подписывание сборки является частью процесса сборки, что затем проверяется при ее загрузке.  
  
 Подписи строгого имени помогают предотвратить подделку сборки на стороне злоумышленника с последующей повторной подписью сборки оригинальным ключом подписавшего. Но ключи строгого имени не содержат никаких сведений об издателе, а также не содержат иерархию сертификатов. Подпись строгого имени не гарантирует, что подписавшему сборку человеку можно доверять, и не указывает на то, что человек является правомерным владельцем ключа; она означает только то, что владелец ключа подписал сборку. Поэтому не рекомендуется использовать подпись строгого имени как средство проверки безопасности на доверие к коду сторонних разработчиков. Рекомендуемым способом проверки подлинности кода является Microsoft Authenticode.  
  
## <a name="limitations-of-conventional-strong-names"></a>Ограничения обычных строгих имен  
 Технология строгого именования, используемая в версиях до .NET Framework 4.5, имеет указанные ниже недостатки:  
  
- Ключи постоянно подвержены атакам, а улучшенные методы и оборудование облегчают поиск закрытого ключа по открытому. Для защиты от атак необходимы более длинные ключи. Версии .NET Framework до .NET Framework 4.5 предоставляют возможность подписывания с помощью ключа любого размера (размер по умолчанию — 1024 бита), но подпись сборки новым ключом испортит все двоичные файлы, ссылающиеся на старый идентификатор сборки. Поэтому изменение размера ключа подписи является крайне сложным, если необходимо обеспечить совместимость.  
  
- Подпись строгого имени поддерживает только алгоритм SHA-1. Недавно было показано, что алгоритма SHA-1 недостаточно для обеспечения безопасности хэширования. Поэтому необходим более надежный алгоритм (SHA-256 или выше). Возможно, алгоритм SHA-1 утратит статус совместимого с FIPS, что станет проблемой для тех, кто предпочитает использовать только FIPS-совместимое программное обеспечение и алгоритмы.  
  
## <a name="advantages-of-enhanced-strong-names"></a>Преимущества улучшенных строгих имен  
 Основными преимуществами улучшенных строгих имен являются совместимость с уже существующими строгими именами и возможность утверждения эквивалентности одного идентификатора другому.  
  
- Разработчики, которые имеют уже существующие подписанные сборки, могут перенести формирование их идентификаторов на алгоритм SHA-2, сохранив при этом совместимость со сборками, которые ссылаются на старые идентификаторы.  
  
- Разработчики, которые создают новые сборки и не имеют существующих подписей строгого имени, могут использовать более безопасные алгоритмы SHA-2 и подписывать сборки так, как они делали всегда.  
  
## <a name="using-enhanced-strong-names"></a>Использование улучшенных строгих имен  
 Ключи строгого имени состоят из ключа подписи и ключа удостоверения. Сборка подписывается с помощью ключа подписи и не зависит от ключа удостоверения. До выхода версии .NET Framework 4.5 эти ключи были идентичными. Начиная с .NET Framework 4.5 ключ удостоверения остается таким же, как и в более ранних версиях платформы .NET Framework, а ключ подписи улучшается с использованием более надежного хэш-алгоритма. Кроме того, ключ подписи подписывается ключом удостоверения для создания подписи другой стороны.  
  
 Атрибут <xref:System.Reflection.AssemblySignatureKeyAttribute> позволяет метаданным сборки использовать уже существующий открытый ключ для идентификации сборки, что позволяет старым ссылкам на сборки продолжать работать.  Атрибут <xref:System.Reflection.AssemblySignatureKeyAttribute> использует подпись другой стороны для проверки того, является ли владелец нового ключа подписи также владельцем старого ключа удостоверения.  
  
### <a name="signing-with-sha-2-without-key-migration"></a>Подписывание с использованием SHA-2 без переноса ключа  
 Чтобы подписать сборку без переноса подписи строгого имени, выполните указанные ниже команды в окне командной строки.  
  
1. Создайте ключ удостоверения (если необходимо).  
  
    ```  
    sn -k IdentityKey.snk  
    ```  
  
2. Извлеките открытый ключ удостоверения и укажите, что при подписывании этим ключом необходимо использовать алгоритм SHA-2.  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk sha256  
    ```  
  
3. Используйте отложенную подпись сборки с помощью файла с открытым ключом удостоверения.  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
4. Повторно подпишите сборку с помощью полной пары ключей удостоверения.  
  
    ```  
    sn -Ra MyAssembly.exe IdentityKey.snk  
    ```  
  
### <a name="signing-with-sha-2-with-key-migration"></a>Подписывание с использованием SHA-2 с переносом ключа  
 Чтобы подписать сборку с переносом подписи строгого имени, выполните указанные ниже команды в окне командной строки.  
  
1. Создайте пару ключей удостоверения и подписи (если необходимо).  
  
    ```  
    sn -k IdentityKey.snk  
    sn -k SignatureKey.snk  
    ```  
  
2. Извлеките открытый ключ подписи и укажите, что при подписывании этим ключом необходимо использовать алгоритм SHA-2.  
  
    ```  
    sn -p SignatureKey.snk SignaturePubKey.snk sha256  
    ```  
  
3. Извлеките открытый ключ удостоверения, определяющий хэш-алгоритм, с помощью которого создается подпись другой стороны.  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk  
    ```  
  
4. Создайте параметры для атрибута <xref:System.Reflection.AssemblySignatureKeyAttribute> и прикрепите атрибут к сборке.  
  
    ```  
    sn -a IdentityPubKey.snk IdentityKey.snk SignaturePubKey.snk  
    ```  

    Вы увидите приблизительно следующее.

    ```
    Information for key migration attribute.
    (System.Reflection.AssemblySignatureKeyAttribute):
    publicKey=
    002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519
    d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936
    e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b4
    3893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a3
    4d153cdd

    counterSignature=
    e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91eb
    e1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8
    ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3
    ae5fec2c682e57b7442738
    ```

    Эти выходные данные затем могут быть преобразованы в AssemblySignatureKeyAttribute.

    ```
    [assembly:System.Reflection.AssemblySignatureKeyAttribute(
    "002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b43893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a34d153cdd",
    "e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91ebe1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3ae5fec2c682e57b7442738"
    )]
    ```
  
5. Используйте отложенную подпись сборки с помощью открытого ключа удостоверения.  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
6. Подпишите сборку с помощью полной пары ключей удостоверения.  
  
    ```  
    sn -Ra MyAssembly.exe SignatureKey.snk  
    ```  
  
## <a name="see-also"></a>См. также

- [Создание и использование сборок со строгими именами](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)
