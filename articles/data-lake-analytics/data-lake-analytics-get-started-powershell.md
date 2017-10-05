---
title: "Introdução ao Azure Data Lake Analytics usando o Azure PowerShell | Microsoft Docs"
description: 'Use o Azure PowerShell para criar uma conta do Data Lake Analytics, criar um trabalho do Data Lake Analytics usando o U-SQL e enviar o trabalho. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: 4f73e27c733edae658d1ea3bdabe48076328279b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="fa708-103">Introdução ao Azure Data Lake Analytics usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa708-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="fa708-104">Saiba como usar o Azure PowerShell para criar contas do Azure Data Lake Analytics e, em seguida, enviar e executar trabalhos do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa708-104">Learn how to use Azure PowerShell to create Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="fa708-105">Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa708-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa708-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fa708-106">Prerequisites</span></span>

<span data-ttu-id="fa708-107">Antes de começar este tutorial, você deve ter as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="fa708-107">Before you begin this tutorial, you must have the following information:</span></span>

* <span data-ttu-id="fa708-108">**Uma conta da Análise Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="fa708-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="fa708-109">Veja [Introdução ao Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="fa708-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="fa708-110">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="fa708-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="fa708-111">Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fa708-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="fa708-112">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="fa708-112">Log in to Azure</span></span>

<span data-ttu-id="fa708-113">Este tutorial pressupõe que você já esteja familiarizado com o uso do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa708-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="fa708-114">Em particular, você precisa saber como fazer logon no Azure.</span><span class="sxs-lookup"><span data-stu-id="fa708-114">In particular, you need to know how to log in to Azure.</span></span> <span data-ttu-id="fa708-115">Veja a [Introdução ao Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) se precisar de ajuda.</span><span class="sxs-lookup"><span data-stu-id="fa708-115">See the [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="fa708-116">Para fazer logon com um nome de assinatura:</span><span class="sxs-lookup"><span data-stu-id="fa708-116">To log in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="fa708-117">Em vez do nome da assinatura, você também pode usar uma id de assinatura para fazer logon:</span><span class="sxs-lookup"><span data-stu-id="fa708-117">Instead of the subscription name, you can also use a subscription id to log in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="fa708-118">Se for bem-sucedido, a saída desse comando se parece com o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="fa708-118">If  successful, the output of this command looks like the following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a><span data-ttu-id="fa708-119">Preparando-se para o tutorial</span><span class="sxs-lookup"><span data-stu-id="fa708-119">Preparing for the tutorial</span></span>

<span data-ttu-id="fa708-120">Os trechos do PowerShell neste tutorial usam essas variáveis para armazenar estas informações:</span><span class="sxs-lookup"><span data-stu-id="fa708-120">The PowerShell snippets in this tutorial use these variables to store this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="fa708-121">Obter informações sobre uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="fa708-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="fa708-122">Enviar um trabalho do U-SQL</span><span class="sxs-lookup"><span data-stu-id="fa708-122">Submit a U-SQL job</span></span>

<span data-ttu-id="fa708-123">Crie uma variável do PowerShell para manter o script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fa708-123">Create a PowerShell variable to hold the U-SQL script.</span></span>

```
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="fa708-124">Enviar o script.</span><span class="sxs-lookup"><span data-stu-id="fa708-124">Submit the script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="fa708-125">Como alternativa, você pode salvar o script como um arquivo e enviar com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="fa708-125">Alternatively, you could save the script as a file and submit with the following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="fa708-126">Obter o status de um trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="fa708-126">Get the status of a specific job.</span></span> <span data-ttu-id="fa708-127">Continue a usar este cmdlet até perceber que o trabalho foi concluído.</span><span class="sxs-lookup"><span data-stu-id="fa708-127">Keep using this cmdlet until you see the job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="fa708-128">Em vez de chamar Get-AdlAnalyticsJob repetidamente até que um trabalho seja concluído, você pode usar o cmdlet espera Wait-AdlJob.</span><span class="sxs-lookup"><span data-stu-id="fa708-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use the Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="fa708-129">Baixe o arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="fa708-129">Download the output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="fa708-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fa708-130">See also</span></span>
* <span data-ttu-id="fa708-131">Para ver o mesmo tutorial usando outras ferramentas, clique nos seletores de guias na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="fa708-131">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="fa708-132">Para aprender a usar o U-SQL, veja [Introdução à linguagem U-SQL da Análise do Azure Data Lake](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa708-132">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="fa708-133">Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fa708-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
