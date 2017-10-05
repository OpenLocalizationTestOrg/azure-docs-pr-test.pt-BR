---
title: "Configurar alertas de cobrança ou de crédito para assinaturas do Azure | Microsoft Docs"
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
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="d0b79-104">Configurar alertas de cobrança ou de crédito para assinaturas do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d0b79-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="d0b79-105">Caso seja o Administrador da Conta de uma assinatura do Azure, você poderá usar o Serviço de Alerta de Cobrança do Azure para criar alertas personalizados de cobrança que ajudam a monitorar e gerenciar a atividade de cobrança de suas contas do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0b79-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="d0b79-106">Esse serviço está no modo preview, de modo que você precisa habilitá-lo primeiro na página Recursos do Preview.</span><span class="sxs-lookup"><span data-stu-id="d0b79-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="d0b79-107">Definir os alertas de limite e destinatários de email</span><span class="sxs-lookup"><span data-stu-id="d0b79-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="d0b79-108">Visite [a página Recursos do Preview](https://account.windowsazure.com/PreviewFeatures) e habilite **Serviço de Alerta de Cobrança**.</span><span class="sxs-lookup"><span data-stu-id="d0b79-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="d0b79-109">Depois de receber o email de confirmação de que o serviço de cobrança foi ativado para a sua assinatura, visite [a página Assinaturas](https://account.windowsazure.com/Subscriptions) no portal da conta.</span><span class="sxs-lookup"><span data-stu-id="d0b79-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="d0b79-110">Clique na assinatura que você deseja monitorar e, em seguida, clique em **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="d0b79-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Captura de tela da exibição de assinaturas do Centro de Contas do Azure, com Alertas realçado][Image1]

2. <span data-ttu-id="d0b79-112">Em seguida, clique em **Adicionar Alerta** para criar o primeiro.</span><span class="sxs-lookup"><span data-stu-id="d0b79-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="d0b79-113">Você pode configurar até cinco alertas de cobrança por assinatura, com um limite diferente e até dois destinatários de email para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="d0b79-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Captura de tela da exibição Alertas, na qual é possível adicionar alertas][Image2]

3. <span data-ttu-id="d0b79-115">Ao adicionar um alerta, você informa um nome exclusivo, escolhe um limite de gastos e escolhe os endereços de email para os quais os alertas serão enviados.</span><span class="sxs-lookup"><span data-stu-id="d0b79-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="d0b79-116">Ao configurar o limite, você pode escolher um **Total de cobrança** ou um **Crédito Monetário** na lista **Alerta para**.</span><span class="sxs-lookup"><span data-stu-id="d0b79-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="d0b79-117">Para total de cobrança, um alerta é enviado quando o gasto com a assinatura excede o limite.</span><span class="sxs-lookup"><span data-stu-id="d0b79-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="d0b79-118">Para crédito monetário, um alerta é enviado quando os créditos monetários reduzem abaixo do limite.</span><span class="sxs-lookup"><span data-stu-id="d0b79-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="d0b79-119">Créditos monetários geralmente se aplicam a assinaturas de Avaliação Gratuita e do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0b79-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Captura de tela da exibição de adição de alerta, na qual é possível configurar destinatários][Image3]

<span data-ttu-id="d0b79-121">O Azure é compatível com qualquer endereço de email, mas não verifica se este funciona, por isso, verifique atentamente se digitou corretamente.</span><span class="sxs-lookup"><span data-stu-id="d0b79-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="d0b79-122">Verificar os seus alertas</span><span class="sxs-lookup"><span data-stu-id="d0b79-122">Check on your alerts</span></span>
<span data-ttu-id="d0b79-123">Depois de configurar os alertas, o Centro de Contas lista e mostra quantos mais você pode configurar.</span><span class="sxs-lookup"><span data-stu-id="d0b79-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="d0b79-124">Para cada alerta, você verá a data e a hora de envio, se é um alerta do Total de Cobrança ou de Crédito Monetário e o limite definido.</span><span class="sxs-lookup"><span data-stu-id="d0b79-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="d0b79-125">O formato de data e hora é 24 horas - Hora Universal Coordenada (UTC) e a data usa o formato aaaa-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="d0b79-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="d0b79-126">Clique no sinal de adição de um alerta na lista para editá-lo ou clique na lixeira para excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="d0b79-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="d0b79-127">Alertas de cobrança para clientes do EA (Enterprise Agreement)</span><span class="sxs-lookup"><span data-stu-id="d0b79-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="d0b79-128">Os clientes do EA podem obter alertas para cada departamento em um registro configurando cotas de gasto.</span><span class="sxs-lookup"><span data-stu-id="d0b79-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="d0b79-129">Para começar, confira [Cotas de Gasto por Departamento](https://ea.azure.com/helpdocs/departmentSpendingQuotas) no portal do EA.</span><span class="sxs-lookup"><span data-stu-id="d0b79-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="d0b79-130">Saiba mais sobre o gerenciamento de custos do Azure</span><span class="sxs-lookup"><span data-stu-id="d0b79-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="d0b79-131">Faça uma estimativa dos custos usando a [calculadora de preços](https://azure.microsoft.com/pricing/calculator/), a [calculadora do custo total de propriedade](https://aka.ms/azure-tco-calculator) e quando você adiciona um serviço.</span><span class="sxs-lookup"><span data-stu-id="d0b79-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="d0b79-132">[Analise o uso e os custos regularmente no Portal do Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="d0b79-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="d0b79-133">Ative [Recomendações de custo do Assistente do Azure](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="d0b79-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="d0b79-134">Para saber mais, confira [Orientações sobre o gerenciamento de custos do Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0b79-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
