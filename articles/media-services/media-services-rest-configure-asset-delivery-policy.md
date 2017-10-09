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
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="cfa93-103">Configuração de políticas de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="cfa93-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="cfa93-104">Se você planejar ativos toodeliver dinamicamente criptografado, uma saudação etapas no hello conteúdo de fluxo de trabalho de entrega está configurando políticas de entrega de ativos de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="cfa93-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="cfa93-105">política de entrega de ativos de saudação informa os serviços de mídia como você deseja para sua toobe ativo entregue: em qual protocolo de streaming deve seu ativo dinamicamente empacotado (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), se você deseja toodynamically ou não criptografar seu ativo e como (envelope ou criptografia comum).</span><span class="sxs-lookup"><span data-stu-id="cfa93-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="cfa93-106">Este tópico discute por que e como toocreate e configurar políticas de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="cfa93-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="cfa93-107">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="cfa93-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="cfa93-108">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="cfa93-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="cfa93-109">Além disso, o empacotamento dinâmico capaz de toouse toobe e criptografia dinâmica seu ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="cfa93-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="cfa93-110">Você pode aplicar políticas diferentes toohello mesmo ativo.</span><span class="sxs-lookup"><span data-stu-id="cfa93-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="cfa93-111">Por exemplo, você pode aplicar PlayReady criptografia tooSmooth Streaming e Envelope AES criptografia tooMPEG DASH e HLS.</span><span class="sxs-lookup"><span data-stu-id="cfa93-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="cfa93-112">Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming.</span><span class="sxs-lookup"><span data-stu-id="cfa93-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="cfa93-113">Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida.</span><span class="sxs-lookup"><span data-stu-id="cfa93-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="cfa93-114">Em seguida, todos os protocolos poderão ser em Olá clara.</span><span class="sxs-lookup"><span data-stu-id="cfa93-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="cfa93-115">Se você quiser toodeliver um ativo de armazenamento criptografado, você deve configurar a política de entrega do hello ativo.</span><span class="sxs-lookup"><span data-stu-id="cfa93-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="cfa93-116">Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado a política de distribuição.</span><span class="sxs-lookup"><span data-stu-id="cfa93-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="cfa93-117">Por exemplo, toodeliver seu ativo criptografado com chave de criptografia de envelope AES Advanced Encryption Standard (), defina o tipo de política de saudação muito**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="cfa93-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="cfa93-118">criptografia de armazenamento tooremove e ativo de saudação do fluxo em Olá claro, defina tipo de política de saudação muito**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="cfa93-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="cfa93-119">Exemplos que mostram como tooconfigure esses tipos de política execute.</span><span class="sxs-lookup"><span data-stu-id="cfa93-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="cfa93-120">Dependendo de como você configurar a política de distribuição do ativo Olá seria ser capaz de toodynamically pacote dinamicamente criptografar e Olá seguintes protocolos de transmissão de fluxo: Smooth Streaming, HLS, fluxos MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="cfa93-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="cfa93-121">Olá seguinte lista mostra Olá formatos que você use toostream Smooth, HLS, traço.</span><span class="sxs-lookup"><span data-stu-id="cfa93-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="cfa93-122">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="cfa93-122">Smooth Streaming:</span></span>

<span data-ttu-id="cfa93-123">{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="cfa93-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="cfa93-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="cfa93-124">HLS:</span></span>

<span data-ttu-id="cfa93-125">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="cfa93-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="cfa93-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="cfa93-126">MPEG DASH</span></span>

<span data-ttu-id="cfa93-127">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="cfa93-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="cfa93-128">Para obter instruções sobre como toopublish um ativo e compilar uma URL de streaming, consulte [construir uma URL de streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="cfa93-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="cfa93-129">Considerações</span><span class="sxs-lookup"><span data-stu-id="cfa93-129">Considerations</span></span>
* <span data-ttu-id="cfa93-130">Você não pode excluir um AssetDeliveryPolicy associado a um ativo enquanto um localizador OnDemand (streaming) existir para esse ativo.</span><span class="sxs-lookup"><span data-stu-id="cfa93-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="cfa93-131">recomendação de saudação é tooremove política de saudação do ativo de saudação antes de excluir a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfa93-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="cfa93-132">Não é possível criar um localizador de streaming em um ativo criptografado para armazenamento quando nenhuma política de entrega de ativo estiver definida.</span><span class="sxs-lookup"><span data-stu-id="cfa93-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="cfa93-133">Se Olá ativo não criptografado de armazenamento, o sistema Olá permitem criar um ativo de localizador e o fluxo Olá Olá desmarque sem uma política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="cfa93-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="cfa93-134">Você pode ter várias políticas de entrega de ativo associadas a um único ativo, mas você só pode especificar uma maneira toohandle AssetDeliveryProtocol um determinado.</span><span class="sxs-lookup"><span data-stu-id="cfa93-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="cfa93-135">Que significa que se você tentar toolink duas políticas de entrega que especificar o protocolo de AssetDeliveryProtocol.SmoothStreaming de saudação resultará em um erro porque o sistema Olá não sabe qual deles você deseja tooapply quando um cliente faz uma solicitação de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="cfa93-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="cfa93-136">Se você tiver um ativo com um localizador de streaming existente, você não pode vincular um novo ativo toohello política, desvincular uma política existente de ativo de saudação ou atualizar uma política de distribuição associada a saudação ativo.</span><span class="sxs-lookup"><span data-stu-id="cfa93-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="cfa93-137">Primeiro ter localizador de transmissão tooremove hello, ajustar as diretivas de saudação e recrie o hello localizador de streaming.</span><span class="sxs-lookup"><span data-stu-id="cfa93-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="cfa93-138">Você pode usar o hello locatorId mesmo quando você recriar Olá streaming localizador, mas você deve garantir que não causar problemas para os clientes desde que o conteúdo pode ser armazenado em cache por origem hello ou um CDN de downstream.</span><span class="sxs-lookup"><span data-stu-id="cfa93-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="cfa93-139">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="cfa93-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="cfa93-140">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cfa93-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="cfa93-141">Conectar os serviços de tooMedia</span><span class="sxs-lookup"><span data-stu-id="cfa93-141">Connect tooMedia Services</span></span>

<span data-ttu-id="cfa93-142">Para obter informações sobre como tooconnect toohello AMS API, consulte [Olá acesso API de serviços de mídia do Azure com a autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="cfa93-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="cfa93-143">Após conectar-se toohttps://media.windows.net, você receberá um redirecionamento 301 que especifica outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="cfa93-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="cfa93-144">Você deve fazer chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="cfa93-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="cfa93-145">Política de entrega de ativos clara</span><span class="sxs-lookup"><span data-stu-id="cfa93-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="cfa93-146"><a id="create_asset_delivery_policy"></a>Criar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="cfa93-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="cfa93-147">Olá, solicitação HTTP a seguir cria uma política de entrega de ativos que especifica toonot aplicar criptografia dinâmica e protocolos de fluxo de saudação toodeliver em qualquer Olá a seguir: protocolos MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="cfa93-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="cfa93-148">Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.</span><span class="sxs-lookup"><span data-stu-id="cfa93-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="cfa93-149">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="cfa93-149">Request:</span></span>

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

<span data-ttu-id="cfa93-150">Resposta:</span><span class="sxs-lookup"><span data-stu-id="cfa93-150">Response:</span></span>

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

### <span data-ttu-id="cfa93-151"><a id="link_asset_with_asset_delivery_policy"></a>Ativos de link com a política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="cfa93-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="cfa93-152">Olá Olá de links de solicitação HTTP a seguir especificado a política de distribuição do ativo toohello ativo para.</span><span class="sxs-lookup"><span data-stu-id="cfa93-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="cfa93-153">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="cfa93-153">Request:</span></span>

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

<span data-ttu-id="cfa93-154">Resposta:</span><span class="sxs-lookup"><span data-stu-id="cfa93-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="cfa93-155">Política de entrega de ativos DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="cfa93-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="cfa93-156">Criar chave de conteúdo do tipo de EnvelopeEncryption hello e vinculá-lo ativo toohello</span><span class="sxs-lookup"><span data-stu-id="cfa93-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="cfa93-157">Ao especificar a política de distribuição DynamicEnvelopeEncryption, é necessário toolink se toomake a chave de conteúdo ativo tooa de saudação tipo EnvelopeEncryption.</span><span class="sxs-lookup"><span data-stu-id="cfa93-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="cfa93-158">Para saber mais, confira: [Criando uma chave de conteúdo](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="cfa93-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="cfa93-159"><a id="get_delivery_url"></a>Obter URL de entrega</span><span class="sxs-lookup"><span data-stu-id="cfa93-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="cfa93-160">URL de envio de saudação Get para Olá especificado método de entrega da chave de conteúdo Olá criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="cfa93-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="cfa93-161">Um cliente usa Olá retornado URL toorequest uma chave AES ou uma licença do PlayReady Olá de tooplayback ordem conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="cfa93-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="cfa93-162">Especifique o tipo de saudação de Olá URL tooget no corpo de saudação de solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfa93-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="cfa93-163">Se você estiver protegendo o conteúdo com PlayReady, solicite uma URL de aquisição de licença do PlayReady dos serviços de mídia, usando 1 para Olá keyDeliveryType: {"keyDeliveryType": 1}.</span><span class="sxs-lookup"><span data-stu-id="cfa93-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="cfa93-164">Se você estiver protegendo o conteúdo com criptografia de envelope hello, solicite uma URL de aquisição de chaves especificando 2 para keyDeliveryType: {"keyDeliveryType": 2}.</span><span class="sxs-lookup"><span data-stu-id="cfa93-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="cfa93-165">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="cfa93-165">Request:</span></span>

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

<span data-ttu-id="cfa93-166">Resposta:</span><span class="sxs-lookup"><span data-stu-id="cfa93-166">Response:</span></span>

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


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="cfa93-167">Criar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="cfa93-167">Create asset delivery policy</span></span>
<span data-ttu-id="cfa93-168">Olá, solicitação HTTP a seguir cria Olá **AssetDeliveryPolicy** tooapply configurado que é a criptografia de envelope dinâmica (**DynamicEnvelopeEncryption**) toohello **HLS**protocolo (neste exemplo, outros protocolos serão impedidos de streaming).</span><span class="sxs-lookup"><span data-stu-id="cfa93-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="cfa93-169">Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.</span><span class="sxs-lookup"><span data-stu-id="cfa93-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="cfa93-170">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="cfa93-170">Request:</span></span>

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


<span data-ttu-id="cfa93-171">Resposta:</span><span class="sxs-lookup"><span data-stu-id="cfa93-171">Response:</span></span>

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


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="cfa93-172">Ativos de link com a política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="cfa93-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="cfa93-173">Confira [Ativos de link com a política de entrega de ativos](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="cfa93-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="cfa93-174">Política de entrega de ativos DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="cfa93-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="cfa93-175">Criar chave de conteúdo do tipo de CommonEncryption hello e vinculá-lo ativo toohello</span><span class="sxs-lookup"><span data-stu-id="cfa93-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="cfa93-176">Ao especificar a política de distribuição DynamicCommonEncryption, é necessário toolink se toomake a chave de conteúdo ativo tooa de saudação tipo CommonEncryption.</span><span class="sxs-lookup"><span data-stu-id="cfa93-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="cfa93-177">Para saber mais, confira: [Criando uma chave de conteúdo](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="cfa93-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="cfa93-178">Obter URL de entrega</span><span class="sxs-lookup"><span data-stu-id="cfa93-178">Get Delivery URL</span></span>
<span data-ttu-id="cfa93-179">Obter URL de entrega de Olá Olá PlayReady método de entrega da chave de conteúdo Olá criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="cfa93-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="cfa93-180">Um cliente usa Olá retornado toorequest URL protegida de uma licença do PlayReady Olá de tooplayback ordem conteúdo.</span><span class="sxs-lookup"><span data-stu-id="cfa93-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="cfa93-181">Para saber mais, confira [Obter a URL de entrega](#get_delivery_url)</span><span class="sxs-lookup"><span data-stu-id="cfa93-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="cfa93-182">Criar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="cfa93-182">Create asset delivery policy</span></span>
<span data-ttu-id="cfa93-183">Olá, solicitação HTTP a seguir cria Olá **AssetDeliveryPolicy** que é configurado tooapply comuns criptografia dinâmica (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocolo (neste exemplo, outros protocolos serão impedidos de streaming).</span><span class="sxs-lookup"><span data-stu-id="cfa93-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="cfa93-184">Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.</span><span class="sxs-lookup"><span data-stu-id="cfa93-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="cfa93-185">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="cfa93-185">Request:</span></span>

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


<span data-ttu-id="cfa93-186">Se você quiser tooprotect seu conteúdo usando Widevine DRM, atualizar Olá AssetDeliveryConfiguration valores toouse WidevineLicenseAcquisitionUrl (que tem o valor de saudação do 7) e especifique Olá URL de um serviço de entrega de licença.</span><span class="sxs-lookup"><span data-stu-id="cfa93-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="cfa93-187">Você pode usar o hello AMS parceiros toohelp fornecer licenças Widevine a seguir: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="cfa93-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="cfa93-188">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cfa93-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="cfa93-189">Ao criptografar com Widevine, seria apenas toodeliver capaz de usar o traço.</span><span class="sxs-lookup"><span data-stu-id="cfa93-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="cfa93-190">Verifique o protocolo de entrega do se toospecify DASH (2) Olá no ativo.</span><span class="sxs-lookup"><span data-stu-id="cfa93-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="cfa93-191">Ativos de link com a política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="cfa93-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="cfa93-192">Confira [Ativos de link com a política de entrega de ativos](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="cfa93-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="cfa93-193"><a id="types"></a>Tipos usados ao definir AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="cfa93-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="cfa93-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="cfa93-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="cfa93-195">Hello enum seguinte descreve os valores que você pode definir para o protocolo de entrega de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfa93-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="cfa93-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="cfa93-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="cfa93-197">Hello enum seguir descreve os valores que você pode definir para o tipo de política de entrega de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cfa93-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="cfa93-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="cfa93-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="cfa93-199">Hello enum seguinte descreve os valores que você pode usar o método de entrega tooconfigure saudação do cliente de conteúdo toohello chave hello.</span><span class="sxs-lookup"><span data-stu-id="cfa93-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="cfa93-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="cfa93-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="cfa93-201">Olá enum a seguir descreve os valores que você pode definir tooconfigure chaves usadas tooget configuração específica de uma política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="cfa93-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="cfa93-202">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="cfa93-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cfa93-203">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="cfa93-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

