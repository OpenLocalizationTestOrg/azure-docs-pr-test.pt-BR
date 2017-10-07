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
# <a name="create-contentkeys-with-net"></a>Criar ContentKeys com .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Serviços de mídia permitem toocreate e entregar ativos criptografados. Um **ContentKey** fornece acesso seguro tooyour **ativo**s. 

Quando você cria um novo ativo (por exemplo, antes de você [carregar arquivos](media-services-dotnet-upload-files.md)), você pode especificar Olá as opções de criptografia a seguir: **StorageEncrypted**, **CommonEncryptionProtected**, ou **EnvelopeEncryptionProtected**. 

Quando você entregar ativos tooyour clientes, você pode [configurar para toobe ativos criptografado dinamicamente](media-services-dotnet-configure-asset-delivery-policy.md) com uma saudação dois criptografias a seguir: **DynamicEnvelopeEncryption** ou  **DynamicCommonEncryption**.

Ativos criptografados têm toobe associado **ContentKey**s. Este artigo descreve como toocreate uma chave de conteúdo.

> [!NOTE]
> Ao criar um novo **StorageEncrypted** ativo usando Olá SDK do Media Services .NET hello **ContentKey** é automaticamente criado e vinculado com ativo hello.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
Um dos valores de saudação que você deve definir quando criar um conteúdo de chave é o tipo de chave de conteúdo de saudação. Escolha uma saudação valores a seguir. 

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

## <a id="envelope_contentkey"></a>Criar um tipo de envelope de ContentKey
Olá trecho de código a seguir cria uma chave de conteúdo do tipo de criptografia de envelope hello. Em seguida, associa chave Olá com ativo especificado hello.

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

chamada

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>Criar um tipo comum de ContentKey
Hello trecho de código a seguir cria uma chave de conteúdo Olá comuns do tipo de criptografia. Em seguida, associa chave Olá com ativo especificado hello.

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
chamada

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

