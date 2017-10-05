---
title: Assinatura e contas para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre as principais diretrizes de design e de implementação para assinaturas e contas no Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 19695a9960d8e8f0dfca4bf0ca10761fe6ae7ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="faf78-103">Diretrizes de contas e assinaturas do Azure para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="faf78-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="faf78-104">Este artigo se concentra em explicar como abordar o gerenciamento de assinaturas e de contas à medida que seu ambiente e sua base de usuários aumentam.</span><span class="sxs-lookup"><span data-stu-id="faf78-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="faf78-105">Diretrizes de implementação para contas e assinaturas</span><span class="sxs-lookup"><span data-stu-id="faf78-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="faf78-106">Decisões:</span><span class="sxs-lookup"><span data-stu-id="faf78-106">Decisions:</span></span>

* <span data-ttu-id="faf78-107">De que conjunto de assinaturas e contas você precisa para hospedar a infraestrutura ou carga de trabalho de TI?</span><span class="sxs-lookup"><span data-stu-id="faf78-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="faf78-108">Como dividir a hierarquia de acordo com sua organização?</span><span class="sxs-lookup"><span data-stu-id="faf78-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="faf78-109">Tarefas:</span><span class="sxs-lookup"><span data-stu-id="faf78-109">Tasks:</span></span>

* <span data-ttu-id="faf78-110">Defina a hierarquia da organização lógica como você gostaria de gerenciá-la em um nível de assinatura.</span><span class="sxs-lookup"><span data-stu-id="faf78-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="faf78-111">Para corresponder a essa hierarquia lógica, defina as contas e as assinaturas necessárias em cada conta.</span><span class="sxs-lookup"><span data-stu-id="faf78-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="faf78-112">Crie o conjunto de assinaturas e contas usando sua convenção de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="faf78-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="faf78-113">Assinaturas e contas</span><span class="sxs-lookup"><span data-stu-id="faf78-113">Subscriptions and accounts</span></span>
<span data-ttu-id="faf78-114">Para trabalhar com o Azure, você precisa de uma ou mais assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="faf78-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="faf78-115">Recursos como VMs (máquinas virtuais) ou redes virtuais existem em todas essas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="faf78-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="faf78-116">Os clientes corporativos normalmente têm um Registro Enterprise, que é o recurso mais alto na hierarquia e está associado a uma ou mais contas.</span><span class="sxs-lookup"><span data-stu-id="faf78-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="faf78-117">Para consumidores e clientes sem um Registro Enterprise, o recurso mais alto é a Conta.</span><span class="sxs-lookup"><span data-stu-id="faf78-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="faf78-118">As assinaturas estão associadas a contas, e pode haver uma ou mais assinaturas por conta.</span><span class="sxs-lookup"><span data-stu-id="faf78-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="faf78-119">O Azure registra as informações de cobrança no nível de assinatura.</span><span class="sxs-lookup"><span data-stu-id="faf78-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="faf78-120">Devido ao limite de dois níveis de hierarquia na relação de Conta/Assinatura, é importante alinhar a convenção de nomenclatura das contas e assinaturas às necessidades de cobrança.</span><span class="sxs-lookup"><span data-stu-id="faf78-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="faf78-121">Por exemplo, se uma empresa global usar o Azure, poderá optar por ter uma conta por região e gerenciar as assinaturas no nível de região:</span><span class="sxs-lookup"><span data-stu-id="faf78-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="faf78-122">Por exemplo, você pode usar a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="faf78-122">For instance, you might use the following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="faf78-123">Se uma região decide ter mais de uma assinatura associada a um determinado grupo, a convenção de nomenclatura deve incorporar uma forma de codificar os dados adicionais no nome da conta ou da assinatura.</span><span class="sxs-lookup"><span data-stu-id="faf78-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="faf78-124">Essa organização permite manipular os dados de faturamento para gerar os novos níveis de hierarquia durante os relatórios de cobrança:</span><span class="sxs-lookup"><span data-stu-id="faf78-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="faf78-125">A organização pode ser parecida com o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="faf78-125">The organization could look like the following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="faf78-126">Fornecemos cobrança detalhada por meio de um arquivo para download, para uma única conta ou para todas as contas em um contrato empresarial.</span><span class="sxs-lookup"><span data-stu-id="faf78-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="faf78-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="faf78-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

