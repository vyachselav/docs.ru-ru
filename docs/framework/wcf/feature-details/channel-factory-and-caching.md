---
title: "Производство каналов и кэширование | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 954f030e-091c-4c0e-a7a2-10f9a6b1f529
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Производство каналов и кэширование
Клиентские приложения WCF используют класс <xref:System.ServiceModel.ChannelFactory%601> для создания коммуникационного канала со службой WCF.Создание экземпляров класса <xref:System.ServiceModel.ChannelFactory%601> оказывает определенное влияние на производительность, поскольку выполняются следующие операции:  
  
-   Построение дерева <xref:System.ServiceModel.Description.ContractDescription>  
  
-   Отображение всех необходимых типов CLR  
  
-   Построение стека каналов  
  
-   Освобождение ресурсов  
  
 Чтобы помочь минимизировать это влияние, WCF может кэшировать фабрики каналов при использовании прокси клиента WCF.  
  
> [!TIP]
>  Вы непосредственно управляете созданием фабрики каналов, когда класс <xref:System.ServiceModel.ChannelFactory%601> используется напрямую.  
  
 Клиентские классы\-посредники WCF, сформированные с помощью [Служебное средство ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md), являются производными от <xref:System.ServiceModel.ClientBase%601>.<xref:System.ServiceModel.ClientBase%601> определяет статическое свойство <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A>, которое определяет режим кэширования фабрики каналов.Параметры кэша задаются для определенного типа.Например, установка `ClientBase<ITest>.CacheSettings` в одно из значений, указанных ниже, повлияет только на класс\-посредник или ClientBase типа `ITest`.Параметры кэша для конкретного <xref:System.ServiceModel.ClientBase%601> являются неизменяемыми после создания первого экземпляра класса\-посредника или ClientBase.  
  
## Установка режима кэширования  
 Режим кэширования задается установкой свойства <xref:System.ServiceModel.ClientBase%601.CacheSetting> в одно из следующих значений.  
  
|Значение параметра кэша|Описание|  
|-----------------------------|--------------|  
|<xref:System.ServiceModel.CacheSetting.AlwaysOn>|Все экземпляры <xref:System.ServiceModel.ClientBase%601> в пределах домена приложения могут участвовать в кэшировании.Разработчик определил, что при кэшировании не будет неблагоприятных последствий для безопасности.Кэширование не будет отключаться даже во время доступа к «секретным» свойствам <xref:System.ServiceModel.ClientBase%601>.«Секретные» свойства <xref:System.ServiceModel.ClientBase%601> — это <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A>, <xref:System.ServiceModel.ClientBase%601.Endpoint%2A> и <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A>.|  
|<xref:System.ServiceModel.CacheSetting.Default>|Только экземпляры <xref:System.ServiceModel.ClientBase%601>, созданные на основе конечных точек, определенных в файлах конфигурации, участвуют в кэшировании внутри домена приложения.Ни один экземпляр <xref:System.ServiceModel.ClientBase%601>, созданный программно внутри домена приложения, не будет участвовать в кэшировании.Кроме этого, кэширование будет отключено для экземпляра <xref:System.ServiceModel.ClientBase%601> в случае доступа к «секретным» свойствам.|  
|<xref:System.ServiceModel.CacheSetting.AlwaysOff>|Кэширование отключается для всех экземпляров <xref:System.ServiceModel.ClientBase%601> определенного типа в пределах домена приложений.|  
  
 Следующие фрагменты кода показывают использование свойства <xref:System.ServiceModel.ClientBase%601.CacheSetting%2A>.  
  
```  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase<ITest>.CacheSettings = CacheSettings.AlwaysOn;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient (new BasicHttpBinding(), new EndpointAddress(address)))   
         {   
            // ...  
            proxy.Test(msg);   
            // ...  
         }   
      }   
   }   
}  
// Generated by SvcUtil.exe     
public partial class TestClient : System.ServiceModel.ClientBase, ITest { }  
  
```  
  
 В приведенном выше коде все экземпляры `TestClient` будут использовать одну и ту же фабрику каналов.  
  
```  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase.CacheSettings = CacheSettings.Default;   
      int i = 1;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient (“MyEndpoint”, new EndpointAddress(address)))   
         {   
            if (i == 4)   
            {   
               ServiceEndpoint endpoint = proxy.Endpoint;   
               ... // use endpoint in some way   
            }   
            proxy.Test(msg);   
         }   
         i++;   
   }   
}   
  
// Generated by SvcUtil.exe     
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}  
```  
  
 В приведенном выше примере все экземпляры `TestClient` будут использовать одну и ту же фабрику каналов, за исключением экземпляра №4.Экземпляр №4 будет использовать фабрику каналов, созданную специально для этой цели.Этот параметр не работает в сценариях, где определенной конечной точке необходимы различные параметры безопасности из других конечных точек того же типа фабрики каналов \(в данном случае `ITest`\).  
  
```  
class Program   
{   
   static void Main(string[] args)   
   {   
      ClientBase.CacheSettings = CacheSettings.AlwaysOff;   
      foreach (string msg in messages)   
      {   
         using (TestClient proxy = new TestClient (“MyEndpoint”, new EndpointAddress(address)))   
         {   
            proxy.Test(msg);   
         }           
      }   
   }  
}  
  
// Generated by SvcUtil.exe   
public partial class TestClient : System.ServiceModel.ClientBase, ITest {}  
```  
  
 В приведенном выше примере все экземпляры `TestClient` будут использовать различные фабрики каналов.Это может оказаться полезным в том случае, если каждая конечная точка имеет различные требования к безопасности и нет смысла выполнять кэширование.  
  
## См. также  
 <xref:System.ServiceModel.ClientBase%601>   
 [Построение клиентов](../../../../docs/framework/wcf/building-clients.md)   
 [Клиенты](../../../../docs/framework/wcf/feature-details/clients.md)   
 [Обращение к службам с использованием клиента WCF](../../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md)   
 [Практическое руководство. Использование ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)