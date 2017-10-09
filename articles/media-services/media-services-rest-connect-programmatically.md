---
title: "aaaConnecting tooMedia conta de serviços usando a API REST | Microsoft Docs"
description: "Este tópico demonstra como usar do tooconnect tooMedia serviços REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Conectando tooMedia conta de serviços usando a API de REST de serviços de mídia
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Este tópico descreve como tooobtain tooMicrosoft uma conexão programática Azure Media Services quando você está programando com hello API de REST de serviços de mídia.

Duas coisas são necessárias ao acessar os serviços de mídia do Microsoft Azure: um token de acesso fornecido pelo Azure Access Control Services (ACS) e Olá URI do Media Services em si. Você pode usar os meios que desejar ao criar essas solicitações desde que você especifique valores de cabeçalho corretos hello e passa no token de acesso de saudação corretamente ao chamar nos serviços de mídia.

Olá, as etapas a seguir descreve o fluxo de trabalho de mais comuns do hello quando usar Olá API REST do Media Services tooconnect tooMedia serviços:

1. Obtendo um token de acesso 
2. Conectando toohello URI do Media Services 
   
   > [!NOTE]
   > Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI.
   > Você também pode receber uma resposta HTTP/1.1 200 que contém Olá descrição de metadados ODATA API.
   > 
   > 
3. POST suas chamadas API subsequentes toohello nova URL. 
   
    Por exemplo, se depois de tentar tooconnect, você obteve seguinte hello:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Você deve publicar seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.

    >[!NOTE]
    >Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

## <a name="access-control-address"></a>Endereço de controle de acesso
O endereço de controle de acesso de serviços de mídia é https://wamsprodglobal001acs.accesscontrol.windows.net, exceto para a região norte da China, onde é https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.

## <a name="getting-an-access-token"></a>Obtendo um token de acesso
tooaccess serviços de mídia diretamente por meio da API REST do hello, recuperar um token de acesso do ACS e usá-lo durante cada solicitação HTTP que fizer no serviço de saudação. Esse token é semelhante tokens tooother fornecidos pelo ACS, com base em declarações de acesso fornecidas no cabeçalho de saudação de uma solicitação HTTP e usar o protocolo de saudação OAuth v2. Não é necessário qualquer outro pré-requisito antes de conectar diretamente tooMedia serviços.

Olá exemplo a seguir mostra cabeçalho de solicitação HTTP hello e tooretrieve do corpo usado um token.

**Cabeçalho**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Corpo**:

Você precisa os valores tooprove client_id e o client_secret de saudação no corpo de saudação desta solicitação; client_id e o client_secret correspondem toohello AccountName e AccountKey valores, respectivamente. Esses valores são fornecidos tooyou pelos serviços de mídia quando você configurar sua conta. 

Observe que Olá AccountKey para sua conta de serviços de mídia deve ser codificados de URL (consulte [codificação por percentual](http://tools.ietf.org/html/rfc3986#section-2.1) quando usá-lo como o valor de client_secret Olá em sua solicitação de token de acesso.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Por exemplo: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Hello exemplo a seguir mostra Olá HTTP resposta que contém o acesso de saudação token no corpo de resposta de saudação.

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> É recomendável toocache hello "access_token" e "expires_in" valores tooan armazenamento externo. dados do token Olá posteriormente foi recuperados do armazenamento hello e reutilizados em suas chamadas de API de REST de serviços de mídia. Isso é especialmente útil para cenários onde Olá token pode ser compartilhado com segurança entre vários processos ou computadores.
> 
> 

Certifique-se de valor de "expires_in" hello toomonitor de acesso de saudação token e atualizar suas chamadas de API REST com novos tokens, conforme necessário.

### <a name="connecting-toohello-media-services-uri"></a>Conectando toohello URI do Media Services
Olá URI raiz para os serviços de mídia é https://media.windows.net/. Você deve conectar toothis URI e se você receber um redirecionamento 301 em resposta, você deve fazer chamadas subsequentes toohello novo URI. Além disso, não use nenhuma lógica de redirecionamento/acompanhamento automático nas solicitações. Verbos HTTP e corpos de solicitação não serão encaminhados toohello novo URI.

Observe que raiz Olá URI para carregar e baixar arquivos de ativo https://yourstorageaccount.blob.core.windows.net/ onde é o nome de conta de armazenamento Olá Olá um mesmo usada durante a configuração da conta de serviços de mídia.

saudação de exemplo a seguir demonstra toohello a solicitação HTTP raiz de serviços de mídia URI (https://media.windows.net/). solicitação de saudação obtém um redirecionamento 301 em resposta. Olá solicitação subsequente é usando Olá novo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**Solicitação HTTP**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**Resposta HTTP**:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**Solicitação HTTP** (usando Olá novo URI):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta HTTP**:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> Depois de obter Olá novo URI, que é hello URI que deve ser usado toocommunicate com serviços de mídia. 
> 
> 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

