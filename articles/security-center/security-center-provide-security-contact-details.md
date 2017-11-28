---
title: "Fornecer detalhes de contato de segurança na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como fornecer detalhes de contato de segurança na Central de Segurança do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="40f06-103">Fornecer detalhes de contato de segurança na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="40f06-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="40f06-104">A Central de Segurança do Azure recomendará que você forneça detalhes de contato de segurança para sua assinatura do Azure se ainda não fez isso.</span><span class="sxs-lookup"><span data-stu-id="40f06-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="40f06-105">Essas informações serão usadas pela Microsoft para contatá-lo se o MSRC (Microsoft Security Response Center) descobrir que os dados do cliente têm sido acessados por uma pessoa não autorizada ou ilegal.</span><span class="sxs-lookup"><span data-stu-id="40f06-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="40f06-106">O MSRC executa determinado monitoramento de segurança da rede e da infraestrutura do Azure e recebe reclamações de inteligência e abuso de ameaça de terceiros.</span><span class="sxs-lookup"><span data-stu-id="40f06-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="40f06-107">Uma notificação por email é enviada na primeira ocorrência diária de um alerta e apenas para alertas de gravidade alta.</span><span class="sxs-lookup"><span data-stu-id="40f06-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="40f06-108">As preferências de email só podem ser configuradas para políticas de assinatura.</span><span class="sxs-lookup"><span data-stu-id="40f06-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="40f06-109">Grupos de recursos dentro de uma assinatura herdarão essas configurações.</span><span class="sxs-lookup"><span data-stu-id="40f06-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="40f06-110">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="40f06-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="40f06-111">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="40f06-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="40f06-112">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="40f06-112">Implement the recommendation</span></span>
1. <span data-ttu-id="40f06-113">Na folha **Recomendações**, selecione **Fornecer detalhes de contato de segurança**.</span><span class="sxs-lookup"><span data-stu-id="40f06-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="40f06-114">![Fornecer contato de segurança][1]</span><span class="sxs-lookup"><span data-stu-id="40f06-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="40f06-115">Isso abrirá a folha **Fornecer detalhes de contato de segurança**.</span><span class="sxs-lookup"><span data-stu-id="40f06-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="40f06-116">Selecione a assinatura do Azure para fornecer informações de contato em.</span><span class="sxs-lookup"><span data-stu-id="40f06-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="40f06-117">![forneça detalhes de contato de segurança][2]</span><span class="sxs-lookup"><span data-stu-id="40f06-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="40f06-118">Uma segunda folha **Fornecer detalhes de contato de segurança** será aberta.</span><span class="sxs-lookup"><span data-stu-id="40f06-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="40f06-119">Insira o endereço de email de contato de segurança ou endereços separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="40f06-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="40f06-120">Não há um limite para o número de endereços de email que você pode inserir.</span><span class="sxs-lookup"><span data-stu-id="40f06-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="40f06-121">Insira um número de telefone internacional de contato de segurança.</span><span class="sxs-lookup"><span data-stu-id="40f06-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="40f06-122">Para receber emails sobre alertas de gravidade alta, ative a opção **Enviar-me emails sobre alertas**.</span><span class="sxs-lookup"><span data-stu-id="40f06-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="40f06-123">Futuramente, você terá a opção de enviar notificações por email aos proprietários da assinatura.</span><span class="sxs-lookup"><span data-stu-id="40f06-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="40f06-124">Esta opção está esmaecida no momento.</span><span class="sxs-lookup"><span data-stu-id="40f06-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="40f06-125">Selecione **OK** para aplicar as informações de contato de segurança à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="40f06-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="40f06-126">Consulte também</span><span class="sxs-lookup"><span data-stu-id="40f06-126">See also</span></span>
<span data-ttu-id="40f06-127">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="40f06-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="40f06-128">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="40f06-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="40f06-129">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="40f06-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="40f06-130">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="40f06-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="40f06-131">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="40f06-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="40f06-132">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="40f06-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="40f06-133">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço de localização.</span><span class="sxs-lookup"><span data-stu-id="40f06-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="40f06-134">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="40f06-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
