---
title: "Depurar usando logs de operação e serviço no Stream Analytics | Microsoft Docs"
description: "Como usar logs de operação do Stream Analytics"
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
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="62174-104">Depurar os trabalhos do Stream Analytics usando logs de serviço e operação</span><span class="sxs-lookup"><span data-stu-id="62174-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="62174-105">Todos os serviços do Azure fornecem mensagens em log operacionais aos usuários para registrar detalhes relacionados às operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="62174-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="62174-106">No Stream Analytics, essas informações podem ser usadas para fins de depuração, como exibir o status do trabalho, o progresso do trabalho e as mensagens de falha para rastrear o andamento de um trabalho ao longo do tempo, do início do processamento até a saída.</span><span class="sxs-lookup"><span data-stu-id="62174-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="62174-107">Encontrar logs de operação no Portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="62174-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="62174-108">Os Logs de Operação podem ser acessados de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="62174-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="62174-109">Painel do trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="62174-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="62174-110">Serviços de Gerenciamento no Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="62174-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="62174-111">Painel do trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="62174-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="62174-112">Um link para os logs correspondentes de um trabalho do Stream Analytics é exibido na guia Painel do trabalho. Se você clicar nesse link, ele definirá os filtros para mostrar os últimos logs desse trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="62174-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![Selecionar logs dos Serviços de Gerenciamento](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="62174-114">Serviços de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="62174-114">Management Services</span></span>
<span data-ttu-id="62174-115">Para navegar manualmente até os Logs de Operação do Stream Analytics e outros serviços no Portal Clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="62174-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="62174-116">Clique em **Serviços de Gerenciamento** no [Portal Clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="62174-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="62174-117">Selecione **Stream Analytics** para **Tipo** e o nome do trabalho para **Nome do Serviço**.</span><span class="sxs-lookup"><span data-stu-id="62174-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Selecionar Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="62174-119">Encontrar logs de auditoria no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="62174-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="62174-120">Para encontrar logs operacionais de seu trabalho do Stream Analytics no Portal do Azure, clique em **Procurar** e selecione **Logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="62174-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Selecionar Stream Analytics no Portal do Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="62174-122">Isso abrirá uma folha que mostra os eventos dos últimos sete dias para todos os recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="62174-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="62174-123">É possível filtrar para ver os eventos de um tipo ou período especificado clicando no comando **Filtro** .</span><span class="sxs-lookup"><span data-stu-id="62174-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Selecionar Stream Analytics no Portal do Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="62174-125">Obter detalhes de log</span><span class="sxs-lookup"><span data-stu-id="62174-125">Get log details</span></span>
<span data-ttu-id="62174-126">Você pode filtrar por Intervalo de Tempo e Status para exibir os logs do seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="62174-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="62174-127">No portal de Gerenciamento do Azure, clique no botão **Detalhes** na parte inferior da janela para exibir mais detalhes sobre um evento selecionado.</span><span class="sxs-lookup"><span data-stu-id="62174-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![Selecionar Detalhes](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="62174-129">No Portal do Azure, clique em uma entrada de log para ver os eventos detalhados dentro dela.</span><span class="sxs-lookup"><span data-stu-id="62174-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Selecionar Detalhes no Portal do Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="62174-131">A partir daí, você pode abrir a folha **Detalhes** clicando no evento.</span><span class="sxs-lookup"><span data-stu-id="62174-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Selecionar Detalhes no Portal do Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="62174-133">Depurar um trabalho com falha</span><span class="sxs-lookup"><span data-stu-id="62174-133">Debug a failed job</span></span>
<span data-ttu-id="62174-134">No portal de Gerenciamento do Azure, clique no ícone Pesquisa e digite “com falha”.</span><span class="sxs-lookup"><span data-stu-id="62174-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="62174-135">Isso fornece um resultado de todos os logs com falhas.</span><span class="sxs-lookup"><span data-stu-id="62174-135">This gives a result of all logs with failures.</span></span> 

  ![Depurando um trabalho com falha](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="62174-137">No portal do Azure, é possível filtrar por nível de mensagem para exibir eventos **Críticos** .</span><span class="sxs-lookup"><span data-stu-id="62174-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Depurar o Portal do Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="62174-139">É possível selecionar qualquer uma das falhas e clicar nos **Detalhes** para obter mais informações sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="62174-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="62174-140">Algumas mensagens de erro também fornecem informações sobre como a minimizar o problema.</span><span class="sxs-lookup"><span data-stu-id="62174-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![Detalhes da Operação](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="62174-142">Caso precise entrar em contato com o [Suporte](https://azure.microsoft.com/support/options/) ou fornecer informações à equipe pelo [fórum do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), anote os Detalhes da Operação, especificamente a **ID de Correlação**.</span><span class="sxs-lookup"><span data-stu-id="62174-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="62174-143">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="62174-143">Get help</span></span>
<span data-ttu-id="62174-144">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="62174-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="62174-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="62174-145">Next steps</span></span>
* [<span data-ttu-id="62174-146">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="62174-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="62174-147">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="62174-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="62174-148">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="62174-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="62174-149">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="62174-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="62174-150">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="62174-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

