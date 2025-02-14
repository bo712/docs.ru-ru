---
title: Сериализация (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 67379a76-5465-4af8-a781-0b0b25a62d9a
ms.openlocfilehash: 947b38e8166ba05d871aafbaba5766aa9dab21f4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61751117"
---
# <a name="serialization-visual-basic"></a>Сериализация (Visual Basic)
Сериализация — это процесс преобразования объекта в поток байтов для сохранения или передачи в память, в базу данных или в файл. Эта операция предназначена для того, чтобы сохранить состояния объекта для последующего воссоздания при необходимости. Обратный процесс называется десериализацией.  
  
## <a name="how-serialization-works"></a>Как работает сериализация  
 На этом рисунке показан общий процесс сериализации.  
  
![График сериализации](./media/index/serialization-process.gif)
  
 Объект сериализуется в поток, который содержит не только данные, но и сведения о типе объекта, например номер версии, язык и региональные параметры, имя сборки. В этом формате потока объект можно сохранить в базе данных, файле или памяти.  
  
### <a name="uses-for-serialization"></a>Применение сериализации  
 Сериализация позволяет разработчику сохранять состояние объекта и воссоздавать его при необходимости. Это полезно для длительного хранения объектов или для обмена данными. Используя сериализацию, разработчик может, например, отправить объект удаленному приложению через веб-службу, передать объект из одного домена в другой, передать объект через брандмауэр в виде XML-строки, обеспечить защиту или сохранность сведений о пользователях в разных приложениях.  
  
### <a name="making-an-object-serializable"></a>Превращение объекта в сериализуемый  
 Чтобы сериализовать объект, вам нужен сам этот объект, поток, который будет содержать объект, и класс <xref:System.Runtime.Serialization.Formatter>. Классы для сериализации и десериализации объектов содержатся в <xref:System.Runtime.Serialization>.  
  
 Примените к типу атрибут <xref:System.SerializableAttribute>, чтобы указать возможность сериализации экземпляров этого типа. Если в типе нет атрибута <xref:System.SerializableAttribute> при попытке сериализации, выдается исключение <xref:System.Runtime.Serialization.SerializationException>.  
  
 Если вы не хотите, чтобы поле в классе было сериализуемым, примените атрибут <xref:System.NonSerializedAttribute>. Если поле сериализуемого типа содержит указатель, дескриптор или специальные структуры данных для определенной среды, и содержимое этого поле невозможно разумно воссоздать в другой среде, такое поле лучше сделать несериализуемым.  
  
 Если сериализуемый класс содержит ссылки на объекты других классов, имеющие пометку <xref:System.SerializableAttribute>, эти объекты тоже будут сериализованы.  
  
## <a name="binary-and-xml-serialization"></a>Двоичная сериализация и сериализация XML  
 Вы можете использовать двоичную сериализацию или XML-сериализацию. Процесс двоичной сериализации сериализует все элементы, даже доступные только для чтения. Также этот вариант имеет более высокую производительность. XML-сериализация создает более удобочитаемый код и предоставляет больше возможностей для совместного доступа к объектам и использования объектов в процессах взаимодействия.  
  
### <a name="binary-serialization"></a>Двоичная сериализация  
 Двоичная сериализация использует двоичное кодирование, создавая компактные потоки для хранения или передачи через сетевые сокеты.  
  
### <a name="xml-serialization"></a>XML-сериализация  
 При XML-сериализации все открытые поля и свойства объекта (или параметры и возвращаемые значения метода) сериализуются в XML-поток по правилам определенного документа XSD (язык определения схемы XML). XML-сериализация создает строго типизированные классы с открытыми свойствами и полями, которые преобразуются в формат XML. Пространство имен <xref:System.Xml.Serialization> содержит классы, которые нужны для сериализации и десериализации XML.  
  
 Чтобы контролировать сериализацию и десериализацию экземпляров класса, осуществляемую <xref:System.Xml.Serialization.XmlSerializer>, вы можете применять к классам и их членам специальные атрибуты.  
  
## <a name="basic-and-custom-serialization"></a>Базовая и пользовательская сериализация  
 Существует два способа выполнить сериализацию — базовый и пользовательский. Базовая сериализация использует платформу .NET Framework для автоматической сериализации объекта.  
  
### <a name="basic-serialization"></a>Базовая сериализация  
 Единственное условие для выполнения базовой сериализации — наличие атрибута <xref:System.SerializableAttribute> у сериализуемого объекта. Атрибут <xref:System.NonSerializedAttribute> также можно использовать для исключения из сериализации определенных полей.  
  
 При использовании базовой сериализации возможны проблемы с управлением версиями объектов. Если для вас это важно, рассмотрите вариант пользовательской сериализации. Базовая сериализация является самым простым способом сериализации, но не дает почти никакого контроля над процессом.  
  
### <a name="custom-serialization"></a>Пользовательская сериализация  
 Используя пользовательскую сериализацию, вы можете точно указать, какие объекты и как будут сериализованы. Класс должен иметь отметку <xref:System.SerializableAttribute> и реализовывать интерфейс <xref:System.Runtime.Serialization.ISerializable>.  
  
 Если вы хотите настраивать и десериализацию объекта, необходимо использовать пользовательский конструктор.  
  
## <a name="designer-serialization"></a>Сериализация конструктора  
 Сериализация конструктора — это особая форма сериализации, при которой применяется способ постоянного хранения объектов, обычно используемый в средствах разработки. Сериализация конструктора выполняет преобразование графа объекта в файл исходного кода, с помощью которого впоследствии можно восстановить граф объекта. Этот файл исходного кода может содержать программный код, разметку или даже информацию из таблицы SQL.  
  
## <a name="BKMK_RelatedTopics"></a> Связанные разделы и примеры  
 [Пошаговое руководство: Сохранение объекта в Visual Studio (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/walkthrough-persisting-an-object-in-visual-studio.md)  
 Демонстрирует, как с помощью сериализации сохранить данные объекта между экземплярами, чтобы сохранять значения и извлекать их при следующем создании экземпляра объекта.  
  
 [Практическое руководство. Чтение данных объекта из XML-файл (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-read-object-data-from-an-xml-file.md)  
 Показывает считывание данных объекта, которые ранее были записаны в XML-файл с помощью класса <xref:System.Xml.Serialization.XmlSerializer>.  
  
 [Практическое руководство. Запись данных объекта в XML-файл (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md)  
 Показывает, как записать объект из класса в XML-файл с помощью класса <xref:System.Xml.Serialization.XmlSerializer>.
