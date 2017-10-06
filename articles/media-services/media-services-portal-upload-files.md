---
title: "AAA\"carregar arquivos em uma conta de serviços de mídia usando Olá portal do Azure | Microsoft Docs\""
description: "Este tutorial orienta você pelas etapas de saudação de carregar arquivos em uma conta de serviços de mídia usando Olá portal do Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Carregar arquivos em uma conta de serviços de mídia usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 


Nos serviços de mídia, você pode carregar seus arquivos digitais em um ativo. Olá ativo pode conter vídeo, áudio, imagens, coleções de miniaturas, texto rastreia e legenda codificada arquivos (e Olá metadados sobre esses arquivos.) Depois que forem carregados arquivos hello, seu conteúdo é armazenado com segurança na nuvem de saudação para processamento adicional e streaming.


## <a name="upload-files"></a>Carregar arquivos

>[!NOTE]
>Há um limite toohello tamanho máximo com suporte para o processamento de serviços de mídia. Consulte [isso](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre a limitação de tamanho de arquivo hello.
>

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Em Olá **configurações** folha, clique em **ativos**.
   
    ![Carregar arquivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Clique em Olá **carregar** botão.
   
    Olá **carregar um ativo de vídeo** janela é exibida.
   
   > [!NOTE]
   > Não há nenhuma limitação de tamanho do arquivo.
   > 
   > 
4. Procurar vídeo toohello desejado no seu computador, selecioná-la e Okey de ocorrências.  
   
    Olá upload é iniciado e você pode ver o progresso de saudação em nome do arquivo hello.  

Após a conclusão do carregamento de Olá, você verá o novo ativo de saudação listado no hello **ativos** janela. 

## <a name="next-steps"></a>Próximas etapas
Agora você pode codificar seus ativos carregados. Para saber mais, veja [Codificar ativos](media-services-portal-encode.md).

Você também pode usar as funções do Azure tootrigger um trabalho de codificação com base em um arquivo que chegam no contêiner de saudação configurada. Para obter mais informações, confira [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

