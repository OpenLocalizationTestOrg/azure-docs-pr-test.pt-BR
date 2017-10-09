---
title: "detalhes de contato de segurança aaaProvide na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como segurança tooprovide contatar detalhes na Central de segurança do Azure."
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
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="66c2f-103">Fornecer detalhes de contato de segurança na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="66c2f-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="66c2f-104">A Central de Segurança do Azure recomendará que você forneça detalhes de contato de segurança para sua assinatura do Azure se ainda não fez isso.</span><span class="sxs-lookup"><span data-stu-id="66c2f-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="66c2f-105">Essa informação será usada pelo Microsoft toocontact se Olá Microsoft Security Response Center (MSRC) descobre que seu cliente tiver sido acessado por uma parte ilegal ou não autorizada.</span><span class="sxs-lookup"><span data-stu-id="66c2f-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="66c2f-106">MSRC executa selecione segurança monitoramento de saudação rede do Azure e a infraestrutura e recebe reclamações abuso e de inteligência de ameaça de terceiros.</span><span class="sxs-lookup"><span data-stu-id="66c2f-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="66c2f-107">Uma notificação por email seja enviada na Olá primeiro diário ocorrência de um alerta e apenas para alertas de gravidade.</span><span class="sxs-lookup"><span data-stu-id="66c2f-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="66c2f-108">As preferências de email só podem ser configuradas para políticas de assinatura.</span><span class="sxs-lookup"><span data-stu-id="66c2f-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="66c2f-109">Grupos de recursos dentro de uma assinatura herdarão essas configurações.</span><span class="sxs-lookup"><span data-stu-id="66c2f-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="66c2f-110">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="66c2f-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="66c2f-111">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="66c2f-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="66c2f-112">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="66c2f-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="66c2f-113">Em Olá **recomendações** folha, selecione **fornecer detalhes de contato de segurança**.</span><span class="sxs-lookup"><span data-stu-id="66c2f-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="66c2f-114">![Fornecer contato de segurança][1]</span><span class="sxs-lookup"><span data-stu-id="66c2f-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="66c2f-115">Isso abre a folha de saudação **fornecer detalhes de contato de segurança**.</span><span class="sxs-lookup"><span data-stu-id="66c2f-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="66c2f-116">Selecione informações de contato tooprovide do hello assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="66c2f-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="66c2f-117">![Fornecer detalhes de contato de segurança][2]</span><span class="sxs-lookup"><span data-stu-id="66c2f-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="66c2f-118">Uma segunda folha **Fornecer detalhes de contato de segurança** será aberta.</span><span class="sxs-lookup"><span data-stu-id="66c2f-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="66c2f-119">Insira o endereço de email de contato de segurança hello ou endereços separados por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="66c2f-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="66c2f-120">Não é um número de toohello limite de endereços de email que você pode inserir.</span><span class="sxs-lookup"><span data-stu-id="66c2f-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="66c2f-121">Insira um número de telefone internacional de contato de segurança.</span><span class="sxs-lookup"><span data-stu-id="66c2f-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="66c2f-122">tooreceive emails sobre alertas de gravidade, ative a opção de saudação **enviar-me emails sobre alertas**.</span><span class="sxs-lookup"><span data-stu-id="66c2f-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="66c2f-123">Olá futuro, você terá os proprietários de toosubscription de notificações de email toosend de opção hello.</span><span class="sxs-lookup"><span data-stu-id="66c2f-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="66c2f-124">Esta opção está esmaecida no momento.</span><span class="sxs-lookup"><span data-stu-id="66c2f-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="66c2f-125">Selecione **Okey** tooapply segurança de saudação entre em contato com assinatura de tooyour de informações.</span><span class="sxs-lookup"><span data-stu-id="66c2f-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="66c2f-126">Consulte também</span><span class="sxs-lookup"><span data-stu-id="66c2f-126">See also</span></span>
<span data-ttu-id="66c2f-127">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="66c2f-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="66c2f-128">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="66c2f-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="66c2f-129">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="66c2f-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="66c2f-130">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="66c2f-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="66c2f-131">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="66c2f-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="66c2f-132">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="66c2f-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="66c2f-133">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="66c2f-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="66c2f-134">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="66c2f-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
