---
title: consultas de toowrite aaaHow no Stream Analytics | Microsoft Docs
description: Escrever consultas no Stream Analytics e consultar dados | segmento do roteiro de aprendizagem.
keywords: como toowrite consultas, dados de consulta, escrever uma consulta, escrever consultas
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Como as consultas toowrite no Stream Analytics
Escrever consultas para o fluxo de processamento da lógica no Azure Stream Analytics é implementado como uma "consulta permanente" está definida antes de um trabalho é iniciado e executado nos dados que ele atinge o trabalho hello. transformação de dados Olá é expresso em uma linguagem de consulta do tipo SQL, que é basicamente um subconjunto de T-SQL com alguns adicionadas extensões de linguagem como [janelas](https://msdn.microsoft.com/library/azure/dn835019.aspx) usado semântica temporal tooexpress.

## <a name="writing-queries"></a>Escrevendo consultas:
1. No seu trabalho do Stream Analytics no portal de gerenciamento do Azure hello, clique em **consulta**.
   
    ![Selecionar Consulta](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    No Portal do Azure do hello, clique em **consulta**.
   
    ![Selecionar Visualização da Consulta](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Novos trabalhos tem uma toohelp de modelo de consulta começar. consulta Olá modelo executa "passagem" a consulta que projetos de todos os campos de eventos de entrada em saída hello.  
   
   * Se você tiver definido a pelo menos uma entrada e saída do seu trabalho, você pode substituir o espaço reservado de hello "[YourOutputAlias]" e "[YourInputAlias]" campos com aliases de saudação de saudação de entrada e saída que você deseja usar primeiro. Além disso, você ainda pode criar e teste sua consulta Olá Portal clássico do Azure sem definir entradas e saídas no trabalho de saudação.
   * Se você quiser tooperform mais processamento de passagem simple, você pode editar a definição de consulta de saudação. tooget iniciar a criação de consultas, dar uma olhada em alguns padrões são capturados de consulta comum [aqui](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Janela de Consulta de dados](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>dados de consulta toovalidate está funcionando:
Você pode testar sua consulta se comporta como esperado executando-o no navegador de saudação em um ou mais arquivos locais JSON que contém dados de teste. Isso não iniciar o trabalho de saudação ou ter nenhuma implicação de cobrança.

> [!NOTE]
> Teste de consulta no navegador não é suportada atualmente no hello Portal do Azure.  
> 
> 

1. Certifique-se de que não há nenhum erro na consulta de saudação (caso contrário, Olá teste botão será desabilitado) e, em seguida, clique o botão de teste de saudação.  
   
   ![Teste de Consultar de dados](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. Será solicitada toospecify arquivos para cada uma das entradas de saudação referenciadas na consulta de saudação. Neste exemplo, a consulta de modelo Olá será deixada como-é, portanto, caixa de diálogo hello está solicitando uma entrada denominada "yourinputalias".  
   
   ![Testar Consulta de dados](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Procure arquivo de teste de tooa. Vários arquivos de exemplo estão disponíveis em [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) e você também pode recuperar dados de exemplo de suas próprias entradas de fluxo de dados por meio de saudação função dados de exemplo na guia de entradas de saudação.  
   
   ![Entrada de Consulta](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Depois de fechar a caixa de diálogo de Olá, sua consulta será executada em dados de teste hello e você verá resultados Olá final Olá Olá consulta página.  
   
   ![Resumo da Consulta](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

