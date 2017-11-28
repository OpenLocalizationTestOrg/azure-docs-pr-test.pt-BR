---
title: "Análise técnica aprofundada sobre a migração com suporte da plataforma do clássico para o Azure Resource Manager | Microsoft Docs"
description: "Este artigo faz uma análise técnica detalhada sobre a migração de recursos com suporte da plataforma do clássico para o Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 29267453-f894-4180-bb67-dce2a0e062bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 557a61f266c494cb6b8003cff945fa1a14348898
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="technical-deep-dive-on-platform-supported-migration-from-classic-to-azure-resource-manager"></a><span data-ttu-id="07d5a-103">Análise técnica aprofundada sobre a migração com suporte da plataforma do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07d5a-103">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>

<span data-ttu-id="07d5a-104">Vamos fazer uma análise aprofundada da migração do modelo de implantação clássico do Azure para o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="07d5a-104">Let's take a deep-dive on migrating from the Azure classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="07d5a-105">Nós vamos examinar os recursos no nível da funcionalidade e do recurso para ajudá-lo a entender como a plataforma do Azure migra recursos entre os dois modelos de implantação.</span><span class="sxs-lookup"><span data-stu-id="07d5a-105">We look at resources at a resource and feature level to help you understand how the Azure platform migrates resources between the two deployment models.</span></span> <span data-ttu-id="07d5a-106">Para obter mais informações, leia o artigo de comunicado do serviço - [Migração de recursos de IaaS com suporte da plataforma do clássico para o Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="07d5a-106">For more information, please read the service announcement article: [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-migration-deep-dive](../../../includes/virtual-machines-common-classic-resource-manager-migration-deep-dive.md)]

## <a name="next-steps"></a><span data-ttu-id="07d5a-107">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07d5a-107">Next steps</span></span>

* [<span data-ttu-id="07d5a-108">Visão geral da migração de recursos de IaaS com suporte da plataforma do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07d5a-108">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="07d5a-109">Planejamento para a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07d5a-109">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="07d5a-110">Usar o PowerShell para migrar recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07d5a-110">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="07d5a-111">Usar a CLI para migrar recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07d5a-111">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="07d5a-112">Ferramentas da comunidade para ajudar com a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07d5a-112">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="07d5a-113">Examinar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="07d5a-113">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="07d5a-114">Confira as perguntas mais frequentes sobre a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07d5a-114">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
