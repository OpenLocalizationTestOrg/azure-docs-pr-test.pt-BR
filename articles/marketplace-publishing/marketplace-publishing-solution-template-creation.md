---
title: "aaaGuide toocreating um modelo de solução para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implantar um modelo de solução de imagem de várias VMs para compra em hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="67793-103">Guia toocreate um modelo de solução para o Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="67793-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="67793-104">Depois de concluir a etapa 1, [criação de conta e registro][link-acct-creation], podemos guiada por você na criação de saudação de um modelo de solução compatível com o Azure em [pré-requisitos técnicos para a criação de um modelo de solução](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="67793-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="67793-105">Agora podemos irá orientá-lo pelas etapas de saudação para criar um modelo de solução para várias VMs Olá [Portal de publicação] [ link-pubportal] para hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="67793-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="67793-106">Criar sua oferta de modelo de solução em Olá Portal de publicação</span><span class="sxs-lookup"><span data-stu-id="67793-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="67793-107">Vá muito [https://publish.windowsazure.com](http://publish.windowsazure.com). Ao entrar para Olá primeiro tempo toohello [Portal de publicação](https://publish.windowsazure.com/), use Olá mesma conta com o perfil de vendedor da sua empresa que foi registrado.</span><span class="sxs-lookup"><span data-stu-id="67793-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="67793-108">Posteriormente, você pode adicionar qualquer funcionário da sua empresa como um administrador de co Olá Portal de publicação.</span><span class="sxs-lookup"><span data-stu-id="67793-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="67793-109">1. Selecione "Modelos de solução"</span><span class="sxs-lookup"><span data-stu-id="67793-109">1. Select "Solution templates"</span></span>
  ![desenho][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="67793-111">2. Crie um novo modelo de solução</span><span class="sxs-lookup"><span data-stu-id="67793-111">2. Create a new solution template</span></span>
  ![desenho][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="67793-113">3. Comece com as topologias</span><span class="sxs-lookup"><span data-stu-id="67793-113">3. Start with topologies</span></span>
<span data-ttu-id="67793-114">Um modelo de solução é um tooall "pai" de suas topologias.</span><span class="sxs-lookup"><span data-stu-id="67793-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="67793-115">Você pode definir várias topologias em uma oferta/modelo de solução.</span><span class="sxs-lookup"><span data-stu-id="67793-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="67793-116">Quando uma oferta é impulsionada toostaging, ela é enviada por push com todas as suas topologias de.</span><span class="sxs-lookup"><span data-stu-id="67793-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="67793-117">Siga as etapas de saudação abaixo toodefine sua oferta:</span><span class="sxs-lookup"><span data-stu-id="67793-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="67793-118">Crie uma topologia: "Identificador de topologia" normalmente é nome de saudação da topologia Olá para o modelo de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="67793-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="67793-119">Identificador da topologia de saudação é usado na URL de hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="67793-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="67793-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="67793-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="67793-121">Portal do Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="67793-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="67793-122">Adicionar uma nova versão.</span><span class="sxs-lookup"><span data-stu-id="67793-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="67793-123">4. Certifique as versões de sua topologia</span><span class="sxs-lookup"><span data-stu-id="67793-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="67793-124">Carregar um arquivo zip que contém essa versão específica da topologia de saudação de tooprovision de todos os arquivos necessários.</span><span class="sxs-lookup"><span data-stu-id="67793-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="67793-125">O arquivo zip deve conter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="67793-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="67793-126">Arquivo *mainTemplate.json* e *createUiDefinition.json* no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="67793-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="67793-127">Quaisquer modelos vinculados e todos os scripts necessários.</span><span class="sxs-lookup"><span data-stu-id="67793-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="67793-128">Enquanto os desenvolvedores de trabalho sobre a criação de solução Olá topologias de modelo e recuperá-las certificados, negócios Olá, departamentos de marketing e/ou legais da sua empresa podem trabalhar no conteúdo de marketing e legal de saudação.</span><span class="sxs-lookup"><span data-stu-id="67793-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="67793-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67793-129">Next steps</span></span>
<span data-ttu-id="67793-130">Agora que você criou o modelo de solução e carregado o arquivo zip de hello, siga as instruções de Olá Olá [guia de conteúdo de marketing do Marketplace](marketplace-publishing-push-to-staging.md) antes de enviar Olá oferta toostaging.</span><span class="sxs-lookup"><span data-stu-id="67793-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="67793-131">conjunto completo de toosee saudação do marketplace publicando artigos, visite [guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="67793-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="67793-132">Você também pode se interessar por estes artigos relacionados:</span><span class="sxs-lookup"><span data-stu-id="67793-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="67793-133">Imagens de VM: [Sobre Imagens da Máquina Virtual no Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="67793-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="67793-134">Extensões de VM: [Visão geral sobre Agente de VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) e [Extensões de VM e Extensões de VM e recursos do Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="67793-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="67793-135">Azure Resource Manager: [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [Exemplos de modelos simples](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="67793-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="67793-136">Conta de armazenamento limita: [como tooMonitor limitação da conta de armazenamento de](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) e [armazenamento Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="67793-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
