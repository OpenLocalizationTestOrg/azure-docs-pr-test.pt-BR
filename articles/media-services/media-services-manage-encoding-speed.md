---
title: "velocidade de gerenciar AAA e a simultaneidade de sua codificação com os serviços de mídia do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral de como você pode gerenciar a velocidade e a simultaneidade de seus trabalhos/tarefas de codificação com os Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Gerenciar a velocidade e a simultaneidade de sua codificação

Este artigo fornece uma visão geral de como você pode gerenciar a velocidade e a simultaneidade de seus trabalhos/tarefas de codificação.

## <a name="overview"></a>Visão geral

Nos serviços de mídia, um **o tipo de unidade reservada** determina a velocidade de saudação com a qual a mídia de processamento de tarefas é processada. Você pode escolher entre os seguintes Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**. Por exemplo, Olá mesmo trabalho de codificação é executada mais rapidamente ao usar o hello **S2** tipo de unidade reservada comparar toohello **S1** tipo. Olá [dimensionamento unidades de codificação](media-services-scale-media-processing-overview.md) tópico mostra uma tabela que ajuda a tomar decisões ao escolher entre diferentes velocidades de codificação.

Além disso, toospecifying Olá reservado tipo de unidade, você pode especificar tooprovision sua conta com **unidades reservadas**. número de saudação de unidades reservadas provisionadas determina o número de saudação de tarefas de mídia que podem ser processadas simultaneamente em uma determinada conta. Por exemplo, se sua conta tiver cinco unidades reservadas, tarefas de cinco mídia serão executados simultaneamente desde pois há tarefas toobe processado. as tarefas restantes Olá aguardarão na fila hello e serão escolhidas para processamento sequencialmente quando uma tarefa em execução for concluída. Se uma conta não tiver nenhuma unidade reservada provisionada, as tarefas serão selecionadas sequencialmente. Nesse caso, Olá aguardar o tempo entre a conclusão de uma tarefa e hello seguir dependerá disponibilidade Olá dos recursos no sistema de saudação.

Para obter informações detalhadas e exemplos que mostram como unidades de codificação tooscale, consulte [isso](media-services-scale-media-processing-overview.md) tópico.

## <a name="next-step"></a>Próxima etapa

[Dimensionamento de unidades de codificação](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

