---
title: "Migrar uma rede virtual do Azure (clássica) de um grupo de afinidades para uma região | Microsoft Docs"
description: "Saiba como migrar uma rede virtual (clássica) de um grupo de afinidades para uma região."
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
ms.openlocfilehash: b9b3bd0f2184ac85261166d5fe2ab67e1bf319d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-to-a-region"></a><span data-ttu-id="f5abf-103">Migrar uma rede virtual (clássica) de um grupo de afinidades para uma região</span><span class="sxs-lookup"><span data-stu-id="f5abf-103">Migrate a virtual network (classic) from an affinity group to a region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5abf-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f5abf-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f5abf-105">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="f5abf-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="f5abf-106">A Microsoft recomenda que a maioria das implantações novas use o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="f5abf-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="f5abf-107">Grupos de afinidades asseguram que recursos criados dentro do mesmo grupo de afinidades sejam fisicamente hospedados por servidores próximos uns dos outros, permitindo a esses recursos comuniquem-se mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f5abf-107">Affinity groups ensure that resources created within the same affinity group are physically hosted by servers that are close together, enabling these resources to communicate quicker.</span></span> <span data-ttu-id="f5abf-108">Antigamente, os grupos de afinidades eram um requisito para a criação de redes virtuais (clássicas).</span><span class="sxs-lookup"><span data-stu-id="f5abf-108">In the past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="f5abf-109">Na época, o serviço gerenciador de rede que gerenciava as redes virtuais (clássicas) podia funcionar somente dentro de um conjunto de servidores físicos ou unidade de escala.</span><span class="sxs-lookup"><span data-stu-id="f5abf-109">At that time, the network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="f5abf-110">As melhorias de arquitetura aumentaram o escopo de gerenciamento de rede para uma região.</span><span class="sxs-lookup"><span data-stu-id="f5abf-110">Architectural improvements have increased the scope of network management to a region.</span></span>

<span data-ttu-id="f5abf-111">Como resultado dessas melhorias na arquitetura, os grupos de afinidade não são mais recomendados nem obrigatórios para redes virtuais (clássicas).</span><span class="sxs-lookup"><span data-stu-id="f5abf-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="f5abf-112">O uso de grupos de afinidade para redes virtuais (clássicas) é substituído por regiões.</span><span class="sxs-lookup"><span data-stu-id="f5abf-112">The use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="f5abf-113">Redes virtuais (clássicas) associadas a regiões são chamadas de redes virtuais regionais.</span><span class="sxs-lookup"><span data-stu-id="f5abf-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="f5abf-114">Recomendamos que você não use grupos de afinidades em geral.</span><span class="sxs-lookup"><span data-stu-id="f5abf-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="f5abf-115">Além do requisito de rede virtual, os grupos de afinidades também foram importantes para garantir que recursos como computação (clássico) e armazenamento (clássico) fossem colocados próximos uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="f5abf-115">Aside from the virtual network requirement, affinity groups were also important to use to ensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="f5abf-116">No entanto, com a arquitetura atual de rede do Azure, esses requisitos de colocação não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="f5abf-116">However, with the current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5abf-117">Embora ainda seja tecnicamente possível criar uma rede virtual associada a um grupo de afinidades, não há nenhum motivo relevante para fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="f5abf-117">Although it is still technically possible to create a virtual network that is associated with an affinity group, there is no compelling reason to do so.</span></span> <span data-ttu-id="f5abf-118">Muitos recursos de rede virtual, como grupos de segurança de rede, estão disponíveis somente com o uso de uma rede virtual regional e não estão disponíveis para redes virtuais associadas a grupos de afinidades.</span><span class="sxs-lookup"><span data-stu-id="f5abf-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-the-network-configuration-file"></a><span data-ttu-id="f5abf-119">Editar o arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="f5abf-119">Edit the network configuration file</span></span>

1. <span data-ttu-id="f5abf-120">Exportar o arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="f5abf-120">Export the network configuration file.</span></span> <span data-ttu-id="f5abf-121">Para saber como exportar um arquivo de configuração de rede usando o PowerShell ou a interface de linha de comando (CLI) 1.0 do Azure, consulte [Configurar uma rede virtual usando um arquivo de configuração de rede](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="f5abf-121">To learn how to export a network configuration file using PowerShell or the Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="f5abf-122">Edite o arquivo de configuração de rede substituindo **AffinityGroup** por **Local**.</span><span class="sxs-lookup"><span data-stu-id="f5abf-122">Edit the network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="f5abf-123">Especifique uma [região](https://azure.microsoft.com/regions) do Azure para **Local**.</span><span class="sxs-lookup"><span data-stu-id="f5abf-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f5abf-124">O **Local** é a região que você especificou para o grupo de afinidades associado à sua rede virtual (clássica).</span><span class="sxs-lookup"><span data-stu-id="f5abf-124">The **Location** is the region that you specified for the affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="f5abf-125">Por exemplo, se sua rede virtual (clássica) estiver associada a um grupo de afinidades localizado no Oeste dos EUA, quando você migrar, seu **Local** deverá apontar para o Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="f5abf-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point to West US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="f5abf-126">Edite as seguintes linhas no arquivo de configuração de rede substituindo os valores pelos seus:</span><span class="sxs-lookup"><span data-stu-id="f5abf-126">Edit the following lines in your network configuration file, replacing the values with your own:</span></span> 
   
    <span data-ttu-id="f5abf-127">**Valor antigo:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="f5abf-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="f5abf-128">**Novo valor:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span><span class="sxs-lookup"><span data-stu-id="f5abf-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="f5abf-129">Salve suas alterações e [importe](virtual-networks-using-network-configuration-file.md#import) a configuração de rede para o Azure.</span><span class="sxs-lookup"><span data-stu-id="f5abf-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) the network configuration to Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f5abf-130">Esta migração NÃO gera tempo de inatividade para seus serviços.</span><span class="sxs-lookup"><span data-stu-id="f5abf-130">This migration does NOT cause any downtime to your services.</span></span>
> 
> 

## <a name="what-to-do-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="f5abf-131">O que fazer se você tiver uma VM (clássica) em um grupo de afinidades</span><span class="sxs-lookup"><span data-stu-id="f5abf-131">What to do if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="f5abf-132">VMs (clássicas) que estão atualmente em um grupo de afinidades não precisam ser removidas do grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="f5abf-132">VMs (classic) that are currently in an affinity group do not need to be removed from the affinity group.</span></span> <span data-ttu-id="f5abf-133">Quando uma máquina virtual é implantada, ela é implantada em uma única unidade de escala.</span><span class="sxs-lookup"><span data-stu-id="f5abf-133">Once a VM is deployed, it is deployed to a single scale unit.</span></span> <span data-ttu-id="f5abf-134">Os grupos de afinidades pode restringir o conjunto de tamanhos de VM disponíveis para uma nova implantação de VM, mas qualquer VM existente já implantada fica restrita ao conjunto de tamanhos de VM disponíveis na unidade de escala em que a VM estiver implantada.</span><span class="sxs-lookup"><span data-stu-id="f5abf-134">Affinity groups can restrict the set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted to the set of VM sizes available in the scale unit in which the VM is deployed.</span></span> <span data-ttu-id="f5abf-135">Porque a VM já está implantada para uma unidade de escala, remover uma VM de um grupo de afinidades não tem nenhum efeito sobre a VM.</span><span class="sxs-lookup"><span data-stu-id="f5abf-135">Because the VM is already deployed to a scale unit, removing a VM from an affinity group has no effect on the VM.</span></span>
