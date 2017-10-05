---
title: "Configuração de políticas de entrega de ativos usando API REST dos Serviços de Mídia | Microsoft Docs"
description: "Este tópico mostra como configurar políticas de entrega de ativos diferentes usando a API REST dos Serviços de Mídia."
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
ms.openlocfilehash: 7ffbde11b943961dd3a3b5edebd0cfd52429e845
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="af4d4-103">Configuração de políticas de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="af4d4-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="af4d4-104">Se você planeja entregar dinamicamente ativos criptografados, uma das etapas do fluxo de trabalho de distribuição de conteúdo de Serviços de Mídia é configurar políticas de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="af4d4-104">If you plan to deliver dynamically encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="af4d4-105">A política de entrega de ativos informa aos serviços de mídia como você deseja que o ativo seja entregue: em que protocolo de fluxo seu ativo deve ser dinamicamente empacotado (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), se você deseja criptografar dinamicamente seu ativo ou não e como (criptografia de envelope ou comum).</span><span class="sxs-lookup"><span data-stu-id="af4d4-105">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="af4d4-106">Este tópico discute como e por que criar e configurar políticas de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="af4d4-106">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="af4d4-107">Quando sua conta AMS é criada, um ponto de extremidade de streaming **padrão** é adicionado à sua conta em estado **Parado**.</span><span class="sxs-lookup"><span data-stu-id="af4d4-107">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="af4d4-108">Para iniciar seu conteúdo de streaming e tirar proveito do empacotamento dinâmico e da criptografia dinâmica, o ponto de extremidade de streaming do qual você deseja transmitir o conteúdo deve estar em estado **Executando**.</span><span class="sxs-lookup"><span data-stu-id="af4d4-108">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="af4d4-109">Além disso, para poder usar o empacotamento dinâmico e a criptografia dinâmica, seu ativo deve conter um conjunto de arquivos MP4 de taxa de bits adaptável ou de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="af4d4-109">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="af4d4-110">Você pode aplicar políticas diferentes para o mesmo ativo.</span><span class="sxs-lookup"><span data-stu-id="af4d4-110">You could apply different policies to the same asset.</span></span> <span data-ttu-id="af4d4-111">Por exemplo, você poderia aplicar criptografia PlayReady para criptografia de Envelope AES e Smooth Streaming para MPEG DASH e HLS.</span><span class="sxs-lookup"><span data-stu-id="af4d4-111">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="af4d4-112">Todos os protocolos que não são definidos em uma política de entrega (por exemplo, você adicionar uma única política que só especifica HLS como o protocolo) será bloqueado a partir do streaming.</span><span class="sxs-lookup"><span data-stu-id="af4d4-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="af4d4-113">A exceção a isso é se você não tiver nenhuma política de entrega de ativos definida em todos.</span><span class="sxs-lookup"><span data-stu-id="af4d4-113">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="af4d4-114">Em seguida, todos os protocolos poderão ser criptografados.</span><span class="sxs-lookup"><span data-stu-id="af4d4-114">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="af4d4-115">Se você quiser entregar um ativo de armazenamento criptografado, configure a política de entrega do ativo.</span><span class="sxs-lookup"><span data-stu-id="af4d4-115">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="af4d4-116">Antes que seu ativo possa ser transmitido, o servidor de streaming remove a criptografia de armazenamento e transmite o conteúdo usando a política de entrega especificada.</span><span class="sxs-lookup"><span data-stu-id="af4d4-116">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="af4d4-117">Por exemplo, para entregar o ativo criptografado com chave de criptografia de envelope de AES (Criptografia Avançada Padrão), defina o tipo de política como **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="af4d4-117">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="af4d4-118">Para remover a criptografia de armazenamento e transmitir o ativo não criptografado, defina o tipo de política como **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="af4d4-118">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="af4d4-119">Seguem exemplos que mostram como configurar esses tipos de política.</span><span class="sxs-lookup"><span data-stu-id="af4d4-119">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="af4d4-120">Dependendo de como você configura a política de entrega de ativos, poderá empacotar e criptografar dinamicamente, bem como transmitir os seguintes protocolos de streaming: Smooth Streaming, HLS, MPEG DASH e transmissões.</span><span class="sxs-lookup"><span data-stu-id="af4d4-120">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="af4d4-121">A lista a seguir mostra os formatos usados para transmitir Smooth, HLS e DASH.</span><span class="sxs-lookup"><span data-stu-id="af4d4-121">The following list shows the formats that you use to stream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="af4d4-122">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="af4d4-122">Smooth Streaming:</span></span>

<span data-ttu-id="af4d4-123">{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="af4d4-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="af4d4-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="af4d4-124">HLS:</span></span>

<span data-ttu-id="af4d4-125">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="af4d4-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="af4d4-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="af4d4-126">MPEG DASH</span></span>

<span data-ttu-id="af4d4-127">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="af4d4-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="af4d4-128">Para obter instruções sobre como publicar um ativo e criar uma URL de streaming, consulte [Criar uma URL de streaming](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="af4d4-128">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="af4d4-129">Considerações</span><span class="sxs-lookup"><span data-stu-id="af4d4-129">Considerations</span></span>
* <span data-ttu-id="af4d4-130">Você não pode excluir um AssetDeliveryPolicy associado a um ativo enquanto um localizador OnDemand (streaming) existir para esse ativo.</span><span class="sxs-lookup"><span data-stu-id="af4d4-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="af4d4-131">A recomendação é remover a política do ativo antes de excluir a política.</span><span class="sxs-lookup"><span data-stu-id="af4d4-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="af4d4-132">Não é possível criar um localizador de streaming em um ativo criptografado para armazenamento quando nenhuma política de entrega de ativo estiver definida.</span><span class="sxs-lookup"><span data-stu-id="af4d4-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="af4d4-133">Se o Ativo não estiver criptografado para armazenamento, o sistema permitirá que você crie um localizador e transmita o ativo sem uma política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="af4d4-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="af4d4-134">Você pode ter várias políticas de entrega de ativos associadas a um único ativo, mas pode especificar apenas uma maneira de lidar com um determinado AssetDeliveryProtocol.</span><span class="sxs-lookup"><span data-stu-id="af4d4-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="af4d4-135">Isso significa que se você tentar vincular duas políticas de entrega que especificam o protocolo AssetDeliveryProtocol.SmoothStreaming, o resultado será um erro pois o sistema não sabe qual delas você deseja aplicar quando um cliente fizer uma solicitação de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="af4d4-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="af4d4-136">Se você tiver um ativo com um localizador de streaming existente, não poderá vincular uma nova política ao ativo, desvincular uma política existente do ativo ou atualizar uma política de entrega associada ao ativo.</span><span class="sxs-lookup"><span data-stu-id="af4d4-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset, unlink an existing policy from the asset, or update a delivery policy associated with the asset.</span></span>  <span data-ttu-id="af4d4-137">Primeiro, você precisa remover o localizador de streaming, ajustar as políticas e, em seguida, recriar o localizador de streaming.</span><span class="sxs-lookup"><span data-stu-id="af4d4-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="af4d4-138">Você pode usar o mesmo locatorId quando recriar o localizador de streaming, mas certifique-se de que isso não causará problemas para os clientes uma vez que o conteúdo pode ser armazenado em cache pelo CDN de origem ou downstream.</span><span class="sxs-lookup"><span data-stu-id="af4d4-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="af4d4-139">Ao acessar entidades nos serviços de mídia, você deve definir valores e campos de cabeçalho específicos nas suas solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="af4d4-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="af4d4-140">Para obter mais informações, consulte [Configuração para desenvolvimento da API REST dos Serviços de Mídia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="af4d4-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="af4d4-141">Conectar-se aos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="af4d4-141">Connect to Media Services</span></span>

<span data-ttu-id="af4d4-142">Para saber mais sobre como conectar-se à API do AMS, veja [Acessar a API dos Serviços de Mídia do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="af4d4-142">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="af4d4-143">Depois de se conectar com êxito em https://media.windows.net, você receberá um redirecionamento 301 especificando outro URI dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="af4d4-143">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="af4d4-144">Você deve fazer chamadas subsequentes para o novo URI.</span><span class="sxs-lookup"><span data-stu-id="af4d4-144">You must make subsequent calls to the new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="af4d4-145">Política de entrega de ativos clara</span><span class="sxs-lookup"><span data-stu-id="af4d4-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="af4d4-146"><a id="create_asset_delivery_policy"></a>Criar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="af4d4-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="af4d4-147">A solicitação HTTP a seguir cria uma política de entrega de ativos que especifica a não aplicação de criptografia dinâmica e a entrega do fluxo em qualquer um dos seguintes protocolos: MPEG DASH, HLS e protocolos Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="af4d4-147">The following HTTP request creates an asset delivery policy that specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="af4d4-148">Para obter informações sobre os valores que você pode especificar ao criar um AssetDeliveryPolicy, consulte a seção [Tipos usados ao definir AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="af4d4-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="af4d4-149">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="af4d4-149">Request:</span></span>

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

<span data-ttu-id="af4d4-150">Resposta:</span><span class="sxs-lookup"><span data-stu-id="af4d4-150">Response:</span></span>

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

### <span data-ttu-id="af4d4-151"><a id="link_asset_with_asset_delivery_policy"></a>Ativos de link com a política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="af4d4-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="af4d4-152">A seguinte solicitação HTTP vincula o ativo especificado na política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="af4d4-152">The following HTTP request links the specified asset to the asset delivery policy to.</span></span>

<span data-ttu-id="af4d4-153">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="af4d4-153">Request:</span></span>

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

<span data-ttu-id="af4d4-154">Resposta:</span><span class="sxs-lookup"><span data-stu-id="af4d4-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="af4d4-155">Política de entrega de ativos DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="af4d4-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-envelopeencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="af4d4-156">Cria chave de conteúdo do tipo EnvelopeEncryption e a vincula ao ativo</span><span class="sxs-lookup"><span data-stu-id="af4d4-156">Create content key of the EnvelopeEncryption type and link it to the asset</span></span>
<span data-ttu-id="af4d4-157">Ao especificar a política de entrega DynamicEnvelopeEncryption, você precisa certificar-se de vincular seu ativo a uma chave de conteúdo do tipo EnvelopeEncryption.</span><span class="sxs-lookup"><span data-stu-id="af4d4-157">When specifying DynamicEnvelopeEncryption delivery policy, you need to make sure to link your asset to a content key of the EnvelopeEncryption type.</span></span> <span data-ttu-id="af4d4-158">Para saber mais, confira: [Criando uma chave de conteúdo](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="af4d4-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="af4d4-159"><a id="get_delivery_url"></a>Obter URL de entrega</span><span class="sxs-lookup"><span data-stu-id="af4d4-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="af4d4-160">Obter a URL de entrega para o método de entrega especificado da chave de conteúdo criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="af4d4-160">Get the delivery URL for the specified delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="af4d4-161">Um cliente usa a URL retornada para solicitar uma chave AES ou uma licença PlayReady a fim de reproduzir o conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="af4d4-161">A client uses the returned URL to request an AES key or a PlayReady license in order to playback the protected content.</span></span>

<span data-ttu-id="af4d4-162">Especifique o tipo da URL para obter no corpo da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="af4d4-162">Specify the type of the URL to get in the body of the HTTP request.</span></span> <span data-ttu-id="af4d4-163">Se você estiver protegendo o conteúdo com PlayReady, solicite uma URL de aquisição de licenças PlayReady dos Serviços de Mídia usando 1 para o keyDeliveryType: {"keyDeliveryType":1}.</span><span class="sxs-lookup"><span data-stu-id="af4d4-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for the keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="af4d4-164">Se você estiver protegendo seu conteúdo com a criptografia de envelope, solicite uma URL de aquisição de chave especificando 2 para keyDeliveryType: {"keyDeliveryType":2}.</span><span class="sxs-lookup"><span data-stu-id="af4d4-164">If you are protecting your content with the envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="af4d4-165">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="af4d4-165">Request:</span></span>

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

<span data-ttu-id="af4d4-166">Resposta:</span><span class="sxs-lookup"><span data-stu-id="af4d4-166">Response:</span></span>

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


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="af4d4-167">Criar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="af4d4-167">Create asset delivery policy</span></span>
<span data-ttu-id="af4d4-168">A solicitação HTTP a seguir cria a **AssetDeliveryPolicy** que é configurada para aplicar a criptografia de envelope dinâmico (**DynamicEnvelopeEncryption**) para o protocolo **HLS** (neste exemplo, outros protocolos serão impedidos de realizar streaming).</span><span class="sxs-lookup"><span data-stu-id="af4d4-168">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to the **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="af4d4-169">Para obter informações sobre os valores que você pode especificar ao criar um AssetDeliveryPolicy, consulte a seção [Tipos usados ao definir AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="af4d4-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="af4d4-170">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="af4d4-170">Request:</span></span>

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


<span data-ttu-id="af4d4-171">Resposta:</span><span class="sxs-lookup"><span data-stu-id="af4d4-171">Response:</span></span>

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


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="af4d4-172">Ativos de link com a política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="af4d4-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="af4d4-173">Confira [Ativos de link com a política de entrega de ativos](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="af4d4-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="af4d4-174">Política de entrega de ativos DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="af4d4-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-commonencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="af4d4-175">Cria chave de conteúdo do tipo CommonEncryption e a vincule ao ativo</span><span class="sxs-lookup"><span data-stu-id="af4d4-175">Create content key of the CommonEncryption type and link it to the asset</span></span>
<span data-ttu-id="af4d4-176">Ao especificar a política de entrega DynamicCommonEncryption, você precisa certificar-se de vincular seu ativo a uma chave de conteúdo do tipo CommonEncryption.</span><span class="sxs-lookup"><span data-stu-id="af4d4-176">When specifying DynamicCommonEncryption delivery policy, you need to make sure to link your asset to a content key of the CommonEncryption type.</span></span> <span data-ttu-id="af4d4-177">Para saber mais, confira: [Criando uma chave de conteúdo](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="af4d4-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="af4d4-178">Obter URL de entrega</span><span class="sxs-lookup"><span data-stu-id="af4d4-178">Get Delivery URL</span></span>
<span data-ttu-id="af4d4-179">Obter a URL de entrega para o método de entrega PlayReady da chave de conteúdo criada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="af4d4-179">Get the delivery URL for the PlayReady delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="af4d4-180">Um cliente usa a URL retornada para solicitar uma licença do PlayReady a fim de reproduzir o conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="af4d4-180">A client uses the returned URL to request a PlayReady license in order to playback the protected content.</span></span> <span data-ttu-id="af4d4-181">Para saber mais, confira [Obter a URL de entrega](#get_delivery_url)</span><span class="sxs-lookup"><span data-stu-id="af4d4-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="af4d4-182">Criar política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="af4d4-182">Create asset delivery policy</span></span>
<span data-ttu-id="af4d4-183">A solicitação HTTP a seguir cria o **AssetDeliveryPolicy** que é configurado para aplicar a criptografia comum dinâmica (**DynamicCommonEncryption**) para o protocolo **Smooth Streaming** (neste exemplo, outros protocolos serão impedidos de realizar streaming).</span><span class="sxs-lookup"><span data-stu-id="af4d4-183">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to the **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="af4d4-184">Para obter informações sobre os valores que você pode especificar ao criar um AssetDeliveryPolicy, consulte a seção [Tipos usados ao definir AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="af4d4-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="af4d4-185">Solicitação:</span><span class="sxs-lookup"><span data-stu-id="af4d4-185">Request:</span></span>

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


<span data-ttu-id="af4d4-186">Se você deseja proteger o conteúdo usando Widevine DRM, atualize os valores de AssetDeliveryConfiguration para usar WidevineLicenseAcquisitionUrl (que tem o valor de 7) e especifique a URL de um serviço de fornecimento de licença.</span><span class="sxs-lookup"><span data-stu-id="af4d4-186">If you want to protect your content using Widevine DRM, update the AssetDeliveryConfiguration values to use WidevineLicenseAcquisitionUrl (which has the value of 7) and specify the URL of a license delivery service.</span></span> <span data-ttu-id="af4d4-187">Você pode usar os seguintes parceiros do AMS para ajudá-lo a fornecer licenças Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/) e [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="af4d4-187">You can use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="af4d4-188">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="af4d4-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="af4d4-189">Ao criptografar com Widevine, você só seria capaz de fornecer usando um DASH.</span><span class="sxs-lookup"><span data-stu-id="af4d4-189">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="af4d4-190">Certifique-se de especificar DASH (2) no protocolo de fornecimento de ativos.</span><span class="sxs-lookup"><span data-stu-id="af4d4-190">Make sure to specify DASH (2) in the asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="af4d4-191">Ativos de link com a política de entrega de ativos</span><span class="sxs-lookup"><span data-stu-id="af4d4-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="af4d4-192">Confira [Ativos de link com a política de entrega de ativos](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="af4d4-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="af4d4-193"><a id="types"></a>Tipos usados ao definir AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="af4d4-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="af4d4-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="af4d4-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="af4d4-195">O enum a seguir descreve os valores que podem ser definidos para o protocolo de entrega de ativo.</span><span class="sxs-lookup"><span data-stu-id="af4d4-195">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="af4d4-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="af4d4-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="af4d4-197">O enum a seguir descreve os valores que podem ser definidos para o tipo de política de entrega de ativo.</span><span class="sxs-lookup"><span data-stu-id="af4d4-197">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="af4d4-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="af4d4-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="af4d4-199">O enum a seguir descreve os valores que você pode usar para configurar o método de entrega da chave de conteúdo para o cliente.</span><span class="sxs-lookup"><span data-stu-id="af4d4-199">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="af4d4-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="af4d4-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="af4d4-201">O enum a seguir descreve os valores que você pode definir para configurar as chaves usadas para obter uma configuração específica para uma política de entrega de ativo.</span><span class="sxs-lookup"><span data-stu-id="af4d4-201">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="af4d4-202">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="af4d4-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="af4d4-203">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="af4d4-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

