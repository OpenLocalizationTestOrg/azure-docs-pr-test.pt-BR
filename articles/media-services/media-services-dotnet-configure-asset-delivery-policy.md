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
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>Configurar políticas de entrega de ativos usando o SDK do .NET
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>Visão geral
Se você planejar ativos toodelivery criptografado, uma saudação etapas no hello conteúdo de fluxo de trabalho de entrega está configurando políticas de entrega de ativos de serviços de mídia. política de entrega de ativos de saudação informa os serviços de mídia como você deseja para sua toobe ativo entregue: em qual protocolo de streaming deve seu ativo dinamicamente empacotado (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), se você deseja toodynamically ou não criptografar seu ativo e como (envelope ou criptografia comum).

Este tópico discute por que e como toocreate e configurar políticas de entrega de ativos.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 
>
>Além disso, o empacotamento dinâmico capaz de toouse toobe e criptografia dinâmica seu ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável.


Você pode aplicar políticas diferentes toohello mesmo ativo. Por exemplo, você pode aplicar PlayReady criptografia tooSmooth Streaming e Envelope AES criptografia tooMPEG DASH e HLS. Todos os protocolos que não estão definidos em uma política de entrega (por exemplo, você adiciona uma única política que só especifica HLS como protocolo de saudação) serão impedidos de streaming. Olá toothis de exceção é se você não tiver nenhuma política de entrega de ativo definida. Em seguida, todos os protocolos poderão ser em Olá clara.

Se você quiser toodeliver um ativo de armazenamento criptografado, você deve configurar a política de entrega do hello ativo. Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado a política de distribuição. Por exemplo, toodeliver seu ativo criptografado com chave de criptografia de envelope AES Advanced Encryption Standard (), defina o tipo de política de saudação muito**DynamicEnvelopeEncryption**. criptografia de armazenamento tooremove e ativo de saudação do fluxo em Olá claro, defina tipo de política de saudação muito**NoDynamicEncryption**. Exemplos que mostram como tooconfigure esses tipos de política execute.

Dependendo de como você configurar a política de distribuição do ativo Olá seria ser capaz de toodynamically pacote dinamicamente criptografar e Olá seguintes protocolos de transmissão de fluxo: fluxos de Smooth Streaming, HLS e MPEG DASH.

Olá lista a seguir mostra os formatos de saudação que você use toostream Smooth, HLS e DASH.

Smooth Streaming:

{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest

HLS:

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>Considerações
* Você não pode excluir um AssetDeliveryPolicy associado a um ativo enquanto um localizador OnDemand (streaming) existir para esse ativo. recomendação de saudação é tooremove política de saudação do ativo de saudação antes de excluir a política de saudação.
* Não é possível criar um localizador de streaming em um ativo criptografado para armazenamento quando nenhuma política de entrega de ativo estiver definida.  Se Olá ativo não criptografado de armazenamento, o sistema Olá permitem criar um ativo de localizador e o fluxo Olá Olá desmarque sem uma política de entrega de ativos.
* Você pode ter várias políticas de entrega de ativo associadas a um único ativo, mas você só pode especificar uma maneira toohandle AssetDeliveryProtocol um determinado.  Que significa que se você tentar toolink duas políticas de entrega que especificar o protocolo de AssetDeliveryProtocol.SmoothStreaming de saudação resultará em um erro porque o sistema Olá não sabe qual deles você deseja tooapply quando um cliente faz uma solicitação de Smooth Streaming.
* Se você tiver um ativo com um localizador de streaming existente, você não pode vincular um novo ativo de toohello política (você pode desvincular uma política existente de ativo hello, ou atualizar uma política de distribuição associada a saudação ativo).  Primeiro ter localizador de transmissão tooremove hello, ajustar as diretivas de saudação e recrie o hello localizador de streaming.  Você pode usar o hello locatorId mesmo quando você recriar Olá streaming localizador, mas você deve garantir que não causar problemas para os clientes desde que o conteúdo pode ser armazenado em cache por origem hello ou um CDN de downstream.

## <a name="clear-asset-delivery-policy"></a>Política de entrega de ativos clara

a seguir Olá **ConfigureClearAssetDeliveryPolicy** método especifica toonot aplicar criptografia dinâmica e protocolos de fluxo de saudação toodeliver em qualquer Olá a seguir: protocolos MPEG DASH, HLS e Smooth Streaming. Talvez você queira tooapply ativos de armazenamento criptografado de tooyour essa política.

Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>Política de entrega de ativos DynamicCommonEncryption

a seguir Olá **CreateAssetDeliveryPolicy** método cria Olá **AssetDeliveryPolicy** que é configurado tooapply comuns criptografia dinâmica (**DynamicCommonEncryption**) tooa smooth streaming protocol (outros protocolos serão impedidos de streaming). método Hello usa dois parâmetros: **ativos** (Olá toowhich ativo que você deseja que a política de distribuição Olá tooapply) e **IContentKey** (chave de conteúdo de saudação do hello **CommonEncryption**tipo, para obter mais informações, consulte: [criando uma chave de conteúdo](media-services-dotnet-create-contentkey.md#common_contentkey)).

Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.

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

Serviços de mídia do Azure também permite que você tooadd Widevine criptografia. Olá exemplo a seguir demonstra PlayReady e Widevine que está sendo adicionado toohello política de entrega de ativos.

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
> Ao criptografar com Widevine, seria apenas toodeliver capaz de usar o traço. Verifique se toospecify traço no protocolo de entrega de ativos de saudação.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>Política de entrega de ativos DynamicEnvelopeEncryption
a seguir Olá **CreateAssetDeliveryPolicy** método cria Olá **AssetDeliveryPolicy** tooapply configurado que é a criptografia de envelope dinâmica (**DynamicEnvelopeEncryption** ) tooSmooth protocolos de Streaming, HLS e DASH (se você decidir toonot especificar alguns protocolos, eles serão impedidos de streaming). método Hello usa dois parâmetros: **ativos** (Olá toowhich ativo que você deseja que a política de distribuição Olá tooapply) e **IContentKey** (chave de conteúdo de saudação do hello **EnvelopeEncryption**tipo, para obter mais informações, consulte: [criando uma chave de conteúdo](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Para obter informações sobre quais valores que você podem especificar ao criar um AssetDeliveryPolicy, consulte Olá [tipos usados ao definir AssetDeliveryPolicy](#types) seção.   

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


## <a id="types"></a>Tipos usados ao definir AssetDeliveryPolicy

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

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

