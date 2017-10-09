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
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="0c767-104">Depurar os trabalhos do Stream Analytics usando logs de serviço e operação</span><span class="sxs-lookup"><span data-stu-id="0c767-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="0c767-105">Todos os detalhes do log operacional de fornecimento de serviços do Azure mensagens toousers toorecord relacionadas a operações de toomanagement.</span><span class="sxs-lookup"><span data-stu-id="0c767-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="0c767-106">No Azure Stream Analytics, essas informações podem ser usadas para fins como exibir o status do trabalho, o andamento do trabalho e o andamento de Olá de tootrack de mensagens de falha de um trabalho ao longo do tempo de início tooprocessing toooutput de depuração.</span><span class="sxs-lookup"><span data-stu-id="0c767-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="0c767-107">Localizar os logs da operação no portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="0c767-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="0c767-108">Os Logs de Operação podem ser acessados de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="0c767-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="0c767-109">Painel de trabalho do Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="0c767-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="0c767-110">Serviços de gerenciamento no portal clássico do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="0c767-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="0c767-111">Painel de trabalho do Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="0c767-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="0c767-112">Um toohello link correspondente logs de um trabalho de análise de fluxo é exibido na guia do painel de controle do trabalho hello. Se você clicar nesse link, ele definirá filtros de saudação de forma que ela mostra logs mais recentes para esse trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="0c767-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Selecionar logs dos Serviços de Gerenciamento](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="0c767-114">Serviços de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0c767-114">Management Services</span></span>
<span data-ttu-id="0c767-115">toomanually navegue toohello Logs de operação de análise de fluxo e outros serviços no portal clássico do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="0c767-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="0c767-116">Clique em **Management Services** em Olá [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0c767-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0c767-117">Selecione **do Stream Analytics** para **tipo** e o nome de saudação do trabalho Olá para **nome do serviço**.</span><span class="sxs-lookup"><span data-stu-id="0c767-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Selecionar Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="0c767-119">Localizar os logs de auditoria em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0c767-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="0c767-120">toofind a logs operacionais para o trabalho de análise de fluxo em Olá portal do Azure, clique em **procurar** e, em seguida, selecione **logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="0c767-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Selecionar Stream Analytics no Portal do Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="0c767-122">Isso abrirá uma folha mostrando eventos de saudação últimos 7 dias para todos os recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0c767-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="0c767-123">Você pode filtrar eventos toosee de um período de tempo ou o tipo de especificar clicando Olá **filtro** comando.</span><span class="sxs-lookup"><span data-stu-id="0c767-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Selecionar Stream Analytics no Portal do Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="0c767-125">Obter detalhes de log</span><span class="sxs-lookup"><span data-stu-id="0c767-125">Get log details</span></span>
<span data-ttu-id="0c767-126">Você pode filtrar por intervalo de tempo e logs de saudação do Status tooview para seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="0c767-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="0c767-127">No portal de gerenciamento do Azure hello, clique em Olá **detalhes** botão na parte inferior de saudação do hello janela tooview mais detalhes sobre um evento selecionado.</span><span class="sxs-lookup"><span data-stu-id="0c767-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Selecionar Detalhes](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="0c767-129">Em Olá portal do Azure, clique em um toosee de entrada de log Olá eventos detalhados dentro dele.</span><span class="sxs-lookup"><span data-stu-id="0c767-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Selecionar Detalhes no Portal do Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="0c767-131">A partir daí, você pode abrir Olá **detalhes** folha clicando-se no evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c767-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Selecionar Detalhes no Portal do Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="0c767-133">Depurar um trabalho com falha</span><span class="sxs-lookup"><span data-stu-id="0c767-133">Debug a failed job</span></span>
<span data-ttu-id="0c767-134">No portal de gerenciamento do Azure hello, clique no ícone de pesquisa hello e digite 'com falha'.</span><span class="sxs-lookup"><span data-stu-id="0c767-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="0c767-135">Isso fornece um resultado de todos os logs com falhas.</span><span class="sxs-lookup"><span data-stu-id="0c767-135">This gives a result of all logs with failures.</span></span> 

  ![Depurando um trabalho com falha](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="0c767-137">Olá portal do Azure, você pode filtrar por nível de mensagem tooview **crítico** eventos.</span><span class="sxs-lookup"><span data-stu-id="0c767-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Depurar o Portal do Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="0c767-139">Você pode selecionar qualquer uma das falhas de saudação e clicar em Olá **detalhes** para obter mais informações sobre o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c767-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="0c767-140">Algumas mensagens de erro também fornecem informações sobre como toomitigate Olá problema.</span><span class="sxs-lookup"><span data-stu-id="0c767-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Detalhes da Operação](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="0c767-142">Caso você precise toocontact [suporte](https://azure.microsoft.com/support/options/) ou fornecer equipe toohello de informações por meio de saudação [Fórum do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), especificamente Observação Olá detalhes da operação, Olá **ID de correlação**.</span><span class="sxs-lookup"><span data-stu-id="0c767-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="0c767-143">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="0c767-143">Get help</span></span>
<span data-ttu-id="0c767-144">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="0c767-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c767-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c767-145">Next steps</span></span>
* [<span data-ttu-id="0c767-146">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0c767-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0c767-147">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="0c767-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0c767-148">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="0c767-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0c767-149">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="0c767-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0c767-150">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0c767-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

