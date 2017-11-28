---
title: "políticas de entrega de ativos aaaConfigure com o SDK .NET | Microsoft Docs"
description: "Este tópico mostra como as políticas de entrega de ativo diferente tooconfigure com o SDK do Azure Media Services .NET."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="ddb49-103">Configurar políticas de entrega de ativos usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="ddb49-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="ddb49-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ddb49-104">Overview</span></span>
<span data-ttu-id="ddb49-105">Se você planejar ativos toodelivery criptografado, uma saudação etapas no hello conteúdo de fluxo de trabalho de entrega está configurando políticas de entrega de ativos de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="ddb49-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="ddb49-106">política de entrega de ativos de saudação informa os serviços de mídia como você deseja para sua toobe ativo entregue: em qual protocolo de streaming deve seu ativo dinamicamente empacotado (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), se você deseja toodynamically ou não criptografar seu ativo e como (envelope ou criptografia comum).</span><span class="sxs-lookup"><span data-stu-id="ddb49-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="ddb49-107">Este tópico discute por que e como toocreate e configurar políticas de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="ddb49-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="ddb49-108">Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="ddb49-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="ddb49-109">toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado.</span><span class="sxs-lookup"><span data-stu-id="ddb49-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="ddb49-110">Além disso, o empacotamento dinâmico capaz de toouse toobe e criptografia dinâmica seu ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.</span><span class="sxs-lookup"><span data-stu-id="ddb49-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="ddb49-111">Você pode aplicar políticas diferentes toohello mesmo ativo.</span><span class="sxs-lookup"><span data-stu-id="ddb49-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="ddb49-112">Por exemplo, você pode aplicar PlayReady criptografia tooSmooth Streaming e Envelope AES criptografia tooMPEG DASH e HLS.</span><span class="sxs-lookup"><span data-stu-id="ddb49-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="ddb49-113">Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming.</span><span class="sxs-lookup"><span data-stu-id="ddb49-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="ddb49-114">Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida.</span><span class="sxs-lookup"><span data-stu-id="ddb49-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="ddb49-115">Em seguida, todos os protocolos poderão ser em Olá clara.</span><span class="sxs-lookup"><span data-stu-id="ddb49-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="ddb49-116">Se você quiser toodeliver um ativo de armazenamento criptografado, você deve configurar a política de entrega do hello ativo.</span><span class="sxs-lookup"><span data-stu-id="ddb49-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="ddb49-117">Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado a política de distribuição.</span><span class="sxs-lookup"><span data-stu-id="ddb49-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="ddb49-118">Por exemplo, toodeliver seu ativo criptografado com chave de criptografia de envelope AES Advanced Encryption Standard (), defina o tipo de política de saudação muito**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ddb49-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="ddb49-119">criptografia de armazenamento tooremove e ativo de saudação do fluxo em Olá claro, defina tipo de política de saudação muito**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ddb49-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="ddb49-120">Exemplos que mostram como tooconfigure esses tipos de política execute.</span><span class="sxs-lookup"><span data-stu-id="ddb49-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="ddb49-121">Dependendo de como você configurar a política de distribuição do ativo Olá seria ser capaz de toodynamically pacote dinamicamente criptografar e Olá seguintes protocolos de transmissão de fluxo: fluxos de Smooth Streaming, HLS e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="ddb49-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="ddb49-122">Olá lista a seguir mostra os formatos de saudação que você use toostream Smooth, HLS e DASH.</span><span class="sxs-lookup"><span data-stu-id="ddb49-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="ddb49-123">Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="ddb49-123">Smooth Streaming:</span></span>

<span data-ttu-id="ddb49-124">{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="ddb49-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="ddb49-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="ddb49-125">HLS:</span></span>

<span data-ttu-id="ddb49-126">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="ddb49-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="ddb49-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="ddb49-127">MPEG DASH</span></span>

<span data-ttu-id="ddb49-128">{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="ddb49-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="ddb49-129">Considerações</span><span class="sxs-lookup"><span data-stu-id="ddb49-129">Considerations</span></span>
* <span data-ttu-id="ddb49-130">Você não pode excluir um AssetDeliveryPolicy associado a um ativo enquanto um localizador OnDemand (streaming) existir para esse ativo.</span><span class="sxs-lookup"><span data-stu-id="ddb49-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="ddb49-131">recomendação de saudação é tooremove política de saudação do ativo de saudação antes de excluir a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddb49-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="ddb49-132">Não é possível criar um localizador de streaming em um ativo criptografado para armazenamento quando nenhuma política de entrega de ativo estiver definida.</span><span class="sxs-lookup"><span data-stu-id="ddb49-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="ddb49-133">Se Olá ativo não criptografado de armazenamento, o sistema Olá permitem criar um ativo de localizador e o fluxo Olá Olá desmarque sem uma política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="ddb49-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="ddb49-134">Você pode ter várias políticas de entrega de ativo associadas a um único ativo, mas você só pode especificar uma maneira toohandle AssetDeliveryProtocol um determinado.</span><span class="sxs-lookup"><span data-stu-id="ddb49-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="ddb49-135">Que significa que se você tentar toolink duas políticas de entrega que especificar o protocolo de AssetDeliveryProtocol.SmoothStreaming de saudação resultará em um erro porque o sistema Olá não sabe qual deles você deseja tooapply quando um cliente faz uma solicitação de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="ddb49-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="ddb49-136">Se você tiver um ativo com um localizador de streaming existente, você não pode vincular um novo ativo de toohello política (você pode desvincular uma política existente de ativo hello, ou atualizar uma política de distribuição associada a saudação ativo).</span><span class="sxs-lookup"><span data-stu-id="ddb49-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="ddb49-137">Primeiro ter localizador de transmissão tooremove hello, ajustar as diretivas de saudação e recrie o hello localizador de streaming.</span><span class="sxs-lookup"><span data-stu-id="ddb49-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="ddb49-138">Você pode usar o hello locatorId mesmo quando você recriar Olá streaming localizador, mas você deve garantir que não causar problemas para os clientes desde que o conteúdo pode ser armazenado em cache por origem hello ou um CDN de downstream.</span><span class="sxs-lookup"><span data-stu-id="ddb49-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="ddb49-139">Política de entrega de ativos clara</span><span class="sxs-lookup"><span data-stu-id="ddb49-139">Clear asset delivery policy</span></span>

<span data-ttu-id="ddb49-140">a seguir Olá **ConfigureClearAssetDeliveryPolicy** método especifica toonot aplicar criptografia dinâmica e protocolos de fluxo de saudação toodeliver em qualquer Olá a seguir: protocolos MPEG DASH, HLS e Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="ddb49-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="ddb49-141">Talvez você queira tooapply ativos de armazenamento criptografado de tooyour essa política.</span><span class="sxs-lookup"><span data-stu-id="ddb49-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="ddb49-142">Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.</span><span class="sxs-lookup"><span data-stu-id="ddb49-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="ddb49-143">Política de entrega de ativos DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="ddb49-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="ddb49-144">a seguir Olá **CreateAssetDeliveryPolicy** método cria Olá **AssetDeliveryPolicy** que é configurado tooapply comuns criptografia dinâmica (**DynamicCommonEncryption**) tooa smooth streaming protocol (outros protocolos serão impedidos de streaming).</span><span class="sxs-lookup"><span data-stu-id="ddb49-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="ddb49-145">método Hello usa dois parâmetros: **ativos** (Olá toowhich ativo que você deseja que a política de distribuição Olá tooapply) e **IContentKey** (chave de conteúdo de saudação do hello **CommonEncryption**tipo, para obter mais informações, consulte: [criando uma chave de conteúdo](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ddb49-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="ddb49-146">Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.</span><span class="sxs-lookup"><span data-stu-id="ddb49-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="ddb49-147">Serviços de mídia do Azure também permite que você tooadd Widevine criptografia.</span><span class="sxs-lookup"><span data-stu-id="ddb49-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="ddb49-148">Olá exemplo a seguir demonstra PlayReady e Widevine que está sendo adicionado toohello política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="ddb49-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="ddb49-149">Ao criptografar com Widevine, seria apenas toodeliver capaz de usar o traço.</span><span class="sxs-lookup"><span data-stu-id="ddb49-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="ddb49-150">Verifique se toospecify traço no protocolo de entrega de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddb49-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="ddb49-151">Política de entrega de ativos DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="ddb49-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="ddb49-152">a seguir Olá **CreateAssetDeliveryPolicy** método cria Olá **AssetDeliveryPolicy** tooapply configurado que é a criptografia de envelope dinâmica (**DynamicEnvelopeEncryption** ) tooSmooth protocolos de Streaming, HLS e DASH (se você decidir toonot especificar alguns protocolos, eles serão impedidos de streaming).</span><span class="sxs-lookup"><span data-stu-id="ddb49-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="ddb49-153">método Hello usa dois parâmetros: **ativos** (Olá toowhich ativo que você deseja que a política de distribuição Olá tooapply) e **IContentKey** (chave de conteúdo de saudação do hello **EnvelopeEncryption**tipo, para obter mais informações, consulte: [criando uma chave de conteúdo](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ddb49-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="ddb49-154">Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.</span><span class="sxs-lookup"><span data-stu-id="ddb49-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="ddb49-155"><a id="types"></a>Tipos usados ao definir AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="ddb49-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="ddb49-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="ddb49-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="ddb49-157">Hello enum seguinte descreve os valores que você pode definir para o protocolo de entrega de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddb49-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="ddb49-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="ddb49-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="ddb49-159">Hello enum seguir descreve os valores que você pode definir para o tipo de política de entrega de ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddb49-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="ddb49-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="ddb49-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="ddb49-161">Hello enum seguinte descreve os valores que você pode usar o método de entrega tooconfigure saudação do cliente de conteúdo toohello chave hello.</span><span class="sxs-lookup"><span data-stu-id="ddb49-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="ddb49-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="ddb49-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="ddb49-163">Olá enum a seguir descreve os valores que você pode definir tooconfigure chaves usadas tooget configuração específica de uma política de entrega de ativos.</span><span class="sxs-lookup"><span data-stu-id="ddb49-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="ddb49-164">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ddb49-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ddb49-165">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ddb49-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

