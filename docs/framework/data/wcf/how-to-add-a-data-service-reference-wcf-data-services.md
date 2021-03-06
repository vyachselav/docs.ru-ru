---
title: "Как добавить ссылку на службу данных (службы WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Службы WCF Data Services, настройка"
ms.assetid: 62c6f318-3ee1-433a-b7a3-efa234c3034c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Как добавить ссылку на службу данных (службы WCF Data Services)
Для добавления ссылки на службу [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] можно использовать диалоговое окно **Добавление ссылки на службу** в среде Visual Studio.  Это позволяет упростить доступ к службе данных в клиентском приложении, разрабатываемом в среде Visual Studio.  По завершении этой процедуры формируются классы данных на основе метаданных, полученных от службы данных.  Для получения дополнительной информации см. [Формирование клиентской библиотеки службы данных](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md).  
  
### Добавление ссылки на службу данных  
  
1.  Если служба данных не является частью решения и пока не запущена, запустите ее и отметьте ее URI. \(Необязательно.\)  
  
2.  Щелкните правой кнопкой мыши клиентский проект и выберите команду **Добавить ссылку на службу**.  
  
3.  Если служба данных является частью текущего решения, нажмите кнопку **Обнаружить**.  
  
     \-или\-  
  
     В текстовом поле **Адрес** введите базовый URL\-адрес службы данных, например `http://localhost:1234/Northwind.svc`, и нажмите кнопку **Перейти**.  
  
4.  Нажмите кнопку **ОК**.  
  
     При этом добавляется новый файл кода, содержащий классы данных, которые используются для обращения и взаимодействия с ресурсами службы данных как с объектами.  
  
## См. также  
 [Краткое руководство](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)