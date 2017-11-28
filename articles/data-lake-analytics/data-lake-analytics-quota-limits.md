---
title: "aaaAzure limites de cota de análise Data Lake | Microsoft Docs"
description: Saiba como tooadjust e aumentar a cota limita em contas do Azure Data Lake Analytics (ADLA).
services: data-lake-analytics
keywords: "Análise Azure Data Lake"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="0fb1c-104">Limites de Cota do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0fb1c-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="0fb1c-105">Saiba como tooadjust e aumentar a cota limita em contas do Azure Data Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="0fb1c-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="0fb1c-106">Conhecer esses limites pode ajudar você a entender o comportamento do seu trabalho U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="0fb1c-107">Todos os limites de cota são flexíveis, para que você pode aumentar os limites máximos Olá alcançar toous.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="0fb1c-108">Limites das assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="0fb1c-108">Azure subscriptions limits</span></span>

<span data-ttu-id="0fb1c-109">**Número máximo de contas do ADLA por assinatura:**5</span><span class="sxs-lookup"><span data-stu-id="0fb1c-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="0fb1c-110">Este é o número de máximo de saudação de contas ADLA que pode ser criado por assinatura.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="0fb1c-111">Se você tentar conta ADLA toocreate um sexto, você obterá um erro "Você atingiu Olá o número máximo de contas da análise Data Lake permitidas (5) na região em nome de assinatura".</span><span class="sxs-lookup"><span data-stu-id="0fb1c-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="0fb1c-112">Nesse caso, exclua todas as contas ADLA não utilizadas ou chegar toous por [abrindo um tíquete de suporte](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="0fb1c-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="0fb1c-113">Limites da conta do ADLA</span><span class="sxs-lookup"><span data-stu-id="0fb1c-113">ADLA account limits</span></span>

<span data-ttu-id="0fb1c-114">**Número máximo de AUs (Unidades de Análise) por conta:** 250</span><span class="sxs-lookup"><span data-stu-id="0fb1c-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="0fb1c-115">Este é o número de máximo de saudação de AUs que podem ser executados simultaneamente em sua conta.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="0fb1c-116">Se o total de AUs em execução em todos os trabalhos exceder esse limite, novos trabalhos serão colocados na fila automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="0fb1c-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0fb1c-117">For example:</span></span>

* <span data-ttu-id="0fb1c-118">Se você tiver apenas um trabalho em execução com 250 Austrália, quando você enviar um segundo trabalho que irá esperar na fila de trabalhos Olá Olá primeiro trabalho é concluído.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="0fb1c-119">Se você já tiver cinco trabalhos em execução e cada um está usando 50 Austrália, quando você enviar um trabalho sexto que precisa de 20 Austrália aguardar na fila de trabalhos Olá até que haja 20 Austrália disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="0fb1c-120">**Número máximo de trabalhos U-SQL simultâneos por conta:**  20</span><span class="sxs-lookup"><span data-stu-id="0fb1c-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="0fb1c-121">Este é o número máximo de saudação de trabalhos que podem ser executados simultaneamente em sua conta.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="0fb1c-122">Exceder esse valor faz com que os trabalhos mais recentes sejam enfileirados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="0fb1c-123">Ajustar os limites de cota do ADLA por conta</span><span class="sxs-lookup"><span data-stu-id="0fb1c-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="0fb1c-124">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0fb1c-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0fb1c-125">Escolha uma conta ADLA que você já criou.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="0fb1c-126">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-126">Click **Properties**.</span></span>
4. <span data-ttu-id="0fb1c-127">Ajustar **paralelismo** e **trabalhos simultâneos** toosuit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="0fb1c-129">Aumente os limites máximos de cota</span><span class="sxs-lookup"><span data-stu-id="0fb1c-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="0fb1c-130">Abra uma solicitação de suporte no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-130">Open a support request in Azure Portal.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="0fb1c-133">Selecione o tipo de problema Olá **cota**.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="0fb1c-134">Selecione sua **Assinatura**(Verifique se ela não é uma assinatura de "teste").</span><span class="sxs-lookup"><span data-stu-id="0fb1c-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="0fb1c-135">Selecione o tipo de cota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="0fb1c-137">Na folha de problema hello, explique o limite de aumento solicitado com **detalhes** de por que você precisa que essa capacidade extra.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="0fb1c-139">Verifique se suas informações de contato e criar solicitação de suporte de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="0fb1c-140">A Microsoft analisa sua solicitação e tenta tooaccommodate necessidades de sua empresa assim que possível.</span><span class="sxs-lookup"><span data-stu-id="0fb1c-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fb1c-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fb1c-141">Next steps</span></span>

* [<span data-ttu-id="0fb1c-142">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="0fb1c-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="0fb1c-143">Gerenciar a Análise Azure Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fb1c-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="0fb1c-144">Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0fb1c-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
