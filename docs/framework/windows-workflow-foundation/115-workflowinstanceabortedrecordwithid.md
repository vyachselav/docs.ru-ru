---
title: "115 - WorkflowInstanceAbortedRecordWithId | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0293dd4e-e6ae-473a-b3d6-c2d38f9bd875
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 115 - WorkflowInstanceAbortedRecordWithId
## Свойства  
  
|||  
|-|-|  
|Идентификатор|115|  
|Ключевые слова|HealthMonitoring, WFTracking|  
|Уровень|Предупреждение|  
|Канал|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Описание  
 Это событие создается участником отслеживания ETW, когда экземпляр рабочего процесса создает запись WorkflowInstanceAbortedRecord.  
  
## Сообщение  
 TrackRecord \= WorkflowInstanceAbortedRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, Reason \= %5, Annotations \= %6, ProfileName \= %7, WorkflowDefinitionIdentity \= %8  
  
## Подробные сведения  
  
|Имя элемента данных|Тип элемента данных|Описание|  
|-------------------------|-------------------------|--------------|  
|InstanceId|xs:GUID|Идентификатор экземпляра для рабочего процесса.|  
|RecordNumber|xs:long|Порядковый номер созданной записи.|  
|EventTime|xs:dateTime|Время в формате UTC, когда было создано событие.|  
|ActivityDefinitionId|xs:string|Имя корневого действия в рабочем процессе.|  
|Состояние|xs:string|Текущее состояние рабочего процесса.|  
|Заметки|xs:string|Заметки, добавленные к этому событию.  Значения хранятся в XML\-элементе в формате \<items\>\< item name \= "annotationName" type\="System.String"\>annotationValue\<\/item\>\<\/items\>.  Если ни одной заметки не указано, строка содержит \<items\/\>.  Размер событий ETW ограничен размером буфера ETW или максимальным размером полезных данных для события ETW.  Если размер события превышает пределы трассировки событий Windows, событие усекается путем отбрасывания заметок и замены значения заметок значением \<items\>...\<\/items\>.|  
|ProfileName|xs:string|Имя или профиль отслеживания, который привел к созданию этого события.|  
|WorkflowDefinitionIdentity|xs:string|Идентификатор определения рабочего процесса|  
|AppDomain|xs:string|Строка, возвращаемая AppDomain.CurrentDomain.FriendlyName.|