---
title: "Recomendações de segurança do Azure Advisor | Microsoft Docs"
description: "Use o Azure Advisor para melhorar a segurança das implantações do Azure."
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="4285b-103">Recomendações de segurança do Advisor</span><span class="sxs-lookup"><span data-stu-id="4285b-103">Advisor Security recommendations</span></span>

<span data-ttu-id="4285b-104">O Assistente do Azure fornece uma exibição consistente e consolidada de recomendações para todos os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4285b-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="4285b-105">Ele se integra à Central de Segurança do Azure para fornecer recomendações de segurança.</span><span class="sxs-lookup"><span data-stu-id="4285b-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="4285b-106">Você pode obter recomendações de segurança na guia **Segurança** do painel do Assistente.</span><span class="sxs-lookup"><span data-stu-id="4285b-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![O botão Segurança do Assistente](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="4285b-108">A Central de Segurança ajuda você a impedir, detectar e responder a ameaças com maior visibilidade e controle sobre a segurança dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4285b-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="4285b-109">Ela analisa periodicamente o estado de segurança de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4285b-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="4285b-110">Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, cria recomendações.</span><span class="sxs-lookup"><span data-stu-id="4285b-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="4285b-111">As recomendações o orientam pelo processo de configuração dos controles necessários.</span><span class="sxs-lookup"><span data-stu-id="4285b-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![A guia Segurança do Assistente](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="4285b-113">Para obter mais informações sobre as recomendações de segurança, consulte [Gerenciando recomendações de segurança na Central de Segurança do Azure](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="4285b-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="4285b-114">Como acessar as recomendações de Segurança no Assistente do Azure</span><span class="sxs-lookup"><span data-stu-id="4285b-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="4285b-115">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4285b-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4285b-116">No painel esquerdo, clique em **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="4285b-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="4285b-117">No painel do menu de serviço, em **Monitoramento e Gerenciamento**, clique em **Assistente do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4285b-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="4285b-118">O painel Assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="4285b-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="4285b-119">No painel do Assistente, clique na guia **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="4285b-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="4285b-120">Selecione a assinatura para a qual você deseja receber recomendações e, em seguida, clique em **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="4285b-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="4285b-121">Para acessar as recomendações do Assistente, você deve primeiro *registrar sua assinatura* no Assistente.</span><span class="sxs-lookup"><span data-stu-id="4285b-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="4285b-122">Uma assinatura é registrada quando um *Proprietário de assinatura* inicia o painel do Assistente e clica no botão **Obter recomendações**.</span><span class="sxs-lookup"><span data-stu-id="4285b-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="4285b-123">Essa é uma *operação única*.</span><span class="sxs-lookup"><span data-stu-id="4285b-123">This is a *one-time operation*.</span></span> <span data-ttu-id="4285b-124">Depois que a assinatura for registrada, você poderá acessar as recomendações do Assistente como *Proprietário*, *Colaborador* ou *Leitor* de uma assinatura, um grupo de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="4285b-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4285b-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4285b-125">Next steps</span></span>

<span data-ttu-id="4285b-126">Para saber mais sobre as recomendações do Assistente, consulte:</span><span class="sxs-lookup"><span data-stu-id="4285b-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="4285b-127">Introdução ao Advisor</span><span class="sxs-lookup"><span data-stu-id="4285b-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="4285b-128">Introdução ao Advisor</span><span class="sxs-lookup"><span data-stu-id="4285b-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="4285b-129">Recomendações de custo do Advisor</span><span class="sxs-lookup"><span data-stu-id="4285b-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="4285b-130">Recomendações de desempenho do Advisor</span><span class="sxs-lookup"><span data-stu-id="4285b-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="4285b-131">Recomendações de alta disponibilidade do Advisor</span><span class="sxs-lookup"><span data-stu-id="4285b-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
