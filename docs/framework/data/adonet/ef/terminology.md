---
title: "Терминология платформы Entity Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: fa2a1bd1-6118-487b-8673-eebc66b92945
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Терминология платформы Entity Framework
В этом разделе определены термины, которые часто встречаются в документации по [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Даны ссылки на соответствующие разделы, содержащие дополнительные сведения.  
  
|Термин|Определение|  
|------------|-----------------|  
|ассоциация|Определение отношения между двумя типами сущностей.<br /><br /> Дополнительные сведения см. в разделах [Association Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/c305169a-8af7-432f-9ba7-800a163aed41) и [тип ассоциации](../../../../../docs/framework/data/adonet/association-type.md).|  
|набор ассоциаций|Логический контейнер для экземпляров ассоциаций одного типа.<br /><br /> Дополнительные сведения см. в разделах [AssociationSet Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/512cbb75-cebe-4f3f-970d-3419deeff684) и [набор ассоциаций](../../../../../docs/framework/data/adonet/association-set.md).|  
|Code First|Начиная с версии 4.1 платформы Entity Framework, модель можно создавать программно с помощью шаблона разработки Code First.  Шаблон разработки Code First имеет два различных сценария.  В обоих случаях разработчик определяет модель, задавая в коде определения классов .NET Framework, а затем выборочно определяет дополнительные сопоставления или конфигурации с помощью заметок к данным или fluent API.<br /><br /> Следует иметь в виду, что шаблон разработки Code First является частью [платформы Entity Framework 5.0](http://go.microsoft.com/fwlink/?LinkId=234900).  Платформа Entity Framework 5.0 не является частью платформы .NET Framework, но построена на .NET Framework 4.5.  Платформа Entity Framework 5.0 доступна в качестве пакета [NuGet](http://go.microsoft.com/fwlink/?LinkId=232488) [«Entity Framework»](http://go.microsoft.com/fwlink/?LinkID=215714).  Дополнительные сведения см. в разделе [Выпуски и управление версиями платформы Entity Framework](http://go.microsoft.com/fwlink/?LinkId=234899).|  
|дерево команд|Типовое программное представление всех запросов [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], состоящих из одного или нескольких выражений.<br /><br /> Для получения дополнительной информации см. [Общие сведения о платформе Entity Framework](../../../../../docs/framework/data/adonet/ef/overview.md).|  
|сложный тип|Класс [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)], представляющий сложное свойство согласно определению в концептуальной модели.  Сложные типы позволяют организовать скалярные свойства внутри сущностей.  Сложные объекты являются экземплярами сложных типов.  Дополнительные сведения см. в разделах [ComplexType Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/f1c2f311-9889-4b87-abd8-a94f322052e3) и [сложный тип](../../../../../docs/framework/data/adonet/complex-type.md).|  
|ComplexType|Спецификация типа данных, которая представляет нескалярное свойство типа сущности, не имеющего ключевого свойства.<br /><br /> Дополнительные сведения см. в разделах [ComplexType Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/f1c2f311-9889-4b87-abd8-a94f322052e3) и [сложный тип](../../../../../docs/framework/data/adonet/complex-type.md).|  
|концептуальная модель|Абстрактная спецификация для типов сущностей, сложных типов, сопоставлений, контейнеров сущностей, наборов сущностей и наборов сопоставлений в домене приложения [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Концептуальная модель определяется на языке CSDL в CSDL\-файле.<br /><br /> Для получения дополнительной информации см. [Моделирование и сопоставление](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md).|  
|CSDL\-файл|XML\-файл, содержащий концептуальную модель на языке CSDL.|  
|CSDL \(язык определения концептуальной схемы\)|Основанный на XML язык, используемый для определения типов сущностей, ассоциаций, контейнеров сущностей, наборов сущностей и наборов ассоциаций концептуальной модели.<br /><br /> Для получения дополнительной информации см. [Спецификация языка CSDL](../../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md).|  
|контейнер|Логическое группирование наборов сущностей и ассоциаций.<br /><br /> Дополнительные сведения см. в разделах [EntityContainer Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/06d03ecb-3b7a-4e7f-95d5-b95307d47a27) и [контейнер сущностей](../../../../../docs/framework/data/adonet/entity-container.md).|  
|параллельность|Позволяет нескольким пользователям одновременно обращаться и изменять совместно используемые данные.  По умолчанию в платформе [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] реализуется модель оптимистичного параллелизма.|  
|направление|Указывает асимметричную природу некоторых сопоставлений.  Направление указывается с помощью атрибутов `FromRole` и `ToRole` элемента `NavigationProperty` или `ReferentialConstraint` в схеме.<br /><br /> Дополнительные сведения см. в разделах [NavigationProperty Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/5829a238-a50e-4c81-901d-7b54fc00f27e) и [свойство навигации](../../../../../docs/framework/data/adonet/navigation-property.md).|  
|безотлагательная загрузка|Процесс загрузки конкретного набора связанных между собой объектов вместе с объектами, которые были запрошены явным образом.|  
|EDMX\-файл|XML\-файл, содержащий концептуальную модель \(на языке CSDL\), модель хранения \(на языке SSDL\) и сопоставления между ними \(на языке MSL\).  Edmx\-файл создается средствами [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)]. Дополнительные сведения см. в разделе [.edmx File Overview](http://msdn.microsoft.com/ru-ru/f4c8e7ce-1db6-417e-9759-15f8b55155d4).|  
|end|Сущность, участвующая в ассоциации.<br /><br /> Дополнительные сведения см. в разделах [End Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/04f3c141-95bc-424b-989b-1c071b449e7c) и [конечная точка ассоциации](../../../../../docs/framework/data/adonet/association-end.md).|  
|сущность|Концепция в области приложения, по которой определен тип данных.<br /><br /> Дополнительные сведения см. в разделах [EntityType Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/19562e9f-fd70-4b59-bc15-3e289cbb6054) и [тип сущности](../../../../../docs/framework/data/adonet/entity-type.md).|  
|EntityClient|Независимый от хранилища поставщик данных [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)], содержащий такие классы, как `EntityConnection`, `EntityCommand` и `EntityDataReader`.  Работает с [!INCLUDE[esql](../../../../../includes/esql-md.md)] и подключается к зависящим от хранилища поставщикам данных [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)], таким как `SqlClient`.<br /><br /> Для получения дополнительной информации см. [Поставщик EntityClient для платформы Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).|  
|контейнер сущностей|Задает наборы сущностей и наборы ассоциаций, которые будут реализованы в заданном пространстве имен.<br /><br /> Дополнительные сведения см. в разделах [EntityContainer Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/06d03ecb-3b7a-4e7f-95d5-b95307d47a27) и [контейнер сущностей](../../../../../docs/framework/data/adonet/entity-container.md).|  
|Модель EDM|Набор понятий, описывающих структуру данных \(например, сущности и отношения\) независимо от формы ее хранения.<br /><br /> Для получения дополнительной информации см. [Модель EDM](../../../../../docs/framework/data/adonet/entity-data-model.md).|  
|Entity Framework|Набор технологий, который поддерживает разработку приложений, связанных с обработкой данных, позволяя программистам работать с концептуальными моделями, сопоставленными логическим схемам в источниках данных.<br /><br /> Для получения дополнительной информации см. [Общие сведения о платформе Entity Framework](../../../../../docs/framework/data/adonet/ef/overview.md).|  
|набор сущностей|Логический контейнер для сущностей данного типа и его подтипов.  Наборы сущностей сопоставляются таблицам в базе данных.<br /><br /> Дополнительные сведения см. в разделах [EntitySet Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/ec56db77-718d-4c0e-adc9-f1d33c896287) и [набор сущностей](../../../../../docs/framework/data/adonet/entity-set.md).|  
|Entity SQL|Независимый от хранилища диалект SQL, который работает непосредственно с концептуальными схемами сущностей и поддерживает такие понятия концептуальной модели, как наследование и отношения.<br /><br /> Для получения дополнительной информации см. [Язык Entity SQL](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md).|  
|тип сущности|Класс [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)], представляющий сущность согласно определению в концептуальной модели.  Типы сущностей могут иметь скалярные и сложные свойства, а также свойства навигации.  Объекты являются экземплярами типов сущностей.  Для получения дополнительной информации см. [Работа с объектами](../../../../../docs/framework/data/adonet/ef/working-with-objects.md).|  
|EntityType|Спецификация для типа данных, которая содержит ключ и именованный набор свойств, и представляет элемент верхнего уровня в концептуальной модели или модели хранения.<br /><br /> Дополнительные сведения см. в разделах [EntityType Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/19562e9f-fd70-4b59-bc15-3e289cbb6054) и [тип сущности](../../../../../docs/framework/data/adonet/entity-type.md).|  
|явная загрузка|Когда запрос возвращает объекты, связанные объекты не загружаются.  По умолчанию они не загружаются до тех пор, пока не будут явным образом запрошены вызовом метода `Load` для свойства навигации.|  
|сопоставление на основе внешнего ключа|Сопоставление между сущностями, управляемая через свойства внешнего ключа.|  
|идентифицирующее отношение|Отношение, в котором первичный ключ основной сущности является частью первичного ключа зависимой сущности.  В таком отношении зависимая сущность не может существовать без основной.|  
|независимое сопоставление|Сопоставленение между сущностями, представляемое и отслеживаемое независимым объектом.|  
|клавиша|Атрибут типа сущности, который указывает, какое свойство или набор свойств используется для определения уникальных экземпляров типа сущности.  Представлен на уровне объектов классом <xref:System.Data.EntityKey>.<br /><br /> Дополнительные сведения см. в разделах [Key Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/0cdb1402-dbc7-4a04-a11e-5729cdf7431b) и [ключ сущности](../../../../../docs/framework/data/adonet/entity-key.md).|  
|отложенная загрузка|Когда запрос возвращает объекты, связанные объекты не загружаются.  Вместо этого они загружаются автоматически, когда производится доступ к свойству навигации.|  
|[!INCLUDE[linq_entities](../../../../../includes/linq-entities-md.md)]|Синтаксис запроса, который определяет набор операторов запроса, обеспечивающих операции просмотра, фильтрации и проекции, выражаемые прямым, декларативным способом в [!INCLUDE[csprcs](../../../../../includes/csprcs-md.md)] и [!INCLUDE[vbprvb](../../../../../includes/vbprvb-md.md)].<br /><br /> Для получения дополнительной информации см. [LINQ to Entities](../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md).|  
|сопоставление|Спецификация соответствий между элементами в концептуальной модели и элементами в модели хранения.<br /><br /> Для получения дополнительной информации см. [Спецификация языка MSL](../../../../../docs/framework/data/adonet/ef/language-reference/msl-specification.md).|  
|MSL\-файл|XML\-файл, содержащий сопоставление концептуальной модели и модели хранения, описанное на языке MSL.|  
|MSL \(язык определения соответствий\)|Основанный на XML язык, используемый для сопоставления элементов, определенных в концептуальной модели, элементам в модели хранилища.<br /><br /> Для получения дополнительной информации см. [Спецификация языка MSL](../../../../../docs/framework/data/adonet/ef/language-reference/msl-specification.md).|  
|функции изменения|Хранимые процедуры, которые используются для вставки, обновления и удаления данных, находящихся в источнике данных.  Эти функции используются вместо сформированных команд [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Функции изменения определены элементом `Function` в модели хранения.  Элемент [ModificationFunctionMapping](http://msdn.microsoft.com/ru-ru/b44b5b13-9937-448b-ba36-7a0cfefea782) сопоставляет эти функции изменения операциям вставки, обновления и удаления для сущностей, определенных в концептуальной модели.|  
|кратность|Количество сущностей, которые могут существовать на каждой стороне связи, как определено ассоциацией.  Также называется мощностью или количеством элементов.<br /><br /> Дополнительные сведения см. в разделах [End Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/04f3c141-95bc-424b-989b-1c071b449e7c) и [конечная точка ассоциации](../../../../../docs/framework/data/adonet/association-end.md).|  
|несколько наборов сущностей на тип|Возможность определить тип сущности в более чем одном наборе сущностей.<br /><br /> Дополнительные сведения см. в разделах [EntitySet Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/ec56db77-718d-4c0e-adc9-f1d33c896287) и [How to: Define a Model with Multiple Entity Sets per Type](http://msdn.microsoft.com/ru-ru/61aa4fca-5ac0-4f47-9bc8-46e8c2965ef7).|  
|свойство навигации|Свойство типа сущности, которое представляет связь с другим типом сущности, как определено ассоциацией.  Свойства навигации используются, чтобы возвратить связанные объекты как <xref:System.Data.Objects.DataClasses.EntityCollection%601> или <xref:System.Data.Objects.DataClasses.EntityReference%601>, в зависимости от кратности другого элемента сопоставления.<br /><br /> Дополнительные сведения см. в разделах [NavigationProperty Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/5829a238-a50e-4c81-901d-7b54fc00f27e) и [свойство навигации](../../../../../docs/framework/data/adonet/navigation-property.md).|  
|путь запроса|Строковое представление пути, которое показывает, какие связанные объекты будут возвращены при выполнении запроса объектов.  Путь запроса определяется путем вызова метода <xref:System.Data.Objects.ObjectQuery%601.Include%2A> объекта <xref:System.Data.Objects.ObjectQuery%601>.<br /><br /> Для получения дополнительной информации см. [Loading Related Objects](http://msdn.microsoft.com/ru-ru/452347d2-7b3b-44cd-9001-231299a28cb1).|  
|контекст объекта|Представляет контейнер сущностей, определенный в концептуальной модели.  Содержит соединение с базовым источником данных и предоставляет такие службы, как отслеживание изменений и разрешение идентификаторов.  Контекст объекта представлен экземпляром класса <xref:System.Data.Objects.ObjectContext> или `DbContext`.<br /><br /> `DbContext` является частью [платформы Entity Framework 5.0](http://go.microsoft.com/fwlink/?LinkId=234900).  Платформа Entity Framework 5.0 не является частью платформы .NET Framework, но построена на .NET Framework 4.5.  Платформа Entity Framework 5.0 доступна в качестве пакета [NuGet](http://go.microsoft.com/fwlink/?LinkId=232488) [«Entity Framework»](http://go.microsoft.com/fwlink/?LinkID=215714).  Дополнительные сведения см. в разделе [Выпуски и управление версиями платформы Entity Framework](http://go.microsoft.com/fwlink/?LinkId=234899).|  
|уровень объектов|Типы сущностей и определения контекста объектов, используемых платформой Entity Framework.|  
|запросы объектов|Запрос, выполняемый в контексте объекта на концептуальной модели, возвращающий данные как объекты.<br /><br /> Для получения дополнительной информации см. [Object Queries](http://msdn.microsoft.com/ru-ru/0768033c-876f-471d-85d5-264884349276).|  
|объектно\-реляционное сопоставление|Метод преобразования данных из реляционной базы данных в типы данных, которые могут быть использованы в объектно\-ориентированных приложениях.<br /><br /> Платформа [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] обеспечивает объектно\-реляционное сопоставление, которое сопоставляет реляционные данные, определенные в модели хранения, с типами данных, определенными в концептуальной модели.<br /><br /> Для получения дополнительной информации см. [Моделирование и сопоставление](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md).|  
|службы объектов|Службы, предоставленные платформой [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], которые позволяют коду приложения работать с такими сущностями, как объекты [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)].|  
|объекты, игнорирующие сохраняемость|Объект, который не содержит никакой логики, относящейся к хранилищу данных.  Также называется сущностью POCO.|  
|POCO|Традиционный объект среды CLR.  Объект, который не является производным от другого класса и не реализует интерфейсы.|  
|сущность POCO|Сущность [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], которая не является производной от классов <xref:System.Data.Objects.DataClasses.EntityObject> и <xref:System.Data.Objects.DataClasses.ComplexObject> и не реализует интерфейсы [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Сущности POCO часто представляют существующие объекты домена, используемые в приложении [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Эти сущности поддерживают пропуск сохраняемости.  Для получения дополнительной информации см. [Working with POCO Entities](http://msdn.microsoft.com/ru-ru/5e0fb82a-b6d1-41a1-b37b-c12db61629d3).|  
|прокси\-объект|Объект, который является производным от класса POCO и формируется платформой [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] для поддержки отложенной загрузки и отслеживания изменений.  Для получения дополнительной информации см. [Requirements for Creating POCO Proxies](http://msdn.microsoft.com/ru-ru/dcdbf982-9b9d-4582-806a-64de4a1c03c8).|  
|справочное ограничение|Ограничение, которое определено в концептуальной модели и указывает, что сущность имеет зависимое отношение с другой сущностью.  Это ограничение означает, что экземпляр зависимой сущности не может существовать без соответствующего экземпляра главной сущности.<br /><br /> Дополнительные сведения см. в разделах [ReferentialConstraint Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/24f96a80-85b5-4f2e-a14c-0e3eb6796fa0) и [ограничение ссылочной целостности](../../../../../docs/framework/data/adonet/referential-integrity-constraint.md).|  
|отношение|Логическое соединение между сущностями.|  
|роль|Имя, данное каждому `End` сопоставления, чтобы сделать более ясной семантику отношения.<br /><br /> Дополнительные сведения см. в разделах [End Element \(CSDL\)](http://msdn.microsoft.com/ru-ru/04f3c141-95bc-424b-989b-1c071b449e7c) и [конечная точка ассоциации](../../../../../docs/framework/data/adonet/association-end.md).|  
|скалярное свойство|Свойство сущности, которое сопоставляется одному полю в модели хранения.|  
|сущность с самостоятельным отслеживанием|Сущность, построенная средствами преобразования текстовых шаблонов \(T4\), которая может записывать изменения скалярных свойств, сложных свойств и свойств навигации.|  
|простой тип|Тип\-примитив, который используется для определения свойств в концептуальной модели.<br /><br /> Дополнительные сведения см. в разделах [Conceptual Model Types \(CSDL\)](http://msdn.microsoft.com/ru-ru/987b995f-e429-4569-9559-b4146744def4) и [Модель EDM. Примитивные типы данных](../../../../../docs/framework/data/adonet/entity-data-model-primitive-data-types.md).|  
|разделенная сущность|Тип сущности, сопоставляемый с двумя отдельными типами в модели хранения.<br /><br /> Для получения дополнительной информации см. [How to: Define a Model with a Single Entity Mapped to Two Tables](http://msdn.microsoft.com/ru-ru/01762517-e4ab-439d-99e6-564ab7d6f3ed).|  
|модель хранения|Определение для логической модели данных в поддерживаемом источнике данных, таком как реляционная база данных.  Модель хранения определяется на языке SSDL в SSDL\-файле модели хранения.<br /><br /> Дополнительные сведения см. в разделах [Моделирование и сопоставление](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md) и [Спецификация языка SSDL](../../../../../docs/framework/data/adonet/ef/language-reference/ssdl-specification.md).|  
|SSDL\-файл|XML\-файл, содержащий модель хранения, описанную на языке SSDL.|  
|SSDL \(язык определения структуры схемы\)|Язык на основе XML, который используется для определения типов сущностей, ассоциаций, контейнеров сущностей, наборов сущностей и наборов ассоциаций модели хранения, которая часто соответствует схеме базы данных.<br /><br /> Для получения дополнительной информации см. [Спецификация языка SSDL](../../../../../docs/framework/data/adonet/ef/language-reference/ssdl-specification.md).|  
|одна таблица на иерархию|Метод моделирования иерархии типов в базе данных, согласно которому атрибуты всех типов в иерархии помещаются в одну таблицу.|  
|одна таблица на тип|Метод моделирования иерархии типов в базе данных, согласно которому для моделирования разных типов используются разные таблицы, связанные отношением «один к одному».|  
  
## См. также  
 [Платформа ADO.NET Entity Framework](../../../../../docs/framework/data/adonet/ef/index.md)   
 [Общие сведения о платформе Entity Framework](../../../../../docs/framework/data/adonet/ef/overview.md)   
 [Приступая к работе](../../../../../docs/framework/data/adonet/ef/getting-started.md)   
 [Ресурсы платформы Entity Framework](../../../../../docs/framework/data/adonet/ef/resources.md)