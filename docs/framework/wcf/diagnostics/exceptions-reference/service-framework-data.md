---
title: "Данные инфраструктуры службы | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2a2c8ddc-4e82-4e7f-a79f-97085c469517
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Данные инфраструктуры службы
В этом разделе перечислены все исключения, вызываемые данными инфраструктуры службы.  
  
## Список исключений  
  
|Код ресурса|Строка ресурса|  
|-----------------|--------------------|  
|AddressingExtensionInBadNS|Указанный элемент в указанном пространстве имен является недопустимым.Это означает, что указанный элемент или является дублирующим элементом, или представляет собой недопустимое расширение, так как пространство имен адресации не может содержать элементы расширения.|  
|BinaryEncoderSessionInvalid|Сеанс двоичного кодировщика является недопустимым, поскольку при декодировании предыдущего сообщения произошла ошибка.|  
|CannotDetectAddressingVersion|Не удалось обнаружить версию WS\-Addressing.Адрес EndpointAddress не начинается с элемента.|  
|CouldNotFindNamespaceForPrefix|В области указанного префикса нет привязки пространства имен.|  
|EncoderBadContentType|Не удалось обработать contentType.|  
|EncoderEnvelopeVersionMismatch|Версия конверта указанного входящего сообщения не соответствует указанному кодировщику.Убедитесь, что привязка настроена с использованием той же версии, что и ожидаемые сообщения.|  
|EncoderMessageVersionMismatch|Версия сообщения указанного исходящего сообщения не соответствует указанному кодировщику.Убедитесь, что привязка настроена с использованием той же версии, что и сообщение.|  
|ExtraContentIsPresentInFaultDetail|В элементе подробностей ошибки присутствует дополнительное XML\-содержимое.Допускается только один элемент.|  
|FilterBadTableType|Таблица IMessageFilterTable, созданная для Filter, не может принадлежать к типу MessageFilterTable или наследовать от MessageFilterTable.|  
|FilterTableInvalidForLookup|Состояние MessageFilterTable повреждено.Запрошенный поиск не может быть выполнен.|  
|MandatoryHeaderNotUnderstood|Один или несколько обязательных блоков заголовка SOAP не распознаны.|  
|MessageBodyIsStream|Тело сообщения представляет собой поток.|  
|MessageBodyIsUnknown|Формат тела сообщения неизвестен.|  
|MessageBodyReaderInvalidReadState|Указанное состояние ReadState модуля чтения тела сообщения не может быть использовано.|  
|MessageTextEncodingNotSupported|Указанная кодировка текста, используемая в формате текстового сообщения, не поддерживается.|  
|MissingMessageID|В сообщении запроса отсутствует заголовок MessageID.Заголовок MessageID требуется для корреляции ответа.|  
|MultipleMessageHeaders|Найдено несколько заголовков с указанными именем и пространством имен.|  
|MultipleMessageHeadersWithActor|Найдено несколько заголовков с указанными именем, пространством имен и ролью.|  
|MultipleRelatesToHeaders|Найдено несколько заголовков RelatesTo с указанным отношением.Допускается только один заголовок для каждого отношения.|  
|QueryFunctionTypeNotSupported|Указанный тип возвращаемого значения для функции IXsltContextFunction не поддерживается.|  
|QueryIteratorOutOfScope|XPathNodeIterator сделан недействительным.Объекты XPathNodeIterator, переданные в качестве аргументов функции IXsltContextFunction, допустимы только в рамках этой функции.Их нельзя поместить в кэш для дальнейшего использования или возвратить в качестве результата этой функции.|  
|QueryVariableNull|Методы IXsltContextVariable не могут возвращать значение NULL.|  
|QueryVariableTypeNotSupported|Указанный тип, производный от IXsltContextVariable, не поддерживается.|  
|ReceiveShutdownReturnedMessage|Во время закрытия канал получил неожиданное входящее сообщение с указанным Action.Канал можно закрывать, когда больше не ожидаются входящие сообщения.|  
|XmlBufferInInvalidState|Произошла внутренняя ошибка.Невозможно выполнить операцию из\-за состояния буфера XML.|  
|XmlBufferQuotaExceeded|Размер, необходимый для помещения XML\-содержимого в буфер обмена, превысил квоту буфера.|