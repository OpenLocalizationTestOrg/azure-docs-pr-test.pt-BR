---
title: "aaaToken (HTTP/2) autenticação de APNS em Hubs de notificação do Azure | Microsoft Docs"
description: "Este tópico explica como tooleverage Olá nova autenticação de token para o APNS"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a>Autenticação baseada em token (HTTP/2) para o APNS
## <a name="overview"></a>Visão geral
Este artigo fornece detalhes sobre como toouse Olá novo APNS HTTP/2 protocolo com token de autenticação com base em.

Olá principais benefícios de usar o novo protocolo de saudação incluem:
-   Geração de token é relativamente complicações livre (em comparação com toocertificates)
-   Não há mais dadas de expiração – você está no controle dos seus tokens de autenticação e sua revogação
-   Cargas agora podem ser o too4 KB
- Comentários síncronos
-   Você está usando o protocolo mais recente da Apple – certificados ainda usam protocolo binário hello, que está marcado para substituição

O uso desse novo mecanismo pode ser feito em duas etapas, em alguns minutos:
1.  Obter informações necessárias de saudação do portal de conta de desenvolvedor da Apple Olá
2.  Configurar seu hub de notificação com novas informações de saudação

Hubs de notificação é agora todos os conjunto toouse Olá novo sistema de autenticação com APNS. 

Observe que se você migrou usando as credenciais de certificado para APNS:
- Propriedades do token Olá substituir o certificado em nosso sistema
- mas o aplicativo continua tooreceive notificações perfeitamente.

## <a name="obtaining-authentication-information-from-apple"></a>Obtendo informações de autenticação da Apple
a autenticação baseada em token tooenable, você precisa Olá seguintes propriedades da conta do desenvolvedor Apple:
### <a name="key-identifier"></a>Identificador de chave
Identificador de chave Olá pode ser obtido da página de "Chaves" hello em sua conta de desenvolvedor da Apple

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Identificador do aplicativo e nome do aplicativo
nome do aplicativo Hello está disponível por meio de página de IDs de aplicativo Olá Olá conta de desenvolvedor. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

Identificador do aplicativo Hello está disponível por meio da página de detalhes de associação Olá no hello conta de desenvolvedor.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Token de autenticação
o token de autenticação Olá pode ser baixado depois de gerar um token para o seu aplicativo. Para obter detalhes sobre como toogenerate esse token, consulte muito[documentação do desenvolvedor da Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Configurando a autenticação de baseado em token do toouse de hub de notificação
### <a name="configure-via-hello-azure-portal"></a>Configurar por meio de saudação portal do Azure
token tooenable com base em autenticação no portal de hello, log em toohello portal do Azure e vá tooyour Hub de notificação > Serviços de notificação > Painel APNS. 

Há uma nova propriedade – *Modo de Autenticação*. Selecionar Token permite que você tooupdate seu hub com todas as propriedades token de relevantes de saudação.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Inserir propriedades de saudação recuperados de sua conta de desenvolvedor da Apple, 
- escolha o modo de aplicativo (Produção ou Área Restrita) 
- Clique em Salvar tooupdate suas credenciais APNS. 

### <a name="configure-via-management-api-rest"></a>Configurar por meio da API de gerenciamento (REST)

Você pode usar nosso [APIs de gerenciamento](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate sua autenticação notificação hub toouse baseado em token.
Dependendo se o aplicativo hello a que você estiver configurando é um aplicativo de área restrita ou de produção (especificado na sua conta de desenvolvedor da Apple), use um dos pontos de extremidade correspondente hello:

- Ponto de extremidade da Área Restrita: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)
- Ponto de extremidade de Produção: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> A autenticação baseada em token requer uma versão de API de: **2017-04 ou posterior**.
> 
> 

Aqui está um exemplo de uma solicitação PUT tooupdate um hub com autenticação baseada em token:


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a>Configurar por meio de saudação SDK .NET
Você pode configurar seu hub toouse autenticação baseada em token usando nosso [SDK mais recente do cliente](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Aqui está um exemplo de código que ilustram o uso correto da saudação:


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Autenticação baseada em certificado do toousing reversão
Você pode reverter em qualquer autenticação baseada em certificado do tempo toousing usando qualquer certificado de saudação do método e passando anterior em vez de propriedades de token hello. Ação substitui Olá anteriormente credenciais armazenadas.
