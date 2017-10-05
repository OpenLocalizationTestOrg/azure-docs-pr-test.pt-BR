---
title: "Introdução ao Azure Advisor | Microsoft Docs"
description: "Use o Azure Advisor para otimizar as implantações do Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="f548e-103">Introdução ao Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="f548e-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="f548e-104">Saiba mais sobre o Assistente do Azure e suas principais funcionalidades e obtenha respostas para perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="f548e-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="f548e-105">O que é o Assistente?</span><span class="sxs-lookup"><span data-stu-id="f548e-105">What is Advisor?</span></span>
<span data-ttu-id="f548e-106">O Assistente é um consultor de nuvem personalizado que ajuda você a seguir as melhores práticas para otimizar suas implantações do Azure.</span><span class="sxs-lookup"><span data-stu-id="f548e-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="f548e-107">Ele analisa a telemetria de uso e configuração do recurso e, depois, recomenda soluções que podem ajudar você a melhorar a economia, o desempenho, a alta disponibilidade e a segurança de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f548e-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="f548e-108">Com o Assistente, é possível:</span><span class="sxs-lookup"><span data-stu-id="f548e-108">With Advisor, you can:</span></span>
* <span data-ttu-id="f548e-109">Obter recomendações de melhores práticas proativas, personalizadas e prontas para uso.</span><span class="sxs-lookup"><span data-stu-id="f548e-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="f548e-110">Melhorar o desempenho, a segurança e a alta disponibilidade de seus recursos, enquanto você identifica oportunidades para reduzir o gasto geral do Azure.</span><span class="sxs-lookup"><span data-stu-id="f548e-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="f548e-111">Obter recomendações com ações propostas embutidas.</span><span class="sxs-lookup"><span data-stu-id="f548e-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="f548e-112">Você pode acessar o Advisor pelo [Portal do Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="f548e-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="f548e-113">Entre no [portal](https://portal.azure.com), selecione **Procurar** e, em seguida, role até **Assistente do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f548e-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="f548e-114">O painel do Advisor exibe recomendações personalizadas para uma assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="f548e-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="f548e-115">As recomendações são divididas em quatro categorias:</span><span class="sxs-lookup"><span data-stu-id="f548e-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="f548e-116">**Alta Disponibilidade**: para garantir e melhorar a continuidade dos aplicativos críticos para os negócios.</span><span class="sxs-lookup"><span data-stu-id="f548e-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="f548e-117">Para saber mais, veja [Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Recomendações de alta disponibilidade do Advisor).</span><span class="sxs-lookup"><span data-stu-id="f548e-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="f548e-118">**Segurança**: para detectar ameaças e vulnerabilidades que podem levar a possíveis violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="f548e-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="f548e-119">Para saber mais, veja [Advisor Security recommendations](advisor-security-recommendations.md) (Recomendações de segurança do Advisor).</span><span class="sxs-lookup"><span data-stu-id="f548e-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="f548e-120">**Desempenho**: para melhorar a velocidade dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f548e-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="f548e-121">Para saber mais, veja [Advisor Performance recommendations](advisor-performance-recommendations.md) (Recomendações de desempenho do Advisor).</span><span class="sxs-lookup"><span data-stu-id="f548e-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="f548e-122">**Custo**: para otimizar e reduzir o gasto geral do Azure.</span><span class="sxs-lookup"><span data-stu-id="f548e-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="f548e-123">Para saber mais, veja [Advisor Cost recommendations](advisor-cost-recommendations.md) (Recomendações de custo do Advisor).</span><span class="sxs-lookup"><span data-stu-id="f548e-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Tipos de recomendação do Advisor](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="f548e-125">Para acessar as recomendações do Assistente, você deve primeiro *registrar sua assinatura* no Assistente.</span><span class="sxs-lookup"><span data-stu-id="f548e-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="f548e-126">Uma assinatura é registrada quando um *Proprietário de assinatura* inicia o painel do Assistente e clica no botão **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="f548e-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="f548e-127">Essa é uma *operação única*.</span><span class="sxs-lookup"><span data-stu-id="f548e-127">This is a *one-time operation*.</span></span> <span data-ttu-id="f548e-128">Depois que a assinatura for registrada, você poderá acessar as recomendações do Assistente como *Proprietário*, *Colaborador* ou *Leitor* de uma assinatura, um grupo de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="f548e-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="f548e-129">Clique em uma recomendação para saber mais sobre ela.</span><span class="sxs-lookup"><span data-stu-id="f548e-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="f548e-130">Saiba mais sobre as ações que você pode realizar para aproveitar uma oportunidade ou resolver um problema.</span><span class="sxs-lookup"><span data-stu-id="f548e-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="f548e-131">O Advisor oferece recomendações com ações embutidas ou links de documentação.</span><span class="sxs-lookup"><span data-stu-id="f548e-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="f548e-132">Ao clicar em uma ação embutida, você é levado para uma "jornada interativa de usuário" para implementá-la.</span><span class="sxs-lookup"><span data-stu-id="f548e-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="f548e-133">Clicar em um link de documentação aponta para a documentação que descreve como implementar a ação manualmente.</span><span class="sxs-lookup"><span data-stu-id="f548e-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="f548e-134">O Assistente atualiza as recomendações a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f548e-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="f548e-135">Se você não pretender tomar uma ação imediata de acordo com uma recomendação, será possível adiá-la por um período especificado ou descartá-la.</span><span class="sxs-lookup"><span data-stu-id="f548e-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="f548e-136">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="f548e-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="f548e-137">Como acesso o Advisor?</span><span class="sxs-lookup"><span data-stu-id="f548e-137">How do I access Advisor?</span></span>
<span data-ttu-id="f548e-138">Você pode acessar o Advisor pelo [Portal do Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="f548e-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="f548e-139">Entre no [portal](https://portal.azure.com), selecione **Procurar** e, em seguida, role até **Assistente do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f548e-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="f548e-140">O painel do Advisor exibe recomendações personalizadas para uma assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="f548e-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="f548e-141">Você também pode exibir as recomendações do Advisor por meio da folha de recursos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f548e-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="f548e-142">Escolha uma máquina virtual e role até as recomendações do Advisor no menu.</span><span class="sxs-lookup"><span data-stu-id="f548e-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="f548e-143">De quais permissões preciso para acessar o Advisor?</span><span class="sxs-lookup"><span data-stu-id="f548e-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="f548e-144">Para acessar as recomendações do Assistente, você deve primeiro *registrar sua assinatura* no Assistente.</span><span class="sxs-lookup"><span data-stu-id="f548e-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="f548e-145">Uma assinatura é registrada quando um *Proprietário de assinatura* inicia o painel do Assistente e clica no botão **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="f548e-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="f548e-146">Essa é uma *operação única*.</span><span class="sxs-lookup"><span data-stu-id="f548e-146">This is a *one-time operation*.</span></span> <span data-ttu-id="f548e-147">Depois que a assinatura for registrada, você poderá acessar as recomendações do Assistente como *Proprietário*, *Colaborador* ou *Leitor* de uma assinatura, um grupo de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="f548e-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="f548e-148">Com que frequência as recomendações do Advisor são atualizadas?</span><span class="sxs-lookup"><span data-stu-id="f548e-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="f548e-149">As recomendações do Assistente são atualizadas a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f548e-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="f548e-150">Para quais recursos o Advisor fornece recomendações?</span><span class="sxs-lookup"><span data-stu-id="f548e-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="f548e-151">O Assistente fornece recomendações para máquinas virtuais, conjuntos de disponibilidade, gateways de aplicativo, Serviços de Aplicativos, SQL Servers, bancos de dados SQL e para o Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f548e-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="f548e-152">Posso adiar ou descartar uma recomendação?</span><span class="sxs-lookup"><span data-stu-id="f548e-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="f548e-153">Para adiar ou descartar uma recomendação, clique no botão ou link **Adiar**.</span><span class="sxs-lookup"><span data-stu-id="f548e-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="f548e-154">Você pode especificar uma hora de adiamento ou selecionar **Nunca** para descartar a recomendação.</span><span class="sxs-lookup"><span data-stu-id="f548e-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f548e-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f548e-155">Next steps</span></span>

<span data-ttu-id="f548e-156">Para saber mais sobre as recomendações do Assistente, consulte:</span><span class="sxs-lookup"><span data-stu-id="f548e-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="f548e-157">Introdução ao Advisor</span><span class="sxs-lookup"><span data-stu-id="f548e-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="f548e-158">Recomendações de alta disponibilidade do Advisor</span><span class="sxs-lookup"><span data-stu-id="f548e-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="f548e-159">Recomendações de segurança do Advisor</span><span class="sxs-lookup"><span data-stu-id="f548e-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="f548e-160">Recomendações de desempenho do Advisor</span><span class="sxs-lookup"><span data-stu-id="f548e-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="f548e-161">Recomendações de custo do Advisor</span><span class="sxs-lookup"><span data-stu-id="f548e-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
