---
title: "Carregar arquivos para uma conta dos Serviços de Mídia no portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de carregamento de arquivos para uma conta do Serviços de Mídia do Azure no portal do Azure"
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
ms.openlocfilehash: 7ddfe44918b358a1749640d1c93dba490855cc5a
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2017
---
# <a name="upload-files-to-a-media-services-account-in-the-azure-portal"></a>Carregar arquivos para uma conta dos Serviços de Mídia no portal do Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> Para concluir este tutorial, você precisa de uma conta do Azure. Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 

Nos Serviços de Mídia do Azure, você pode carregar seus arquivos digitais para um ativo. O ativo pode conter vídeo, áudio, imagens, coleções de miniaturas, sequências de texto e arquivos de legendas (e os metadados desses arquivos). Depois que os arquivos são carregados, o conteúdo é armazenado com segurança na nuvem para processamento adicional e transmissão.

> [!NOTE]
> Os Serviços de Mídia têm um tamanho máximo de arquivo para processamento. Para obter detalhes sobre os limites de tamanho de arquivo, confira [Cotas e limitações dos Serviços de Mídia](media-services-quotas-and-limitations.md).
>

## <a name="upload-files"></a>Carregar arquivos
1. No [Portal do Azure](https://portal.azure.com/), selecione sua conta dos Serviços de Mídia do Azure.
2. Selecione **Configurações** > **Ativos**. Em seguida, selecione o botão **Carregar**.
   
    ![Carregar arquivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
   
    A janela **Carregar um ativo de vídeo** é exibida.
   
   > [!NOTE]
   > Os Serviços de Mídia não limitam o tamanho do arquivo no carregamento de vídeos.
 
3. Em seu computador, vá para o vídeo que você deseja carregar. Selecione o vídeo e selecione **OK**.  
   
    O carregamento é iniciado. Você pode ver o progresso abaixo do nome do arquivo.  

Quando o carregamento é concluído, o novo ativo fica listado no painel **Ativos**. 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Próximas etapas
* Saiba como [codificar seus ativos carregados](media-services-portal-encode.md).

* Você também pode usar as Azure Functions para acionar um trabalho de codificação quando arquivo chega no contêiner configurado. Para saber mais, confira o exemplo em [Serviços de Mídia: integração dos Serviços de Mídia do Azure com o Azure Functions e os Aplicativos Lógicos](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/).


