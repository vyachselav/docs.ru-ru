---
title: "Клиент ASMX со службой WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3ea381ee-ac7d-4d62-8c6c-12dc3650879f
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Клиент ASMX со службой WCF
В этом образце показано, как создать службу с помощью [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], а затем получать доступ к службе из клиента, не являющегося [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\-клиентом, например из клиента ASMX.  
  
> [!NOTE]
>  Процедура настройки и инструкции по построению для данного образца приведены в конце этого раздела.  
  
 Этот образец содержит консольную программу клиента \(EXE\) и библиотеку службы \(DLL\), размещаемую в службах IIS.Служба реализует контракт, определяющий шаблон взаимодействия "запрос\-ответ".Контракт определяется интерфейсом `ICalculator`, который предоставляет математические операции \(`Add`, `Subtract`, `Multiply` и `Divide`\).Клиент ASMX осуществляет синхронные вызовы математической операции, а служба отправляет в ответ результат.  
  
 Служба реализует контракт `ICalculator`, как показано в следующем примере кода.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"), XmlSerializerFormat]  
public interface ICalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
    [OperationContract]  
    double Subtract(double n1, double n2);  
    [OperationContract]  
    double Multiply(double n1, double n2);  
    [OperationContract]  
    double Divide(double n1, double n2);  
}  
  
```  
  
 Объекты <xref:System.Runtime.Serialization.DataContractSerializer> и <xref:System.Xml.Serialization.XmlSerializer> сопоставляют типы среды CLR с XML\-представлением.<xref:System.Runtime.Serialization.DataContractSerializer> интерпретирует некоторые XML\-представления не так, как XmlSerializer.Генераторы прокси, не относящиеся к [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], например Wsdl.exe, создают более удобный интерфейс при использовании XmlSerializer.К интерфейсу `ICalculator` применяется атрибут <xref:System.ServiceModel.XmlSerializerFormatAttribute>, чтобы для сопоставления типов среды CLR с XML использовался XmlSerializer.Реализация службы выполняет вычисления и возвращает соответствующий результат.  
  
 Служба предоставляет одну конечную точку для взаимодействия с ней; конечная точка определяется в файле конфигурации \(Web.config\).Конечная точка состоит из адреса, привязки и контракта.Служба предоставляет конечную точку по базовому адресу, предоставляемую узлом IIS.Для атрибута `binding` задается значение basicHttpBinding, что обеспечивает взаимодействие по протоколу HTTP с использованием протокола SOAP 1.1, который совместим со спецификацией WS\-I BasicProfile 1.1, как показано в следующем образце конфигурации.  
  
```  
<services>  
   <service   
       name="Microsoft.ServiceModel.Samples.CalculatorService"  
       behaviorConfiguration="CalculatorServiceBehavior">  
       <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc.  -->  
      <endpoint address=""  
               binding="basicHttpBinding"   
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
   </service>  
</services>  
  
```  
  
 Клиент ASMX взаимодействует со службой [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] с помощью типизированного прокси, создаваемого средством языка описания служб \(Wsdl.exe\).Типизированный прокси содержится в файле generatedClient.cs.Специальная программа WSDL извлекает метаданные для заданной службы и создает типизированный прокси, который будет использоваться клиентом для взаимодействия.По умолчанию платформа не предоставляет никаких метаданных.Чтобы предоставить метаданные, необходимые для создания прокси, следует добавить элемент [\<serviceMetadata\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md) и задать для атрибута `httpGetEnabled` значение `True`, как показано в следующей конфигурации.  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <!-- Setting httpGetEnabled to True on the serviceMetadata  
           behavior exposes the service's wsdl at <base address>?wsdl :  
           http://localhost/servicemodelsamples/service.svc?wsdl -->  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Чтобы создать типизированный прокси, выполните следующую команду из командной строки в каталоге клиента.  
  
```  
wsdl /n:Microsoft.ServiceModel.Samples /o:generatedClient.cs /urlkey:CalculatorServiceAddress http://localhost/servicemodelsamples/service.svc?wsdl  
  
```  
  
 С помощью созданного типизированного прокси клиент может обращаться к заданной конечной точке службы путем задания в конфигурации соответствующего адреса.Чтобы задать конечную точку для взаимодействия, клиент использует файл конфигурации \(App.config\).  
  
```  
<appSettings>  
      <add key="CalculatorServiceAddress"   
      value="http://localhost/ServiceModelSamples/service.svc"/>  
</appSettings>  
  
```  
  
 Реализация клиента создает экземпляр типизированного прокси, чтобы начать взаимодействие со службой.  
  
```  
// Create a client to the CalculatorService.  
using (CalculatorService client = new CalculatorService())  
{  
    // Call the Add service operation.  
    double value1 = 100.00D;  
    double value2 = 15.99D;  
    double result = client.Add(value1, value2);  
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Subtract service operation.  
    value1 = 145.00D;  
    value2 = 76.54D;  
    result = client.Subtract(value1, value2);  
    Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Multiply service operation.  
    value1 = 9.00D;  
    value2 = 81.25D;  
    result = client.Multiply(value1, value2);  
    Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
    // Call the Divide service operation.  
    value1 = 22.00D;  
    value2 = 7.00D;  
    result = client.Divide(value1, value2);  
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
}  
  
Console.WriteLine();  
Console.WriteLine("Press <ENTER> to terminate client.");  
Console.ReadLine();  
  
```  
  
 При выполнении образца запросы и ответы операций отображаются в окне консоли клиента.Чтобы закрыть клиент, нажмите клавишу ВВОД в окне клиента.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
  
```  
  
### Настройка, построение и выполнение образца  
  
1.  Убедитесь, что выполнены процедуры, описанные в разделе [Процедура однократной настройки образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Чтобы создать выпуск решения на языке C\# или Visual Basic .NET, следуйте инструкциям в разделе [Построение образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Чтобы выполнить образец на одном или нескольких компьютерах, следуйте инструкциям в разделе [Выполнение примеров Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!NOTE]
>  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] о передаваемых и возвращаемых типах данных см. в разделах [Привязка данных в клиенте Windows Forms](../../../../docs/framework/wcf/samples/data-binding-in-a-windows-forms-client.md), [Привязка данных в клиенте Windows Presentation Foundation](../../../../docs/framework/wcf/samples/data-binding-in-a-wpf-client.md) и [Привязка данных в клиенте ASP.NET](../../../../docs/framework/wcf/samples/data-binding-in-an-aspnet-client.md)  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Basic\Services\Interop\ASMX`  
  
## См. также