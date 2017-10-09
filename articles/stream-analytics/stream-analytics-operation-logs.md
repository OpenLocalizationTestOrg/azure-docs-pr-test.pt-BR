---
title: "Usando logs de operação e o serviço na análise do fluxo de aaaDebug | Microsoft Docs"
description: "Fluxo de toouse como logs de operação de análise"
keywords: "logs de serviço"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Depurar os trabalhos do Stream Analytics usando logs de serviço e operação
Todos os detalhes do log operacional de fornecimento de serviços do Azure mensagens toousers toorecord relacionadas a operações de toomanagement. No Azure Stream Analytics, essas informações podem ser usadas para fins como exibir o status do trabalho, o andamento do trabalho e o andamento de Olá de tootrack de mensagens de falha de um trabalho ao longo do tempo de início tooprocessing toooutput de depuração.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Localizar os logs da operação no portal de gerenciamento do Azure Olá
Os Logs de Operação podem ser acessados de duas maneiras:  

* Painel de trabalho do Stream Analytics Olá  
* Serviços de gerenciamento no portal clássico do Azure Olá  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Painel de trabalho do Stream Analytics Olá
Um toohello link correspondente logs de um trabalho de análise de fluxo é exibido na guia do painel de controle do trabalho hello. Se você clicar nesse link, ele definirá filtros de saudação de forma que ela mostra logs mais recentes para esse trabalho específico.

  ![Selecionar logs dos Serviços de Gerenciamento](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Serviços de Gerenciamento
toomanually navegue toohello Logs de operação de análise de fluxo e outros serviços no portal clássico do Azure hello:

1. Clique em **Management Services** em Olá [portal clássico do Azure](https://manage.windowsazure.com).
2. Selecione **do Stream Analytics** para **tipo** e o nome de saudação do trabalho Olá para **nome do serviço**.  
   
   ![Selecionar Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Localizar os logs de auditoria em Olá portal do Azure
toofind a logs operacionais para o trabalho de análise de fluxo em Olá portal do Azure, clique em **procurar** e, em seguida, selecione **logs de auditoria**.

  ![Selecionar Stream Analytics no Portal do Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Isso abrirá uma folha mostrando eventos de saudação últimos 7 dias para todos os recursos em sua assinatura.  Você pode filtrar eventos toosee de um período de tempo ou o tipo de especificar clicando Olá **filtro** comando.

  ![Selecionar Stream Analytics no Portal do Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Obter detalhes de log
Você pode filtrar por intervalo de tempo e logs de saudação do Status tooview para seu trabalho.

No portal de gerenciamento do Azure hello, clique em Olá **detalhes** botão na parte inferior de saudação do hello janela tooview mais detalhes sobre um evento selecionado. 

  ![Selecionar Detalhes](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

Em Olá portal do Azure, clique em um toosee de entrada de log Olá eventos detalhados dentro dele.

  ![Selecionar Detalhes no Portal do Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

A partir daí, você pode abrir Olá **detalhes** folha clicando-se no evento de saudação.

  ![Selecionar Detalhes no Portal do Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Depurar um trabalho com falha
No portal de gerenciamento do Azure hello, clique no ícone de pesquisa hello e digite 'com falha'. Isso fornece um resultado de todos os logs com falhas. 

  ![Depurando um trabalho com falha](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

Olá portal do Azure, você pode filtrar por nível de mensagem tooview **crítico** eventos.

  ![Depurar o Portal do Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Você pode selecionar qualquer uma das falhas de saudação e clicar em Olá **detalhes** para obter mais informações sobre o erro de saudação.  Algumas mensagens de erro também fornecem informações sobre como toomitigate Olá problema. 

  ![Detalhes da Operação](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

Caso você precise toocontact [suporte](https://azure.microsoft.com/support/options/) ou fornecer equipe toohello de informações por meio de saudação [Fórum do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), especificamente Observação Olá detalhes da operação, Olá **ID de correlação**. 

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

