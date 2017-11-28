---
title: aaaCreate ContentKeys com .NET
description: "Saiba como chaves de conteúdo toocreate que fornecem seguro acessam tooAssets."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="81b3a-103">Criar ContentKeys com .NET</span><span class="sxs-lookup"><span data-stu-id="81b3a-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81b3a-104">REST</span><span class="sxs-lookup"><span data-stu-id="81b3a-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="81b3a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="81b3a-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="81b3a-106">Serviços de mídia permitem toocreate e entregar ativos criptografados.</span><span class="sxs-lookup"><span data-stu-id="81b3a-106">Media Services enables you toocreate and deliver encrypted assets.</span></span> <span data-ttu-id="81b3a-107">Um **ContentKey** fornece acesso seguro tooyour **ativo**s.</span><span class="sxs-lookup"><span data-stu-id="81b3a-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="81b3a-108">Quando você cria um novo ativo (por exemplo, antes de você [carregar arquivos](media-services-dotnet-upload-files.md)), você pode especificar Olá as opções de criptografia a seguir: **StorageEncrypted**, **CommonEncryptionProtected**, ou **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="81b3a-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="81b3a-109">Quando você entregar ativos tooyour clientes, você pode [configurar para toobe ativos criptografado dinamicamente](media-services-dotnet-configure-asset-delivery-policy.md) com uma saudação dois criptografias a seguir: **DynamicEnvelopeEncryption** ou  **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="81b3a-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="81b3a-110">Ativos criptografados têm toobe associado **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="81b3a-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="81b3a-111">Este artigo descreve como toocreate uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="81b3a-111">This article describes how toocreate a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="81b3a-112">Ao criar um novo **StorageEncrypted** ativo usando Olá SDK do Media Services .NET hello **ContentKey** é automaticamente criado e vinculado com ativo hello.</span><span class="sxs-lookup"><span data-stu-id="81b3a-112">When creating a new **StorageEncrypted** asset using hello Media Services .NET SDK , hello **ContentKey** is automatically created and linked with hello asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="81b3a-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="81b3a-113">ContentKeyType</span></span>
<span data-ttu-id="81b3a-114">Um dos valores de saudação que você deve definir quando criar um conteúdo de chave é o tipo de chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="81b3a-114">One of hello values that you must set when create a content key is hello content key type.</span></span> <span data-ttu-id="81b3a-115">Escolha uma saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="81b3a-115">Choose from one of hello following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <span data-ttu-id="81b3a-116"><a id="envelope_contentkey"></a>Criar um tipo de envelope de ContentKey</span><span class="sxs-lookup"><span data-stu-id="81b3a-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="81b3a-117">Olá trecho de código a seguir cria uma chave de conteúdo do tipo de criptografia de envelope hello.</span><span class="sxs-lookup"><span data-stu-id="81b3a-117">hello following code snippet creates a content key of hello envelope encryption type.</span></span> <span data-ttu-id="81b3a-118">Em seguida, associa chave Olá com ativo especificado hello.</span><span class="sxs-lookup"><span data-stu-id="81b3a-118">It then associates hello key with hello specified asset.</span></span>

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

<span data-ttu-id="81b3a-119">chamada</span><span class="sxs-lookup"><span data-stu-id="81b3a-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="81b3a-120"><a id="common_contentkey"></a>Criar um tipo comum de ContentKey</span><span class="sxs-lookup"><span data-stu-id="81b3a-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="81b3a-121">Hello trecho de código a seguir cria uma chave de conteúdo Olá comuns do tipo de criptografia.</span><span class="sxs-lookup"><span data-stu-id="81b3a-121">hello following code snippet creates a content key of hello common encryption type.</span></span> <span data-ttu-id="81b3a-122">Em seguida, associa chave Olá com ativo especificado hello.</span><span class="sxs-lookup"><span data-stu-id="81b3a-122">It then associates hello key with hello specified asset.</span></span>

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
<span data-ttu-id="81b3a-123">chamada</span><span class="sxs-lookup"><span data-stu-id="81b3a-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="81b3a-124">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="81b3a-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="81b3a-125">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="81b3a-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

