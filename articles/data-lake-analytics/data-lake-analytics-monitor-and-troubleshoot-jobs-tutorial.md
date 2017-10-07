---
title: "trabalhos de análise do Azure Data Lake aaaTroubleshoot usando o Portal do Azure | Microsoft Docs"
description: "Saiba como toouse Olá trabalhos de análise Data Lake tootroubleshoot Portal do Azure. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="b9eef-103">Solucionar problemas em trabalhos da Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9eef-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="b9eef-104">Saiba como toouse Olá trabalhos de análise Data Lake tootroubleshoot Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9eef-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="b9eef-105">Neste tutorial, você será um problema ausente do arquivo de origem de instalação e usar hello Azure Portal tootroubleshoot Olá problema.</span><span class="sxs-lookup"><span data-stu-id="b9eef-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="b9eef-106">Enviar um trabalho da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="b9eef-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="b9eef-107">Envie Olá trabalho U-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9eef-107">Submit hello following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="b9eef-108">Olá definido no script de saudação do arquivo de origem é **/Samples/Data/SearchLog.tsv1**, onde deve ser **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="b9eef-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="b9eef-109">Solucionar problemas de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="b9eef-109">Troubleshoot hello job</span></span>

<span data-ttu-id="b9eef-110">**toosee todos os trabalhos de Olá**</span><span class="sxs-lookup"><span data-stu-id="b9eef-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="b9eef-111">De Olá portal do Azure, clique em **Microsoft Azure** no canto superior esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="b9eef-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="b9eef-112">Clique em Olá lado a lado com o seu nome de conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="b9eef-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="b9eef-113">Resumo do trabalho de saudação é mostrado na Olá **Job Management** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="b9eef-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Gerenciamento de trabalhos da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="b9eef-115">Gerenciamento de trabalho de saudação fornece rapidamente Olá status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="b9eef-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="b9eef-116">Observe que há um trabalho com falha.</span><span class="sxs-lookup"><span data-stu-id="b9eef-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="b9eef-117">Clique em Olá **gerenciamento de trabalho** trabalhos de saudação toosee lado a lado.</span><span class="sxs-lookup"><span data-stu-id="b9eef-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="b9eef-118">trabalhos de saudação são categorizados em **executando**, **em fila**, e **finalizado**.</span><span class="sxs-lookup"><span data-stu-id="b9eef-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="b9eef-119">Você deverá ver o trabalho com falha em Olá **finalizado** seção.</span><span class="sxs-lookup"><span data-stu-id="b9eef-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="b9eef-120">Ele deverá ser o primeiro na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9eef-120">It shall be first one in hello list.</span></span> <span data-ttu-id="b9eef-121">Quando você tiver muitos trabalhos, você pode clicar em **filtro** toohelp você toolocate trabalhos.</span><span class="sxs-lookup"><span data-stu-id="b9eef-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Trabalhos de filtragem da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="b9eef-123">Clique em trabalho com falha de saudação de detalhes do trabalho Olá lista tooopen Olá em uma nova folha:</span><span class="sxs-lookup"><span data-stu-id="b9eef-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Trabalho com falha da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="b9eef-125">Saudação de aviso **reenviar** botão.</span><span class="sxs-lookup"><span data-stu-id="b9eef-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="b9eef-126">Depois de corrigir o problema de saudação, você pode enviar novamente trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="b9eef-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="b9eef-127">Clique em parte destacada da saudação anterior captura de tela tooopen Olá detalhes do erro.</span><span class="sxs-lookup"><span data-stu-id="b9eef-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="b9eef-128">Você verá algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="b9eef-128">You shall see something like:</span></span>

    ![Detalhes do trabalho com falha da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="b9eef-130">Ele informa a pasta de origem Olá não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="b9eef-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="b9eef-131">Clique em **Duplicar Script**.</span><span class="sxs-lookup"><span data-stu-id="b9eef-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="b9eef-132">Saudação de atualização **FROM** a seguir toohello caminho:</span><span class="sxs-lookup"><span data-stu-id="b9eef-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="b9eef-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="b9eef-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="b9eef-134">Clique em **Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="b9eef-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="b9eef-135">Confira também</span><span class="sxs-lookup"><span data-stu-id="b9eef-135">See also</span></span>
* [<span data-ttu-id="b9eef-136">Visão geral da Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b9eef-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b9eef-137">Introdução à Análise Azure Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9eef-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="b9eef-138">Introdução ao U-SQL da Análise Azure Data Lake usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9eef-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="b9eef-139">Gerenciar a Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9eef-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
