---
title: "Автоматическая настройка IPv6 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 581c1d21-1013-43a3-bf3e-2d9ead62b79c
caps.latest.revision: 5
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 5
---
# Автоматическая настройка IPv6
Одна \- важная цель для IP версии 6 поддержки Plug и Play узла.  Это значит, должно быть возможно подключение узел в сети IP версии 6 и его автоматически настроенного естественный без вмешательства.  
  
## Тип Автоматический\-Конфигурации  
 IP версии 6 поддерживает следующие типы автоматическ\-конфигурации:  
  
-   **Stateful auto\-configuration**.  Этот тип конфигурации требует какого\-либо уровня естественный вмешательства поскольку для этого требуется протокол DHCP для сервера IP версии 6 \(DHCPv6\) для установки и администрирования узлов.  Сервер DHCPv6 хранит список узлов, к которым он предоставляет сведения о конфигурации.  Он также хранит сведения о состоянии, поэтому сервер знает, как долго каждый адрес используется, и когда он может быть доступен для переприсвоения.  
  
-   **Stateless auto\-configuration**.  Этот тип конфигурации подходит для небольших и цене.  В этом случае каждое основное приложение определяет его адреса из содержимого получаемых объявления маршрутизатора.  Использование стандарт IEEE EUI\-64 для определения сетевого адреса часть идентификатора, разумно иметь уникальность адреса узла в связи.  
  
 Независимо от способа определить адрес, узел должен проверить, что его потенциальный адрес однозначно локальной ссылки.  Это делается путем отправки сообщения с соседним узлом потенциальному домогательства к адресу.  Если узел получает любой ответ, он знает, что адрес уже используется и должен указать другой адрес.  
  
## Удобоподвижность IP версии 6  
 Пролиферация мобильных устройств вводила новое требование: Устройство должно иметь возможность произвольно изменение местоположения на IP версии 6 Интернете и по\-прежнему поддерживать существующие соединения.  Чтобы обеспечить эту возможность, присвоен передвижному узел главного окна адрес, по которому его всегда может быть достигнута.  Если мобильный узел at home, он соединяется со ссылками дома и использует его адрес главного окна.  Если мобильный узел далеко от дома, домашних агента, который обычно маршрутизатор сообщения передвижным relay между узлом и узлы, с которым он связывается.  
  
## См. также  
 [Протокол IP версии 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)   
 [Сокеты](../../../docs/framework/network-programming/sockets.md)