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
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="753a1-104">Como toocreate um processamento de análise de dados de trabalho para análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="753a1-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="753a1-105">o recurso de nível superior Olá no Azure Stream Analytics é um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="753a1-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="753a1-106">Ele consiste em uma ou mais fontes de dados, uma consulta de expressar a transformação de dados hello e um ou mais destinos de saída que os resultados são gravados de entrada.</span><span class="sxs-lookup"><span data-stu-id="753a1-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="753a1-107">Juntos, eles permitem análises de dados Olá usuário tooperform cenários de processamento de fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="753a1-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="753a1-108">toostart usando a análise de fluxo, comece criando um novo trabalho de análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="753a1-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="753a1-109">Observe que esta ação não tem implicações nenhuma cobrança até o início do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="753a1-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="753a1-110">Entrar em Olá online [portal clássico do Azure](http://manage.windowsazure.com) ou hello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="753a1-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="753a1-111">No portal de saudação: **clique em novo**, em seguida, clique em **Data Services** ou **análises de dados** dependendo do portal e clique **Azure Stream Analytics** ou **Stream Analytics** e **criação rápida**.</span><span class="sxs-lookup"><span data-stu-id="753a1-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Assistente de trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Criar trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="753a1-114">Especifique a configuração desejada Olá para o trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="753a1-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="753a1-115">Em Olá **nome do trabalho** , digite um nome do trabalho do Stream Analytics tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="753a1-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="753a1-116">Olá quando **nome do trabalho** for validado, uma marca de seleção verde é exibida na caixa de nome do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="753a1-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="753a1-117">Olá **nome do trabalho** pode conter apenas caracteres alfanuméricos e hello '-' caracteres e deve ser entre 3 e 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="753a1-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="753a1-118">Use **região** no portal do Azure de saudação ou **local** no hello Azure portal toospecify Olá localização geográfica onde você deseja que o trabalho de saudação toorun.</span><span class="sxs-lookup"><span data-stu-id="753a1-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="753a1-119">Se usar hello portal do Azure, selecione ou crie um toouse de conta de armazenamento como Olá **conta de armazenamento de monitoramento Regional**.</span><span class="sxs-lookup"><span data-stu-id="753a1-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="753a1-120">Essa conta de armazenamento é usado toostore dados de monitoramento de todos os trabalhos do Stream Analytics em execução nesta região.</span><span class="sxs-lookup"><span data-stu-id="753a1-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="753a1-121">Se usar hello portal do Azure, especifique um novo ou existente **grupo de recursos** toohold relacionadas a recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="753a1-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="753a1-122">Quando novas opções de trabalho do Stream Analytics Olá são configuradas, clique em **criar o trabalho do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="753a1-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="753a1-123">Pode levar alguns minutos para toobe de trabalho do Stream Analytics Olá criado.</span><span class="sxs-lookup"><span data-stu-id="753a1-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="753a1-124">status de saudação toocheck, você pode monitorar o progresso de saudação no hub de notificações de saudação.</span><span class="sxs-lookup"><span data-stu-id="753a1-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Hub de notificações de trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Análise de dados do portal do Azure processando o trabalho Criar Trabalho](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="753a1-127">novo trabalho de saudação mostrará um status de **criado**.</span><span class="sxs-lookup"><span data-stu-id="753a1-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="753a1-128">Observe que Olá **iniciar** botão será desabilitado.</span><span class="sxs-lookup"><span data-stu-id="753a1-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="753a1-129">Configure entrada de trabalho hello, consulta e saída antes de iniciar o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="753a1-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Status do trabalho de processamento de análise de dados](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Status do trabalho de processamento de análise de dados no portal do Azure](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="753a1-132">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="753a1-132">Get help</span></span>
<span data-ttu-id="753a1-133">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="753a1-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="753a1-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="753a1-134">Next steps</span></span>
* [<span data-ttu-id="753a1-135">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="753a1-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="753a1-136">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="753a1-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="753a1-137">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="753a1-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="753a1-138">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="753a1-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="753a1-139">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="753a1-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

