---
title: "aaaEncode um ativo usando o codificador de mídia padrão com hello portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de codificar um ativo usando o codificador de mídia padrão com hello portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Codificar um ativo usando o codificador de mídia padrão com hello portal do Azure
> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Ao trabalhar com um dos cenários mais comuns de saudação está entregando uma taxa de bits adaptável streaming tooyour clientes de serviços de mídia do Azure. Serviços de mídia oferece suporte a saudação seguintes tecnologias de streaming de taxa de bits adaptável: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare vídeos para streaming de taxa de bits adaptável, você precisa tooencode sua fonte de vídeo em arquivos de várias taxas de bits. Você deve usar o hello **codificador de mídia padrão** tooencode codificador seus vídeos.  

Serviços de mídia também fornecem empacotamento dinâmico que permite que você toodeliver seus MP4s de múltiplas taxas de bits nos seguintes formatos de streaming de saudação: MPEG DASH, HLS, Smooth Streaming, sem a necessidade de toore-package nesses formatos de fluxo contínuo. Com o empacotamento dinâmico só é necessário toostore e pagamento para arquivos de saudação em único formato de armazenamento e os serviços de mídia criará e enviará a resposta apropriada hello, com base nas solicitações de um cliente.

tootake proveito do empacotamento dinâmico, você precisa de tooencode seu arquivo de origem em um conjunto de arquivos MP4 com múltiplas taxas de bits (etapas de codificação Olá são demonstradas posteriormente nesta seção).

mídia tooscale processamento, consulte [isso](media-services-portal-scale-media-processing.md) tópico.

## <a name="encode-with-hello-azure-portal"></a>Codificar com hello portal do Azure
Esta seção descreve Olá etapas tooencode seu conteúdo com o codificador de mídia padrão.

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Em Olá **configurações** janela, selecione **ativos**.  
3. Em Olá **ativos** janela, ativo Olá selecione que você gostaria que tooencode.
4. Olá pressione **Encode** botão.
5. Em Olá **codificar um ativo** janela, processador "Padrão de codificador de mídia" hello select e uma predefinição. Para saber mais sobre as predefinições, confira [Gerar automaticamente uma escada de taxa de bits](media-services-autogen-bitrate-ladder-with-mes.md) e [Predefinições de tarefa para MES](media-services-mes-presets-overview.md). Se você planejar toocontrol quais predefinição de codificação é usada, lembre-se disso: é importante tooselect Olá predefinição mais apropriado para o vídeo de entrada. Por exemplo, se você souber o vídeo de entrada com uma resolução de 1920 x 1080 pixels, você pode usar hello "H264 taxas de bits múltiplas 1080p" predefinido. Se você tiver um vídeo de baixa resolução (640 x 360), não deverá usar a predefinição "H264 Múltiplas Taxas de Bits 1080p".
   
   Para facilitar o gerenciamento, você tem uma opção da edição nome Olá Olá ativo de saída e o nome de saudação do trabalho de saudação.
   
   ![Codificar ativos](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Pressione **Criar**.

## <a name="next-step"></a>Próxima etapa
Você pode monitorar o andamento do trabalho codificação com hello portal do Azure, conforme descrito em [isso](media-services-portal-check-job-progress.md) artigo.  

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

