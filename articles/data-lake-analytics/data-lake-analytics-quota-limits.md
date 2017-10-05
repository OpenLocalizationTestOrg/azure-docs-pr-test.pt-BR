---
title: Limites de Cota do Azure Data Lake Analytics | Microsoft Docs
description: Saiba como ajustar e aumentar os limites de cota nas contas do ADLA (Azure Data Lake Analytics).
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
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="2e629-104">Limites de Cota do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2e629-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="2e629-105">Saiba como ajustar e aumentar os limites de cota nas contas do ADLA (Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="2e629-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="2e629-106">Conhecer esses limites pode ajudar você a entender o comportamento do seu trabalho U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2e629-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="2e629-107">Todos esses limites de cota são flexíveis, e você pode aumentar os limites máximos entrando em contato conosco.</span><span class="sxs-lookup"><span data-stu-id="2e629-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="2e629-108">Limites das assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="2e629-108">Azure subscriptions limits</span></span>

<span data-ttu-id="2e629-109">**Número máximo de contas do ADLA por assinatura:**5</span><span class="sxs-lookup"><span data-stu-id="2e629-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="2e629-110">Esse é o número máximo de contas do ADLA que você pode criar por assinatura.</span><span class="sxs-lookup"><span data-stu-id="2e629-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="2e629-111">Você recebe o erro "Você atingiu o número máximo de contas do Data Lake Analytics permitidas (5) na região sob o nome da assinatura" ao tentar criar a sexta conta do ADLA.</span><span class="sxs-lookup"><span data-stu-id="2e629-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="2e629-112">Nesse caso, exclua as contas do ADLA não utilizadas ou entre em contato conosco para abrir um [tíquete de suporte](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="2e629-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="2e629-113">Limites da conta do ADLA</span><span class="sxs-lookup"><span data-stu-id="2e629-113">ADLA account limits</span></span>

<span data-ttu-id="2e629-114">**Número máximo de AUs (Unidades de Análise) por conta:** 250</span><span class="sxs-lookup"><span data-stu-id="2e629-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="2e629-115">Esse é o número máximo de AUs que podem ser executadas simultaneamente em sua conta.</span><span class="sxs-lookup"><span data-stu-id="2e629-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="2e629-116">Se o total de AUs em execução em todos os trabalhos exceder esse limite, novos trabalhos serão colocados na fila automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2e629-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="2e629-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2e629-117">For example:</span></span>

* <span data-ttu-id="2e629-118">Caso você possua apenas um trabalho em execução com 250 AUs, ao adicionar um segundo trabalho ele permanecerá na fila até que o primeiro trabalho esteja concluído.</span><span class="sxs-lookup"><span data-stu-id="2e629-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="2e629-119">Caso você já possua cinco trabalhos em execução e cada um estiver utilizando 50 AUs, ao adicionar um sexto trabalho que necessite de 20 AUs ele permanecerá na fila até que 20 AUs se tornem disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2e629-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="2e629-120">**Número máximo de trabalhos U-SQL simultâneos por conta:**  20</span><span class="sxs-lookup"><span data-stu-id="2e629-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="2e629-121">Esse é o número máximo de trabalhos que podem ser executados simultaneamente em sua conta.</span><span class="sxs-lookup"><span data-stu-id="2e629-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="2e629-122">Exceder esse valor faz com que os trabalhos mais recentes sejam enfileirados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2e629-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="2e629-123">Ajustar os limites de cota do ADLA por conta</span><span class="sxs-lookup"><span data-stu-id="2e629-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="2e629-124">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e629-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2e629-125">Escolha uma conta ADLA que você já criou.</span><span class="sxs-lookup"><span data-stu-id="2e629-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="2e629-126">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2e629-126">Click **Properties**.</span></span>
4. <span data-ttu-id="2e629-127">Ajuste **Paralelismo** e **Trabalhos simultâneos** para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="2e629-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="2e629-129">Aumente os limites máximos de cota</span><span class="sxs-lookup"><span data-stu-id="2e629-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="2e629-130">Abra uma solicitação de suporte no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e629-130">Open a support request in Azure Portal.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="2e629-133">Selecione o tipo de problema **Cota**.</span><span class="sxs-lookup"><span data-stu-id="2e629-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="2e629-134">Selecione sua **Assinatura**(Verifique se ela não é uma assinatura de "teste").</span><span class="sxs-lookup"><span data-stu-id="2e629-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="2e629-135">Selecione o tipo de cota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2e629-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="2e629-137">Na folha do problema, explique seu pedido de aumento de limite com **Detalhes**de por que você necessita dessa capacidade extra.</span><span class="sxs-lookup"><span data-stu-id="2e629-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Folha do portal da Análise Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="2e629-139">Verifique suas informações de contato e crie a solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="2e629-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="2e629-140">A Microsoft examina sua solicitação e tenta acomodar suas necessidades de negócios assim que possível.</span><span class="sxs-lookup"><span data-stu-id="2e629-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e629-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e629-141">Next steps</span></span>

* [<span data-ttu-id="2e629-142">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="2e629-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="2e629-143">Gerenciar a Análise Azure Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e629-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="2e629-144">Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2e629-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
