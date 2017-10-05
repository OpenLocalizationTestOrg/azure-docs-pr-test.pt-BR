---
title: Solucionar problemas em trabalhos do Azure Data Lake Analytics usando o Portal do Azure | Microsoft Docs
description: "Saiba como usar o Portal do Azure para solucionar problemas com trabalhos da Análise do Data Lake. "
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
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="bc856-103">Solucionar problemas em trabalhos da Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc856-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="bc856-104">Saiba como usar o Portal do Azure para solucionar problemas com trabalhos da Análise do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bc856-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="bc856-105">Neste tutorial, você criará um problema de arquivo de origem ausente e usará o Portal do Azure para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="bc856-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="bc856-106">Enviar um trabalho da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="bc856-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="bc856-107">Envie o seguinte trabalho U-SQL:</span><span class="sxs-lookup"><span data-stu-id="bc856-107">Submit the following U-SQL job:</span></span>

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
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="bc856-108">O arquivo de origem definido no script é **/Samples/Data/SearchLog.tsv1**, em que ele deverá ser **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="bc856-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="bc856-109">Solucionar problemas no trabalho</span><span class="sxs-lookup"><span data-stu-id="bc856-109">Troubleshoot the job</span></span>

<span data-ttu-id="bc856-110">**Para ver todos os trabalhos**</span><span class="sxs-lookup"><span data-stu-id="bc856-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="bc856-111">No portal do Azure, clique em **Microsoft Azure** no canto superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="bc856-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="bc856-112">Clique no bloco com o nome da conta da Análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bc856-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="bc856-113">O resumo do trabalho é mostrado no bloco **Gerenciamento de Trabalhos** .</span><span class="sxs-lookup"><span data-stu-id="bc856-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Gerenciamento de trabalhos da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="bc856-115">O Gerenciamento do trabalho mostra rapidamente o status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="bc856-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="bc856-116">Observe que há um trabalho com falha.</span><span class="sxs-lookup"><span data-stu-id="bc856-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="bc856-117">Clique no bloco **Gerenciamento de Trabalhos** para ver os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="bc856-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="bc856-118">Os trabalhos são categorizados como **Em execução**, **Em fila** e **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="bc856-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="bc856-119">Você deverá ver o trabalho com falha na seção **Concluído** .</span><span class="sxs-lookup"><span data-stu-id="bc856-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="bc856-120">Ele deve ser primeiro na lista.</span><span class="sxs-lookup"><span data-stu-id="bc856-120">It shall be first one in the list.</span></span> <span data-ttu-id="bc856-121">Quando tiver vários trabalhos, é possível clicar em **Filtrar** para ajudar a encontrar os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="bc856-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Trabalhos de filtragem da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="bc856-123">Clique no trabalho com falha na lista para abrir os detalhes do trabalho em uma nova folha:</span><span class="sxs-lookup"><span data-stu-id="bc856-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Trabalho com falha da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="bc856-125">Observe o botão **Enviar novamente** .</span><span class="sxs-lookup"><span data-stu-id="bc856-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="bc856-126">Depois de corrigir o problema, você poderá enviar novamente o trabalho.</span><span class="sxs-lookup"><span data-stu-id="bc856-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="bc856-127">Clique na parte realçada na captura de tela anterior para abrir os detalhes do erro.</span><span class="sxs-lookup"><span data-stu-id="bc856-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="bc856-128">Você verá algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc856-128">You shall see something like:</span></span>

    ![Detalhes do trabalho com falha da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="bc856-130">Isso indica que a pasta de origem não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="bc856-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="bc856-131">Clique em **Duplicar Script**.</span><span class="sxs-lookup"><span data-stu-id="bc856-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="bc856-132">Atualize o caminho **FROM** para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bc856-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="bc856-133">"/Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="bc856-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="bc856-134">Clique em **Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="bc856-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="bc856-135">Confira também</span><span class="sxs-lookup"><span data-stu-id="bc856-135">See also</span></span>
* [<span data-ttu-id="bc856-136">Visão geral da Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="bc856-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="bc856-137">Introdução à Análise Azure Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc856-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="bc856-138">Introdução ao U-SQL da Análise Azure Data Lake usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc856-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="bc856-139">Gerenciar a Análise do Azure Data Lake usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc856-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
