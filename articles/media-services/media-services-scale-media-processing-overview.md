---
title: "Visão geral de processamento de mídia aaaScaling | Microsoft Docs"
description: "Este tópico é uma visão geral do dimensionamento de processamento de mídia com os Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Visão geral do dimensionamento do processamento de mídia
Esta página fornece uma visão geral de como e por que o processamento de mídia tooscale. 

## <a name="overview"></a>Visão geral
Uma conta de serviços de mídia está associada um tipo de unidade reservada, que determina a velocidade de saudação com a qual a mídia de processamento de tarefas é processada. Você pode escolher entre os seguintes Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**. Por exemplo, Olá mesmo trabalho de codificação é executada mais rapidamente ao usar o hello **S2** tipo de unidade reservada comparar toohello **S1** tipo. Para obter mais informações, consulte Olá [tipos de unidades reservadas](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Além disso, toospecifying Olá reservado tipo de unidade, você pode especificar tooprovision sua conta com unidades reservadas. número de saudação de unidades reservadas provisionadas determina o número de saudação de tarefas de mídia que podem ser processadas simultaneamente em uma determinada conta. Por exemplo, se sua conta tiver cinco unidades reservadas, tarefas de cinco mídia serão executados simultaneamente desde pois há tarefas toobe processado. as tarefas restantes Olá aguardarão na fila hello e serão escolhidas para processamento sequencialmente quando uma tarefa em execução for concluída. Se uma conta não tiver nenhuma unidade reservada provisionada, as tarefas serão selecionadas sequencialmente. Nesse caso, Olá aguardar o tempo entre a conclusão de uma tarefa e hello seguir dependerá disponibilidade Olá dos recursos no sistema de saudação.

## <a name="choosing-between-different-reserved-unit-types"></a>Escolha entre tipos diferentes de unidade reservada
Olá, a tabela a seguir o ajudará a tomar a decisão ao escolher entre diferentes velocidades de codificação. Ele também fornece alguns casos de parâmetro de comparação e fornece URLs da SAS que você pode usar vídeos toodownload na qual você pode executar seus próprios testes:

| Cenários | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Exemplo de uso indicado |Codificação de taxa de bits única. <br/>Arquivos com resoluções SD ou inferiores, não sensível ao tempo, de baixo custo. |Codificação de taxa de bits única e de taxa de bits múltipla.<br/>Uso normal para codificação SD e HD. |Codificação de taxa de bits única e de taxa de bits múltipla.<br/>Vídeos com resolução Full HD e 4K. Codificação urgente com retorno mais rápido. |
| Parâmetro de comparação |[Arquivo de entrada: 5 minutos de duração, 640x360p a 29,97 quadros/segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Codificação de arquivo MP4 de taxa de bits única de tooa, a saudação mesmo resolução, leva cerca de 11 minutos. |[Arquivo de entrada: 5 minutos de duração, 1280x720p a 29,97 quadros/segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/>A codificação com a predefinição "H264 Taxa de Bits Única 720p" leva cerca de 5 minutos.<br/><br/>A codificação com a predefinição "H264 Taxa de Bits Múltipla 720p" levará cerca de 11,5 minutos. |[Arquivo de entrada: 5 minutos de duração, 1920x1080p a 29,97 quadros/segundo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>A codificação com a predefinição "H264 Taxa de Bits Única 1080p" leva cerca de 2,7 minutos.<br/><br/>A codificação com a predefinição "H264 Taxas de Bits Múltiplas 1080p" leva aproximadamente 5,7 minutos. |

## <a name="considerations"></a>Considerações
> [!IMPORTANT]
> Examine as considerações descritas nesta seção.  
> 
> 

* As Unidades Reservadas trabalham para paralelizar todo o processamento de mídia, incluindo trabalhos de indexação usando o Indexador de Mídia do Azure.  No entanto, ao contrário da codificação, a indexação de trabalhos não será processada mais rapidamente com unidades reservadas mais rápidas.
* Se usando Olá compartilhado pool, ou seja, sem nenhuma unidades reservadas e suas tarefas de codificação têm Olá desempenho mesmo assim como acontece com RUs S1. No entanto, há nenhum tempo de toohello limite superior suas tarefas podem gastar no estado em fila, e a qualquer momento, no máximo uma tarefa será executado.
* Olá centros de dados a seguir não oferece Olá **S2** tipo de unidade reservada: Brasil Sul e Oeste da Índia.
* Olá seguintes do Centro de dados não oferecem Olá **S3** tipo de unidade reservada: Oeste da Índia.

## <a name="billing"></a>Cobrança

A cobrança é realizada com base no número real de minutos de uso das Unidades Reservadas de Mídia. Para obter uma explicação detalhada, consulte a seção de saudação perguntas Frequentes de saudação [de preços de serviços de mídia](https://azure.microsoft.com/pricing/details/media-services/) página.   

## <a name="quotas-and-limitations"></a>Cotas e limitações
Para obter informações sobre cotas e limitações e como tooopen um tíquete de suporte, consulte [cotas e limitações](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Próxima etapa
Obter Olá dimensionamento de processamento de tarefa com uma dessas tecnologias de mídia: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

