---
title: "mídia aaaScale processamento usando Olá portal do Azure | Microsoft Docs"
description: "Este tutorial orienta você pelas etapas de saudação de dimensionamento mídia processamento usando Olá portal do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Alterar tipo de unidade de saudação reservado
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Visão geral

Uma conta de serviços de mídia está associada um tipo de unidade reservada, que determina a velocidade de saudação com a qual a mídia de processamento de tarefas é processada. Você pode escolher entre os seguintes Olá reservado tipos de unidade: **S1**, **S2**, ou **S3**. Por exemplo, Olá mesmo trabalho de codificação é executada mais rapidamente ao usar o hello **S2** tipo de unidade reservada comparar toohello **S1** tipo.

Além disso, toospecifying Olá reservado tipo de unidade, você pode especificar tooprovision sua conta com **unidades reservadas** (RUs). número de saudação de RUs provisionados determina o número de saudação de tarefas de mídia que podem ser processadas simultaneamente em uma conta.

>[!NOTE]
>As URs trabalham para paralelizar todo o processamento de mídia, incluindo os trabalhos de indexação, usando o Azure Media Indexer. No entanto, ao contrário da codificação, a indexação de trabalhos não será processada mais rapidamente com unidades reservadas mais rápidas.

> [!IMPORTANT]
> Verifique se Olá de tooreview [visão geral](media-services-scale-media-processing-overview.md) tooget tópico para obter mais informações sobre como dimensionar um tópico de processamento de mídia.
> 
> 

## <a name="scale-media-processing"></a>Processamento de mídia de escala
toochange Olá reservado hello e tipo de número de unidade de unidades reservadas, Olá a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Em Olá **configurações** janela, selecione **unidades reservadas para mídia**.
   
    número de saudação do toochange de unidades reservadas para Olá selecionou o tipo de unidade reservada, use Olá **mídia servido unidades** controle deslizante.
   
    Olá toochange **o tipo de unidade RESERVADA**, pressione S1, S2 ou S3.
   
    ![Página processadores](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Olá Pressione Salvar botão toosave suas alterações.
   
    novas unidades reservadas de saudação são alocadas quando você pressiona Salvar.

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

