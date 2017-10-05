---
title: "Ferramentas da comunidade - Mover recursos clássicos para o Azure Resource Manager | Microsoft Docs"
description: "Este artigo cataloga as ferramentas que foram fornecidas pela comunidade para ajudar a migrar os recursos de IaaS do modelo de implantação clássico para o modelo de implantação do Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: d3fc0246088eddeb345bea0ffbd2c5247b218006
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="community-tools-to-migrate-iaas-resources-from-classic-to-azure-resource-manager"></a><span data-ttu-id="abb0f-103">Ferramentas da comunidade para migrar recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-103">Community tools to migrate IaaS resources from classic to Azure Resource Manager</span></span>
<span data-ttu-id="abb0f-104">Este artigo cataloga as ferramentas que foram fornecidas pela comunidade para auxiliar com a migração dos recursos de IaaS do modelo de implantação clássico para o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abb0f-104">This article catalogs the tools that have been provided by the community to assist with migration of IaaS resources from classic to the Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="abb0f-105">Não há suporte oficial para essas ferramentas no Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="abb0f-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="abb0f-106">Portanto, são software livre no GitHub e aceitamos PRs para correções ou cenários adicionais.</span><span class="sxs-lookup"><span data-stu-id="abb0f-106">Therefore they are open sourced on GitHub and we're happy to accept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="abb0f-107">Para relatar um problema, use o recurso de problemas do GitHub.</span><span class="sxs-lookup"><span data-stu-id="abb0f-107">To report an issue, use the GitHub issues feature.</span></span>
> 
> <span data-ttu-id="abb0f-108">A migração com essas ferramentas causará tempo de inatividade de sua Máquina Virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="abb0f-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="abb0f-109">Se você estiver buscando uma migração da plataforma com suporte, visite</span><span class="sxs-lookup"><span data-stu-id="abb0f-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="abb0f-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack (Migração de recursos de IaaS com suporte da plataforma da pilha Clássica para o Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="abb0f-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="abb0f-111">Análise técnica aprofundada sobre a migração com suporte da plataforma do Clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-111">Technical Deep Dive on Platform supported migration from Classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="abb0f-112">Migrar recursos de IaaS do Clássico para o Azure Resource Manager usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="abb0f-112">Migrate IaaS resources from Classic to Azure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="abb0f-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="abb0f-113">AsmMetadataParser</span></span>
<span data-ttu-id="abb0f-114">Trata-se de uma coleção de ferramentas auxiliares criadas como parte de migrações empresariais do Gerenciamento de Serviços do Azure para o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abb0f-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management to Azure Resource Manager.</span></span> <span data-ttu-id="abb0f-115">Essa ferramenta permite replicar sua infraestrutura para outra assinatura, o que pode ser usado para testar a migração e solucionar problemas antes de executar a migração em sua assinatura de produção.</span><span class="sxs-lookup"><span data-stu-id="abb0f-115">This tool allows you to replicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running the migration on your Production subscription.</span></span>

[<span data-ttu-id="abb0f-116">Link para a documentação da ferramenta</span><span class="sxs-lookup"><span data-stu-id="abb0f-116">Link to the tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="abb0f-117">migAz</span><span class="sxs-lookup"><span data-stu-id="abb0f-117">migAz</span></span>
<span data-ttu-id="abb0f-118">migAz é uma opção adicional para migrar um conjunto completo de recursos de IaaS clássicos para recursos de IaaS do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="abb0f-118">migAz is an additional option to migrate a complete set of classic IaaS resources to Azure Resource Manager IaaS resources.</span></span> <span data-ttu-id="abb0f-119">A migração pode ocorrer na mesma assinatura ou entre assinaturas e tipos de assinatura diferentes (por ex.: assinaturas do CSP).</span><span class="sxs-lookup"><span data-stu-id="abb0f-119">The migration can occur within the same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="abb0f-120">Link para a documentação da ferramenta</span><span class="sxs-lookup"><span data-stu-id="abb0f-120">Link to the tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="abb0f-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abb0f-121">Next Steps</span></span>

* [<span data-ttu-id="abb0f-122">Visão geral da migração de recursos de IaaS com suporte da plataforma do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-122">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abb0f-123">Análise técnica aprofundada sobre a migração com suporte da plataforma do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-123">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abb0f-124">Planejamento para a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-124">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abb0f-125">Usar o PowerShell para migrar recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-125">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abb0f-126">Usar a CLI para migrar recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-126">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abb0f-127">Examinar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="abb0f-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abb0f-128">Confira as perguntas mais frequentes sobre a migração de recursos de IaaS do clássico para o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abb0f-128">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

