---
title: "dados de tooconfigure aaaHow saídas para trabalhos do Stream Analytics | Microsoft Docs"
description: "Configurar saídas para trabalhos do Stream Analytics | segmento do roteiro de aprendizagem."
keywords: "dados de saída, movimentação de dados"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Como os dados tooconfigure saídas para trabalhos do Stream Analytics

Trabalhos do Stream Analytics do Azure podem ser conectado tooone ou mais saídas de dados, que definem um coletor de dados existente de conexão tooan. Como o trabalho do Stream Analytics processa e transforma os dados de entrada, um fluxo de dados de eventos de saída é gravado saída tooyour do trabalho.

Saídas de fluxo de dados de análise podem ser painéis em tempo real usado toosource ou alertas, gatilho fluxos de trabalho de movimentação de dados ou simplesmente arquivar dados para processamento em lote posteriormente. O Stream Analytics integra-se perfeitamente a vários serviços do Azure, que são documentados em detalhes aqui.

tooadd um trabalho de análise de fluxo de tooyour de saída:

1. Em Olá [portal do Azure](https://portal.azure.com), abra seu trabalho e clique em **saídas** e, em seguida, clique em **adicionar** na folha de saídas de saudação que aparece.
   
    ![Adicionar saídas](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Forneça um nome amigável para essa saída no hello **Alias de saída** caixa. Esse nome pode ser usado na consulta do trabalho posteriormente na saída de toohello toorefer.  
   
    Preencha o restante Olá Olá necessário conexão propriedades tooconnect tooyour saída.  Esses campos variam de acordo com o tipo de saída e são definidos em detalhes aqui.  
   
    ![Escolher o tipo de movimentação de dados](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. Dependendo do tipo de saída de hello, talvez seja necessário toospecify como dados de saudação são serializados ou formatados. configurações de serialização específico Olá para cada tipo de saída são documentadas aqui.
   
    Preencha o restante de Olá Olá necessária conexão propriedades tooconnect tooyour da fonte de dados. Esses campos variam de acordo com o tipo de entrada e origem e são definidos em detalhes em Olá [artigo criar trabalho](stream-analytics-create-a-job.md).  

> [!Note]
>
> Qualquer trabalho de toohello adicionado do elemento de saída, deve existir antes Olá trabalho é iniciado e eventos que fluem de início. Por exemplo, se você usar o armazenamento de Blob como uma saída, o trabalho de saudação não criará uma conta de armazenamento automaticamente. Ele precisa toobe criado pelo usuário Olá antes Olá ASA trabalho é iniciado.
> 
 

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

