---
title: diretrizes - Linux de nomenclatura de infraestrutura de aaaAzure | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para nomear nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="f328b-103">Diretrizes de nomenclatura de infraestrutura do Azure para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="f328b-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="f328b-104">Este artigo se concentra em entender como tooapproach convenções de nomenclatura para todos os seus toobuild vários recursos do Azure a lógica e facilmente identificável conjunto de recursos em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="f328b-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="f328b-105">Diretrizes de implementação de convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="f328b-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="f328b-106">Decisões:</span><span class="sxs-lookup"><span data-stu-id="f328b-106">Decisions:</span></span>

* <span data-ttu-id="f328b-107">Quais são as suas convenções de nomenclatura de recursos do Azure?</span><span class="sxs-lookup"><span data-stu-id="f328b-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="f328b-108">Tarefas:</span><span class="sxs-lookup"><span data-stu-id="f328b-108">Tasks:</span></span>

* <span data-ttu-id="f328b-109">Defina o hello afixos toouse em sua consistência toomaintain de recursos.</span><span class="sxs-lookup"><span data-stu-id="f328b-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="f328b-110">Defina a conta de armazenamento nomes Olá requisito para que eles toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="f328b-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="f328b-111">Saudação de documento toobe de convenção de nomenclatura usada e distribuir tooall partes envolvidas tooensure consistência em implantações.</span><span class="sxs-lookup"><span data-stu-id="f328b-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="f328b-112">Convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="f328b-112">Naming conventions</span></span>
<span data-ttu-id="f328b-113">Você deve ter uma boa convenção de nomenclatura definida para criar qualquer coisa no Azure.</span><span class="sxs-lookup"><span data-stu-id="f328b-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="f328b-114">Uma convenção de nomenclatura garante que todos os recursos de saudação tenham um nome previsível, o que ajuda a menor sobrecarga administrativa de saudação associada ao gerenciamento desses recursos.</span><span class="sxs-lookup"><span data-stu-id="f328b-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="f328b-115">Você pode escolher um conjunto específico de convenções de nomenclatura definidas para toda a organização ou para uma assinatura do Azure específica ou uma conta de toofollow.</span><span class="sxs-lookup"><span data-stu-id="f328b-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="f328b-116">Embora seja fácil para pessoas físicas em regras implícitas de tooestablish organizações ao trabalhar com recursos do Azure, você precisa tooscale capaz de toobe para equipes que trabalham juntas no Azure.</span><span class="sxs-lookup"><span data-stu-id="f328b-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="f328b-117">Entrem em um acordo sobre um conjunto de convenções de nomenclatura antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="f328b-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="f328b-118">Há algumas considerações sobre convenções de nomenclatura que abrangem vários conjuntos de regras.</span><span class="sxs-lookup"><span data-stu-id="f328b-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="f328b-119">Afixos</span><span class="sxs-lookup"><span data-stu-id="f328b-119">Affixes</span></span>
<span data-ttu-id="f328b-120">Como analisar toodefine uma convenção de nomenclatura, uma decisão é se afixo Olá em:</span><span class="sxs-lookup"><span data-stu-id="f328b-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="f328b-121">início de saudação do nome de saudação (prefixo)</span><span class="sxs-lookup"><span data-stu-id="f328b-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="f328b-122">final de saudação do nome de saudação (sufixo)</span><span class="sxs-lookup"><span data-stu-id="f328b-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="f328b-123">Por exemplo, aqui estão dois nomes possíveis para um grupo de recursos usando Olá `rg` fixar:</span><span class="sxs-lookup"><span data-stu-id="f328b-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="f328b-124">Rg-WebApp (prefixo)</span><span class="sxs-lookup"><span data-stu-id="f328b-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="f328b-125">WebApp-Rg (sufixo)</span><span class="sxs-lookup"><span data-stu-id="f328b-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="f328b-126">Afixos podem se referir a toodifferent aspectos que descrevem recursos específicos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f328b-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="f328b-127">Olá tabela a seguir mostra alguns exemplos usados normalmente.</span><span class="sxs-lookup"><span data-stu-id="f328b-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="f328b-128">Aspecto</span><span class="sxs-lookup"><span data-stu-id="f328b-128">Aspect</span></span> | <span data-ttu-id="f328b-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f328b-129">Examples</span></span> | <span data-ttu-id="f328b-130">Observações</span><span class="sxs-lookup"><span data-stu-id="f328b-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f328b-131">Ambiente</span><span class="sxs-lookup"><span data-stu-id="f328b-131">Environment</span></span> |<span data-ttu-id="f328b-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="f328b-132">dev, stg, prod</span></span> |<span data-ttu-id="f328b-133">Dependendo da finalidade hello e o nome de cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="f328b-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="f328b-134">Local</span><span class="sxs-lookup"><span data-stu-id="f328b-134">Location</span></span> |<span data-ttu-id="f328b-135">usw (Oeste dos EUA), use (Leste dos EUA 2)</span><span class="sxs-lookup"><span data-stu-id="f328b-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="f328b-136">Dependendo da região de saudação do datacenter hello ou região de saudação da organização hello.</span><span class="sxs-lookup"><span data-stu-id="f328b-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="f328b-137">Componente, serviço ou produto do Azure</span><span class="sxs-lookup"><span data-stu-id="f328b-137">Azure component, service, or product</span></span> |<span data-ttu-id="f328b-138">Rg para o grupo de recursos, VNet para a rede virtual</span><span class="sxs-lookup"><span data-stu-id="f328b-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="f328b-139">Dependendo do produto Olá para qual Olá recursos oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="f328b-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="f328b-140">Função</span><span class="sxs-lookup"><span data-stu-id="f328b-140">Role</span></span> |<span data-ttu-id="f328b-141">db, app, web</span><span class="sxs-lookup"><span data-stu-id="f328b-141">db, app, web</span></span> |<span data-ttu-id="f328b-142">Dependendo da função hello da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f328b-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="f328b-143">Instância</span><span class="sxs-lookup"><span data-stu-id="f328b-143">Instance</span></span> |<span data-ttu-id="f328b-144">01, 02, 03 etc.</span><span class="sxs-lookup"><span data-stu-id="f328b-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="f328b-145">Para recursos com mais de uma instância.</span><span class="sxs-lookup"><span data-stu-id="f328b-145">For resources that have more than one instance.</span></span> <span data-ttu-id="f328b-146">Por exemplo, servidores Web com balanceamento de carga em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="f328b-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="f328b-147">Ao estabelecer convenções de nomenclatura, certifique-se de que elas determinam claramente que affixes toouse para cada tipo de recurso e em qual posição (prefixo sufixo do vs).</span><span class="sxs-lookup"><span data-stu-id="f328b-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="f328b-148">Datas</span><span class="sxs-lookup"><span data-stu-id="f328b-148">Dates</span></span>
<span data-ttu-id="f328b-149">Geralmente é data de saudação toodetermine importante da criação do nome de saudação de um recurso.</span><span class="sxs-lookup"><span data-stu-id="f328b-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="f328b-150">Recomendamos que o formato de data Olá AAAAMMDD.</span><span class="sxs-lookup"><span data-stu-id="f328b-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="f328b-151">Esse formato garante que não só Olá completo data é registrada, mas também que dois recursos cujos nomes são diferentes apenas em data Olá são classificados em ordem alfabética e em ordem cronológica.</span><span class="sxs-lookup"><span data-stu-id="f328b-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="f328b-152">Recursos de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="f328b-152">Naming resources</span></span>
<span data-ttu-id="f328b-153">Defina cada tipo de recurso na convenção de nomenclatura hello, que deve ter regras que definem como tooassign nomes de recurso de tooeach que é criado.</span><span class="sxs-lookup"><span data-stu-id="f328b-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="f328b-154">Essas regras devem se aplicam a tipos de tooall de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f328b-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="f328b-155">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="f328b-155">Subscriptions</span></span>
* <span data-ttu-id="f328b-156">Contas</span><span class="sxs-lookup"><span data-stu-id="f328b-156">Accounts</span></span>
* <span data-ttu-id="f328b-157">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f328b-157">Storage accounts</span></span>
* <span data-ttu-id="f328b-158">Redes virtuais</span><span class="sxs-lookup"><span data-stu-id="f328b-158">Virtual networks</span></span>
* <span data-ttu-id="f328b-159">Sub-redes</span><span class="sxs-lookup"><span data-stu-id="f328b-159">Subnets</span></span>
* <span data-ttu-id="f328b-160">Conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="f328b-160">Availability sets</span></span>
* <span data-ttu-id="f328b-161">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="f328b-161">Resource groups</span></span>
* <span data-ttu-id="f328b-162">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f328b-162">Virtual machines</span></span>
* <span data-ttu-id="f328b-163">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="f328b-163">Endpoints</span></span>
* <span data-ttu-id="f328b-164">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f328b-164">Network security groups</span></span>
* <span data-ttu-id="f328b-165">Funções</span><span class="sxs-lookup"><span data-stu-id="f328b-165">Roles</span></span>

<span data-ttu-id="f328b-166">tooensure que Olá nome fornece recursos de toowhich suficientes informações toodetermine refere-se, você deve usar nomes descritivos.</span><span class="sxs-lookup"><span data-stu-id="f328b-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="f328b-167">Nomes de computadores</span><span class="sxs-lookup"><span data-stu-id="f328b-167">Computer names</span></span>
<span data-ttu-id="f328b-168">Quando você cria uma máquina virtual (VM), o Azure requer um nome de VM do too64 caracteres que é usado para o nome do recurso hello.</span><span class="sxs-lookup"><span data-stu-id="f328b-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="f328b-169">Azure usa Olá mesmo nome para o sistema operacional de saudação instalado na VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="f328b-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="f328b-170">No entanto, esses nomes podem não sempre ser Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="f328b-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="f328b-171">Se uma VM é criada a partir de um arquivo de imagem. vhd que já contém um sistema operacional, nome da VM Olá no Azure pode diferir da saudação nome de computador do sistema operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="f328b-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="f328b-172">Essa situação pode adicionar um grau de gerenciamento de tooVM dificuldade, que, portanto, não é recomendável.</span><span class="sxs-lookup"><span data-stu-id="f328b-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="f328b-173">Atribua Olá Olá do recurso de VM do Azure mesmo nome como nome do computador Olá que você atribua toohello sistema de operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="f328b-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="f328b-174">É recomendável que esse nome de VM do Azure Olá é Olá igual a saudação subjacente de nome de computador do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f328b-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="f328b-175">Nomes de contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f328b-175">Storage account names</span></span>
<span data-ttu-id="f328b-176">Esta seção não se aplica muito[discos gerenciado do Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), pois você não criar uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="f328b-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="f328b-177">Para discos não gerenciados, as contas de armazenamento têm regras especiais que regem seus nomes.</span><span class="sxs-lookup"><span data-stu-id="f328b-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="f328b-178">Você pode usar apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="f328b-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="f328b-179">Para obter mais informações, consulte [Criar uma conta de armazenamento](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="f328b-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="f328b-180">Além disso, o nome de conta de armazenamento hello, com t, deve ser um nome DNS global válido e exclusivo.</span><span class="sxs-lookup"><span data-stu-id="f328b-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="f328b-181">Por exemplo, se a conta de armazenamento Olá é chamada mystorageaccount, hello nomes DNS resultantes a seguir devem ser exclusivos:</span><span class="sxs-lookup"><span data-stu-id="f328b-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="f328b-182">minhacontadearmazenamento.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f328b-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="f328b-183">minhacontadearmazenamento.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f328b-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="f328b-184">minhacontadearmazenamento.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f328b-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="f328b-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f328b-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

