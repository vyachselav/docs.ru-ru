---
title: "Утверждения и маркеры SAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "федерация"
  - "выданные маркеры"
  - "маркер SAML"
  - "WCF, федерация"
ms.assetid: 930b6e34-9eab-4e95-826c-4e06659bb977
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Утверждения и маркеры SAML
*Маркеры* языка SAML \(Security Assertions Markup Language\) являются XML\-представлением утверждений.По умолчанию маркеры SAML [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] используются в сценариях федеративной безопасности в качестве *выданных маркеров*.  
  
 Маркеры SAML содержат операторы, которые являются набором утверждений, выполненных одной сущностью в отношении другой сущности.Например, в сценариях федеративной безопасности операторы относительно пользователя выполняются в системе службой маркеров безопасности.Служба маркеров безопасности подписывает маркер SAML, чтобы подтвердить достоверность оператора, содержащегося в маркере.Кроме того, маркер SAML связан с материалом ключа шифрования, который должен быть известен пользователю маркера SAML.Эта проверка убеждает проверяющую сторону, что на самом деле маркер SAML был выдан указанному пользователю.Например, в типичном сценарии происходит следующее.  
  
1.  Клиент запрашивает маркер SAML у службы маркеров безопасности, проходя проверку подлинности в службе маркеров безопасности с использованием учетных данных Windows.  
  
2.  Служба маркеров безопасности выдает маркер SAML клиенту.Маркер SAML подписан сертификатом, связанным со службой маркеров безопасности, и содержит ключ проверки, зашифрованный для целевой службы.  
  
3.  Клиент также получает копию *ключа проверки*.Затем клиент представляет маркер SAML службе приложений \(*проверяющая сторона*\) и подписывает сообщение при помощи этого ключа проверки.  
  
4.  Подпись маркера SAML указывает проверяющей стороне, что маркер выдан службой маркеров безопасности.Подпись сообщения, созданная при помощи ключа проверки, указывает проверяющей стороне, что маркер был выдан клиенту.  
  
## От Claims к SamlAttributes  
 В [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] операторы в маркерах SAML моделируются как объекты <xref:System.IdentityModel.Tokens.SamlAttribute>, которые могут заполняться прямо из объектов <xref:System.IdentityModel.Claims.Claim>. Если у предоставляемого объекта <xref:System.IdentityModel.Claims.Claim> есть свойство <xref:System.IdentityModel.Claims.Claim.Right%2A> равное <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>, и свойство <xref:System.IdentityModel.Claims.Claim.Resource%2A> принадлежит к типу <xref:System.String>.Пример:  
  
 [!code-csharp[c_CreateSTS#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#8)]
 [!code-vb[c_CreateSTS#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#8)]  
  
> [!NOTE]
>  Если в сообщениях маркеры SAML сериализуются, выдаются они службой маркеров безопасности или предоставляются клиентами службам как часть проверки подлинности, максимальный размер квоты сообщения должен быть достаточно большим, чтобы вместить маркер SAML и другие части сообщения.Как правило, по умолчанию квоты на размер сообщения являются достаточными.Впрочем, в случае большого размера маркера SAML \(когда он содержит сотни утверждений\), может потребоваться увеличение квот для выделения места сериализованному маркеру.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Вопросы безопасности для данных](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md).  
  
## От SamlAttributes к Claims  
 Различные операторы в маркере SAML преобразуются в объекты <xref:System.IdentityModel.Policy.IAuthorizationPolicy>, которые помещаются в класс <xref:System.IdentityModel.Policy.AuthorizationContext>, когда в сообщении содержатся маркеры SAML.Утверждения от каждого оператора SAML возвращаются свойством <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> класса <xref:System.IdentityModel.Policy.AuthorizationContext> и могут быть проверены на необходимость проверки подлинности и авторизации пользователя.  
  
## См. также  
 <xref:System.IdentityModel.Policy.AuthorizationContext>   
 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>   
 <xref:System.IdentityModel.Claims.ClaimSet>   
 [Федерация](../../../../docs/framework/wcf/feature-details/federation.md)   
 [Как создавать федеративный клиент](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [Как настраивать учетные данные службы федерации](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)   
 [Управление утверждениями и авторизацией с помощью модели удостоверения](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)   
 [Утверждения и маркеры](../../../../docs/framework/wcf/feature-details/claims-and-tokens.md)   
 [Создание утверждений и значения ресурсов](../../../../docs/framework/wcf/feature-details/claim-creation-and-resource-values.md)   
 [Практическое руководство. Создание пользовательского утверждения](../../../../docs/framework/wcf/extending/how-to-create-a-custom-claim.md)