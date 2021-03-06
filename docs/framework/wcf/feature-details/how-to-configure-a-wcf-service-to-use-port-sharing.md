---
title: "Как настраивать службы Windows Communication Foundation на совместное использование портов | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6400bc71-a858-4ac2-8d5a-caa72d3b5482
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Как настраивать службы Windows Communication Foundation на совместное использование портов
Самый простой способ совместно использовать порт net.tcp:\/\/ в приложении [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] — раскрыть службу для использования с помощью <xref:System.ServiceModel.NetTcpBinding>.  
  
 Эта привязка предоставляет свойство <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A>, которое определяет, включено ли совместное использование порта net.tcp:\/\/ для службы, настраиваемой с этой привязкой.  
  
 Следующая процедура показывает, как использовать класс <xref:System.ServiceModel.NetTcpBinding>, чтобы открыть конечную точку по универсальному коду ресурса \(URI\) net.tcp:\/\/localhost\/MyService, сначала в коде, а затем с помощью элементов конфигурации.  
  
### Включение совместного использования порта net.tcp:\/\/ в привязке NetTcpBinding с помощью кода  
  
1.  Создайте службу, реализующую контракт с именем `IMyService` , и вызовите ее `MyService`.  
  
     [!code-csharp[c_ConfigurePortSharing#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_configureportsharing/cs/source.cs#1)]
     [!code-vb[c_ConfigurePortSharing#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_configureportsharing/vb/source.vb#1)]  
  
2.  Создайте экземпляр класса <xref:System.ServiceModel.NetTcpBinding> и задайте для свойства <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A> значение `true`.  
  
     [!code-csharp[c_ConfigurePortSharing#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_configureportsharing/cs/source.cs#2)]
     [!code-vb[c_ConfigurePortSharing#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_configureportsharing/vb/source.vb#2)]  
  
3.  Создайте <xref:System.ServiceModel.ServiceHost> и добавьте в него конечную точку службы для `MyService`, использующей привязку <xref:System.ServiceModel.NetTcpBinding>, поддерживающую совместное использование порта, и ожидающей передачи данных по универсальному коду ресурса \(URI\) адреса конечной точки "net.tcp:\/\/localhost\/MyService".  
  
     [!code-csharp[c_ConfigurePortSharing#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_configureportsharing/cs/source.cs#3)]
     [!code-vb[c_ConfigurePortSharing#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_configureportsharing/vb/source.vb#3)]  
  
    > [!NOTE]
    >  В этом примере используется TCP\-порт 808 по умолчанию, так как в универсальном коде ресурса \(URI\) адреса конечной точки не указан другой номер порта.Так как в транспортной привязке явно включено совместное использование порта, эта служба может использовать порт 808 совместно с другими службами в других процессах.Если бы совместное использование порта не было бы разрешено и порт 808 уже использовался бы другим приложением, то при открытии данной службы она бы создала исключение <xref:System.ServiceModel.AddressAlreadyInUseException>.  
  
### Включение совместного использования порта net.tcp:\/\/ в привязке NetTcpBinding с помощью конфигурации  
  
1.  В следующем примере показано, как включить совместное использование порта и добавить конечную точку службы с помощью элементов конфигурации.  
  
```  
<system.serviceModel>  
  <bindings>  
    <netTcpBinding name="portSharingBinding"   
                   portSharingEnabled="true" />  
  </bindings>  
  <services>  
    <service name="MyService">  
        <endpoint address="net.tcp://localhost/MyService"  
                  binding="netTcpBinding"  
                  contract="IMyService"  
                  bindingConfiguration="portSharingBinding" />  
    </service>  
  </services>  
</system.serviceModel>  
```  
  
## См. также  
 [Net.TCP Port Sharing](http://msdn.microsoft.com/ru-ru/f13692ee-a179-4439-ae72-50db9534eded)   
 [Практическое руководство. Включение службы совместного использования портов Net.TCP](../../../../docs/framework/wcf/feature-details/how-to-enable-the-net-tcp-port-sharing-service.md)