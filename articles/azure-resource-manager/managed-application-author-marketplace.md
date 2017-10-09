---
title: "aaaAzure gerenciados aplicativos Olá Marketplace | Microsoft Docs"
description: "Descreve o Azure aplicativos gerenciados que estão disponíveis por meio de saudação Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="2a6d6-103">Aplicativos no hello Marketplace de gerenciado do Azure</span><span class="sxs-lookup"><span data-stu-id="2a6d6-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="2a6d6-104">MSPs, ISVs e integradores de sistema (SIs) podem usar aplicativos toooffer gerenciado do Azure aos clientes do Azure Marketplace de tooall soluções.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="2a6d6-105">Essas soluções reduzem manutenção hello e sobrecarga de manutenção para os clientes.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="2a6d6-106">Editores podem vender infraestrutura e software por meio de saudação Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="2a6d6-107">Eles podem anexar suporte operacional toomanaged aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="2a6d6-108">Para saber mais, consulte [Visão geral do aplicativo gerenciado](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="2a6d6-109">Este artigo explica como um MSP, ISV ou SI pode publicar um aplicativo toohello Marketplace e torná-lo toocustomers amplamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="2a6d6-110">Pré-requisitos para publicar um aplicativo gerenciado</span><span class="sxs-lookup"><span data-stu-id="2a6d6-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="2a6d6-111">Pré-requisitos toolisting em Olá Marketplace:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="2a6d6-112">Técnicos</span><span class="sxs-lookup"><span data-stu-id="2a6d6-112">Technical</span></span>

    *  <span data-ttu-id="2a6d6-113">Para obter informações sobre a estrutura básica de saudação e a sintaxe de modelos do Azure Resource Manager, consulte [modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="2a6d6-114">soluções de modelo completa tooview, consulte [modelos de início rápido do Azure](https://azure.microsoft.com/en-us/documentation/templates/) ou hello [repositório de modelos de início rápido](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="2a6d6-115">Para obter informações sobre como toocreate Olá interface para os clientes que implantar seu aplicativo por meio de saudação Marketplace, consulte [criar um arquivo de definição de interface do usuário](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="2a6d6-116">Não técnico (requisitos de negócios)</span><span class="sxs-lookup"><span data-stu-id="2a6d6-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="2a6d6-117">Sua empresa ou a sua subsidiária deve estar localizada em um país onde as vendas são suportadas pelo Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="2a6d6-118">O produto deve ser licenciado de forma que seja compatível com modelos de cobrança com suporte Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="2a6d6-119">Você é responsável para fazer toocustomers de suporte técnico disponíveis de forma comercialmente razoável.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="2a6d6-120">suporte de saudação pode ser gratuito, paga, ou por meio da comunidade de suporte.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="2a6d6-121">Você é responsável pelo licenciamento do software e quaisquer dependências de software de terceiros.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="2a6d6-122">Você deve fornecer o conteúdo que atenda aos critérios para sua oferta toobe listados no hello Marketplace e no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="2a6d6-123">Você deve aceitar os termos de toohello de saudação do Azure Marketplace participação políticas e contrato do publicador.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="2a6d6-124">Você deve concordar toocomply com hello termos de uso, declaração de privacidade da Microsoft e contrato de programa de certificados do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="2a6d6-125">Criar uma nova oferta de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2a6d6-125">Create a new Azure application offer</span></span>

<span data-ttu-id="2a6d6-126">Depois que você atenda aos pré-requisitos de hello, você está pronto toocreate sua oferta do aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="2a6d6-127">Vamos analisar rapidamente uma visão geral de uma oferta e um SKU.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="2a6d6-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="2a6d6-128">Offer</span></span>

<span data-ttu-id="2a6d6-129">oferta de saudação de um aplicativo gerenciado corresponde classe tooa do produto da oferta do publicador.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="2a6d6-130">Se você tiver um novo tipo de solução/aplicativo que você deseja toomake disponível no hello Marketplace, você pode configurá-lo como uma oferta nova.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="2a6d6-131">Uma oferta é uma coleção de SKUs.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="2a6d6-132">Cada oferta aparece como sua própria entidade em Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="2a6d6-133">SKU</span><span class="sxs-lookup"><span data-stu-id="2a6d6-133">SKU</span></span>

<span data-ttu-id="2a6d6-134">Um SKU é Olá menor podem ser comprados unidade de uma oferta.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="2a6d6-135">Você pode usar um SKU dentro Olá mesmo toodifferentiate de classe (oferta) de produto entre:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="2a6d6-136">Diferentes recursos com suporte.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-136">Different features that are supported.</span></span>
* <span data-ttu-id="2a6d6-137">Se a oferta de saudação é gerenciada ou não.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="2a6d6-138">Modelos de cobrança com suporte.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-138">Billing models that are supported.</span></span>

<span data-ttu-id="2a6d6-139">Um SKU aparece sob Olá pai oferta no hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="2a6d6-140">Ele aparecerá como sua própria entidade pode ser adquirida em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="2a6d6-141">Configurar uma oferta</span><span class="sxs-lookup"><span data-stu-id="2a6d6-141">Set up an offer</span></span>

1. <span data-ttu-id="2a6d6-142">Entrar toohello [portal Cloud Partner](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="2a6d6-143">No painel de navegação Olá Olá esquerda, selecione **+ nova oferta** > **aplicativos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nova oferta](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="2a6d6-145">Preencher formulários Olá que aparecem no hello deixado no hello **Editor** exibição.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="2a6d6-146">Os campos obrigatórios estão marcados com um asterisco vermelho (*).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Configurações da oferta](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="2a6d6-148">Quatro formulários principais são usado toocreate um aplicativo gerenciado:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="2a6d6-149">a.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-149">a.</span></span> <span data-ttu-id="2a6d6-150">Configurações da oferta</span><span class="sxs-lookup"><span data-stu-id="2a6d6-150">Offer Settings</span></span>

    <span data-ttu-id="2a6d6-151">b.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-151">b.</span></span> <span data-ttu-id="2a6d6-152">SKUs</span><span class="sxs-lookup"><span data-stu-id="2a6d6-152">SKUs</span></span>

    <span data-ttu-id="2a6d6-153">c.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-153">c.</span></span> <span data-ttu-id="2a6d6-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="2a6d6-154">Marketplace</span></span>

    <span data-ttu-id="2a6d6-155">d.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-155">d.</span></span> <span data-ttu-id="2a6d6-156">Suporte</span><span class="sxs-lookup"><span data-stu-id="2a6d6-156">Support</span></span>

<span data-ttu-id="2a6d6-157">Esses formulários são descritos mais detalhadamente nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="2a6d6-158">Formulário de Configurações de Oferta</span><span class="sxs-lookup"><span data-stu-id="2a6d6-158">Offer Settings form</span></span>
<span data-ttu-id="2a6d6-159">Use configurações de oferta este formulário básico toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="2a6d6-160">Preencha Olá **oferecem configurações** formulário.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="2a6d6-161">campos diferentes Olá são:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-161">hello different fields are:</span></span>

    <span data-ttu-id="2a6d6-162">a.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-162">a.</span></span> <span data-ttu-id="2a6d6-163">**ID da oferta**: este identificador exclusivo identifica oferta hello dentro de um perfil do publicador.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="2a6d6-164">Essa ID está visível em URLs de produto, modelos do Resource Manager e relatórios de cobrança.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="2a6d6-165">Ele só pode ser composto de caracteres alfanuméricos minúsculos ou traços (-).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="2a6d6-166">Olá ID não pode terminar com um traço.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="2a6d6-167">Ele é limitado tooa máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="2a6d6-168">Após a ativação da oferta, esse campo é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="2a6d6-169">b.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-169">b.</span></span> <span data-ttu-id="2a6d6-170">**ID do editor**: Use esse perfil de publicador lista suspensa toochoose Olá deseja toopublish esta oferta em.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="2a6d6-171">Após a ativação da oferta, esse campo é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="2a6d6-172">c.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-172">c.</span></span> <span data-ttu-id="2a6d6-173">**Nome**: este nome para exibição para sua oferta aparece no hello Marketplace e no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="2a6d6-174">Ele pode ter um máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="2a6d6-175">Inclua um nome de marca reconhecível para o seu produto.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="2a6d6-176">Não inclua o nome de sua empresa aqui, a menos que seja a maneira como ela é comercializada.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="2a6d6-177">Se você estiver marketing esta oferta em seu próprio site, certifique-se de que o nome hello seja exatamente como ela aparece no seu site.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="2a6d6-178">Selecione **salvar** toosave seu progresso.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="2a6d6-179">Formulário de SKUs</span><span class="sxs-lookup"><span data-stu-id="2a6d6-179">SKUs form</span></span>
<span data-ttu-id="2a6d6-180">Olá próxima etapa é tooadd SKUs para sua oferta.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="2a6d6-181">Selecione **SKUs** > **Novo SKU**.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Selecionar novo SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="2a6d6-183">Insira uma **ID de SKU**.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="2a6d6-184">Uma ID de SKU é um identificador exclusivo para Olá SKU dentro de uma oferta.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="2a6d6-185">Essa ID está visível em URLs de produto, modelos do Resource Manager e relatórios de cobrança.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="2a6d6-186">Ele só pode ser composto de caracteres alfanuméricos minúsculos ou traços (-).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="2a6d6-187">Olá ID não pode terminar com um traço e é limitado tooa máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="2a6d6-188">Após a ativação da oferta, esse campo é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="2a6d6-189">Pode existir várias SKUs em uma oferta.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="2a6d6-190">Você precisa de uma SKU de cada imagem de plano de toopublish.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="2a6d6-191">Preencha Olá **detalhes de SKU** seção Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Fornecer novo SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="2a6d6-193">Preencha Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="2a6d6-194">a.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-194">a.</span></span> <span data-ttu-id="2a6d6-195">**Título**: insira um título para esse SKU.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="2a6d6-196">Esse título aparece na Galeria de saudação para este item.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="2a6d6-197">b.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-197">b.</span></span> <span data-ttu-id="2a6d6-198">**Resumo**: insira um breve resumo para esse SKU.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="2a6d6-199">Esse texto aparece sob o título de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="2a6d6-200">c.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-200">c.</span></span> <span data-ttu-id="2a6d6-201">**Descrição**: insira uma descrição detalhada sobre Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="2a6d6-202">d.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-202">d.</span></span> <span data-ttu-id="2a6d6-203">**Tipo de SKU**: Olá valores permitidos são **aplicativo gerenciado** e **modelos de solução**.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="2a6d6-204">Nesse caso, selecione **Aplicativo Gerenciado**.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="2a6d6-205">Preencha Olá **detalhes do pacote** seção Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Pacote](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="2a6d6-207">Preencha Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="2a6d6-208">a.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-208">a.</span></span> <span data-ttu-id="2a6d6-209">**Versão atual**: insira uma versão para o pacote de saudação carregar.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="2a6d6-210">Ele deve estar no formato de saudação `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="2a6d6-211">b.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-211">b.</span></span> <span data-ttu-id="2a6d6-212">**Selecione um arquivo de pacote**: Este pacote contém os seguintes arquivos compactados em um arquivo. zip de saudação:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="2a6d6-213">**applianceMainTemplate.json**: arquivo de modelo de implantação de saudação que tenha usado o aplicativo da solução toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="2a6d6-214">Para obter informações sobre como toocreate arquivos de modelo de implantação, consulte [criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="2a6d6-215">**appliancecreateUIDefinition.json**: este arquivo é usado pelo Olá toogenerate portal do Azure Olá interface do usuário que tenha usado tooprovision essa solução/aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="2a6d6-216">Para saber mais, consulte [Introdução a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="2a6d6-217">**mainTemplate.json**: este arquivo de modelo contém apenas os recursos de Microsoft.Solution/appliances hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="2a6d6-218">arquivo de mainTemplate Olá inclui Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="2a6d6-219">**tipo**: Use **Marketplace** para aplicativos gerenciados no hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="2a6d6-220">**ManagedResourceGroupId**: este grupo de recursos na assinatura saudação do cliente é onde todos os recursos de saudação definidos no applianceMainTemplate.json são implantados.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="2a6d6-221">**PublisherPackageId**: esta cadeia de caracteres identifica com exclusividade o pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="2a6d6-222">Fornecer valor Olá no formato de saudação do `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="2a6d6-223">Obter Olá **ID oferecem** e **ID do editor** de saudação publicação portal, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![ID da oferta](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="2a6d6-225">Obter Olá **ID do SKU**, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![Id do SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="2a6d6-227">Obter pacote hello **versão**, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Versão do pacote](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="2a6d6-229">Com base em Olá anterior exemplos, Olá valor **PublisherPackageId** é `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="2a6d6-230">Exemplo de mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="2a6d6-231">Este pacote deve conter todos os outros modelos aninhados ou scripts que são necessário toosuccessfully provisionar este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="2a6d6-232">Olá arquivos mainTemplate.json, applianceMainTemplate.json e applianceCreateUIDefinition.json devem estar presentes na pasta raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="2a6d6-233">**Autorizações**: esta propriedade define que obtém acesso e hello nível de acesso a recursos de toohello em assinaturas de clientes.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="2a6d6-234">publicador de saudação pode usá-lo aplicativo hello de toomanage em nome do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="2a6d6-235">**PrincipalId**: esta propriedade é o identificador do hello Azure Active Directory (AD do Azure) de um usuário, grupo de usuários ou aplicativos que concedeu permissões específicas nos recursos Olá Olá a assinatura de cliente.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="2a6d6-236">saudação de definição de função descreve as permissões de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="2a6d6-237">**Definição de função**: esta propriedade é uma lista de todos os hello controle de acesso baseado em função (RBAC) funções internas fornecidas pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="2a6d6-238">Você pode selecionar a função hello que é mais apropriados recursos de saudação do toomanage toouse em nome do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="2a6d6-239">É possível adicionar várias autorizações.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-239">You can add multiple authorizations.</span></span> <span data-ttu-id="2a6d6-240">Recomendamos que você crie um grupo de usuários do AD e especifica sua ID em **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="2a6d6-241">Dessa forma, você pode adicionar mais grupo de usuário toohello usuários sem a necessidade de Olá tooupdate Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="2a6d6-242">Para obter mais informações sobre o RBAC, consulte [Introdução ao RBAC no portal do Azure de saudação](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="2a6d6-243">Formulário do Marketplace</span><span class="sxs-lookup"><span data-stu-id="2a6d6-243">Marketplace form</span></span>

<span data-ttu-id="2a6d6-244">Olá formulário Marketplace solicita para os campos que aparecem na Olá [Azure Marketplace](https://azuremarketplace.microsoft.com) e Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="2a6d6-245">IDs de assinatura para versão prévia</span><span class="sxs-lookup"><span data-stu-id="2a6d6-245">Preview subscription IDs</span></span>

<span data-ttu-id="2a6d6-246">Insira uma lista de IDs que podem acessar a oferta de saudação após a publicação de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="2a6d6-247">Você pode usar esses oferta de saudação visualizada tootest assinaturas listadas em branco antes de você fazê-lo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="2a6d6-248">Você pode compilar uma lista de permissões de backup too100 assinaturas no portal de parceiros de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="2a6d6-249">Categorias sugeridas</span><span class="sxs-lookup"><span data-stu-id="2a6d6-249">Suggested categories</span></span>

<span data-ttu-id="2a6d6-250">Selecione as categorias de toofive da lista de saudação que sua oferta pode ser associada ao melhor.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="2a6d6-251">Essas categorias é usado toomap suas categorias de produtos de toohello de oferta que estão disponíveis no hello [Azure Marketplace](https://azuremarketplace.microsoft.com) e hello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="2a6d6-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2a6d6-252">Azure Marketplace</span></span>

<span data-ttu-id="2a6d6-253">Resumo de saudação do seu aplicativo gerenciado exibe Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-253">hello summary of your managed application displays hello following fields:</span></span>

![Resumo do marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="2a6d6-255">Olá **visão geral** guia de seu aplicativo gerenciado exibe Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Visão geral do Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="2a6d6-257">Olá **planos + preços** guia de seu aplicativo gerenciado exibe Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Planos do marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="2a6d6-259">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2a6d6-259">Azure portal</span></span>

<span data-ttu-id="2a6d6-260">Resumo de saudação do seu aplicativo gerenciado exibe Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-260">hello summary of your managed application displays hello following fields:</span></span>

![Resumo do portal](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="2a6d6-262">Visão geral de saudação do seu aplicativo gerenciado exibe Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-262">hello overview for your managed application displays hello following fields:</span></span>

![Visão geral do portal](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="2a6d6-264">Diretrizes de logotipo</span><span class="sxs-lookup"><span data-stu-id="2a6d6-264">Logo guidelines</span></span>

<span data-ttu-id="2a6d6-265">Siga estas diretrizes para qualquer logotipo que você carrega no portal de parceiros de nuvem de saudação:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="2a6d6-266">Olá design do Azure tem uma paleta de cores simples.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="2a6d6-267">Limitar o número de saudação do primário e secundário cores no logotipo.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="2a6d6-268">cores de tema de saudação do portal de saudação são brancas e preto.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="2a6d6-269">Não use essas cores como cores de plano de fundo Olá do seu logotipo.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="2a6d6-270">Use uma cor que torna seu logotipo proeminente no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="2a6d6-271">É recomendável usar cores primárias simples.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-271">We recommend simple primary colors.</span></span> <span data-ttu-id="2a6d6-272">*Se você usar um plano de fundo transparente, certifique-se de Olá logotipo e o texto não estiverem em branco, preto ou azul.*</span><span class="sxs-lookup"><span data-stu-id="2a6d6-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="2a6d6-273">Não use uma cor de fundo do logotipo hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="2a6d6-274">Não coloque o texto no logotipo hello, nem mesmo sua empresa ou o nome da marca.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="2a6d6-275">Olá aparência de seu logotipo deve ser simples e evitar gradientes.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="2a6d6-276">Certifique-se de logotipo Olá não está ampliado.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="2a6d6-277">Logotipo Hero</span><span class="sxs-lookup"><span data-stu-id="2a6d6-277">Hero logo</span></span>

<span data-ttu-id="2a6d6-278">logotipo do Hello herói é opcional.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-278">hello hero logo is optional.</span></span> <span data-ttu-id="2a6d6-279">publicador de saudação pode escolher não tooupload um logotipo herói.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="2a6d6-280">Depois que o ícone de herói Olá é carregado, ele não pode ser excluído.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="2a6d6-281">Nesse momento, parceiro Olá deve seguir diretrizes de mercado Olá para ícones herói.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="2a6d6-282">Siga estas diretrizes para o ícone do logotipo herói hello:</span><span class="sxs-lookup"><span data-stu-id="2a6d6-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="2a6d6-283">nome de exibição do publicador Hello, título de plano hello e resumo longo de oferta de saudação são exibidos em branco.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="2a6d6-284">Portanto, não use uma cor clara para plano de fundo de saudação do ícone de herói hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="2a6d6-285">Não há permissão para telas de fundo pretas, brancas ou transparentes para ícones hero.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="2a6d6-286">Depois de oferta Olá estiver listada, publisher Olá nome para exibição, título do plano de saudação, resumo longo de oferta hello e Olá **criar** botão são inserido programaticamente no logotipo de herói hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="2a6d6-287">Consequentemente, não digite qualquer texto enquanto você projeta o logotipo de herói hello.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="2a6d6-288">Deixe espaço vazio do hello direita como texto de saudação está incluído programaticamente nesse espaço.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="2a6d6-289">um espaço vazio para o texto de saudação Olá deve ser 415 x 100 pixels saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="2a6d6-290">Ele tem um deslocamento de 370 pixels da saudação esquerda.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-290">It's offset by 370 pixels from hello left.</span></span>

    ![Exemplo de logotipo hero](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="2a6d6-292">Formulário de suporte</span><span class="sxs-lookup"><span data-stu-id="2a6d6-292">Support form</span></span>

<span data-ttu-id="2a6d6-293">Preencha Olá **suporte** entra em contato com o formulário com o suporte da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="2a6d6-294">Essas informações podem ser de contatos da engenharia e do atendimento ao cliente.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="2a6d6-295">Publicar uma oferta</span><span class="sxs-lookup"><span data-stu-id="2a6d6-295">Publish an offer</span></span>

<span data-ttu-id="2a6d6-296">Depois de preencher todas as seções de saudação, selecione **publicar** toostart processo de saudação que torna seu toocustomers disponíveis da oferta.</span><span class="sxs-lookup"><span data-stu-id="2a6d6-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a6d6-297">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a6d6-297">Next steps</span></span>

* <span data-ttu-id="2a6d6-298">Para aplicativos de toomanaged uma introdução, consulte [visão geral do aplicativo gerenciado](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2a6d6-299">Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="2a6d6-300">Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="2a6d6-301">Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="2a6d6-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
