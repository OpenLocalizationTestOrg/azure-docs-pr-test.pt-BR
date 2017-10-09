---
title: "aaaTest sua VM oferecem para Olá Marketplace | Microsoft Docs"
description: Entenda como tootest sua VM da imagem para hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="4363d-103">Testar sua oferta VM para hello Azure Marketplace em preparo</span><span class="sxs-lookup"><span data-stu-id="4363d-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="4363d-104">Significa o SKU em uma "área restrita" onde você pode testar e validar sua funcionalidade antes de implantá-la toohello Marketplace particular de distribuição de preparo.</span><span class="sxs-lookup"><span data-stu-id="4363d-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="4363d-105">Olá SKU aparece no preparo como faria cliente tooa que implantou a ele.</span><span class="sxs-lookup"><span data-stu-id="4363d-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="4363d-106">A imagem VM deve ser toostaging toobe certificados enviada por push.</span><span class="sxs-lookup"><span data-stu-id="4363d-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="4363d-107">Etapa 1: Push toostaging sua oferta</span><span class="sxs-lookup"><span data-stu-id="4363d-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="4363d-108">Em Olá **publicar** , clique em **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="4363d-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![desenho](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="4363d-110">Se Olá Portal de publicação notifica sobre erros, corrija-os.</span><span class="sxs-lookup"><span data-stu-id="4363d-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="4363d-111">Em Olá **quem pode acessar sua oferta preparada?** caixa de diálogo caixa, digite Olá lista de assinaturas do Azure que você usará toopreview sua oferta Olá [portal de visualização do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4363d-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4363d-112">No caso de Máquinas Virtuais e modelos de Solução, **não** coloque em lista de branca assinaturas do tipo CSP, DreamSpark ou Azure via Open.</span><span class="sxs-lookup"><span data-stu-id="4363d-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="4363d-113">No caso de máquinas virtuais, quando você clica no botão Olá **tooSTAGING PUSH**, Olá etapas a seguir é executada por trás da cena hello.</span><span class="sxs-lookup"><span data-stu-id="4363d-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="4363d-114">Você será tooview capaz de andamento de saudação de cada etapa na guia publicação Olá Olá portal de publicação.</span><span class="sxs-lookup"><span data-stu-id="4363d-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="4363d-115">Você deve verificar essa página em intervalos regulares (até o status de saudação mostra teste) para obter quaisquer informações de falha que precisam de correção do seu final.</span><span class="sxs-lookup"><span data-stu-id="4363d-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="4363d-116">No primeiro sua solicitação de preparo vai toohello equipe de certificação que validar Olá vhd.</span><span class="sxs-lookup"><span data-stu-id="4363d-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="4363d-117">No entanto, se sua solicitação tem somente alterações de marketing, em seguida, Olá certificação etapa será ignorada.</span><span class="sxs-lookup"><span data-stu-id="4363d-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="4363d-118">Após a conclusão da certificação Olá, a replicação inicial de oferta Olá em todos os Olá datacenters do Azure.</span><span class="sxs-lookup"><span data-stu-id="4363d-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="4363d-119">Ele geralmente leva 24-48hours para Olá replicação toocomplete mas pode levar até semana tooa dependendo do tamanho de saudação do vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="4363d-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="4363d-120">No entanto, se sua solicitação tem somente alterações de marketing, replicação de saudação é mais rápida.</span><span class="sxs-lookup"><span data-stu-id="4363d-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="4363d-121">Quando Olá replicação for concluída, em seguida, oferta Olá estará disponível no hello [portal do Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4363d-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="4363d-122">Em que Olá tempo status se tornar testados no hello portal de publicação.</span><span class="sxs-lookup"><span data-stu-id="4363d-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="4363d-123">Uma oferta de preparada está visível no hello [portal do Azure](http:/portal.azure.com) usando apenas Olá identificações de email associadas à assinatura Olá preparada com quais Olá oferta.</span><span class="sxs-lookup"><span data-stu-id="4363d-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="4363d-124">Entrar toohello [portal de visualização do Azure](https://portal.azure.com) usando uma saudação assinaturas do Azure listadas na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="4363d-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="4363d-125">Encontre sua oferta e valide seus pontos de imagem VM:</span><span class="sxs-lookup"><span data-stu-id="4363d-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="4363d-126">Certifique-se de que conteúdo de marketing exibida corretamente no hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4363d-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="4363d-127">Implantação de ponta a ponta da imagem VM hello.</span><span class="sxs-lookup"><span data-stu-id="4363d-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="4363d-129">Sua oferta permanecem no preparo até que você notificar a Microsoft por meio do Portal de publicação de saudação [**publicar** guia > clique no botão de saudação **"Solicitar aprovação tooPush tooProduction"**] que você está pronto toopush tooproduction.</span><span class="sxs-lookup"><span data-stu-id="4363d-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="4363d-130">Este é um toohave tempo ideal que verificar todos os membros da equipe sobre tudo em preparação para a sua oferta vai listados.</span><span class="sxs-lookup"><span data-stu-id="4363d-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="4363d-131">Olá plataforma de preparo foi projetado para teste oferta Olá em um modo de visualização, publisher Olá.</span><span class="sxs-lookup"><span data-stu-id="4363d-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="4363d-132">É enfaticamente desaconselhável usar essa plataforma para fins comerciais.</span><span class="sxs-lookup"><span data-stu-id="4363d-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4363d-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4363d-133">Next steps</span></span>
<span data-ttu-id="4363d-134">Agora que sua oferta "preparada" e testar sua funcionalidade e conteúdo de marketing, você poderá publicar final toohello fase, **etapa 4**: [Implantando toohello sua oferta Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="4363d-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4363d-135">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4363d-135">See also</span></span>
* [<span data-ttu-id="4363d-136">Guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4363d-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

