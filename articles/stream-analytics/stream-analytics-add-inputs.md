---
title: "aaaAdd um dados tooyour trabalhos de análise de fluxo de entrada | Microsoft Docs"
description: "Saiba como toohook a uma fonte de dados tooyour análise de fluxo de trabalho como fluxo de entrada de dados de Hubs de eventos ou referência de dados de armazenamento de blob."
keywords: dados de entrada, streaming de dados
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Adicionar um fluxo dados de entrada ou referência dados tooa trabalho do Stream Analytics
Saiba como toohook a uma fonte de dados tooyour análise de fluxo de trabalho como fluxo de entrada de dados de Hubs de eventos ou referência de dados do armazenamento de Blob.

Trabalhos do Stream Analytics do Azure podem ser conectado tooone entrada de dados ou mais, cada um dos quais definir uma fonte de dados conexão tooan existente. Como os dados são enviados a fonte de dados toothat, é consumido pelo trabalho de análise de fluxo de saudação e processado em tempo real, como fluxo de dados. Análise de fluxo tem integração de primeira classe com [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) e [armazenamento de BLOBs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) dentro e fora de assinatura do trabalho hello.

Este artigo é uma etapa Olá [caminho de aprendizagem do Stream Analytics](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Entrada de dados: dados de transmissão e dados de referência
Há dois tipos de entradas diferentes no Stream Analytics: fluxos de dados e dados de referência.

* **Fluxos de dados**: trabalhos do Stream Analytics devem incluir pelo menos um dados fluxo entrada toobe consumidos e transformados por trabalho hello. O Armazenamento de Blob do Azure e os Hubs de Eventos do Azure têm suporte como fontes de entrada de fluxo de dados. Hubs de eventos do Azure são fluxos de eventos usado toocollect dos dispositivos conectados, serviços e aplicativos. O armazenamento Blob do Azure pode ser usado como uma fonte de entrada para ingerir dados em massa como um fluxo.  
* **Dados de referência**: o Stream Analytics oferece suporte a um segundo tipo de entrada auxiliar chamado de dados de referência.  Como toodata contrário em movimento, esses dados são estáticos ou lenta de alteração.  Ela é normalmente usada para realizar pesquisas e correlações com fluxos de dados toocreate um valioso conjunto de dados.  Armazenamento de BLOBs do Azure está atualmente a fonte de entrada hello só tem suportada para dados de referência.  

tooadd um trabalho de análise de fluxo de entrada tooyour:

1. No portal do Azure de saudação clique **entradas** e, em seguida, clique em **adicionar uma entrada** no trabalho do Stream Analytics.
   
    ![Portal clássico do Azure - adicionar uma entrada.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    No hello Azure portal clique Olá **entradas** lado a lado em seu trabalho do Stream Analytics.  
   
    ![Portal do Azure - adicionar entrada de dados.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Especificar o tipo de saudação de entrada hello: qualquer **fluxo de dados** ou **dados de referência**.
   
    ![Adicionar dados corretos Olá de entrada, streaming ou referência](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Adicionar dados corretos Olá de entrada, streaming ou referência](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. Se criar uma entrada de fluxo de dados, especifique o tipo de fonte de Olá Olá entrada.  Essa etapa pode ser ignorada durante a criação dos Dados de Referência, pois atualmente há suporte apenas para o armazenamento de Blob.
   
    ![Adicionar a entrada de dados do streaming de dados](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Adicionar a entrada de dados do streaming de dados](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Forneça um nome amigável para esta entrada no hello caixa Alias de entrada.  Esse nome será usado na consulta do trabalho posteriormente na entrada de toohello toorefer.
   
    Preencha o restante de Olá Olá necessária conexão propriedades tooconnect tooyour da fonte de dados. Esses campos variam de acordo com o tipo de entrada e de fonte e são definidos detalhadamente [aqui](stream-analytics-create-a-job.md).  
   
    ![Adicionar entrada de dados do hub de eventos](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Especifique configurações de serialização Olá Olá para dados de entrada:
   
   * toomake que suas consultas funcionem de maneira Olá esperada, especifique Olá **formato de serialização de evento** de dados de entrada.  Os formatos de serialização com suporte são JSON, CSV e Avro.
   * Verifique se Olá **codificação** para dados de saudação.  UTF-8 é Olá somente suporte para formato de codificação no momento.
     
     ![Configurações de serialização de dados para dados de entrada hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Configurações de serialização de dados para dados de entrada hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. Depois de concluir a criação de entrada hello, análise de fluxo vai verificar que ele possa se conectar a fonte de entrada toohello.  Você pode exibir o status de saudação do hello operação de Conexão de teste no hub de notificação de saudação.
   
    ![Testar a conexão de saudação de fluxo de dados de entrada](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Testar a conexão de saudação de fluxo de dados de entrada](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Obter ajuda com a transmissão de entradas de dados
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

