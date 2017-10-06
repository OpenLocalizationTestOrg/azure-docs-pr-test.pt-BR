---
title: aaaSubscription e conta para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para assinaturas e contas no Azure."
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
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="df501-103">Diretrizes de contas e assinaturas do Azure para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="df501-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="df501-104">Este artigo se concentra em entender como o gerenciamento de conta e assinatura tooapproach como seu ambiente e a base de usuários aumenta.</span><span class="sxs-lookup"><span data-stu-id="df501-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="df501-105">Diretrizes de implementação para contas e assinaturas</span><span class="sxs-lookup"><span data-stu-id="df501-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="df501-106">Decisões:</span><span class="sxs-lookup"><span data-stu-id="df501-106">Decisions:</span></span>

* <span data-ttu-id="df501-107">O conjunto de assinaturas e contas você precisa toohost a infra-estrutura ou carga de trabalho TI?</span><span class="sxs-lookup"><span data-stu-id="df501-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="df501-108">Como toobreak para baixo Olá hierarquia toofit sua organização?</span><span class="sxs-lookup"><span data-stu-id="df501-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="df501-109">Tarefas:</span><span class="sxs-lookup"><span data-stu-id="df501-109">Tasks:</span></span>

* <span data-ttu-id="df501-110">Definir sua hierarquia de organização lógica como você gostaria de toomanage-lo de um nível de assinatura.</span><span class="sxs-lookup"><span data-stu-id="df501-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="df501-111">toomatch essa hierarquia lógica, definir contas Olá necessárias e assinaturas em cada conta.</span><span class="sxs-lookup"><span data-stu-id="df501-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="df501-112">Crie conjunto de saudação de assinaturas e contas usando a convenção de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="df501-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="df501-113">Assinaturas e contas</span><span class="sxs-lookup"><span data-stu-id="df501-113">Subscriptions and accounts</span></span>
<span data-ttu-id="df501-114">toowork com o Azure, você precisa de uma ou mais assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="df501-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="df501-115">Recursos como VMs (máquinas virtuais) ou redes virtuais existem em todas essas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="df501-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="df501-116">Os clientes corporativos normalmente têm um registro Enterprise, que é Olá recurso de mais alto na hierarquia de saudação e é tooone associado ou mais contas.</span><span class="sxs-lookup"><span data-stu-id="df501-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="df501-117">Para clientes sem um registro da empresa e os consumidores, recursos de mais alto de saudação é conta hello.</span><span class="sxs-lookup"><span data-stu-id="df501-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="df501-118">As assinaturas são tooaccounts associado, e pode haver uma ou mais assinaturas por conta.</span><span class="sxs-lookup"><span data-stu-id="df501-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="df501-119">Informações no nível de assinatura de saudação de cobrança de registros do Azure.</span><span class="sxs-lookup"><span data-stu-id="df501-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="df501-120">Devido toohello limite de níveis de hierarquia de duas na relação de conta/assinatura Olá, é importante tooalign Olá convenção de nomeação toohello contas e assinaturas, cobrança necessidades.</span><span class="sxs-lookup"><span data-stu-id="df501-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="df501-121">Por exemplo, se uma empresa global usa o Azure, eles podem escolher toohave uma conta por região e tem assinaturas gerenciadas no nível de região de hello:</span><span class="sxs-lookup"><span data-stu-id="df501-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="df501-122">Por exemplo, você pode usar o hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="df501-122">For instance, you might use hello following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="df501-123">Se uma região decide toohave mais de um grupo específico de tooa associado de uma assinatura, convenção de nomenclatura Olá deve incorporar uma maneira tooencode Olá dados extras na conta hello ou nome de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="df501-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="df501-124">Essa organização permite manipulando cobrança dados toogenerate Olá novos níveis de hierarquia durante a cobrança de relatórios:</span><span class="sxs-lookup"><span data-stu-id="df501-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="df501-125">organização de saudação poderia ser semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="df501-125">hello organization could look like hello following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="df501-126">Fornecemos cobrança detalhada por meio de um arquivo para download, para uma única conta ou para todas as contas em um contrato empresarial.</span><span class="sxs-lookup"><span data-stu-id="df501-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df501-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df501-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

