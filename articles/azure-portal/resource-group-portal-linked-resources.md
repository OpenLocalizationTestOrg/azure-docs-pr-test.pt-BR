---
title: Recursos vinculados e relacionados na galeria de blocos
description: "Saiba mais sobre recursos relacionados e vinculados que são exibidos na galeria de blocos do portal de visualização do Azure."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a><span data-ttu-id="aae18-103">Recursos vinculados e relacionados na galeria de blocos</span><span class="sxs-lookup"><span data-stu-id="aae18-103">Related and linked resources in the tile gallery</span></span>
<span data-ttu-id="aae18-104">A galeria de blocos permite que você encontre blocos para um determinado recurso e arraste-os para sua folha atual.</span><span class="sxs-lookup"><span data-stu-id="aae18-104">The tile gallery enables you to find tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="aae18-105">Usando a galeria de blocos, você pode criar exibições de gerenciamento que abrangem os recursos.</span><span class="sxs-lookup"><span data-stu-id="aae18-105">Using the tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="aae18-106">Para qualquer recurso especificado, os recursos relacionados incluem todos os recursos do grupo de recursos e todos os recursos vinculados para ou por meio do recurso.</span><span class="sxs-lookup"><span data-stu-id="aae18-106">For any specified resource, the related resources include all the resources in its resource group, and any resources that link to or from the resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="aae18-107">Recursos vinculados no Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aae18-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="aae18-108">A vinculação é um recurso do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aae18-108">Linking is a feature of the Resource Manager.</span></span>  <span data-ttu-id="aae18-109">Ela permite que você declare relações entre recursos mesmo se eles não residirem no mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aae18-109">It enables you to declare relationships between resources even if they do not reside in the same resource group.</span></span> <span data-ttu-id="aae18-110">A vinculação não tem impacto sobre o tempo de execução de seus recursos, sem afetar a cobrança e sem afetar o acesso baseado em função.</span><span class="sxs-lookup"><span data-stu-id="aae18-110">Linking has no impact on the runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="aae18-111">Ela é simplesmente um mecanismo que você pode usar para representar as relações para que as ferramentas, como a galeria de blocos, possam fornecer uma experiência de gerenciamento avançada.</span><span class="sxs-lookup"><span data-stu-id="aae18-111">It's simply a mechanism you can use to represent relationships so that tools like the tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="aae18-112">As ferramentas podem inspecionar os links usando a API de links e fornecer experiências de gerenciamento de relacionamento personalizadas também.</span><span class="sxs-lookup"><span data-stu-id="aae18-112">Your tools can inspect the links using the links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="aae18-113">Como vinculo meus recursos?</span><span class="sxs-lookup"><span data-stu-id="aae18-113">How do I link my resources?</span></span>
<span data-ttu-id="aae18-114">Quando você criar recursos por meio do portal ou implantando um modelo por meio do Azure PowerShell ou CLI do Azure, os links são criados automaticamente para alguns recursos dependentes.</span><span class="sxs-lookup"><span data-stu-id="aae18-114">When you create resources through the portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="aae18-115">Também é possível vincular recursos de forma programática usando a [API REST de Recursos Vinculados](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="aae18-115">You can also programmatically link resources by using the [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aae18-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aae18-116">Next steps</span></span>
* <span data-ttu-id="aae18-117">Se precisar de uma introdução à criação de modelos do Resource Manager, consulte [Criando modelos](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="aae18-117">If you need an introduction to writing Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="aae18-118">Para entender mais sobre como trabalhar com grupos de recursos por meio do portal, consulte [Usando o portal do Azure para gerenciar os recursos do Azure](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aae18-118">To understand more about working with resource groups through the portal, see [Using the Azure portal to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

