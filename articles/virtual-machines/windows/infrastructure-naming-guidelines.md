---
title: infraestrutura aaaAzure nomenclatura diretrizes - Windows | Microsoft Docs
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para nomear nos serviços de infraestrutura do Azure."
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
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="e554f-103">Diretrizes de nomenclatura de infraestrutura do Azure para VMs Windows</span><span class="sxs-lookup"><span data-stu-id="e554f-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="e554f-104">Este artigo se concentra em entender como tooapproach convenções de nomenclatura para todos os seus toobuild vários recursos do Azure a lógica e facilmente identificável conjunto de recursos em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e554f-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="e554f-105">Diretrizes de implementação de convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="e554f-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="e554f-106">Decisões:</span><span class="sxs-lookup"><span data-stu-id="e554f-106">Decisions:</span></span>

* <span data-ttu-id="e554f-107">Quais são as suas convenções de nomenclatura de recursos do Azure?</span><span class="sxs-lookup"><span data-stu-id="e554f-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="e554f-108">Tarefas:</span><span class="sxs-lookup"><span data-stu-id="e554f-108">Tasks:</span></span>

* <span data-ttu-id="e554f-109">Defina o hello afixos toouse em sua consistência toomaintain de recursos.</span><span class="sxs-lookup"><span data-stu-id="e554f-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="e554f-110">Defina a conta de armazenamento nomes Olá requisito para que eles toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="e554f-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="e554f-111">Saudação de documento toobe de convenção de nomenclatura usada e distribuir tooall partes envolvidas tooensure consistência em implantações.</span><span class="sxs-lookup"><span data-stu-id="e554f-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="e554f-112">Convenções de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="e554f-112">Naming conventions</span></span>
<span data-ttu-id="e554f-113">Você deve ter uma boa convenção de nomenclatura definida para criar qualquer coisa no Azure.</span><span class="sxs-lookup"><span data-stu-id="e554f-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="e554f-114">Uma convenção de nomenclatura garante que todos os recursos de saudação tenham um nome previsível, o que ajuda a menor sobrecarga administrativa de saudação associada ao gerenciamento desses recursos.</span><span class="sxs-lookup"><span data-stu-id="e554f-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="e554f-115">Você pode escolher um conjunto específico de convenções de nomenclatura definidas para toda a organização ou para uma assinatura do Azure específica ou uma conta de toofollow.</span><span class="sxs-lookup"><span data-stu-id="e554f-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="e554f-116">Embora seja fácil para pessoas físicas em regras implícitas do organizações tooestablish quando estiver trabalhando com recursos do Azure, quando uma equipe precisa toowork em um projeto no Azure, esse modelo não escala bem.</span><span class="sxs-lookup"><span data-stu-id="e554f-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, when a team needs toowork on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="e554f-117">Entrem em um acordo sobre um conjunto de convenções de nomenclatura antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="e554f-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="e554f-118">Há algumas considerações sobre as convenções de nomenclatura que abrangem esses conjuntos de regras.</span><span class="sxs-lookup"><span data-stu-id="e554f-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="e554f-119">Afixos</span><span class="sxs-lookup"><span data-stu-id="e554f-119">Affixes</span></span>
<span data-ttu-id="e554f-120">Como analisar toodefine uma convenção de nomenclatura, uma decisão vem estejam afixo hello:</span><span class="sxs-lookup"><span data-stu-id="e554f-120">As you look toodefine a naming convention, one decision comes whether hello affix is at:</span></span>

* <span data-ttu-id="e554f-121">início de saudação do nome de saudação (prefixo)</span><span class="sxs-lookup"><span data-stu-id="e554f-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="e554f-122">final de saudação do nome de saudação (sufixo)</span><span class="sxs-lookup"><span data-stu-id="e554f-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="e554f-123">Por exemplo, aqui estão dois nomes possíveis para um grupo de recursos usando Olá `rg` fixar:</span><span class="sxs-lookup"><span data-stu-id="e554f-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="e554f-124">Rg-WebApp (prefixo)</span><span class="sxs-lookup"><span data-stu-id="e554f-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="e554f-125">WebApp-Rg (sufixo)</span><span class="sxs-lookup"><span data-stu-id="e554f-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="e554f-126">Afixos podem se referir a toodifferent aspectos que descrevem recursos específicos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e554f-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="e554f-127">Olá tabela a seguir mostra alguns exemplos usados normalmente.</span><span class="sxs-lookup"><span data-stu-id="e554f-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="e554f-128">Aspecto</span><span class="sxs-lookup"><span data-stu-id="e554f-128">Aspect</span></span> | <span data-ttu-id="e554f-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e554f-129">Examples</span></span> | <span data-ttu-id="e554f-130">Observações</span><span class="sxs-lookup"><span data-stu-id="e554f-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e554f-131">Ambiente</span><span class="sxs-lookup"><span data-stu-id="e554f-131">Environment</span></span> |<span data-ttu-id="e554f-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="e554f-132">dev, stg, prod</span></span> |<span data-ttu-id="e554f-133">Dependendo da finalidade hello e o nome de cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="e554f-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="e554f-134">Local</span><span class="sxs-lookup"><span data-stu-id="e554f-134">Location</span></span> |<span data-ttu-id="e554f-135">usw (Oeste dos EUA), use (Leste dos EUA 2)</span><span class="sxs-lookup"><span data-stu-id="e554f-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="e554f-136">Dependendo da região de saudação do datacenter hello ou região de saudação da organização hello.</span><span class="sxs-lookup"><span data-stu-id="e554f-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="e554f-137">Componente, serviço ou produto do Azure</span><span class="sxs-lookup"><span data-stu-id="e554f-137">Azure component, service, or product</span></span> |<span data-ttu-id="e554f-138">Rg para o grupo de recursos, VNet para a rede virtual</span><span class="sxs-lookup"><span data-stu-id="e554f-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="e554f-139">Dependendo do produto Olá para qual Olá recursos oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="e554f-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="e554f-140">Função</span><span class="sxs-lookup"><span data-stu-id="e554f-140">Role</span></span> |<span data-ttu-id="e554f-141">SQL, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="e554f-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="e554f-142">Dependendo da função hello da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e554f-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="e554f-143">Instância</span><span class="sxs-lookup"><span data-stu-id="e554f-143">Instance</span></span> |<span data-ttu-id="e554f-144">01, 02, 03 etc.</span><span class="sxs-lookup"><span data-stu-id="e554f-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="e554f-145">Para recursos com mais de uma instância.</span><span class="sxs-lookup"><span data-stu-id="e554f-145">For resources that have more than one instance.</span></span> <span data-ttu-id="e554f-146">Por exemplo, servidores Web com balanceamento de carga em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e554f-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="e554f-147">Ao estabelecer convenções de nomenclatura, certifique-se de que elas determinam claramente que affixes toouse para cada tipo de recurso e em qual posição (prefixo sufixo do vs).</span><span class="sxs-lookup"><span data-stu-id="e554f-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="e554f-148">Datas</span><span class="sxs-lookup"><span data-stu-id="e554f-148">Dates</span></span>
<span data-ttu-id="e554f-149">Geralmente é data de saudação toodetermine importante da criação do nome de saudação de um recurso.</span><span class="sxs-lookup"><span data-stu-id="e554f-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="e554f-150">Recomendamos que o formato de data Olá AAAAMMDD.</span><span class="sxs-lookup"><span data-stu-id="e554f-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="e554f-151">Esse formato garante que não apenas data completa Olá é registrada, mas também que dois recursos cujos nomes são diferentes apenas na data de saudação é classificada em ordem alfabética e em ordem cronológica em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="e554f-151">This format ensures that not only hello full date is recorded, but also that two resources whose names differ only on hello date is sorted alphabetically and chronologically at hello same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="e554f-152">Recursos de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="e554f-152">Naming resources</span></span>
<span data-ttu-id="e554f-153">Defina cada tipo de recurso na convenção de nomenclatura hello, que deve ter regras que definem como tooassign nomes de recurso de tooeach que é criado.</span><span class="sxs-lookup"><span data-stu-id="e554f-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="e554f-154">Essas regras devem se aplicam a tipos de tooall de recursos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e554f-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="e554f-155">Assinaturas</span><span class="sxs-lookup"><span data-stu-id="e554f-155">Subscriptions</span></span>
* <span data-ttu-id="e554f-156">Contas</span><span class="sxs-lookup"><span data-stu-id="e554f-156">Accounts</span></span>
* <span data-ttu-id="e554f-157">Contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e554f-157">Storage accounts</span></span>
* <span data-ttu-id="e554f-158">Redes virtuais</span><span class="sxs-lookup"><span data-stu-id="e554f-158">Virtual networks</span></span>
* <span data-ttu-id="e554f-159">Sub-redes</span><span class="sxs-lookup"><span data-stu-id="e554f-159">Subnets</span></span>
* <span data-ttu-id="e554f-160">Conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="e554f-160">Availability sets</span></span>
* <span data-ttu-id="e554f-161">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="e554f-161">Resource groups</span></span>
* <span data-ttu-id="e554f-162">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e554f-162">Virtual machines</span></span>
* <span data-ttu-id="e554f-163">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="e554f-163">Endpoints</span></span>
* <span data-ttu-id="e554f-164">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="e554f-164">Network security groups</span></span>
* <span data-ttu-id="e554f-165">Funções</span><span class="sxs-lookup"><span data-stu-id="e554f-165">Roles</span></span>

<span data-ttu-id="e554f-166">tooensure que Olá nome fornece recursos de toowhich suficientes informações toodetermine refere-se, você deve usar nomes descritivos.</span><span class="sxs-lookup"><span data-stu-id="e554f-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="e554f-167">Nomes de computadores</span><span class="sxs-lookup"><span data-stu-id="e554f-167">Computer names</span></span>
<span data-ttu-id="e554f-168">Quando você cria uma máquina virtual (VM), o Microsoft Azure requer um nome de VM do too15 caracteres que é usado para o nome do recurso hello.</span><span class="sxs-lookup"><span data-stu-id="e554f-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up too15 characters which is used for hello resource name.</span></span> <span data-ttu-id="e554f-169">Azure usa Olá mesmo nome para o sistema operacional de saudação instalado na VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="e554f-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="e554f-170">No entanto, esses nomes podem não sempre ser Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="e554f-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="e554f-171">No caso de uma VM é criada a partir de um arquivo de imagem. vhd que já contém um sistema operacional, nome da VM Olá no Azure pode diferir da saudação nome de computador do sistema operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="e554f-171">In case a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="e554f-172">Essa situação pode adicionar um grau de gerenciamento de tooVM dificuldade, que, portanto, não é recomendável.</span><span class="sxs-lookup"><span data-stu-id="e554f-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="e554f-173">Atribua Olá Olá do recurso de VM do Azure mesmo nome como nome do computador Olá que você atribua toohello sistema de operacional da VM.</span><span class="sxs-lookup"><span data-stu-id="e554f-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="e554f-174">É recomendável que esse nome de VM do Azure Olá é Olá igual a saudação subjacente de nome de computador do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="e554f-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="e554f-175">Nomes de contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e554f-175">Storage account names</span></span>
<span data-ttu-id="e554f-176">Esta seção não se aplica muito[discos gerenciado do Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), pois você não criar uma conta de armazenamento separada.</span><span class="sxs-lookup"><span data-stu-id="e554f-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="e554f-177">Para discos não gerenciados, as contas de armazenamento têm regras especiais que regem seus nomes.</span><span class="sxs-lookup"><span data-stu-id="e554f-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="e554f-178">Você pode usar apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="e554f-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="e554f-179">Para obter mais informações, consulte [Criar uma conta de armazenamento](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e554f-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="e554f-180">Além disso, o nome de conta de armazenamento hello, juntamente com t, deve ser um nome DNS exclusivo globalmente válido.</span><span class="sxs-lookup"><span data-stu-id="e554f-180">Additionally, hello storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="e554f-181">Por exemplo, se a conta de armazenamento Olá é chamada mystorageaccount, hello nomes DNS resultantes a seguir devem ser exclusivos:</span><span class="sxs-lookup"><span data-stu-id="e554f-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="e554f-182">minhacontadearmazenamento.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e554f-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="e554f-183">minhacontadearmazenamento.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e554f-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="e554f-184">minhacontadearmazenamento.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e554f-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="e554f-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e554f-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

