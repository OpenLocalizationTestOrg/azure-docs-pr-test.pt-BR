---
title: "aaaGet iniciado com análise Azure Data Lake usando o portal do Azure | Microsoft Docs"
description: "Saiba como Olá toouse toocreate portal do Azure uma conta da análise Data Lake, criar um trabalho de análise Data Lake usando U-SQL e enviar o trabalho de saudação. "
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
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="b9110-103">Introdução ao Azure Data Lake Analytics usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9110-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="b9110-104">Saiba como toouse Olá contas de análise do Azure Data Lake toocreate portal do Azure, definir trabalhos em [U-SQL](data-lake-analytics-u-sql-get-started.md)e envie-o serviço de análise Data Lake toohello trabalhos.</span><span class="sxs-lookup"><span data-stu-id="b9110-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="b9110-105">Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9110-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9110-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b9110-106">Prerequisites</span></span>

<span data-ttu-id="b9110-107">Antes de começar este tutorial, você deve ter uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b9110-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="b9110-108">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9110-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="b9110-109">Criar uma conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="b9110-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="b9110-110">Agora, você criará uma análise Data Lake e um repositório Data Lake conta em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="b9110-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="b9110-111">Esta etapa é simple e leva apenas sobre toofinish de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="b9110-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="b9110-112">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9110-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9110-113">Clique em **Novo** >  **Data + Analytics** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="b9110-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="b9110-114">Selecione os valores para Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9110-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="b9110-115">**Nome**: Nome de sua conta do Data Lake Analytics (são permitidos somente letras minúsculas e números).</span><span class="sxs-lookup"><span data-stu-id="b9110-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="b9110-116">**Assinatura**: escolha Olá assinatura do Azure usada para Olá conta da análise.</span><span class="sxs-lookup"><span data-stu-id="b9110-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="b9110-117">**Grupo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="b9110-117">**Resource Group**.</span></span> <span data-ttu-id="b9110-118">Selecione um Grupo de Recursos do Azure existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="b9110-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="b9110-119">**Local**.</span><span class="sxs-lookup"><span data-stu-id="b9110-119">**Location**.</span></span> <span data-ttu-id="b9110-120">Selecione um data center do Azure para a conta de análise Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="b9110-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="b9110-121">**Repositório data Lake**: siga as instruções de saudação toocreate uma nova conta do repositório Data Lake ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="b9110-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="b9110-122">Opcionalmente, selecione um tipo de preço para sua conta Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b9110-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="b9110-123">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b9110-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="b9110-124">Seu primeiro script U-SQL</span><span class="sxs-lookup"><span data-stu-id="b9110-124">Your first U-SQL script</span></span>

<span data-ttu-id="b9110-125">Olá texto a seguir é um script U-SQL muito simple.</span><span class="sxs-lookup"><span data-stu-id="b9110-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="b9110-126">Tudo o que ele faz é definir um pequeno conjunto de dados no script hello e, em seguida, gravar o conjunto de dados fora do repositório Data Lake do toohello padrão como um arquivo chamado `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="b9110-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
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
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="b9110-127">Enviar um trabalho do U-SQL</span><span class="sxs-lookup"><span data-stu-id="b9110-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="b9110-128">Na conta da análise Data Lake do hello, clique em **novo trabalho**.</span><span class="sxs-lookup"><span data-stu-id="b9110-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="b9110-129">Colar texto de saudação do hello script U-SQL mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="b9110-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="b9110-130">Clique em **Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="b9110-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="b9110-131">Aguarde até que as alterações de status do trabalho Olá muito**êxito**.</span><span class="sxs-lookup"><span data-stu-id="b9110-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="b9110-132">Se a falha no trabalho de hello, consulte [monitorar e solucionar problemas de trabalhos da análise Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b9110-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="b9110-133">Clique em Olá **saída** guia e, em seguida, clique em `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="b9110-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="b9110-134">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b9110-134">See also</span></span>

* <span data-ttu-id="b9110-135">tooget iniciar o desenvolvimento de aplicativos de U-SQL, consulte [scripts de desenvolver U-SQL usando o Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9110-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="b9110-136">toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9110-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="b9110-137">Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b9110-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
