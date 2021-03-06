---
title: "Пример автономного веб-канала диагностики | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d31c6c1f-292c-4d95-8e23-ed8565970ea5
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Пример автономного веб-канала диагностики
В этом примере показано, как создавать канал синдикации RSS\/Atom с помощью [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  Это основная программа "Здравствуй, мир", которая демонстрирует основные возможности объектной модели и способы ее настройки для службы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] моделирует веб\-каналы синдикации как операции службы, возвращающие особый тип данных, <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter>.  Экземпляры <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> могут сериализовать веб\-канал в форматы RSS 2.0 и Atom 1.0.  В следующем примере кода показан использованный контракт.  
  
```  
[ServiceContract(Namespace = "")]  
    interface IDiagnosticsService  
    {  
        [OperationContract]  
        //The [WebGet] attribute controls how WCF dispatches  
        //HTTP requests to service operations based on a URI suffix  
        //(the part of the request URI after the endpoint address)  
        //using the HTTP GET method. The UriTemplate specifies a relative  
        //path of 'feed', and specifies that the format is  
        //supplied using a query string.   
        [WebGet(UriTemplate="feed?format={format}")]  
        [ServiceKnownType(typeof(Atom10FeedFormatter))]  
        [ServiceKnownType(typeof(Rss20FeedFormatter))]  
        SyndicationFeedFormatter GetProcesses(string format);  
    }  
```  
  
 Операция `GetProcesses` аннотируется атрибутом <xref:System.ServiceModel.Web.WebGetAttribute>, который позволяет контролировать, как [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] отправляет запросы HTTP GET в операции службы, и указывать формат отправляемых сообщений.  
  
 Как и любая другая служба [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] веб\-каналы синдикации могут быть резидентными для любого управляемого приложения.  Для правильной работы служб синдикации требуются особая привязка \(<xref:System.ServiceModel.WebHttpBinding>\) и специальное поведение конечной точки \(<xref:System.ServiceModel.Description.WebHttpBehavior>\).  Новый класс <xref:System.ServiceModel.Web.WebServiceHost> обеспечивает удобный программный интерфейс для создания таких конечных точек без особой конфигурации.  
  
```  
WebServiceHost host = new WebServiceHost(typeof(ProcessService), new Uri("http://localhost:8000/diagnostics"));  
  
            //The WebServiceHost will automatically provide a default endpoint at the base address  
            //using the proper binding (the WebHttpBinding) and endpoint behavior (the WebHttpBehavior)  
```  
  
 В качестве альтернативного варианта можно использовать <xref:System.ServiceModel.Activation.WebServiceHostFactory> из размещенного в службах IIS файла SVC, чтобы обеспечить аналогичную функциональность \(этот метод не показан в примере коде\).  
  
```  
<%@ ServiceHost Language="C#|VB" Debug="true" Service="ProcessService" %>  
```  
  
 Поскольку эта служба получает запросы с использованием стандартного метода HTTP GET, для доступа к службе можно использовать любой клиент, поддерживающий RSS или ATOM.  Например, можно просмотреть выходные данные этой службы, перейдя по адресу http:\/\/localhost:8000\/diagnostics\/feed\/?format\=atom or http:\/\/localhost:8000\/diagnostics\/feed\/?format\=rss в таком браузере с поддержкой RSS, как Internet Explorer 7.  
  
 Для чтения синдицированных данных и их обработки с помощью императивного кода также можно использовать [Сопоставление объектной модели синдикации WCF моделям Atom и RSS](../../../../docs/framework/wcf/feature-details/how-the-wcf-syndication-object-model-maps-to-atom-and-rss.md).  
  
```  
XmlReader reader = XmlReader.Create( "http://localhost:8000/diagnostics/feed/?format=rss",  
new XmlReaderSettings()  
{  
//MaxCharactersInDocument can be used to control the maximum amount of data   
//read from the reader and helps prevent OutOfMemoryException  
MaxCharactersInDocument = 1024 * 64  
} );  
  
SyndicationFeed feed = SyndicationFeed.Load( reader );  
  
foreach (SyndicationItem i in feed.Items)  
{  
        XmlSyndicationContent content = i.Content as XmlSyndicationContent;  
        ProcessData pd = content.ReadContent<ProcessData>();  
  
        Console.WriteLine(i.Title.Text);  
        Console.WriteLine(pd.ToString());  
}  
```  
  
### Настройка, сборка и выполнение образца  
  
1.  Обеспечьте правильное разрешение регистрации адреса для HTTP и HTTPS на компьютере согласно инструкциям по настройке в [Процедура однократной настройки образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Постройте решение.  
  
3.  Запустите консольное приложение.  
  
4.  Во время работы консольного приложения перейдите по адресу http:\/\/localhost:8000\/diagnostics\/feed\/?format\=atom или http:\/\/localhost:8000\/diagnostics\/feed\/?format\=rss с помощью браузера с поддержкой RSS.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.  Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Basic\Syndication\DiagnosticsFeed`  
  
## См. также  
 [Модель веб\-программирования HTTP WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [Синдикация WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)