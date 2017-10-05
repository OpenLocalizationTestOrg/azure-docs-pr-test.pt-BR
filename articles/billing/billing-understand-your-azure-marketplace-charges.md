---
title: "Entenda os encargos dos serviços externos do Azure | Microsoft Docs"
description: "Saiba mais sobre a cobrança de serviços externos, anteriormente conhecidos como Marketplace, no Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="11a30-103">Entender a cobrança do Azure de encargos de serviços externos</span><span class="sxs-lookup"><span data-stu-id="11a30-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="11a30-104">Os serviços externos costumavam ser chamados de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="11a30-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="11a30-105">Em geral, eles são os serviços publicados por terceiros disponíveis para o Azure, mas que são totalmente integrados no Azure.</span><span class="sxs-lookup"><span data-stu-id="11a30-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="11a30-106">Por exemplo, ClearDB e SendGrid são serviços externos que você pode adquirir no Azure, mas não são publicados pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="11a30-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="11a30-107">Quando você provisiona um novo recurso ou serviço externo, um aviso é exibido:</span><span class="sxs-lookup"><span data-stu-id="11a30-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Aviso de compra no Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="11a30-109">Os serviços externos são publicados por empresas que não são a Microsoft, embora, às vezes, produtos da Microsoft também sejam categorizados como serviços externos.</span><span class="sxs-lookup"><span data-stu-id="11a30-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="11a30-110">Como os serviços externos são cobrados</span><span class="sxs-lookup"><span data-stu-id="11a30-110">How external services are billed</span></span>
- <span data-ttu-id="11a30-111">Os serviços externos são cobrados separadamente.</span><span class="sxs-lookup"><span data-stu-id="11a30-111">External services are billed separately.</span></span> <span data-ttu-id="11a30-112">Eles são tratados como pedidos individuais dentro da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="11a30-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="11a30-113">O período de cobrança para cada serviço é definido quando você adquire o serviço.</span><span class="sxs-lookup"><span data-stu-id="11a30-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="11a30-114">Ele não deve ser confundido com o período de cobrança da assinatura sob a qual você fez a compra.</span><span class="sxs-lookup"><span data-stu-id="11a30-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="11a30-115">Você também recebe faturas separadas e seu cartão de crédito é cobrado separadamente.</span><span class="sxs-lookup"><span data-stu-id="11a30-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="11a30-116">Cada serviço externo tem um modelo de cobrança diferente.</span><span class="sxs-lookup"><span data-stu-id="11a30-116">Each external service has a different billing model.</span></span> <span data-ttu-id="11a30-117">Alguns serviços são pré-pagos, enquanto outros usam um modelo baseado em pagamento mensal.</span><span class="sxs-lookup"><span data-stu-id="11a30-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="11a30-118">Você precisa de um cartão de crédito para os serviços externos do Azure. Não é possível adquirir serviços externos com pagamento por fatura.</span><span class="sxs-lookup"><span data-stu-id="11a30-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="11a30-119">Não é possível usar créditos gratuitos mensais para serviços externos.</span><span class="sxs-lookup"><span data-stu-id="11a30-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="11a30-120">Se você estiver usando uma assinatura do Azure que inclua [créditos gratuitos](https://azure.microsoft.com/pricing/spending-limits/), eles não poderão ser aplicados a faturas de serviços externos.</span><span class="sxs-lookup"><span data-stu-id="11a30-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="11a30-121">Use um cartão de crédito para adquirir serviços externos.</span><span class="sxs-lookup"><span data-stu-id="11a30-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="11a30-122">Exibir o histórico e os gastos com serviços externos no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="11a30-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="11a30-123">Você pode exibir uma lista dos serviços externos que estão em cada assinatura no [Portal do Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="11a30-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="11a30-124">Entre no [Portal do Azure](https://portal.azure.com/) como administrador da conta.</span><span class="sxs-lookup"><span data-stu-id="11a30-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="11a30-125">No menu Hub, selecione **Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="11a30-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![No menu Hub, selecione Assinaturas](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="11a30-127">Na folha **Assinaturas**, selecione a assinatura que você deseja exibir e selecione **Serviços externos**.</span><span class="sxs-lookup"><span data-stu-id="11a30-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Selecione uma assinatura na folha de cobrança](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="11a30-129">Você deve ver cada um de seus pedidos de serviços externos, o nome do publicador, a camada de serviço adquirida, o nome que você deu ao recurso e o status atual do pedido.</span><span class="sxs-lookup"><span data-stu-id="11a30-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="11a30-130">Para ver as faturas anteriores, selecione um serviço externo.</span><span class="sxs-lookup"><span data-stu-id="11a30-130">To see past bills, select an external service.</span></span>
   
    ![Selecione um serviço externo](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="11a30-132">A partir daqui, você pode exibir os valores de faturas anteriores, incluindo o detalhamento dos impostos.</span><span class="sxs-lookup"><span data-stu-id="11a30-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Exibir histórico de cobrança de serviços externos](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="11a30-134">Exibir gastos com serviços externos para clientes do Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="11a30-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="11a30-135">Os clientes do EA podem visualizar os gastos de serviços externos e baixar relatórios no portal do EA.</span><span class="sxs-lookup"><span data-stu-id="11a30-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="11a30-136">Consulte [Azure Marketplace para clientes do EA](https://ea.azure.com/helpdocs/azureMarketplace) para começar.</span><span class="sxs-lookup"><span data-stu-id="11a30-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="11a30-137">Gerenciar formas de pagamento para pedidos de serviços externos</span><span class="sxs-lookup"><span data-stu-id="11a30-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="11a30-138">Atualize suas formas de pagamento para pedidos de serviços externos no [Centro de Contas](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="11a30-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="11a30-139">Se você adquiriu sua assinatura com uma conta Corporativa ou de Estudante, [contate o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para fazer alterações na forma de pagamento.</span><span class="sxs-lookup"><span data-stu-id="11a30-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="11a30-140">Entre no [Centro de Contas](https://account.windowsazure.com/) e [navegue até a guia **marketplace**](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="11a30-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Selecione marketplace no centro de contas](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="11a30-142">Selecione o serviço externo que você deseja gerenciar</span><span class="sxs-lookup"><span data-stu-id="11a30-142">Select the external service you want to manage</span></span>
   
    ![Selecione o serviço externo que você deseja gerenciar](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="11a30-144">Clique em **Alterar forma de pagamento** no lado direito da página.</span><span class="sxs-lookup"><span data-stu-id="11a30-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="11a30-145">Este link leva você a um portal diferente para gerenciar sua forma de pagamento.</span><span class="sxs-lookup"><span data-stu-id="11a30-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Resumo do pedido](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="11a30-147">Clique em **Editar informações** e siga as instruções para atualizar suas informações de pagamento.</span><span class="sxs-lookup"><span data-stu-id="11a30-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Selecione editar informações](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="11a30-149">Cancelar pedido de serviço externo</span><span class="sxs-lookup"><span data-stu-id="11a30-149">Cancel an external service order</span></span>
<span data-ttu-id="11a30-150">Se você deseja cancelar seu pedido de serviço externo, exclua o recurso no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11a30-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Excluir recurso](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="11a30-152">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="11a30-152">Need help?</span></span> <span data-ttu-id="11a30-153">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="11a30-153">Contact support.</span></span>
<span data-ttu-id="11a30-154">Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.</span><span class="sxs-lookup"><span data-stu-id="11a30-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

