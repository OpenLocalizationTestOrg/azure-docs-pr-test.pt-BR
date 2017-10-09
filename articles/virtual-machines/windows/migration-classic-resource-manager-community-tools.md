---
title: "ferramentas de aaaCommunity - mover recursos clássicos tooAzure Gerenciador de recursos | Microsoft Docs"
description: "Essa ferramenta Olá catálogos de artigo que foram fornecidas pelo Olá comunidade toohelp migra recursos de IaaS do modelo de implantação do Azure Resource Manager toohello clássico."
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
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="ecdf4-103">Recursos de IaaS toomigrate de tooAzure clássico Gerenciador de recursos das ferramentas de comunidade</span><span class="sxs-lookup"><span data-stu-id="ecdf4-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="ecdf4-104">Essa ferramenta de saudação catálogos artigo que foram fornecidas pelo Olá comunidade tooassist com a migração de recursos de IaaS de modelo de implantação do Azure Resource Manager toohello clássico.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="ecdf4-105">Não há suporte oficial para essas ferramentas no Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="ecdf4-106">Portanto estão abertos originado no GitHub e estamos felizes tooaccept PRs para correções ou cenários adicionais.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="ecdf4-107">tooreport um problema, use Olá GitHub problemas de recurso.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="ecdf4-108">A migração com essas ferramentas causará tempo de inatividade de sua Máquina Virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="ecdf4-109">Se você estiver buscando uma migração da plataforma com suporte, visite</span><span class="sxs-lookup"><span data-stu-id="ecdf4-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="ecdf4-110">Migração de plataforma com suporte de recursos de IaaS de pilha de Gerenciador de recursos de tooAzure clássico</span><span class="sxs-lookup"><span data-stu-id="ecdf4-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="ecdf4-111">Migração de clássico tooAzure Gerenciador de recursos de suporte técnico mergulho profundo na plataforma</span><span class="sxs-lookup"><span data-stu-id="ecdf4-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="ecdf4-112">Migrar recursos de IaaS de clássico tooAzure Gerenciador de recursos usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="ecdf4-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="ecdf4-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="ecdf4-113">AsmMetadataParser</span></span>
<span data-ttu-id="ecdf4-114">Esta é uma coleção de ferramentas auxiliar criado como parte de migrações de empresa do gerenciamento de serviços do Azure tooAzure Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="ecdf4-115">Essa ferramenta permite que você tooreplicate sua infraestrutura em outra assinatura, que pode ser usada para teste de migração e passe problemas antes de executar a migração de saudação em sua assinatura de produção.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="ecdf4-116">Documentação da ferramenta de link toohello</span><span class="sxs-lookup"><span data-stu-id="ecdf4-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="ecdf4-117">migAz</span><span class="sxs-lookup"><span data-stu-id="ecdf4-117">migAz</span></span>
<span data-ttu-id="ecdf4-118">migAz é uma opção adicional de toomigrate um conjunto completo de IaaS clássico tooAzure recursos recursos de IaaS do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="ecdf4-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="ecdf4-119">Hello migração pode ocorrer dentro de saudação mesma assinatura ou entre diferentes assinaturas e tipos de assinatura (ex: assinaturas de CSP).</span><span class="sxs-lookup"><span data-stu-id="ecdf4-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="ecdf4-120">Documentação da ferramenta de link toohello</span><span class="sxs-lookup"><span data-stu-id="ecdf4-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="ecdf4-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ecdf4-121">Next Steps</span></span>

* [<span data-ttu-id="ecdf4-122">Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="ecdf4-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ecdf4-123">Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="ecdf4-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ecdf4-124">Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="ecdf4-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ecdf4-125">Usar recursos de IaaS PowerShell toomigrate de tooAzure clássico Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="ecdf4-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ecdf4-126">Usar recursos de IaaS toomigrate CLI do clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="ecdf4-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ecdf4-127">Examinar os erros de migração mais comuns</span><span class="sxs-lookup"><span data-stu-id="ecdf4-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ecdf4-128">Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="ecdf4-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

