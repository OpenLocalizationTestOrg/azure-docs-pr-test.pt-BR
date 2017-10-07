---
title: "máquinas virtuais de aaaReplicate Hyper-V nas nuvens do VMM usando o Azure Site Recovery e PowerShell (Gerenciador de recursos) | Microsoft Docs"
description: "Replicar máquinas virtuais de Hyper-V em nuvens do VMM usando o Azure Site Recovery e PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="69651-103">Replicar máquinas virtuais Hyper-V no tooAzure de nuvens do VMM usando o PowerShell e o Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="69651-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69651-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="69651-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="69651-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="69651-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="69651-106">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="69651-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="69651-107">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="69651-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="69651-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="69651-108">Overview</span></span>
<span data-ttu-id="69651-109">O Azure Site Recovery contribui com a estratégia de recuperação (BCDR) tooyour business desastre e continuidade ao orquestrar a replicação, failover e recuperação de máquinas virtuais em vários cenários de implantação.</span><span class="sxs-lookup"><span data-stu-id="69651-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="69651-110">Para obter uma lista completa de implantação de cenários consulte Olá [visão geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69651-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="69651-111">Este artigo mostra como as tarefas comuns do toouse PowerShell tooautomate precisar tooperform ao configurar máquinas virtuais do Azure Site Recovery tooreplicate Hyper-V no armazenamento do System Center VMM nuvens tooAzure.</span><span class="sxs-lookup"><span data-stu-id="69651-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="69651-112">Olá artigo inclui os pré-requisitos para o cenário de saudação e mostra</span><span class="sxs-lookup"><span data-stu-id="69651-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="69651-113">Como tooset um cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="69651-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="69651-114">Instalar Olá provedor Azure Site Recovery no servidor do VMM de origem de saudação</span><span class="sxs-lookup"><span data-stu-id="69651-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="69651-115">Registrar o servidor de saudação no cofre hello, adicione uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="69651-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="69651-116">Instalar o agente de serviços de recuperação do Azure Olá nos servidores de host do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="69651-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="69651-117">Definir configurações de proteção para nuvens do VMM, que poderá ser máquinas virtuais de tooall aplicada protegido</span><span class="sxs-lookup"><span data-stu-id="69651-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="69651-118">Habilitar a proteção para essas máquina virtuais</span><span class="sxs-lookup"><span data-stu-id="69651-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="69651-119">Teste Olá failover toomake se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="69651-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="69651-120">Se você tiver problemas para configurar esse cenário, publique suas perguntas sobre Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="69651-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="69651-121">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="69651-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="69651-122">Este artigo aborda usando o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="69651-123">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="69651-123">Before you start</span></span>
<span data-ttu-id="69651-124">Verifique se estes pré-requisitos estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="69651-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="69651-125">Pré-requisitos do Azure</span><span class="sxs-lookup"><span data-stu-id="69651-125">Azure prerequisites</span></span>
* <span data-ttu-id="69651-126">Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="69651-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="69651-127">Se não tiver uma, comece com uma [conta gratuita](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="69651-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="69651-128">Além disso, você pode ler sobre Olá [preços do Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="69651-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="69651-129">Se você está experimentando o cenário de assinatura Olá replicação tooa CSP, você terá uma assinatura do CSP.</span><span class="sxs-lookup"><span data-stu-id="69651-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="69651-130">Saiba mais sobre o programa CSP Olá no [como tooenroll no programa CSP Olá](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="69651-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="69651-131">Você precisará de um tooAzure de dados replicados toostore conta do Azure v2 (Gerenciador de recursos) de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="69651-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="69651-132">conta de saudação precisa de replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="69651-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="69651-133">Deve estar no hello mesma região Olá serviço Azure Site Recovery e ser associada a saudação mesma assinatura ou Olá CSP.</span><span class="sxs-lookup"><span data-stu-id="69651-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="69651-134">toolearn mais sobre como configurar o armazenamento do Azure, consulte Olá [tooMicrosoft Introdução armazenamento do Azure](../storage/common/storage-introduction.md) para referência.</span><span class="sxs-lookup"><span data-stu-id="69651-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="69651-135">Você precisará toomake-se de que máquinas virtuais que você deseja tooprotect estejam em conformidade com hello [pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="69651-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="69651-136">Atualmente, apenas operações no nível de VM são possíveis por meio do Powershell.</span><span class="sxs-lookup"><span data-stu-id="69651-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="69651-137">Em breve, será disponibilizado o suporte para operações no nível de plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="69651-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="69651-138">Agora, você está limitado tooperforming falha renovação somente em uma granularidade de 'protected VM' e não em um nível de plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="69651-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="69651-139">Pré-requisitos do VMM</span><span class="sxs-lookup"><span data-stu-id="69651-139">VMM prerequisites</span></span>
* <span data-ttu-id="69651-140">Você precisará do servidor VMM em execução no System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="69651-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="69651-141">Nenhum servidor VMM que contêm máquinas virtuais que você deseja tooprotect devem estar executando o hello provedor Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="69651-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="69651-142">Isso é instalado durante a saudação implantação do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="69651-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="69651-143">Você precisará de pelo menos uma nuvem em Olá servidor VMM que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="69651-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="69651-144">Olá nuvem deve conter:</span><span class="sxs-lookup"><span data-stu-id="69651-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="69651-145">Um ou mais grupos de hosts do VMM</span><span class="sxs-lookup"><span data-stu-id="69651-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="69651-146">Um ou mais servidores de host do Hyper-V ou clusters em cada grupo de host.</span><span class="sxs-lookup"><span data-stu-id="69651-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="69651-147">Um ou mais VMs no servidor de origem Hyper-V de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="69651-148">Saiba mais sobre como configurar nuvens VMM:</span><span class="sxs-lookup"><span data-stu-id="69651-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="69651-149">Leia mais sobre nuvens privadas do VMM no [o que há de novo na nuvem privada com o System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e em [nuvens do VMM 2012 e hello](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="69651-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="69651-150">Saiba mais sobre [Configurando Olá VMM malha de nuvem](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="69651-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="69651-151">Depois que os elementos de malha de nuvem estiverem em vigor, veja como criar nuvens privadas em [Criando uma nuvem privada no VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e [Passo a passo: criando de nuvens privadas com o System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="69651-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="69651-152">Pré-requisitos do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="69651-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="69651-153">Olá servidores host Hyper-V devem estar executando pelo menos **Windows Server 2012** com a função Hyper-V ou **Microsoft Hyper-V Server 2012** e ter Olá as últimas atualizações instaladas.</span><span class="sxs-lookup"><span data-stu-id="69651-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="69651-154">Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereços IP estáticos.</span><span class="sxs-lookup"><span data-stu-id="69651-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="69651-155">Você precisará agente do cluster Olá tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="69651-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="69651-156">Por</span><span class="sxs-lookup"><span data-stu-id="69651-156">For</span></span>
* <span data-ttu-id="69651-157">Para obter instruções, consulte [como tooConfigure agente de réplica do Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="69651-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="69651-158">Qualquer servidor de host do Hyper-V ou cluster para o qual você deseja toomanage proteção deve ser incluído em uma nuvem VMM.</span><span class="sxs-lookup"><span data-stu-id="69651-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="69651-159">Pré-requisitos de mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="69651-159">Network mapping prerequisites</span></span>
<span data-ttu-id="69651-160">Quando você protege as máquinas virtuais no Azure, o mapeamento de rede Olá mapeia redes de máquina virtual Olá no servidor do VMM de origem hello e seguinte de saudação do destino redes do Azure tooenable:</span><span class="sxs-lookup"><span data-stu-id="69651-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="69651-161">Todos os computadores que o failover em Olá mesmo rede pode se conectar a outro, independentemente do plano de recuperação que estão em tooeach.</span><span class="sxs-lookup"><span data-stu-id="69651-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="69651-162">Se um gateway de rede estiver instalado na rede Azure de destino hello, máquinas virtuais podem se conectar a tooother em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="69651-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="69651-163">Se você não configurar o mapeamento de rede, Olá somente máquinas virtuais que falhar em Olá mesmo plano de recuperação será capaz de tooconnect tooeach outros após tooAzure de failover.</span><span class="sxs-lookup"><span data-stu-id="69651-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="69651-164">Se você quiser que o mapeamento de rede toodeploy você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="69651-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="69651-165">saudação de máquinas virtuais que deseja tooprotect no servidor do VMM de origem de saudação deve ser conectado tooa rede VM.</span><span class="sxs-lookup"><span data-stu-id="69651-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="69651-166">Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="69651-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="69651-167">Máquinas de virtuais de toowhich replicado uma rede do Azure podem se conectar após o failover.</span><span class="sxs-lookup"><span data-stu-id="69651-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="69651-168">Você selecionará essa rede no tempo de saudação do failover.</span><span class="sxs-lookup"><span data-stu-id="69651-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="69651-169">rede Olá deve estar no hello mesma região que sua assinatura do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="69651-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="69651-170">Saiba mais sobre mapeamento de rede em</span><span class="sxs-lookup"><span data-stu-id="69651-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="69651-171">Como tooconfigure de redes lógicas no VMM</span><span class="sxs-lookup"><span data-stu-id="69651-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="69651-172">Como tooconfigure VM redes e gateways no VMM</span><span class="sxs-lookup"><span data-stu-id="69651-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="69651-173">Como tooconfigure e monitorar redes virtuais no Azure</span><span class="sxs-lookup"><span data-stu-id="69651-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="69651-174">Pré-requisitos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="69651-174">PowerShell prerequisites</span></span>
<span data-ttu-id="69651-175">Certifique-se de que ter toogo pronto do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="69651-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="69651-176">Se você já estiver usando o PowerShell, você precisará tooupgrade tooversion 0.8.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="69651-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="69651-177">Para obter informações sobre como configurar o PowerShell, consulte Olá [guia tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="69651-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="69651-178">Depois de você ter instalado e configurado o PowerShell, você pode exibir todos os cmdlets de saudação disponíveis para o serviço de saudação [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="69651-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="69651-179">toolearn sobre dicas que podem ajudá-lo a usar os cmdlets de saudação, como como valores de parâmetro, as entradas e saídas são tratadas normalmente no Azure PowerShell, consulte Olá [guia de Introdução aos Cmdlets do Azure de tooget](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="69651-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="69651-180">Etapa 1: Definir a assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="69651-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="69651-181">Do powershell do Azure, logon tooyour conta do Azure: usando Olá cmdlets a seguir</span><span class="sxs-lookup"><span data-stu-id="69651-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="69651-182">Obtenha uma lista das suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="69651-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="69651-183">Isso também listará Olá subscriptionIDs para cada uma das assinaturas hello.</span><span class="sxs-lookup"><span data-stu-id="69651-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="69651-184">Anote a subscriptionID Olá de assinatura Olá no qual você deseja que o Cofre de serviços de recuperação de saudação toocreate</span><span class="sxs-lookup"><span data-stu-id="69651-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="69651-185">Assinatura de saudação conjunto no qual Olá Cofre de serviços de recuperação é toobe criado pelo mencionar Olá ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="69651-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="69651-186">Etapa 2: Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="69651-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="69651-187">Crie um grupo de recursos no Azure Resource Manager se você ainda não tiver um</span><span class="sxs-lookup"><span data-stu-id="69651-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="69651-188">Criar um novo cofre de serviços de recuperação e salve Olá criada o objeto de Cofre de recuperação automatizada do sistema em uma variável (será usada posteriormente).</span><span class="sxs-lookup"><span data-stu-id="69651-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="69651-189">Você também pode recuperar Olá ASR cofre post criação do objeto usando o cmdlet Get-AzureRMRecoveryServicesVault de saudação:-</span><span class="sxs-lookup"><span data-stu-id="69651-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="69651-190">Etapa 3: Definir o contexto de Cofre de serviços de recuperação de saudação</span><span class="sxs-lookup"><span data-stu-id="69651-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="69651-191">Definir o contexto de Cofre de saudação executando Olá comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="69651-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="69651-192">Etapa 4: Instalar Olá provedor Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="69651-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="69651-193">Na máquina do VMM hello, crie um diretório executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="69651-194">Extrair arquivos hello usando o provedor de saudação baixada executando o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="69651-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="69651-195">Instale o provedor de saudação usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-195">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="69651-196">Aguarde Olá toofinish de instalação.</span><span class="sxs-lookup"><span data-stu-id="69651-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="69651-197">Registre o servidor de saudação no cofre de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="69651-198">Etapa 5: criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="69651-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="69651-199">Se você não tiver uma conta de armazenamento do Azure, crie uma conta de replicação geográfica habilitada no hello mesma área geográfica como Olá cofre executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="69651-200">Observe que a conta de armazenamento Olá deve ser Olá mesma região que o serviço do Azure Site Recovery hello e associar Olá a mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="69651-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="69651-201">Etapa 6: Instalar hello Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="69651-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="69651-202">Baixar o agente de serviços de recuperação do Azure Olá em [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e instale-o em cada servidor de host do Hyper-V localizado nas Olá VMM nuvens que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="69651-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="69651-203">Execute Olá comando a seguir em todos os hosts do VMM:</span><span class="sxs-lookup"><span data-stu-id="69651-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="69651-204">Etapa 7: definir as configurações da proteção de nuvem</span><span class="sxs-lookup"><span data-stu-id="69651-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="69651-205">Crie um tooAzure de política de replicação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="69651-206">Obtenha um contêiner de proteção executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="69651-207">Obter Olá política detalhes tooa variável usando Olá trabalho que foi criado e mencione o nome da política amigável hello:</span><span class="sxs-lookup"><span data-stu-id="69651-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="69651-208">Inicie associação de saudação do recipiente de proteção de saudação com a política de replicação hello:</span><span class="sxs-lookup"><span data-stu-id="69651-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="69651-209">Após o trabalho de hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="69651-210">Depois que o trabalho de saudação concluiu o processamento, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="69651-211">conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="69651-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="69651-212">Etapa 8: configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="69651-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="69651-213">Antes de começar o mapeamento de rede Verifique se máquinas virtuais no servidor do VMM de origem de saudação tooa conectado rede VM.</span><span class="sxs-lookup"><span data-stu-id="69651-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="69651-214">Além disso, crie uma ou mais redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="69651-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="69651-215">Saiba mais sobre como toocreate a virtual de rede usando o Gerenciador de recursos do Azure e o PowerShell, no [criar uma rede virtual com uma conexão de VPN site a site usando o Gerenciador de recursos do Azure e o PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="69651-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="69651-216">Observe que várias redes de máquina Virtual podem ser mapeado tooa única rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="69651-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="69651-217">Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover.</span><span class="sxs-lookup"><span data-stu-id="69651-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="69651-218">Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="69651-219">Olá primeiro comando obtém servidores para o Cofre de recuperação de Site do Azure atual hello.</span><span class="sxs-lookup"><span data-stu-id="69651-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="69651-220">comando Olá armazena servidores do Microsoft Azure Site Recovery Olá na variável de matriz de saudação $Servers.</span><span class="sxs-lookup"><span data-stu-id="69651-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="69651-221">Olá segundo comando obtém a rede de recuperação de site Olá para o primeiro servidor de saudação na matriz de saudação $Servers.</span><span class="sxs-lookup"><span data-stu-id="69651-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="69651-222">comando Olá armazena redes Olá na variável de saudação $Networks.</span><span class="sxs-lookup"><span data-stu-id="69651-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="69651-223">Olá terceiro comando obtém as redes virtuais do Azure e, em seguida, esse valor na variável Olá $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="69651-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="69651-224">Olá final cria um mapeamento entre Olá primário e rede Olá máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="69651-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="69651-225">Olá cmdlet especifica a rede primária hello como o primeiro elemento de saudação do $Networks.</span><span class="sxs-lookup"><span data-stu-id="69651-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="69651-226">Olá cmdlet especifica uma rede de máquina virtual como o primeiro elemento de saudação do $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="69651-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="69651-227">Etapa 9: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="69651-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="69651-228">Depois de redes, nuvens e servidores Olá estão configurados corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="69651-229">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="69651-229">Note hello following:</span></span>

* <span data-ttu-id="69651-230">As máquinas virtuais devem cumprir os requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="69651-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="69651-231">Verifique essas [pré-requisitos e suporte](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) no guia de planejamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="69651-232">proteção tooenable, sistema operacional de saudação e propriedades do disco do sistema operacional devem ser definidas para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="69651-233">Quando você cria uma máquina virtual no VMM usando um modelo de máquina virtual, você pode definir propriedade de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="69651-234">Você também pode definir essas propriedades para máquinas virtuais existentes em Olá **geral** e **configuração de Hardware** guias de propriedades de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="69651-235">Se você não definir essas propriedades no VMM, você será capaz de tooconfigure-los no portal do Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="69651-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="69651-236">proteção de tooenable executar Olá contêiner de proteção do comando tooget Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="69651-237">Obtenha a entidade de proteção de saudação (VM) executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="69651-238">Habilite hello DR para Olá VM executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="69651-239">Testar a implantação</span><span class="sxs-lookup"><span data-stu-id="69651-239">Test your deployment</span></span>
<span data-ttu-id="69651-240">tootest sua implantação, você pode executar um teste de failover em uma única máquina virtual, ou crie um plano de recuperação consiste em várias máquinas virtuais e executar um teste de failover para o plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="69651-241">O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.</span><span class="sxs-lookup"><span data-stu-id="69651-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="69651-242">Observe que:</span><span class="sxs-lookup"><span data-stu-id="69651-242">Note that:</span></span>

* <span data-ttu-id="69651-243">Se você quiser tooconnect toohello VM no Azure usando a área de trabalho remota após failover hello, habilite Conexão de área de trabalho remota na máquina virtual de saudação antes de executar o failover de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="69651-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="69651-244">Após o failover, você usará uma público IP endereço tooconnect toohello VM no Azure usando a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="69651-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="69651-245">Se você quiser toodo isso, certifique-se de que você não tem qualquer política de domínio que impedem a máquina de virtual tooa conectar usando um endereço público.</span><span class="sxs-lookup"><span data-stu-id="69651-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="69651-246">conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="69651-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="69651-247">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="69651-247">Run a test failover</span></span>
- <span data-ttu-id="69651-248">Inicie o failover de teste Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="69651-249">Executar um failover planejado</span><span class="sxs-lookup"><span data-stu-id="69651-249">Run a planned failover</span></span>
- <span data-ttu-id="69651-250">Saudação de iniciar o failover planejado executando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="69651-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="69651-251">Executar um failover não planejado</span><span class="sxs-lookup"><span data-stu-id="69651-251">Run an unplanned failover</span></span>
- <span data-ttu-id="69651-252">Iniciar Olá failover não planejado executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="69651-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="69651-253"><a name=monitor></a> Monitorar a atividade</span><span class="sxs-lookup"><span data-stu-id="69651-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="69651-254">Use hello atividade de saudação toomonitor comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="69651-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="69651-255">Observe que você tenha toowait entre trabalhos de saudação toofinish de processamento.</span><span class="sxs-lookup"><span data-stu-id="69651-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="69651-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69651-256">Next steps</span></span>
<span data-ttu-id="69651-257">[Leia mais](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="69651-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
