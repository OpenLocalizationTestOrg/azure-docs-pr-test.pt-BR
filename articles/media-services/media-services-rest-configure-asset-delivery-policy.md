---
title: "políticas de entrega de ativos aaaConfiguring usando a API de REST de serviços de mídia | Microsoft Docs"
description: "Este tópico mostra como tooconfigure políticas de entrega de ativo diferentes usando a API de REST de serviços de mídia."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>Configuração de políticas de entrega de ativos
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Se você planejar ativos toodeliver dinamicamente criptografado, uma saudação etapas no hello conteúdo de fluxo de trabalho de entrega está configurando políticas de entrega de ativos de serviços de mídia. política de entrega de ativos de saudação informa os serviços de mídia como você deseja para sua toobe ativo entregue: em qual protocolo de streaming deve seu ativo dinamicamente empacotado (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), se você deseja toodynamically ou não criptografar seu ativo e como (envelope ou criptografia comum).

Este tópico discute por que e como toocreate e configurar políticas de entrega de ativos.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 
>
>Além disso, o empacotamento dinâmico capaz de toouse toobe e criptografia dinâmica seu ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.

Você pode aplicar políticas diferentes toohello mesmo ativo. Por exemplo, você pode aplicar PlayReady criptografia tooSmooth Streaming e Envelope AES criptografia tooMPEG DASH e HLS. Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming. Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida. Em seguida, todos os protocolos poderão ser em Olá clara.

Se você quiser toodeliver um ativo de armazenamento criptografado, você deve configurar a política de entrega do hello ativo. Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado a política de distribuição. Por exemplo, toodeliver seu ativo criptografado com chave de criptografia de envelope AES Advanced Encryption Standard (), defina o tipo de política de saudação muito**DynamicEnvelopeEncryption**. criptografia de armazenamento tooremove e ativo de saudação do fluxo em Olá claro, defina tipo de política de saudação muito**NoDynamicEncryption**. Exemplos que mostram como tooconfigure esses tipos de política execute.

Dependendo de como você configurar a política de distribuição do ativo Olá seria ser capaz de toodynamically pacote dinamicamente criptografar e Olá seguintes protocolos de transmissão de fluxo: Smooth Streaming, HLS, fluxos MPEG DASH.

Olá seguinte lista mostra Olá formatos que você use toostream Smooth, HLS, traço.

Smooth Streaming:

{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest

HLS:

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=mpd-time-csf)


Para obter instruções sobre como toopublish um ativo e compilar uma URL de streaming, consulte [construir uma URL de streaming](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Considerações
* Você não pode excluir um AssetDeliveryPolicy associado a um ativo enquanto um localizador OnDemand (streaming) existir para esse ativo. recomendação de saudação é tooremove política de saudação do ativo de saudação antes de excluir a política de saudação.
* Não é possível criar um localizador de streaming em um ativo criptografado para armazenamento quando nenhuma política de entrega de ativo estiver definida.  Se Olá ativo não criptografado de armazenamento, o sistema Olá permitem criar um ativo de localizador e o fluxo Olá Olá desmarque sem uma política de entrega de ativos.
* Você pode ter várias políticas de entrega de ativo associadas a um único ativo, mas você só pode especificar uma maneira toohandle AssetDeliveryProtocol um determinado.  Que significa que se você tentar toolink duas políticas de entrega que especificar o protocolo de AssetDeliveryProtocol.SmoothStreaming de saudação resultará em um erro porque o sistema Olá não sabe qual deles você deseja tooapply quando um cliente faz uma solicitação de Smooth Streaming.
* Se você tiver um ativo com um localizador de streaming existente, você não pode vincular um novo ativo toohello política, desvincular uma política existente de ativo de saudação ou atualizar uma política de distribuição associada a saudação ativo.  Primeiro ter localizador de transmissão tooremove hello, ajustar as diretivas de saudação e recrie o hello localizador de streaming.  Você pode usar o hello locatorId mesmo quando você recriar Olá streaming localizador, mas você deve garantir que não causar problemas para os clientes desde que o conteúdo pode ser armazenado em cache por origem hello ou um CDN de downstream.

>[!NOTE]

>Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP. Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Conectar os serviços de tooMedia

Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia. Você deve fazer chamadas subsequentes toohello novo URI.

## <a name="clear-asset-delivery-policy"></a>Política de entrega de ativos clara
### <a id="create_asset_delivery_policy"></a>Criar política de entrega de ativos
Olá, solicitação HTTP a seguir cria uma política de entrega de ativos que especifica toonot aplicar criptografia dinâmica e protocolos de fluxo de saudação toodeliver em qualquer Olá a seguir: protocolos MPEG DASH, HLS e Smooth Streaming. 

Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.   

Solicitação:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

Resposta:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>Ativos de link com a política de entrega de ativos
Olá Olá de links de solicitação HTTP a seguir especificado a política de distribuição do ativo toohello ativo para.

Solicitação:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

Resposta:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Política de entrega de ativos DynamicEnvelopeEncryption
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Criar chave de conteúdo do tipo de EnvelopeEncryption hello e vinculá-lo ativo toohello
Ao especificar a política de distribuição DynamicEnvelopeEncryption, é necessário toolink se toomake a chave de conteúdo ativo tooa de saudação tipo EnvelopeEncryption. Para saber mais, confira: [Criando uma chave de conteúdo](media-services-rest-create-contentkey.md)).

### <a id="get_delivery_url"></a>Obter URL de entrega
URL de envio de saudação Get para Olá especificado método de entrega da chave de conteúdo Olá criado na etapa anterior hello. Um cliente usa Olá retornado URL toorequest uma chave AES ou uma licença do PlayReady Olá de tooplayback ordem conteúdo protegido.

Especifique o tipo de saudação de Olá URL tooget no corpo de saudação de solicitação HTTP de saudação. Se você estiver protegendo o conteúdo com PlayReady, solicite uma URL de aquisição de licença do PlayReady dos serviços de mídia, usando 1 para Olá keyDeliveryType: {"keyDeliveryType": 1}. Se você estiver protegendo o conteúdo com criptografia de envelope hello, solicite uma URL de aquisição de chaves especificando 2 para keyDeliveryType: {"keyDeliveryType": 2}.

Solicitação:

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

Resposta:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>Criar política de entrega de ativos
Olá, solicitação HTTP a seguir cria Olá **AssetDeliveryPolicy** tooapply configurado que é a criptografia de envelope dinâmica (**DynamicEnvelopeEncryption**) toohello **HLS**protocolo (neste exemplo, outros protocolos serão impedidos de streaming). 

Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.   

Solicitação:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


Resposta:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>Ativos de link com a política de entrega de ativos
Confira [Ativos de link com a política de entrega de ativos](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Política de entrega de ativos DynamicCommonEncryption
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Criar chave de conteúdo do tipo de CommonEncryption hello e vinculá-lo ativo toohello
Ao especificar a política de distribuição DynamicCommonEncryption, é necessário toolink se toomake a chave de conteúdo ativo tooa de saudação tipo CommonEncryption. Para saber mais, confira: [Criando uma chave de conteúdo](media-services-rest-create-contentkey.md)).

### <a name="get-delivery-url"></a>Obter URL de entrega
Obter URL de entrega de Olá Olá PlayReady método de entrega da chave de conteúdo Olá criado na etapa anterior hello. Um cliente usa Olá retornado toorequest URL protegida de uma licença do PlayReady Olá de tooplayback ordem conteúdo. Para saber mais, confira [Obter a URL de entrega](#get_delivery_url)

### <a name="create-asset-delivery-policy"></a>Criar política de entrega de ativos
Olá, solicitação HTTP a seguir cria Olá **AssetDeliveryPolicy** que é configurado tooapply comuns criptografia dinâmica (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocolo (neste exemplo, outros protocolos serão impedidos de streaming). 

Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.   

Solicitação:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


Se você quiser tooprotect seu conteúdo usando Widevine DRM, atualizar Olá AssetDeliveryConfiguration valores toouse WidevineLicenseAcquisitionUrl (que tem o valor de saudação do 7) e especifique Olá URL de um serviço de entrega de licença. Você pode usar o hello AMS parceiros toohelp fornecer licenças Widevine a seguir: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Por exemplo: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> Ao criptografar com Widevine, seria apenas toodeliver capaz de usar o traço. Verifique o protocolo de entrega do se toospecify DASH (2) Olá no ativo.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Ativos de link com a política de entrega de ativos
Confira [Ativos de link com a política de entrega de ativos](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>Tipos usados ao definir AssetDeliveryPolicy

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

Hello enum seguinte descreve os valores que você pode definir para o protocolo de entrega de ativos de saudação.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

Hello enum seguir descreve os valores que você pode definir para o tipo de política de entrega de ativos de saudação.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

Hello enum seguinte descreve os valores que você pode usar o método de entrega tooconfigure saudação do cliente de conteúdo toohello chave hello.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

Olá enum a seguir descreve os valores que você pode definir tooconfigure chaves usadas tooget configuração específica de uma política de entrega de ativos.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

