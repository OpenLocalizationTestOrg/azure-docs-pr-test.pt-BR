---
title: Aplicativos gerenciados do Azure no Marketplace | Microsoft Docs
description: "Descreve os aplicativos gerenciados do Azure que estão disponíveis por meio do Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 58ac7665abf7e75a43bb0b92bdf6f41005c3efe8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="bdd5e-103">Aplicativos gerenciados do Azure no Marketplace</span><span class="sxs-lookup"><span data-stu-id="bdd5e-103">Azure managed applications in the Marketplace</span></span>

 <span data-ttu-id="bdd5e-104">MSPs, ISVs e ISs (integradores de sistema) podem usar os aplicativos gerenciados do Azure para oferecer suas soluções para todos os clientes do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications to offer their solutions to all Azure Marketplace customers.</span></span> <span data-ttu-id="bdd5e-105">Essas soluções reduzem a sobrecarga de manutenção e de serviço para os clientes.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-105">Such solutions reduce the maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="bdd5e-106">Os editores podem vender infraestrutura e software por meio do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-106">Publishers can sell infrastructure and software through the Marketplace.</span></span> <span data-ttu-id="bdd5e-107">Eles podem anexar serviços e suporte operacional para aplicativos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-107">They can attach services and operational support to managed applications.</span></span> <span data-ttu-id="bdd5e-108">Para saber mais, consulte [Visão geral do aplicativo gerenciado](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="bdd5e-109">Este artigo explica como um MSP, ISV ou SI pode publicar um aplicativo no Marketplace e torná-lo amplamente disponível aos clientes.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-109">This article explains how an MSP, ISV, or SI can publish an application to the Marketplace and make it broadly available to customers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="bdd5e-110">Pré-requisitos para publicar um aplicativo gerenciado</span><span class="sxs-lookup"><span data-stu-id="bdd5e-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="bdd5e-111">Pré-requisitos para a listagem no Marketplace:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-111">Prerequisites to listing in the Marketplace:</span></span>

* <span data-ttu-id="bdd5e-112">Técnicos</span><span class="sxs-lookup"><span data-stu-id="bdd5e-112">Technical</span></span>

    *  <span data-ttu-id="bdd5e-113">Para obter informações sobre a estrutura básica e a sintaxe de modelos do Azure Resource Manager, consulte [Modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-113">For information about the basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="bdd5e-114">Para exibir as soluções de modelo completas, consulte [Modelos de Início Rápido do Azure](https://azure.microsoft.com/en-us/documentation/templates/) ou [Repositório de modelos Quickstart](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-114">To view complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or the [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="bdd5e-115">Para saber mais sobre como criar a interface para clientes que implantam seu aplicativo por meio do Marketplace, consulte [Criar um arquivo de definição de interface do usuário](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-115">For information about how to create the interface for customers who deploy your application through the Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="bdd5e-116">Não técnico (requisitos de negócios)</span><span class="sxs-lookup"><span data-stu-id="bdd5e-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="bdd5e-117">Sua empresa, ou subsidiária, deve estar localizada em um país no qual as vendas têm suporte no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-117">Your company or its subsidiary must be located in a country where sales are supported by the Marketplace.</span></span>
    *   <span data-ttu-id="bdd5e-118">O produto deve ser licenciado de forma que seja compatível com modelos de cobrança com suporte no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-118">Your product must be licensed in a way that is compatible with billing models supported by the Marketplace.</span></span>
    *   <span data-ttu-id="bdd5e-119">Você é responsável por disponibilizar o suporte técnico a clientes de modo comercialmente razoável.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-119">You're responsible for making technical support available to customers in a commercially reasonable manner.</span></span> <span data-ttu-id="bdd5e-120">O suporte pode ser gratuito, pago ou oferecido por meio de suporte da comunidade.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-120">The support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="bdd5e-121">Você é responsável pelo licenciamento do software e quaisquer dependências de software de terceiros.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="bdd5e-122">Você deve fornecer conteúdo que atenda aos critérios da oferta a serem listados no Marketplace e no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-122">You must provide content that meets criteria for your offering to be listed in the Marketplace and in the Azure portal.</span></span>
    *   <span data-ttu-id="bdd5e-123">Você deve concordar com os termos das Políticas de Participação do Azure Marketplace e com o Contrato do Publicador.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-123">You must agree to the terms of the Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="bdd5e-124">Você deve concordar em cumprir os Termos de uso, a Política de privacidade da Microsoft e o Contrato do programa de certificação do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-124">You must agree to comply with the Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="bdd5e-125">Criar uma nova oferta de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="bdd5e-125">Create a new Azure application offer</span></span>

<span data-ttu-id="bdd5e-126">Após atender aos pré-requisitos, você estará pronto para criar sua oferta de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-126">After you meet the prerequisites, you're ready to create your managed application offer.</span></span> <span data-ttu-id="bdd5e-127">Vamos analisar rapidamente uma visão geral de uma oferta e um SKU.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="bdd5e-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="bdd5e-128">Offer</span></span>

<span data-ttu-id="bdd5e-129">A oferta para um aplicativo gerenciado corresponde a uma classe de oferta de produtos de um publicador.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-129">The offer for a managed application corresponds to a class of product offering from a publisher.</span></span> <span data-ttu-id="bdd5e-130">Se você tiver um novo tipo de solução/aplicativo que queira disponibilizar no Marketplace, configure-o como uma oferta nova.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-130">If you have a new type of solution/application that you want to make available in the Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="bdd5e-131">Uma oferta é uma coleção de SKUs.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="bdd5e-132">Cada oferta aparece como sua própria entidade no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-132">Every offer appears as its own entity in the Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="bdd5e-133">SKU</span><span class="sxs-lookup"><span data-stu-id="bdd5e-133">SKU</span></span>

<span data-ttu-id="bdd5e-134">Uma SKU é a menor unidade de compra de uma oferta.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-134">A SKU is the smallest purchasable unit of an offer.</span></span> <span data-ttu-id="bdd5e-135">Use um SKU dentro da mesma classe de produto (oferta) para diferenciar entre:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-135">You can use a SKU within the same product class (offer) to differentiate between:</span></span>

* <span data-ttu-id="bdd5e-136">Diferentes recursos com suporte.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-136">Different features that are supported.</span></span>
* <span data-ttu-id="bdd5e-137">Se a oferta é gerenciada ou não.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-137">Whether the offer is managed or unmanaged.</span></span>
* <span data-ttu-id="bdd5e-138">Modelos de cobrança com suporte.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-138">Billing models that are supported.</span></span>

<span data-ttu-id="bdd5e-139">Um SKU aparece sob a oferta pai no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-139">A SKU appears under the parent offer in the Marketplace.</span></span> <span data-ttu-id="bdd5e-140">Ele aparece como sua própria entidade disponível para compra no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-140">It appears as its own purchasable entity in the Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="bdd5e-141">Configurar uma oferta</span><span class="sxs-lookup"><span data-stu-id="bdd5e-141">Set up an offer</span></span>

1. <span data-ttu-id="bdd5e-142">Entre no [Portal do Cloud Partner](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-142">Sign in to the [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="bdd5e-143">No painel de navegação à esquerda, selecione **+ Nova oferta** > **Aplicativos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-143">In the navigation pane on the left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nova oferta](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="bdd5e-145">Preencha os formulários à esquerda no modo de exibição do **Editor**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-145">Fill out the forms that appear on the left in the **Editor** view.</span></span> <span data-ttu-id="bdd5e-146">Os campos obrigatórios estão marcados com um asterisco vermelho (*).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Configurações da oferta](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="bdd5e-148">Quatro formulários principais são usados para criar um aplicativo gerenciado:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-148">Four main forms are used to create a managed application:</span></span>

    <span data-ttu-id="bdd5e-149">a.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-149">a.</span></span> <span data-ttu-id="bdd5e-150">Configurações da oferta</span><span class="sxs-lookup"><span data-stu-id="bdd5e-150">Offer Settings</span></span>

    <span data-ttu-id="bdd5e-151">b.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-151">b.</span></span> <span data-ttu-id="bdd5e-152">SKUs</span><span class="sxs-lookup"><span data-stu-id="bdd5e-152">SKUs</span></span>

    <span data-ttu-id="bdd5e-153">c.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-153">c.</span></span> <span data-ttu-id="bdd5e-154">Marketplace</span><span class="sxs-lookup"><span data-stu-id="bdd5e-154">Marketplace</span></span>

    <span data-ttu-id="bdd5e-155">d.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-155">d.</span></span> <span data-ttu-id="bdd5e-156">Suporte</span><span class="sxs-lookup"><span data-stu-id="bdd5e-156">Support</span></span>

<span data-ttu-id="bdd5e-157">Esses formulários são descritos mais detalhadamente nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-157">These forms are described in greater detail in the following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="bdd5e-158">Formulário de Configurações de Oferta</span><span class="sxs-lookup"><span data-stu-id="bdd5e-158">Offer Settings form</span></span>
<span data-ttu-id="bdd5e-159">Use este formulário básico para especificar as configurações da oferta.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-159">Use this basic form to specify the offer settings.</span></span>

1. <span data-ttu-id="bdd5e-160">Preencha o formulário **Configuração da Oferta**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-160">Fill in the **Offer Settings** form.</span></span> <span data-ttu-id="bdd5e-161">Os diferentes campos são:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-161">The different fields are:</span></span>

    <span data-ttu-id="bdd5e-162">a.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-162">a.</span></span> <span data-ttu-id="bdd5e-163">**ID da Oferta**: esse identificador exclusivo identifica a oferta em um perfil de publicador.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-163">**Offer ID**: This unique identifier identifies the offer within a publisher profile.</span></span> <span data-ttu-id="bdd5e-164">Essa ID está visível em URLs de produto, modelos do Resource Manager e relatórios de cobrança.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="bdd5e-165">Ele só pode ser composto de caracteres alfanuméricos minúsculos ou traços (-).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="bdd5e-166">A ID não pode terminar com um traço.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-166">The ID can't end in a dash.</span></span> <span data-ttu-id="bdd5e-167">Ela tem um limite máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-167">It's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="bdd5e-168">Após a ativação da oferta, esse campo é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="bdd5e-169">b.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-169">b.</span></span> <span data-ttu-id="bdd5e-170">**ID do Publicador**: use essa lista suspensa para escolher o perfil de publicador no qual você deseja publicar essa oferta.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-170">**Publisher ID**: Use this drop-down list to choose the publisher profile you want to publish this offer under.</span></span> <span data-ttu-id="bdd5e-171">Após a ativação da oferta, esse campo é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="bdd5e-172">c.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-172">c.</span></span> <span data-ttu-id="bdd5e-173">**Nome**: este nome de exibição de sua oferta aparece no Marketplace e no portal.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-173">**Name**: This display name for your offer appears in the Marketplace and in the portal.</span></span> <span data-ttu-id="bdd5e-174">Ele pode ter um máximo de 50 caracteres.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="bdd5e-175">Inclua um nome de marca reconhecível para o seu produto.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="bdd5e-176">Não inclua o nome de sua empresa aqui, a menos que seja a maneira como ela é comercializada.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="bdd5e-177">Se você estiver comercializando essa oferta em seu próprio site, certifique-se de que o nome seja exatamente como aparece em seu site.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-177">If you're marketing this offer on your own website, ensure that the name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="bdd5e-178">Selecione **Salvar** para salvar o progresso.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-178">Select **Save** to save your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="bdd5e-179">Formulário de SKUs</span><span class="sxs-lookup"><span data-stu-id="bdd5e-179">SKUs form</span></span>
<span data-ttu-id="bdd5e-180">A próxima etapa é adicionar SKUs para a sua oferta.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-180">The next step is to add SKUs for your offer.</span></span>

1. <span data-ttu-id="bdd5e-181">Selecione **SKUs** > **Novo SKU**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Selecionar novo SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="bdd5e-183">Insira uma **ID de SKU**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="bdd5e-184">Uma ID de SKU é um identificador exclusivo para o SKU dentro de uma oferta.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-184">A SKU ID is a unique identifier for the SKU within an offer.</span></span> <span data-ttu-id="bdd5e-185">Essa ID está visível em URLs de produto, modelos do Resource Manager e relatórios de cobrança.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="bdd5e-186">Ele só pode ser composto de caracteres alfanuméricos minúsculos ou traços (-).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="bdd5e-187">A ID não pode terminar com um traço e está limitada a 50 caracteres no máximo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-187">The ID can't end in a dash, and it's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="bdd5e-188">Após a ativação da oferta, esse campo é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="bdd5e-189">Pode existir várias SKUs em uma oferta.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="bdd5e-190">Você precisa de um SKU para cada imagem que planeja publicar.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-190">You need a SKU for each image you plan to publish.</span></span>

3. <span data-ttu-id="bdd5e-191">Preencha a seção **Detalhes do SKU** no seguinte formulário:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-191">Fill out the **SKU Details** section on the following form:</span></span>

    ![Fornecer novo SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="bdd5e-193">Preencha os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-193">Fill out the following fields:</span></span>
    
    <span data-ttu-id="bdd5e-194">a.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-194">a.</span></span> <span data-ttu-id="bdd5e-195">**Título**: insira um título para esse SKU.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="bdd5e-196">Esse título aparecerá na galeria para este item.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-196">This title appears in the gallery for this item.</span></span>

    <span data-ttu-id="bdd5e-197">b.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-197">b.</span></span> <span data-ttu-id="bdd5e-198">**Resumo**: insira um breve resumo para esse SKU.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="bdd5e-199">Esse texto aparece abaixo do título.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-199">This text appears underneath the title.</span></span>

    <span data-ttu-id="bdd5e-200">c.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-200">c.</span></span> <span data-ttu-id="bdd5e-201">**Descrição**: insira uma descrição detalhada sobre a SKU.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-201">**Description**: Enter a detailed description about the SKU.</span></span>

    <span data-ttu-id="bdd5e-202">d.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-202">d.</span></span> <span data-ttu-id="bdd5e-203">**Tipo de SKU**: os valores permitidos são **Aplicativo Gerenciado** e **Modelos de Solução**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-203">**SKU Type**: The allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="bdd5e-204">Nesse caso, selecione **Aplicativo Gerenciado**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="bdd5e-205">Preencha a seção **Detalhes do Pacote** no seguinte formulário:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-205">Fill out the **Package Details** section on the following form:</span></span>

    ![Pacote](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="bdd5e-207">Preencha os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-207">Fill out the following fields:</span></span>

    <span data-ttu-id="bdd5e-208">a.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-208">a.</span></span> <span data-ttu-id="bdd5e-209">**Versão Atual**: insira uma versão para o pacote que você carregar.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-209">**Current Version**: Enter a version for the package you upload.</span></span> <span data-ttu-id="bdd5e-210">Ela deve estar no formato `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-210">It should be in the format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="bdd5e-211">b.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-211">b.</span></span> <span data-ttu-id="bdd5e-212">**Selecionar um arquivo de pacote**: esse pacote contém os seguintes arquivos que estão compactados em um arquivo .zip:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-212">**Select a package file**: This package contains the following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="bdd5e-213">**applianceMainTemplate.json**: o arquivo do modelo de implantação que é usado para implantar a solução/aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-213">**applianceMainTemplate.json**: The deployment template file that's used to deploy the solution/application.</span></span> <span data-ttu-id="bdd5e-214">Para saber mais sobre como criar arquivos de modelo de implantação, confira [Criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-214">For information about how to create deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="bdd5e-215">**appliancecreateUIDefinition.json**: esse arquivo é usado pelo portal do Azure para gerar a interface do usuário usada para provisionar essa solução/aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-215">**appliancecreateUIDefinition.json**: This file is used by the Azure portal to generate the user interface that's used to provision this solution/application.</span></span> <span data-ttu-id="bdd5e-216">Para saber mais, consulte [Introdução a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="bdd5e-217">**mainTemplate.json**: esse arquivo de modelo que contém somente o recurso Microsoft.Solution/appliances.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-217">**mainTemplate.json**: This template file contains only the Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="bdd5e-218">O arquivo mainTemplate inclui as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-218">The mainTemplate file includes the following properties:</span></span>

        *  <span data-ttu-id="bdd5e-219">**tipo**: use **Marketplace** para aplicativos gerenciados no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-219">**kind**: Use **Marketplace** for managed applications in the Marketplace.</span></span>
        *  <span data-ttu-id="bdd5e-220">**ManagedResourceGroupId**: esse grupo de recursos na assinatura do cliente em que todos os recursos definidos no applianceMainTemplate.json são implantados.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-220">**ManagedResourceGroupId**: This resource group in the customer's subscription is where all the resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="bdd5e-221">**PublisherPackageId**: essa cadeia de caracteres que identifica exclusivamente o pacote.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-221">**PublisherPackageId**: This string uniquely identifies the package.</span></span> <span data-ttu-id="bdd5e-222">Forneça o valor no formato de `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-222">Provide the value in the format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="bdd5e-223">Obtenha a **ID da oferta**  e a **ID do publicador** do portal de publicação, conforme mostra a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-223">Obtain the **Offer ID** and **Publisher ID** from the publishing portal, as shown in the following image:</span></span>

![ID da oferta](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="bdd5e-225">Obtenha a **ID do SKU**, conforme mostra a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-225">Obtain the **SKU ID**, as shown in the following image:</span></span>

![Id do SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="bdd5e-227">Obtenha a **Versão** do pacote, conforme mostra a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-227">Obtain the package **Version**, as shown in the following image:</span></span>

![Versão do pacote](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="bdd5e-229">Com base nos exemplos anteriores, o valor de **PublisherPackageId** é `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-229">Based on the preceding examples, the value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="bdd5e-230">Exemplo de mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify the name of the storage account"
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

<span data-ttu-id="bdd5e-231">Esse pacote deve conter quaisquer outros modelos ou scripts aninhados que sejam necessários para provisionar com êxito esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-231">This package should contain any other nested templates or scripts that are required to successfully provision this application.</span></span> <span data-ttu-id="bdd5e-232">Os arquivos mainTemplate.json, applianceMainTemplate.json e applianceCreateUIDefinition.json devem estar presentes na pasta raiz.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-232">The mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at the root folder.</span></span>

* <span data-ttu-id="bdd5e-233">**Autorizações**: essa propriedade define quem obtém acesso e o nível de acesso aos recursos em assinaturas de clientes.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-233">**Authorizations**: This property defines who gets access and the level of access to the resources in customers' subscriptions.</span></span> <span data-ttu-id="bdd5e-234">O publicador pode usar isso para gerenciar o aplicativo em nome do cliente.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-234">The publisher can use it to manage the application on behalf of the customer.</span></span>
* <span data-ttu-id="bdd5e-235">**PrincipalId**: essa propriedade é o identificador do Azure AD (Azure Active Directory) de um usuário, grupo de usuários ou aplicativo que recebeu determinadas permissões nos recursos na assinatura de clientes.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-235">**PrincipalId**: This property is the Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on the resources in the customer's subscription.</span></span> <span data-ttu-id="bdd5e-236">A Definição de Função descreve as permissões.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-236">The Role Definition describes the permissions.</span></span> 
* <span data-ttu-id="bdd5e-237">**Definição de Função**: essa propriedade é uma lista de todas as funções RBAC (Controle de acesso baseado em função) internas fornecidas pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-237">**Role Definition**: This property is a list of all the built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="bdd5e-238">Você pode selecionar a função mais apropriada para gerenciar os recursos em nome do cliente.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-238">You can select the role that's most appropriate to use to manage the resources on behalf of the customer.</span></span>

<span data-ttu-id="bdd5e-239">É possível adicionar várias autorizações.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-239">You can add multiple authorizations.</span></span> <span data-ttu-id="bdd5e-240">Recomendamos que você crie um grupo de usuários do AD e especifica sua ID em **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="bdd5e-241">Dessa forma, você pode adicionar mais usuários ao grupo de usuários sem a necessidade de atualizar o SKU.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-241">This way, you can add more users to the user group without the need to update the SKU.</span></span>

<span data-ttu-id="bdd5e-242">Para saber mais sobre RBAC, consulte [Introdução ao RBAC no Portal do Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-242">For more information about RBAC, see [Get started with RBAC in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="bdd5e-243">Formulário do Marketplace</span><span class="sxs-lookup"><span data-stu-id="bdd5e-243">Marketplace form</span></span>

<span data-ttu-id="bdd5e-244">O formulário do Marketplace pede campos que aparecem no [Azure Marketplace](https://azuremarketplace.microsoft.com) e no [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-244">The Marketplace form asks for fields that show up on the [Azure Marketplace](https://azuremarketplace.microsoft.com) and on the [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="bdd5e-245">IDs de assinatura para versão prévia</span><span class="sxs-lookup"><span data-stu-id="bdd5e-245">Preview subscription IDs</span></span>

<span data-ttu-id="bdd5e-246">Insira uma lista de IDs de assinatura do Azure que podem acessar a oferta após a publicação.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-246">Enter a list of Azure subscription IDs that can access the offer after it's published.</span></span> <span data-ttu-id="bdd5e-247">Use essas assinaturas da lista branca para testar a oferta de versão prévia antes de ativá-la.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-247">You can use these white-listed subscriptions to test the previewed offer before you make it live.</span></span> <span data-ttu-id="bdd5e-248">Você pode compilar uma lista branca com até 100 assinaturas no portal de parceiros.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-248">You can compile a white list of up to 100 subscriptions in the partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="bdd5e-249">Categorias sugeridas</span><span class="sxs-lookup"><span data-stu-id="bdd5e-249">Suggested categories</span></span>

<span data-ttu-id="bdd5e-250">Selecione até cinco categorias da lista às quais sua oferta pode ser associada.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-250">Select up to five categories from the list that your offer can be best associated with.</span></span> <span data-ttu-id="bdd5e-251">Essas categorias selecionadas serão usadas para mapear sua oferta para as categorias de produto disponíveis no [Azure Marketplace](https://azuremarketplace.microsoft.com) e no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-251">These categories are used to map your offer to the product categories that are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com) and the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="bdd5e-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="bdd5e-252">Azure Marketplace</span></span>

<span data-ttu-id="bdd5e-253">O resumo de seu aplicativo gerenciado exibe os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-253">The summary of your managed application displays the following fields:</span></span>

![Resumo do marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="bdd5e-255">A guia **Visão geral** de seu aplicativo gerenciado exibe os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-255">The **Overview** tab for your managed application displays the following fields:</span></span>

![Visão geral do Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="bdd5e-257">A guia **Planos + Preços** de seu aplicativo gerenciado exibe os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-257">The **Plans + Pricing** tab for your managed application displays the following fields:</span></span>

![Planos do marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="bdd5e-259">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bdd5e-259">Azure portal</span></span>

<span data-ttu-id="bdd5e-260">O resumo de seu aplicativo gerenciado exibe os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-260">The summary of your managed application displays the following fields:</span></span>

![Resumo do portal](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="bdd5e-262">A guia visão geral de seu aplicativo gerenciado exibe os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-262">The overview for your managed application displays the following fields:</span></span>

![Visão geral do portal](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="bdd5e-264">Diretrizes de logotipo</span><span class="sxs-lookup"><span data-stu-id="bdd5e-264">Logo guidelines</span></span>

<span data-ttu-id="bdd5e-265">Siga estas diretrizes para qualquer logotipo carregado no Portal do Cloud Partner:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-265">Follow these guidelines for any logo that you upload in the Cloud Partner portal:</span></span>

*   <span data-ttu-id="bdd5e-266">O design do Azure tem uma paleta de cores simples.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-266">The Azure design has a simple color palette.</span></span> <span data-ttu-id="bdd5e-267">Limite o número de cores primárias e secundárias em seu logotipo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-267">Limit the number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="bdd5e-268">As cores do tema do portal são branca e preta.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-268">The theme colors of the portal are white and black.</span></span> <span data-ttu-id="bdd5e-269">Não use essas cores como a cor de fundo de seu logotipo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-269">Don't use these colors as the background color for your logo.</span></span> <span data-ttu-id="bdd5e-270">Use uma cor que destaque seu logotipo no portal.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-270">Use a color that makes your logo prominent in the portal.</span></span> <span data-ttu-id="bdd5e-271">É recomendável usar cores primárias simples.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-271">We recommend simple primary colors.</span></span> <span data-ttu-id="bdd5e-272">*Se você usar um plano de fundo transparente, certifique-se de que o logotipo e o texto não sejam branco, preto ou azul.*</span><span class="sxs-lookup"><span data-stu-id="bdd5e-272">*If you use a transparent background, make sure that the logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="bdd5e-273">Não use um fundo gradiente no logotipo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-273">Don't use a gradient background on the logo.</span></span>
*   <span data-ttu-id="bdd5e-274">Não coloque texto no logotipo, nem mesmo o nome ou marca da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-274">Don't place text on the logo, not even your company or brand name.</span></span> <span data-ttu-id="bdd5e-275">A aparência de seu logotipo deve ser simples e evitar gradientes.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-275">The look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="bdd5e-276">Verifique se o logotipo não está esticado.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-276">Make sure the logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="bdd5e-277">Logotipo Hero</span><span class="sxs-lookup"><span data-stu-id="bdd5e-277">Hero logo</span></span>

<span data-ttu-id="bdd5e-278">O logotipo hero é opcional.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-278">The hero logo is optional.</span></span> <span data-ttu-id="bdd5e-279">O publicador pode optar por não carregar um logotipo hero.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-279">The publisher can choose not to upload a hero logo.</span></span> <span data-ttu-id="bdd5e-280">Após o upload do logotipo hero, não é possível exclui-lo.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-280">After the hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="bdd5e-281">Nessa ocasião, o parceiro deve seguir as diretrizes do Azure Marketplace para ícones hero.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-281">At that time, the partner must follow the Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="bdd5e-282">Siga estas diretrizes para o ícone do logotipo hero:</span><span class="sxs-lookup"><span data-stu-id="bdd5e-282">Follow these guidelines for the hero logo icon:</span></span>

*   <span data-ttu-id="bdd5e-283">O nome de exibição do publicador, o título do plano e o resumo longo da oferta são exibidas em branco.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-283">The publisher display name, the plan title, and the offer long summary are displayed in white.</span></span> <span data-ttu-id="bdd5e-284">Portanto, não use uma cor clara de fundo do ícone hero.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-284">Therefore, don't use a light color for the background of the hero icon.</span></span> <span data-ttu-id="bdd5e-285">Não há permissão para telas de fundo pretas, brancas ou transparentes para ícones hero.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="bdd5e-286">Após a listagem da oferta, o nome de exibição do publicador, o título do plano, o resumo longo da oferta e o botão **Criar** são inseridos programaticamente no logotipo hero.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-286">After the offer is listed, the publisher display name, the plan title, the offer long summary, and the **Create** button are embedded programmatically inside the hero logo.</span></span> <span data-ttu-id="bdd5e-287">Consequentemente, não insira qualquer texto enquanto projeta o logotipo hero.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-287">Consequently, don't enter any text while you design the hero logo.</span></span> <span data-ttu-id="bdd5e-288">Deixe o espaço vazio à direita, pois o texto é incluído nesse espaço por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-288">Leave empty space on the right because the text is included programmatically in that space.</span></span> <span data-ttu-id="bdd5e-289">O espaço vazio para o texto deve ter 415 x 100 pixels à direita.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-289">The empty space for the text should be 415 x 100 pixels on the right.</span></span> <span data-ttu-id="bdd5e-290">É um deslocamento de 370 pixels a partir da esquerda.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-290">It's offset by 370 pixels from the left.</span></span>

    ![Exemplo de logotipo hero](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="bdd5e-292">Formulário de suporte</span><span class="sxs-lookup"><span data-stu-id="bdd5e-292">Support form</span></span>

<span data-ttu-id="bdd5e-293">Preencha o formulário **Suporte** com contatos de suporte de sua empresa.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-293">Fill out the **Support** form with support contacts from your company.</span></span> <span data-ttu-id="bdd5e-294">Essas informações podem ser de contatos da engenharia e do atendimento ao cliente.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="bdd5e-295">Publicar uma oferta</span><span class="sxs-lookup"><span data-stu-id="bdd5e-295">Publish an offer</span></span>

<span data-ttu-id="bdd5e-296">Depois de preencher todas as seções, selecione **Publicar** para iniciar o processo de disponibilização de sua oferta aos clientes.</span><span class="sxs-lookup"><span data-stu-id="bdd5e-296">After you fill out all the sections, select **Publish** to start the process that makes your offer available to customers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdd5e-297">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bdd5e-297">Next steps</span></span>

* <span data-ttu-id="bdd5e-298">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-298">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="bdd5e-299">Para obter informações sobre como consumir um aplicativo gerenciado do Marketplace, consulte [Consumir aplicativos gerenciados pelo Azure no Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-299">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="bdd5e-300">Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="bdd5e-301">Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5e-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
