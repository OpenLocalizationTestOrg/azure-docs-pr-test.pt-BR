---
title: "um trabalho de processamento de análise de dados para análise de fluxo de toocreate de aaaHow | Microsoft Docs"
description: "Criar um trabalho de processamento de análise de dados para o Stream Analytics | segmento de roteiro de aprendizagem."
keywords: "processamento de análise de dados"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>Como toocreate um processamento de análise de dados de trabalho para análise de fluxo
o recurso de nível superior Olá no Azure Stream Analytics é um trabalho do Stream Analytics.  Ele consiste em uma ou mais fontes de dados, uma consulta de expressar a transformação de dados hello e um ou mais destinos de saída que os resultados são gravados de entrada. Juntos, eles permitem análises de dados Olá usuário tooperform cenários de processamento de fluxo de dados.

toostart usando a análise de fluxo, comece criando um novo trabalho de análise de fluxo.  Observe que esta ação não tem implicações nenhuma cobrança até o início do trabalho de saudação.

1. Entrar em Olá online [portal clássico do Azure](http://manage.windowsazure.com) ou hello [portal do Azure](https://portal.azure.com/).
2. No portal de saudação: **clique em novo**, em seguida, clique em **Data Services** ou **análises de dados** dependendo do portal e clique **Azure Stream Analytics** ou **Stream Analytics** e **criação rápida**.
   
   ![Assistente de trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Criar trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Especifique a configuração desejada Olá para o trabalho de análise de fluxo de saudação.
   
   * Em Olá **nome do trabalho** , digite um nome do trabalho do Stream Analytics tooidentify hello. Olá quando **nome do trabalho** for validado, uma marca de seleção verde é exibida na caixa de nome do trabalho de saudação. Olá **nome do trabalho** pode conter apenas caracteres alfanuméricos e hello '-' caracteres e deve ser entre 3 e 63 caracteres.
   * Use **região** no portal do Azure de saudação ou **local** no hello Azure portal toospecify Olá localização geográfica onde você deseja que o trabalho de saudação toorun.
   * Se usar hello portal do Azure, selecione ou crie um toouse de conta de armazenamento como Olá **conta de armazenamento de monitoramento Regional**. Essa conta de armazenamento é usado toostore dados de monitoramento de todos os trabalhos do Stream Analytics em execução nesta região.
   * Se usar hello portal do Azure, especifique um novo ou existente **grupo de recursos** toohold relacionadas a recursos para seu aplicativo.
4. Quando novas opções de trabalho do Stream Analytics Olá são configuradas, clique em **criar o trabalho do Stream Analytics**. Pode levar alguns minutos para toobe de trabalho do Stream Analytics Olá criado. status de saudação toocheck, você pode monitorar o progresso de saudação no hub de notificações de saudação.
   
   ![Hub de notificações de trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Análise de dados do portal do Azure processando o trabalho Criar Trabalho](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. novo trabalho de saudação mostrará um status de **criado**. Observe que Olá **iniciar** botão será desabilitado. Configure entrada de trabalho hello, consulta e saída antes de iniciar o trabalho de saudação.
   
   ![Status do trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Status do trabalho de processamento de análise de dados no portal do Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

