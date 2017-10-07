---
title: "aaaGet iniciado com análise Azure Data Lake usando o Azure PowerShell | Microsoft Docs"
description: "Usar o Azure PowerShell toocreate uma conta da análise Data Lake, criar um trabalho de análise Data Lake usando U-SQL e enviar o trabalho de saudação. "
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
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="bcb62-103">Introdução ao Azure Data Lake Analytics usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcb62-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="bcb62-104">Saiba como toouse toocreate do PowerShell do Azure análise Azure Data Lake contas e, em seguida, enviar e executar trabalhos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bcb62-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="bcb62-105">Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcb62-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcb62-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bcb62-106">Prerequisites</span></span>

<span data-ttu-id="bcb62-107">Antes de começar este tutorial, você deve ter Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="bcb62-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="bcb62-108">**Uma conta da Análise Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="bcb62-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="bcb62-109">Veja [Introdução ao Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="bcb62-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="bcb62-110">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bcb62-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="bcb62-111">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bcb62-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="bcb62-112">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="bcb62-112">Log in tooAzure</span></span>

<span data-ttu-id="bcb62-113">Este tutorial pressupõe que você já esteja familiarizado com o uso do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcb62-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="bcb62-114">Em particular, você precisa tooknow como toolog em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bcb62-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="bcb62-115">Consulte Olá [começar com o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) se precisar de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="bcb62-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="bcb62-116">toolog com um nome de assinatura:</span><span class="sxs-lookup"><span data-stu-id="bcb62-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="bcb62-117">Em vez do nome da assinatura hello, você também pode usar um toolog de id de assinatura em:</span><span class="sxs-lookup"><span data-stu-id="bcb62-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="bcb62-118">Se for bem-sucedido, saída desse comando Olá aparência Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="bcb62-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="bcb62-119">Preparando para o tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="bcb62-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="bcb62-120">trechos do PowerShell Olá neste tutorial usam essas variáveis toostore essas informações:</span><span class="sxs-lookup"><span data-stu-id="bcb62-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="bcb62-121">Obter informações sobre uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="bcb62-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="bcb62-122">Enviar um trabalho do U-SQL</span><span class="sxs-lookup"><span data-stu-id="bcb62-122">Submit a U-SQL job</span></span>

<span data-ttu-id="bcb62-123">Crie um script do PowerShell toohold variável Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="bcb62-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

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
    too"/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="bcb62-124">Envie o script hello.</span><span class="sxs-lookup"><span data-stu-id="bcb62-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="bcb62-125">Como alternativa, você pode salvar o script hello como um arquivo e enviar com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bcb62-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="bcb62-126">Obter status de saudação de um trabalho específico.</span><span class="sxs-lookup"><span data-stu-id="bcb62-126">Get hello status of a specific job.</span></span> <span data-ttu-id="bcb62-127">Continue a usar este cmdlet até que você veja Olá trabalho está concluído.</span><span class="sxs-lookup"><span data-stu-id="bcb62-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="bcb62-128">Em vez de chamar Get-AdlAnalyticsJob repetidamente até que um trabalho é concluído, você pode usar o hello espera AdlJob cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bcb62-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="bcb62-129">Baixe o arquivo de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="bcb62-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="bcb62-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bcb62-130">See also</span></span>
* <span data-ttu-id="bcb62-131">toosee Olá mesmo tutorial usando outras ferramentas, clique em seletores de guia Olá na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="bcb62-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="bcb62-132">toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bcb62-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="bcb62-133">Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bcb62-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
