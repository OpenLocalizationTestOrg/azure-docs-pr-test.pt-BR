---
title: Criar ContentKeys com .NET
description: "Saiba como criar chaves de conteúdo que fornecem acesso seguro aos ativos."
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
ms.openlocfilehash: 3280a6fcde59bae360da7cb9fea4bb649f984e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="a8c10-103">Criar ContentKeys com .NET</span><span class="sxs-lookup"><span data-stu-id="a8c10-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8c10-104">REST</span><span class="sxs-lookup"><span data-stu-id="a8c10-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="a8c10-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a8c10-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="a8c10-106">Os serviços de mídia permitem que você crie ativos e forneça ativos criptografados.</span><span class="sxs-lookup"><span data-stu-id="a8c10-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="a8c10-107">Uma **ContentKey** fornece acesso seguro aos seus **ativos**.</span><span class="sxs-lookup"><span data-stu-id="a8c10-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="a8c10-108">Ao criar um novo ativo (por exemplo, antes de [carregar arquivos](media-services-dotnet-upload-files.md)), você pode especificar as seguintes opções de criptografia: **StorageEncrypted**, **CommonEncryptionProtected** ou **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="a8c10-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="a8c10-109">Quando você fornece ativos para seus clientes, é possível [configurar para que os ativos sejam criptografados dinamicamente](media-services-dotnet-configure-asset-delivery-policy.md) com uma das duas criptografias a seguir: **DynamicEnvelopeEncryption** ou **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="a8c10-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="a8c10-110">Os ativos criptografados precisam ser associados a **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="a8c10-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="a8c10-111">Este artigo descreve como criar uma chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a8c10-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="a8c10-112">Ao criar um novo ativo **StorageEncrypted** usando o SDK do .NET dos Serviços de Mídia, a **ContentKey** é automaticamente criada e vinculada ao ativo.</span><span class="sxs-lookup"><span data-stu-id="a8c10-112">When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="a8c10-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="a8c10-113">ContentKeyType</span></span>
<span data-ttu-id="a8c10-114">Um dos valores que você deve definir ao criar um conteúdo da chave é o tipo de chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a8c10-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="a8c10-115">Escolha um dos seguintes valores.</span><span class="sxs-lookup"><span data-stu-id="a8c10-115">Choose from one of the following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
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

## <span data-ttu-id="a8c10-116"><a id="envelope_contentkey"></a>Criar um tipo de envelope de ContentKey</span><span class="sxs-lookup"><span data-stu-id="a8c10-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="a8c10-117">O trecho de código a seguir cria uma chave de conteúdo do tipo de criptografia de envelope.</span><span class="sxs-lookup"><span data-stu-id="a8c10-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="a8c10-118">Em seguida, associa a chave com o ativo especificado.</span><span class="sxs-lookup"><span data-stu-id="a8c10-118">It then associates the key with the specified asset.</span></span>

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

<span data-ttu-id="a8c10-119">chamada</span><span class="sxs-lookup"><span data-stu-id="a8c10-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="a8c10-120"><a id="common_contentkey"></a>Criar um tipo comum de ContentKey</span><span class="sxs-lookup"><span data-stu-id="a8c10-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="a8c10-121">O trecho de código a seguir cria uma chave de conteúdo do tipo de criptografia comum.</span><span class="sxs-lookup"><span data-stu-id="a8c10-121">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="a8c10-122">Em seguida, associa a chave com o ativo especificado.</span><span class="sxs-lookup"><span data-stu-id="a8c10-122">It then associates the key with the specified asset.</span></span>

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

        // Associate the key with the asset.
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
<span data-ttu-id="a8c10-123">chamada</span><span class="sxs-lookup"><span data-stu-id="a8c10-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="a8c10-124">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a8c10-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a8c10-125">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="a8c10-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

