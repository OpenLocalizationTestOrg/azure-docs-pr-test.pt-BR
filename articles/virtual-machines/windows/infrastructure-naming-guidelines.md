---
title: Diretrizes de nomenclatura de infraestrutura do Azure - Windows | Microsoft Docs
description: "Saiba mais sobre as principais diretrizes de design e implementação referentes à nomenclatura em serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a595d5c2f0316b5214af7b8939f1af8da187ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="1d536-103">Diretrizes de nomenclatura de infraestrutura do Azure para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="1d536-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="1d536-104">Este artigo destaca as noções básicas sobre como abordar as convenções de nomenclatura para todos os vários recursos do Azure para compilar um conjunto de recursos lógico e facilmente identificável em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="1d536-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="1d536-105">Diretrizes de implementação de convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="1d536-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="1d536-106">Decisões:</span><span class="sxs-lookup"><span data-stu-id="1d536-106">Decisions:</span></span>

* <span data-ttu-id="1d536-107">Quais são as suas convenções de nomenclatura de recursos do Azure?</span><span class="sxs-lookup"><span data-stu-id="1d536-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="1d536-108">Tarefas:</span><span class="sxs-lookup"><span data-stu-id="1d536-108">Tasks:</span></span>

* <span data-ttu-id="1d536-109">Definir os afixos que serão usados entre os recursos para que a consistência seja mantida.</span><span class="sxs-lookup"><span data-stu-id="1d536-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="1d536-110">Definir os nomes de conta de armazenamento de acordo com o requisito para que elas possam ser globalmente exclusivas.</span><span class="sxs-lookup"><span data-stu-id="1d536-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="1d536-111">Documentar a convenção de nomenclatura a ser usada e distribuí-la para todas as partes envolvidas, a fim de garantir a consistência entre as implantações.</span><span class="sxs-lookup"><span data-stu-id="1d536-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="1d536-112">Convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="1d536-112">Naming conventions</span></span>
<span data-ttu-id="1d536-113">Você deve ter uma boa convenção de nomenclatura definida para criar qualquer coisa no Azure.</span><span class="sxs-lookup"><span data-stu-id="1d536-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="1d536-114">Uma convenção de nomenclatura garante que todos os recursos tenham um nome previsível, o que ajuda a reduzir a carga administrativa associada ao gerenciamento desses recursos.</span><span class="sxs-lookup"><span data-stu-id="1d536-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="1d536-115">Você pode optar por seguir um conjunto específico de convenções de nomenclatura definido para toda a organização ou para uma determinada conta ou assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d536-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="1d536-116">Embora seja fácil para os indivíduos das organizações estabelecerem regras implícitas ao trabalharem com os recursos do Azure, quando uma equipe precisa trabalhar em um projeto no Azure, esse modelo não se adapta bem.</span><span class="sxs-lookup"><span data-stu-id="1d536-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, when a team needs to work on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="1d536-117">Entrem em um acordo sobre um conjunto de convenções de nomenclatura antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="1d536-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="1d536-118">Há algumas considerações sobre as convenções de nomenclatura que abrangem esses conjuntos de regras.</span><span class="sxs-lookup"><span data-stu-id="1d536-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="1d536-119">Afixos</span><span class="sxs-lookup"><span data-stu-id="1d536-119">Affixes</span></span>
<span data-ttu-id="1d536-120">Durante a definição de uma convenção de nomenclatura, surge uma decisão sobre se o afixo deverá ficar:</span><span class="sxs-lookup"><span data-stu-id="1d536-120">As you look to define a naming convention, one decision comes whether the affix is at:</span></span>

* <span data-ttu-id="1d536-121">No início do nome (prefixo)</span><span class="sxs-lookup"><span data-stu-id="1d536-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="1d536-122">No final do nome (sufixo)</span><span class="sxs-lookup"><span data-stu-id="1d536-122">The end of the name (suffix)</span></span>

<span data-ttu-id="1d536-123">Por exemplo, estes são dois nomes possíveis para um Grupo de Recursos usando o afixo `rg` :</span><span class="sxs-lookup"><span data-stu-id="1d536-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="1d536-124">Rg-WebApp (prefixo)</span><span class="sxs-lookup"><span data-stu-id="1d536-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="1d536-125">WebApp-Rg (sufixo)</span><span class="sxs-lookup"><span data-stu-id="1d536-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="1d536-126">Os afixos podem se referir a diversos aspectos que descrevam os recursos em questão.</span><span class="sxs-lookup"><span data-stu-id="1d536-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="1d536-127">A tabela a seguir mostra alguns exemplos normalmente usados.</span><span class="sxs-lookup"><span data-stu-id="1d536-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="1d536-128">Aspecto</span><span class="sxs-lookup"><span data-stu-id="1d536-128">Aspect</span></span> | <span data-ttu-id="1d536-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1d536-129">Examples</span></span> | <span data-ttu-id="1d536-130">Observações</span><span class="sxs-lookup"><span data-stu-id="1d536-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1d536-131">Ambiente</span><span class="sxs-lookup"><span data-stu-id="1d536-131">Environment</span></span> |<span data-ttu-id="1d536-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="1d536-132">dev, stg, prod</span></span> |<span data-ttu-id="1d536-133">Dependendo da finalidade e do nome de cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="1d536-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="1d536-134">Local</span><span class="sxs-lookup"><span data-stu-id="1d536-134">Location</span></span> |<span data-ttu-id="1d536-135">usw (Oeste dos EUA), use (Leste dos EUA 2)</span><span class="sxs-lookup"><span data-stu-id="1d536-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="1d536-136">Dependendo da região do datacenter ou da região da organização.</span><span class="sxs-lookup"><span data-stu-id="1d536-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="1d536-137">Componente, serviço ou produto do Azure</span><span class="sxs-lookup"><span data-stu-id="1d536-137">Azure component, service, or product</span></span> |<span data-ttu-id="1d536-138">Rg para o grupo de recursos, VNet para a rede virtual</span><span class="sxs-lookup"><span data-stu-id="1d536-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="1d536-139">Dependendo do produto para o qual o recurso oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="1d536-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="1d536-140">Função</span><span class="sxs-lookup"><span data-stu-id="1d536-140">Role</span></span> |<span data-ttu-id="1d536-141">SQL, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="1d536-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="1d536-142">Dependendo da função da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1d536-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="1d536-143">Instância</span><span class="sxs-lookup"><span data-stu-id="1d536-143">Instance</span></span> |<span data-ttu-id="1d536-144">01, 02, 03 etc.</span><span class="sxs-lookup"><span data-stu-id="1d536-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="1d536-145">Para recursos com mais de uma instância.</span><span class="sxs-lookup"><span data-stu-id="1d536-145">For resources that have more than one instance.</span></span> <span data-ttu-id="1d536-146">Por exemplo, servidores Web com balanceamento de carga em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="1d536-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="1d536-147">Ao estabelecer as convenções de nomenclatura, verifique se elas determinam claramente quais afixos devem ser usados para cada tipo de recurso e em qual posição (sufixo versus prefixo).</span><span class="sxs-lookup"><span data-stu-id="1d536-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="1d536-148">Datas</span><span class="sxs-lookup"><span data-stu-id="1d536-148">Dates</span></span>
<span data-ttu-id="1d536-149">Muitas vezes é importante determinar a data da criação do nome de um recurso.</span><span class="sxs-lookup"><span data-stu-id="1d536-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="1d536-150">Recomendamos que o formato de data seja AAAAMMDD.</span><span class="sxs-lookup"><span data-stu-id="1d536-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="1d536-151">Esse formato garante não apenas que a data completa seja registrada, mas também que dois recursos cujos nomes diferem apenas na data sejam classificados em ordem alfabética e em ordem cronológica ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="1d536-151">This format ensures that not only the full date is recorded, but also that two resources whose names differ only on the date is sorted alphabetically and chronologically at the same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="1d536-152">Recursos de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="1d536-152">Naming resources</span></span>
<span data-ttu-id="1d536-153">Defina cada tipo de recurso na convenção de nomenclatura, que deve ter regras que definem como atribuir nomes a cada recurso criado.</span><span class="sxs-lookup"><span data-stu-id="1d536-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="1d536-154">Essas regras devem se aplicar a todos os tipos de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1d536-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="1d536-155">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="1d536-155">Subscriptions</span></span>
* <span data-ttu-id="1d536-156">Contas</span><span class="sxs-lookup"><span data-stu-id="1d536-156">Accounts</span></span>
* <span data-ttu-id="1d536-157">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1d536-157">Storage accounts</span></span>
* <span data-ttu-id="1d536-158">Redes virtuais</span><span class="sxs-lookup"><span data-stu-id="1d536-158">Virtual networks</span></span>
* <span data-ttu-id="1d536-159">Sub-redes</span><span class="sxs-lookup"><span data-stu-id="1d536-159">Subnets</span></span>
* <span data-ttu-id="1d536-160">Conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="1d536-160">Availability sets</span></span>
* <span data-ttu-id="1d536-161">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="1d536-161">Resource groups</span></span>
* <span data-ttu-id="1d536-162">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="1d536-162">Virtual machines</span></span>
* <span data-ttu-id="1d536-163">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="1d536-163">Endpoints</span></span>
* <span data-ttu-id="1d536-164">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="1d536-164">Network security groups</span></span>
* <span data-ttu-id="1d536-165">Funções</span><span class="sxs-lookup"><span data-stu-id="1d536-165">Roles</span></span>

<span data-ttu-id="1d536-166">Para garantir que o nome possa fornecer informações suficientes para determinar a qual recurso ele se refere, você deve usar nomes descritivos.</span><span class="sxs-lookup"><span data-stu-id="1d536-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="1d536-167">Nomes de computadores</span><span class="sxs-lookup"><span data-stu-id="1d536-167">Computer names</span></span>
<span data-ttu-id="1d536-168">Quando você cria uma VM (máquina virtual), o Microsoft Azure exige um nome da VM de até 15 caracteres que é usado para o nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="1d536-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up to 15 characters which is used for the resource name.</span></span> <span data-ttu-id="1d536-169">O Azure usa o mesmo nome para o sistema operacional instalado na VM.</span><span class="sxs-lookup"><span data-stu-id="1d536-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="1d536-170">No entanto, esses nomes nem sempre serão os mesmos.</span><span class="sxs-lookup"><span data-stu-id="1d536-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="1d536-171">No caso de uma VM ser criada por meio de um arquivo de imagem .vhd que já contenha um sistema operacional, o nome da VM no Azure poderá ser diferente do nome do computador do sistema operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="1d536-171">In case a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="1d536-172">Essa situação pode adicionar um grau de dificuldade ao gerenciamento da VM, que, portanto, não é recomendável.</span><span class="sxs-lookup"><span data-stu-id="1d536-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="1d536-173">Atribua ao recurso da VM do Azure o mesmo nome do computador atribuído ao sistema operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="1d536-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="1d536-174">Recomendamos que o nome da VM do Azure seja igual ao nome do computador do sistema operacional subjacente.</span><span class="sxs-lookup"><span data-stu-id="1d536-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="1d536-175">Nomes de contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1d536-175">Storage account names</span></span>
<span data-ttu-id="1d536-176">Esta seção não se aplica ao [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), pois você não cria uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="1d536-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="1d536-177">Para discos não gerenciados, as contas de armazenamento têm regras especiais que regem seus nomes.</span><span class="sxs-lookup"><span data-stu-id="1d536-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="1d536-178">Você pode usar apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="1d536-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="1d536-179">Para obter mais informações, consulte [Criar uma conta de armazenamento](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1d536-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="1d536-180">Além disso, o nome da conta de armazenamento com core.windows.net deve ser um nome DNS exclusivo e globalmente válido.</span><span class="sxs-lookup"><span data-stu-id="1d536-180">Additionally, the storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="1d536-181">Por exemplo, se a conta de armazenamento for chamada de mystorageaccount, os seguintes nomes DNS resultantes devem ser exclusivos:</span><span class="sxs-lookup"><span data-stu-id="1d536-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="1d536-182">minhacontadearmazenamento.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1d536-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="1d536-183">minhacontadearmazenamento.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1d536-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="1d536-184">minhacontadearmazenamento.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1d536-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d536-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d536-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

