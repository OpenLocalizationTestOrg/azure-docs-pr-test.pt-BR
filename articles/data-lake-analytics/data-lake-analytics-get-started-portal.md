---
title: "Introdução ao Azure Data Lake Analytics usando o Portal do Azure | Microsoft Docs"
description: 'Saiba como usar o portal do Azure para criar uma conta do Data Lake Analytics, criar um trabalho do Data Lake Analytics usando o U-SQL e enviar o trabalho. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 2722a2d72ed90ea0005362563ecaee30750c040a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="4106f-103">Introdução ao Azure Data Lake Analytics usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4106f-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="4106f-104">Saiba como usar o portal do Azure para criar contas do Azure Data Lake Analytics, definir trabalhos no [U-SQL](data-lake-analytics-u-sql-get-started.md) e enviar trabalhos ao serviço do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4106f-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="4106f-105">Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4106f-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4106f-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4106f-106">Prerequisites</span></span>

<span data-ttu-id="4106f-107">Antes de começar este tutorial, você deve ter uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4106f-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="4106f-108">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4106f-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="4106f-109">Criar uma conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="4106f-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="4106f-110">Agora, você criará um Data Lake Analytics e uma conta do Data Lake Store simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="4106f-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at the same time.</span></span>  <span data-ttu-id="4106f-111">Esta etapa é simples e demora apenas 60 segundos para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="4106f-111">This step is simple and only takes about 60 seconds to finish.</span></span>

1. <span data-ttu-id="4106f-112">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4106f-112">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4106f-113">Clique em **Novo** >  **Data + Analytics** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4106f-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="4106f-114">Selecione os valores para os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4106f-114">Select values for the following items:</span></span>
   * <span data-ttu-id="4106f-115">**Nome**: Nome de sua conta do Data Lake Analytics (são permitidos somente letras minúsculas e números).</span><span class="sxs-lookup"><span data-stu-id="4106f-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="4106f-116">**Assinatura**: escolha a assinatura do Azure usada para a conta da Análise.</span><span class="sxs-lookup"><span data-stu-id="4106f-116">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="4106f-117">**Grupo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="4106f-117">**Resource Group**.</span></span> <span data-ttu-id="4106f-118">Selecione um Grupo de Recursos do Azure existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="4106f-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="4106f-119">**Local**.</span><span class="sxs-lookup"><span data-stu-id="4106f-119">**Location**.</span></span> <span data-ttu-id="4106f-120">Selecione um datacenter do Azure para a conta da Análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4106f-120">Select an Azure data center for the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="4106f-121">**Data Lake Store**: siga as instruções para criar uma nova conta do Data Lake Store ou selecione uma existente.</span><span class="sxs-lookup"><span data-stu-id="4106f-121">**Data Lake Store**: Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="4106f-122">Opcionalmente, selecione um tipo de preço para sua conta Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4106f-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="4106f-123">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4106f-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="4106f-124">Seu primeiro script U-SQL</span><span class="sxs-lookup"><span data-stu-id="4106f-124">Your first U-SQL script</span></span>

<span data-ttu-id="4106f-125">O texto a seguir é um script U-SQL muito simples.</span><span class="sxs-lookup"><span data-stu-id="4106f-125">The following text is a very simple U-SQL script.</span></span> <span data-ttu-id="4106f-126">Tudo o que ele faz é definir um pequeno conjunto de dados dentro do script e, em seguida, gravar a esse conjunto de dados no Data Lake Store como um arquivo chamado `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="4106f-126">All it does is define a small dataset within the script and then write that dataset out to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
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
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="4106f-127">Enviar um trabalho do U-SQL</span><span class="sxs-lookup"><span data-stu-id="4106f-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="4106f-128">Na conta do Data Lake Analytics, clique em **Novo Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="4106f-128">From the Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="4106f-129">Cole o texto do script U-SQL mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="4106f-129">Paste in the text of the U-SQL script shown above.</span></span> 
3. <span data-ttu-id="4106f-130">Clique em **Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="4106f-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="4106f-131">Aguarde até que o status do trabalho seja alterado para **Êxito**.</span><span class="sxs-lookup"><span data-stu-id="4106f-131">Wait until the job status changes to **Succeeded**.</span></span>
5. <span data-ttu-id="4106f-132">Se o trabalho falhar, veja [Monitorar e solucionar problemas dos trabalhos do Data Lake Analytics](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4106f-132">If the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="4106f-133">Clique na guia **Saída** e em `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="4106f-133">Click the **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="4106f-134">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4106f-134">See also</span></span>

* <span data-ttu-id="4106f-135">Para começar a desenvolver aplicativos U-SQL, consulte [Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4106f-135">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="4106f-136">Para aprender a usar o U-SQL, veja [Introdução à linguagem U-SQL da Análise do Azure Data Lake](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4106f-136">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="4106f-137">Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4106f-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
