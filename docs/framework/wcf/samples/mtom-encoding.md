---
title: "Кодирование MTOM | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 820e316f-4ee1-4eb5-ae38-b6a536e8a14f
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Кодирование MTOM
В данном образце демонстрируется использование кодирования сообщений с помощью механизма оптимизации передачи сообщений \(MTOM\) с WSHttpBinding.MTOM — это механизм передачи больших вложений в двоичном формате с сообщениями протокола SOAP как необработанных байтов, допустимых для меньших сообщений.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MTOM`  
  
 По умолчанию WSHttpBinding отправляет и принимает сообщения как нормальный XML\-текст.Для включения отправки и получения MTOM\-сообщений задайте атрибут `messageEncoding` в конфигурации привязки \(как в следующем примере кода\) или непосредственно в привязке с помощью свойства `MessageEncoding`.Теперь служба или клиент могут отправлять или получать MTOM\-сообщения.  
  
```  
<wsHttpBinding>  
    <binding name="WSHttpBinding_IUpload" messageEncoding="Mtom"/>  
</wsHttpBinding>  
```  
  
 Кодировщик MTOM может оптимизировать массивы байтов и потоки.В данном образце операция использует параметр `Stream` и, следовательно, может быть оптимизирована.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
  public interface IUpload  
  {  
      [OperationContract]  
      int Upload(Stream data);  
  }  
```  
  
 Контракт, выбранный для данного образца, передает двоичные данные службе и в качестве возвращаемого значения получает число загруженных байтов.Если служба установлена и запущен клиент, он выводит на печать число 1000, указывающее, что было получено 1000 байт.В напоминании вывода приводятся списки размеров оптимизированных и неоптимизированных сообщений для различных нагрузок.  
  
```  
Output:  
1000  
  
Text encoding with a 100 byte payload: 433  
MTOM encoding with a 100 byte payload: 912  
  
Text encoding with a 1000 byte payload: 1633  
MTOM encoding with a 1000 byte payload: 2080  
  
Text encoding with a 10000 byte payload: 13633  
MTOM encoding with a 10000 byte payload: 11080  
  
Text encoding with a 100000 byte payload: 133633  
MTOM encoding with a 100000 byte payload: 101080  
  
Text encoding with a 1000000 byte payload: 1333633  
MTOM encoding with a 1000000 byte payload: 1001080  
  
Press <ENTER> to terminate client.  
```  
  
 Цель использования MTOM — оптимизация передачи больших двоичных нагрузок.Отправка SOAP\-сообщения с помощью MTOM имеет значительные издержки для небольших двоичных нагрузок, но позволяет значительно сэкономить, когда нагрузка превышает несколько тысяч байт.Причина заключается в том, что нормальный XML\-текст кодирует двоичные данные с помощью Base64, который требует четыре символа на каждые три байта и увеличивает размер данных на одну треть.Механизм MTOM способен передавать двоичные данные в виде необработанных байтов, позволяя тем самым сэкономить время на кодирование\/декодирование и способствуя уменьшению размера сообщений.Порог в несколько тысяч байт мал по сравнению с размером современных деловых документов и цифровых фотографий.  
  
### Настройка, построение и выполнение образца  
  
1.  Установите [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0, выполнив следующую команду.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Убедитесь, что выполнена процедура, описанная в разделе [Процедура однократной настройки образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Чтобы создать версию решения на языке C\# или Visual Basic .NET, следуйте инструкциям в разделе [Построение образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Чтобы выполнить образец на одном или нескольких компьютерах, следуйте инструкциям раздела [Выполнение примеров Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## См. также