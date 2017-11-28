---
title: "aaaSet os alertas de crédito ou de cobrança de assinaturas do Azure | Microsoft Docs"
description: "Descreve como você pode configurar alertas na sua conta do Azure para que possa evitar surpresas na cobrança."
keywords: "alerta de crédito, alerta de cobrança"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="91cc3-104">Configurar alertas de cobrança ou de crédito para assinaturas do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="91cc3-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="91cc3-105">Se você estiver Olá administrador da conta para uma assinatura do Azure, você pode usar o hello Azure cobrança serviço Alerta alertas de cobrança toocreate personalizado que ajudam a monitorar e gerenciar a atividade de cobrança para suas contas do Azure.</span><span class="sxs-lookup"><span data-stu-id="91cc3-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="91cc3-106">Esse serviço é na visualização, portanto, você precisa tooenable-lo na página de recursos de visualização de saudação primeiro.</span><span class="sxs-lookup"><span data-stu-id="91cc3-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="91cc3-107">Definir Olá alertas limite e destinatários de email</span><span class="sxs-lookup"><span data-stu-id="91cc3-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="91cc3-108">Visite [página de recursos de visualização de saudação](https://account.windowsazure.com/PreviewFeatures) e habilitar **serviço de alerta de cobrança**.</span><span class="sxs-lookup"><span data-stu-id="91cc3-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="91cc3-109">Após receber a confirmação de email de Olá Olá serviço de cobrança é ativado para sua assinatura, visite [página de assinaturas Olá](https://account.windowsazure.com/Subscriptions) no portal de conta hello.</span><span class="sxs-lookup"><span data-stu-id="91cc3-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="91cc3-110">Clique na assinatura Olá você deseja toomonitor e, em seguida, clique em **alertas**.</span><span class="sxs-lookup"><span data-stu-id="91cc3-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Captura de tela da exibição de assinaturas de saudação do Centro de conta do Azure, com alertas realçado][Image1]

2. <span data-ttu-id="91cc3-112">Em seguida, clique em **adicionar alerta** toocreate o primeiro deles.</span><span class="sxs-lookup"><span data-stu-id="91cc3-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="91cc3-113">Você pode definir um total de cinco alertas de cobrança por assinatura, com um limite diferente e até tootwo destinatários de email para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="91cc3-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Captura de tela da saudação exibir alertas, onde você pode adicionar alerta][Image2]

3. <span data-ttu-id="91cc3-115">Quando você adiciona um alerta, dê a ele um nome exclusivo, escolha um limite de gasto e escolha Olá endereços de email onde os alertas são enviados.</span><span class="sxs-lookup"><span data-stu-id="91cc3-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="91cc3-116">Ao configurar o limite de saudação, você pode escolher um **Total de cobrança** ou um **crédito monetário** de saudação **alerta para** lista.</span><span class="sxs-lookup"><span data-stu-id="91cc3-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="91cc3-117">Para um total de cobrança, um alerta é enviado quando o gasto da assinatura excede o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="91cc3-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="91cc3-118">Para um crédito monetário, um alerta é enviado quando os créditos monetários caem abaixo do limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="91cc3-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="91cc3-119">Créditos monetários geralmente se aplicam a assinaturas de avaliação e o Visual Studio tooFree.</span><span class="sxs-lookup"><span data-stu-id="91cc3-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Captura de tela de modo de exibição de alerta de adição de hello, onde você pode configurar os destinatários][Image3]

<span data-ttu-id="91cc3-121">O Azure suporta qualquer endereço de email mas não verifique se o endereço de email Olá funciona, portanto, verifique erros de digitação.</span><span class="sxs-lookup"><span data-stu-id="91cc3-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="91cc3-122">Verificar os seus alertas</span><span class="sxs-lookup"><span data-stu-id="91cc3-122">Check on your alerts</span></span>
<span data-ttu-id="91cc3-123">Depois de configurar alertas, Olá Centro de contas lista e mostra quantos mais você pode configurar.</span><span class="sxs-lookup"><span data-stu-id="91cc3-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="91cc3-124">Para cada alerta, você pode ver Olá data e hora de envio, se é um alerta do Total de cobrança ou crédito monetário e limite Olá que você configurar.</span><span class="sxs-lookup"><span data-stu-id="91cc3-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="91cc3-125">formato de data e hora da saudação é 24 horas Hora Universal coordenada (UTC) e data de saudação é o formato aaaa-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="91cc3-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="91cc3-126">Clique Olá além de assiná-lo para um alerta no hello lista tooedit ou Olá Lixeira toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="91cc3-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="91cc3-127">Alertas de cobrança para clientes do EA (Enterprise Agreement)</span><span class="sxs-lookup"><span data-stu-id="91cc3-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="91cc3-128">Os clientes do EA podem obter alertas para cada departamento em um registro configurando cotas de gasto.</span><span class="sxs-lookup"><span data-stu-id="91cc3-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="91cc3-129">Consulte [departamento gastos cotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) em tooget portal de EA Olá iniciado.</span><span class="sxs-lookup"><span data-stu-id="91cc3-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="91cc3-130">Saiba mais sobre o gerenciamento de custos do Azure</span><span class="sxs-lookup"><span data-stu-id="91cc3-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="91cc3-131">Estimar os custos usando Olá [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/), [custo total de cálculo de propriedade](https://aka.ms/azure-tco-calculator), e quando você adiciona um serviço.</span><span class="sxs-lookup"><span data-stu-id="91cc3-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="91cc3-132">[Analise o uso e os custos regularmente no Portal do Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="91cc3-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="91cc3-133">Ative [Recomendações de custo do Assistente do Azure](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="91cc3-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="91cc3-134">mais, consulte toolearn [orientações sobre o gerenciamento de custos do Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="91cc3-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
