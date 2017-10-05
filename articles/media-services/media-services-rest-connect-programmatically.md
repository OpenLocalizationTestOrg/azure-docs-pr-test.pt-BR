---
title: "Conectando a Conta dos Serviços de Mídia usando a API REST | Microsoft Docs"
description: "Este tópico demonstra como conectar os Serviços de Mídia usando a API REST."
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
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a>Conectando-se a conta dos serviços de mídia usando a API REST dos serviços de mídia
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Este tópico descreve como obter uma conexão programática com os Serviços de Mídia do Microsoft Azure quando você está programando com a API REST dos Serviços de Mídia.

Duas coisas são necessárias ao acessar os Serviços de Mídia do Microsoft Azure: um token de acesso fornecido pelos ACSs (Serviços de Controle de Acesso) e o URI dos Serviços de Mídia em si. Você pode usar os meios que desejar ao criar essas solicitações desde que especifique os valores de cabeçalho corretos e passar o token de acesso corretamente ao chamar nos serviços de mídia.

As etapas a seguir descrevem o fluxo de trabalho mais comum ao usar a API REST dos serviços de mídia para se conectar aos serviços de mídia:

1. Obtendo um token de acesso 
2. Conectando o URI dos serviços de mídia 
   
   > [!NOTE]
   > Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes para o novo URI.
   > Você também poderá receber uma resposta HTTP/1.1 200 que contém a descrição de metadados API ODATA.
   > 
   > 
3. Poste suas chamadas de API subsequentes para a nova URL. 
   
    Por exemplo, se depois de tentar se conectar, você tem o seguinte:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Você deve postar suas chamadas de API subsequentes para https://wamsbayclus001rest-hs.cloudapp.net/api/.

    >[!NOTE]
    >Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Use a mesma ID de política, se você estiver sempre usando os mesmos dias/permissões de acesso, por exemplo, políticas de localizadores que devem permanecer no local por um longo período (políticas de não carregamento). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

## <a name="access-control-address"></a>Endereço de controle de acesso
O endereço de controle de acesso de serviços de mídia é https://wamsprodglobal001acs.accesscontrol.windows.net, exceto para a região norte da China, onde é https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.

## <a name="getting-an-access-token"></a>Obtendo um token de acesso
Para acessar os serviços de mídia diretamente por meio da API REST, recupere um token de acesso do ACS e use-o durante todas as solicitações HTTP feitas no serviço. Esse token é semelhante aos outros tokens fornecidos pelo ACS com base nas declarações de acesso fornecidas no cabeçalho de uma solicitação HTTP e usando o protocolo OAuth v2. Não é necessário qualquer outro pré-requisito antes de conectar-se diretamente aos serviços de mídia.

O exemplo a seguir mostra o cabeçalho de solicitação HTTP e o corpo usado para recuperar um token.

**Cabeçalho**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Corpo**:

Você precisa provar os valores de client_id e client_secret no corpo dessa solicitação. O client_id e client_secret correspondem a valores AccountName e AccountKey, respectivamente. Esses valores são fornecidos a você pelos serviços de mídia ao configurar sua conta. 

Observe que a AccountKey da sua conta de Serviços de Mídia deve ter a codificação de URL (consulte [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) ao ser usado como o valor de client_secret em sua solicitação de token de acesso.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Por exemplo: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


O exemplo a seguir mostra a resposta HTTP que contém o token de acesso no corpo da resposta.

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
> É recomendável armazenar em cache os valores "access_token" e "expires_in" em um armazenamento externo. Os dados do token podem ser recuperados posteriormente a partir do armazenamento e reutilizados em suas chamadas de API REST dos serviços de mídia. Isso é especialmente útil para cenários em que o token pode ser compartilhado com segurança entre vários processos ou computadores.
> 
> 

Certifique-se de monitorar o valor "expires_in" do token de acesso e atualizar suas chamadas de API REST com novos tokens, conforme necessário.

### <a name="connecting-to-the-media-services-uri"></a>Conectando o URI dos serviços de mídia
O URI raiz para os serviços de mídia é https://media.windows.net/. Inicialmente, você deve se conectar a esse URI, e se obtiver um redirecionamento 301 em resposta, deverá fazer chamadas subsequentes para o novo URI. Além disso, não use nenhuma lógica de redirecionamento/acompanhamento automático nas solicitações. Verbos HTTP e corpos de solicitação não serão encaminhados para o novo URI.

Observe que o URI raiz para carregar e baixar arquivos de ativo é https://yourstorageaccount.blob.core.windows.net/ onde o nome da conta de armazenamento é o mesmo usado durante a configuração da conta de serviços de mídia.

O exemplo a seguir demonstra a solicitação HTTP para o URI raiz dos Serviços de Mídia (https://media.windows.net/). A solicitação obtém um redirecionamento 301 em resposta. A solicitação subsequente está usando o novo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

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
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**Solicitação HTTP** (usando o novo URI):

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
> Depois que obtiver o novo URI, este é o URI que deve ser usado para se comunicar com os serviços de mídia. 
> 
> 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

