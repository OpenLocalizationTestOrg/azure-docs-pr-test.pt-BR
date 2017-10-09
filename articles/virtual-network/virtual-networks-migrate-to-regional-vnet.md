---
title: "aaaMigrate uma rede virtual do Azure (clássica) de uma área do grupo de afinidade tooa | Microsoft Docs"
description: "Saiba como toomigrate uma rede virtual (clássica) de uma afinidade agrupar tooa região."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a><span data-ttu-id="6afc9-103">Migrar de uma rede virtual (clássica) de uma região de tooa do grupo de afinidade</span><span class="sxs-lookup"><span data-stu-id="6afc9-103">Migrate a virtual network (classic) from an affinity group tooa region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6afc9-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6afc9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="6afc9-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="6afc9-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6afc9-106">A Microsoft recomenda que mais novas implantações de usam o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6afc9-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="6afc9-107">Grupos de afinidade Certifique-se de que os recursos criados no mesmo grupo de afinidade fisicamente hospedadas por servidores que estão próximos uns dos outros, permitindo que essas toocommunicate recursos mais rápida de saudação.</span><span class="sxs-lookup"><span data-stu-id="6afc9-107">Affinity groups ensure that resources created within hello same affinity group are physically hosted by servers that are close together, enabling these resources toocommunicate quicker.</span></span> <span data-ttu-id="6afc9-108">Em Olá passado, grupos de afinidade eram um requisito para criar redes virtuais (clássico).</span><span class="sxs-lookup"><span data-stu-id="6afc9-108">In hello past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="6afc9-109">Nesse momento, serviço de Gerenciador de rede Olá gerenciados redes virtuais (clássico) funcionaria apenas dentro de um conjunto de servidores físicos ou unidade de escala.</span><span class="sxs-lookup"><span data-stu-id="6afc9-109">At that time, hello network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="6afc9-110">Melhorias na arquitetura aumentaram o escopo de saudação da região de tooa de gerenciamento de rede.</span><span class="sxs-lookup"><span data-stu-id="6afc9-110">Architectural improvements have increased hello scope of network management tooa region.</span></span>

<span data-ttu-id="6afc9-111">Como resultado dessas melhorias na arquitetura, os grupos de afinidade não são mais recomendados nem obrigatórios para redes virtuais (clássicas).</span><span class="sxs-lookup"><span data-stu-id="6afc9-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="6afc9-112">uso de saudação de grupos de afinidade para redes virtuais (clássico) é substituído por regiões.</span><span class="sxs-lookup"><span data-stu-id="6afc9-112">hello use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="6afc9-113">Redes virtuais (clássicas) associadas a regiões são chamadas de redes virtuais regionais.</span><span class="sxs-lookup"><span data-stu-id="6afc9-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="6afc9-114">Recomendamos que você não use grupos de afinidades em geral.</span><span class="sxs-lookup"><span data-stu-id="6afc9-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="6afc9-115">Além de requisito de rede virtual hello, grupos de afinidade também foram toouse importante tooensure recursos, como (clássico) de computação e armazenamento (clássico), foram colocados próximos um do outro.</span><span class="sxs-lookup"><span data-stu-id="6afc9-115">Aside from hello virtual network requirement, affinity groups were also important toouse tooensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="6afc9-116">No entanto, com a arquitetura de rede do Azure atual hello, esses requisitos de colocação não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="6afc9-116">However, with hello current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6afc9-117">Embora seja tecnicamente possível toocreate uma rede virtual que está associada um grupo de afinidade, não há nenhum toodo motivo convincente para.</span><span class="sxs-lookup"><span data-stu-id="6afc9-117">Although it is still technically possible toocreate a virtual network that is associated with an affinity group, there is no compelling reason toodo so.</span></span> <span data-ttu-id="6afc9-118">Muitos recursos de rede virtual, como grupos de segurança de rede, estão disponíveis somente com o uso de uma rede virtual regional e não estão disponíveis para redes virtuais associadas a grupos de afinidades.</span><span class="sxs-lookup"><span data-stu-id="6afc9-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-hello-network-configuration-file"></a><span data-ttu-id="6afc9-119">Editar o arquivo de configuração de rede Olá</span><span class="sxs-lookup"><span data-stu-id="6afc9-119">Edit hello network configuration file</span></span>

1. <span data-ttu-id="6afc9-120">Exporte arquivo de configuração de rede hello.</span><span class="sxs-lookup"><span data-stu-id="6afc9-120">Export hello network configuration file.</span></span> <span data-ttu-id="6afc9-121">toolearn como tooexport uma configuração de rede de arquivo usando o PowerShell ou hello Azure interface de linha de comando (CLI) 1.0, consulte [configurar uma rede virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="6afc9-121">toolearn how tooexport a network configuration file using PowerShell or hello Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="6afc9-122">Editar o arquivo de configuração de rede hello, substituindo **AffinityGroup** com **local**.</span><span class="sxs-lookup"><span data-stu-id="6afc9-122">Edit hello network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="6afc9-123">Especifique uma [região](https://azure.microsoft.com/regions) do Azure para **Local**.</span><span class="sxs-lookup"><span data-stu-id="6afc9-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6afc9-124">Olá **local** é Olá região que você especificou para o grupo de afinidade Olá associado a sua rede virtual (clássica).</span><span class="sxs-lookup"><span data-stu-id="6afc9-124">hello **Location** is hello region that you specified for hello affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="6afc9-125">Por exemplo, se sua rede virtual (clássica) é associado um grupo de afinidade que está localizado no Oeste dos EUA, quando você migra, sua **local** deve apontar tooWest dos EUA.</span><span class="sxs-lookup"><span data-stu-id="6afc9-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point tooWest US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="6afc9-126">Edite saudação linhas no arquivo de configuração de rede a seguir, substituindo valores hello com seu próprio:</span><span class="sxs-lookup"><span data-stu-id="6afc9-126">Edit hello following lines in your network configuration file, replacing hello values with your own:</span></span> 
   
    <span data-ttu-id="6afc9-127">**Valor antigo:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="6afc9-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="6afc9-128">**Novo valor:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span><span class="sxs-lookup"><span data-stu-id="6afc9-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="6afc9-129">Salve suas alterações e [importar](virtual-networks-using-network-configuration-file.md#import) Olá tooAzure de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="6afc9-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) hello network configuration tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="6afc9-130">Essa migração não causa nenhum tempo de inatividade tooyour serviços.</span><span class="sxs-lookup"><span data-stu-id="6afc9-130">This migration does NOT cause any downtime tooyour services.</span></span>
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="6afc9-131">Quais toodo se você tiver uma VM (clássico) em um grupo de afinidade</span><span class="sxs-lookup"><span data-stu-id="6afc9-131">What toodo if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="6afc9-132">Máquinas virtuais (clássicos) que estão atualmente em um grupo de afinidade não é necessário toobe removido do grupo de afinidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="6afc9-132">VMs (classic) that are currently in an affinity group do not need toobe removed from hello affinity group.</span></span> <span data-ttu-id="6afc9-133">Depois de uma VM é implantada, é implantado tooa unidade de escala única.</span><span class="sxs-lookup"><span data-stu-id="6afc9-133">Once a VM is deployed, it is deployed tooa single scale unit.</span></span> <span data-ttu-id="6afc9-134">Grupos de afinidade pode restringir o conjunto de saudação de tamanhos VM disponíveis para uma nova implantação de VM, mas qualquer VM existente que é implantado já está restrita tamanhos de conjunto de toohello de VM disponível na unidade de escala Olá quais Olá VM é implantada.</span><span class="sxs-lookup"><span data-stu-id="6afc9-134">Affinity groups can restrict hello set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted toohello set of VM sizes available in hello scale unit in which hello VM is deployed.</span></span> <span data-ttu-id="6afc9-135">Como Olá que VM já está implantada tooa unidade de escala, remover uma máquina virtual de um grupo de afinidade não tem efeito sobre Olá VM.</span><span class="sxs-lookup"><span data-stu-id="6afc9-135">Because hello VM is already deployed tooa scale unit, removing a VM from an affinity group has no effect on hello VM.</span></span>
