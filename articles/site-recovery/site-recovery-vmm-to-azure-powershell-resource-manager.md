---
title: "Replicar máquinas virtuais Hyper-V em nuvens do VMM usando o Azure Site Recovery e o PowerShell (Resource Manager) | Microsoft Docs"
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
ms.openlocfilehash: 34086044db752f09f1282517b59856091e85c2fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="a2c19-103">Replicar máquinas virtuais Hyper-V em nuvens VMM para Azure usando o PowerShell e o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a2c19-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2c19-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a2c19-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="a2c19-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a2c19-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="a2c19-106">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="a2c19-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="a2c19-107">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="a2c19-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="a2c19-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a2c19-108">Overview</span></span>
<span data-ttu-id="a2c19-109">O Azure Site Recovery colabora com sua estratégia de BCDR (continuidade de negócios e recuperação de desastre) gerenciando replicação, failover e recuperação de máquinas virtuais em vários cenários de implantação.</span><span class="sxs-lookup"><span data-stu-id="a2c19-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="a2c19-110">Para obter uma lista completa de cenários de implantação, consulte a [Visão geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2c19-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="a2c19-111">Este artigo mostra como usar o PowerShell para automatizar tarefas comuns que você precisa executar quando você configura o Azure Site Recovery para replicar máquinas virtuais Hyper-V em nuvens do System Center VMM para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="a2c19-112">O artigo inclui pré-requisitos para o cenário e mostra a você como:</span><span class="sxs-lookup"><span data-stu-id="a2c19-112">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="a2c19-113">Configurar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="a2c19-113">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="a2c19-114">Instalar o Provedor do Azure Site Recovery no servidor VMM de origem</span><span class="sxs-lookup"><span data-stu-id="a2c19-114">Install the Azure Site Recovery Provider on the source VMM server</span></span>
* <span data-ttu-id="a2c19-115">Registrar o servidor no cofre e adicionar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a2c19-115">Register the server in the vault, add an Azure storage account</span></span>
* <span data-ttu-id="a2c19-116">Instalar o agente dos Serviços de Recuperação do Azure nos servidores host do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a2c19-116">Install the Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="a2c19-117">Configurar as definições de proteção para nuvens VMM, que serão aplicadas a todas as máquinas virtuais protegidas</span><span class="sxs-lookup"><span data-stu-id="a2c19-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="a2c19-118">Habilitar a proteção para essas máquina virtuais</span><span class="sxs-lookup"><span data-stu-id="a2c19-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="a2c19-119">Testar o failover para garantir que tudo esteja funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="a2c19-119">Test the fail-over to make sure everything's working as expected.</span></span>

<span data-ttu-id="a2c19-120">Se você enfrentar problemas ao configurar esse cenário, publique suas perguntas no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a2c19-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="a2c19-121">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a2c19-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a2c19-122">Este artigo aborda o uso do modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="a2c19-122">This article covers using the Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="a2c19-123">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a2c19-123">Before you start</span></span>
<span data-ttu-id="a2c19-124">Verifique se estes pré-requisitos estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="a2c19-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="a2c19-125">Pré-requisitos do Azure</span><span class="sxs-lookup"><span data-stu-id="a2c19-125">Azure prerequisites</span></span>
* <span data-ttu-id="a2c19-126">Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="a2c19-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="a2c19-127">Se não tiver uma, comece com uma [conta gratuita](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="a2c19-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="a2c19-128">Além disso, você pode ler sobre os [preços do Gerenciador do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a2c19-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="a2c19-129">Você precisará de uma assinatura CSP se estiver tentando a replicação em um cenário de assinatura CSP.</span><span class="sxs-lookup"><span data-stu-id="a2c19-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span></span> <span data-ttu-id="a2c19-130">Saiba mais sobre o programa CSP em [como se registrar no programa CSP](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2c19-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="a2c19-131">Será necessária uma conta de armazenamento do Azure v2 (Resource Manager) para armazenar os dados replicados no Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span></span> <span data-ttu-id="a2c19-132">A conta precisa estar com a replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="a2c19-132">The account needs geo-replication enabled.</span></span> <span data-ttu-id="a2c19-133">Ela deve estar localizada na mesma região que o serviço Azure Site Recovery e estar associada à mesma assinatura ou assinatura CSP.</span><span class="sxs-lookup"><span data-stu-id="a2c19-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span></span> <span data-ttu-id="a2c19-134">Para aprender mais sobre como configurar o armazenamento do Azure, confira [Introdução ao Armazenamento do Microsoft Azure](../storage/common/storage-introduction.md) para obter uma referência.</span><span class="sxs-lookup"><span data-stu-id="a2c19-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="a2c19-135">Você precisará verificar se as máquinas virtuais que deseja proteger atendem aos [requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="a2c19-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="a2c19-136">Atualmente, apenas operações no nível de VM são possíveis por meio do Powershell.</span><span class="sxs-lookup"><span data-stu-id="a2c19-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="a2c19-137">Em breve, será disponibilizado o suporte para operações no nível de plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="a2c19-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="a2c19-138">Por enquanto, você está limitado a executar failovers somente em granularidade de 'VM protegida', e não em um nível de Plano de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="a2c19-138">For now, you are limited to performing fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="a2c19-139">Pré-requisitos do VMM</span><span class="sxs-lookup"><span data-stu-id="a2c19-139">VMM prerequisites</span></span>
* <span data-ttu-id="a2c19-140">Você precisará do servidor VMM em execução no System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a2c19-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="a2c19-141">Qualquer servidor VMM que contenha máquinas virtuais que você deseje proteger deverá estar executando o Provedor do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a2c19-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span></span> <span data-ttu-id="a2c19-142">Ele é instalado durante a implantação do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a2c19-142">This is installed during the Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="a2c19-143">Você precisará de pelo menos uma nuvem no servidor VMM que deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="a2c19-143">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="a2c19-144">A nuvem deve conter:</span><span class="sxs-lookup"><span data-stu-id="a2c19-144">The cloud should contain:</span></span>
  * <span data-ttu-id="a2c19-145">Um ou mais grupos de hosts do VMM</span><span class="sxs-lookup"><span data-stu-id="a2c19-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="a2c19-146">Um ou mais servidores de host do Hyper-V ou clusters em cada grupo de host.</span><span class="sxs-lookup"><span data-stu-id="a2c19-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="a2c19-147">Uma ou mais máquinas virtuais no servidor Hyper-V de origem.</span><span class="sxs-lookup"><span data-stu-id="a2c19-147">One or more virtual machines on the source Hyper-V server.</span></span>
* <span data-ttu-id="a2c19-148">Saiba mais sobre como configurar nuvens VMM:</span><span class="sxs-lookup"><span data-stu-id="a2c19-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="a2c19-149">Leia mais sobre nuvens VMM privadas em [Novidades da nuvem privada com o System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e em [VMM 2012 e as nuvens](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="a2c19-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="a2c19-150">Saiba mais em [Configurando a malha de nuvem VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="a2c19-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="a2c19-151">Depois que os elementos de malha de nuvem estiverem em vigor, veja como criar nuvens privadas em [Criando uma nuvem privada no VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e [Passo a passo: criando de nuvens privadas com o System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="a2c19-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="a2c19-152">Pré-requisitos do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a2c19-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="a2c19-153">Os servidores host do Hyper-V devem estar executando pelo menos o **Windows Server 2012** com a função Hyper-V ou o **Microsoft Hyper-V Server 2012** e ter as atualizações mais recentes instaladas.</span><span class="sxs-lookup"><span data-stu-id="a2c19-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="a2c19-154">Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereços IP estáticos.</span><span class="sxs-lookup"><span data-stu-id="a2c19-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="a2c19-155">Você precisará configurar o agente de cluster manualmente.</span><span class="sxs-lookup"><span data-stu-id="a2c19-155">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="a2c19-156">Por</span><span class="sxs-lookup"><span data-stu-id="a2c19-156">For</span></span>
* <span data-ttu-id="a2c19-157">Para obter instruções, confira [Como Configurar o Agente de Réplica do Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2c19-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="a2c19-158">Qualquer cluster ou servidor host Hyper-V para o qual você desejar gerenciar a proteção deverá ser incluído em uma nuvem VMM.</span><span class="sxs-lookup"><span data-stu-id="a2c19-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="a2c19-159">Pré-requisitos de mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="a2c19-159">Network mapping prerequisites</span></span>
<span data-ttu-id="a2c19-160">Quando você proteger máquinas virtuais no Azure, o mapeamento de rede mapeará as redes de máquina virtual no servidor VMM de origem e nas redes do Azure de destino para habilitar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a2c19-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="a2c19-161">Todas as máquinas que passarem por failover na mesma rede poderão se conectar entre si, independentemente do plano de recuperação em que estão.</span><span class="sxs-lookup"><span data-stu-id="a2c19-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="a2c19-162">Além disso, se um gateway de rede for configurado na rede Azure de destino, as máquinas virtuais poderão se conectar a outras máquinas virtuais locais.</span><span class="sxs-lookup"><span data-stu-id="a2c19-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="a2c19-163">Se você não configurar o mapeamento de rede, somente as máquinas virtuais que fazem failover no mesmo plano de recuperação poderão se conectar entre si após failover no Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span></span>

<span data-ttu-id="a2c19-164">Se desejar implantar o mapeamento de rede, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="a2c19-164">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="a2c19-165">As máquinas virtuais que você deseja proteger no servidor VMM de origem devem estar conectadas a uma rede VM.</span><span class="sxs-lookup"><span data-stu-id="a2c19-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="a2c19-166">Essa rede deve ser vinculada a uma rede lógica que esteja associada à nuvem.</span><span class="sxs-lookup"><span data-stu-id="a2c19-166">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="a2c19-167">Uma rede do Azure à qual as máquinas virtuais replicadas possam se conectar após o failover.</span><span class="sxs-lookup"><span data-stu-id="a2c19-167">An Azure network to which replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="a2c19-168">Você selecionará essa rede no momento do failover.</span><span class="sxs-lookup"><span data-stu-id="a2c19-168">You'll select this network at the time of fail-over.</span></span> <span data-ttu-id="a2c19-169">A rede deve estar na mesma região de sua assinatura do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a2c19-169">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="a2c19-170">Saiba mais sobre mapeamento de rede em</span><span class="sxs-lookup"><span data-stu-id="a2c19-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="a2c19-171">Como configurar redes lógicas no VMM</span><span class="sxs-lookup"><span data-stu-id="a2c19-171">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="a2c19-172">Como configurar redes e gateways de VMs no VMM</span><span class="sxs-lookup"><span data-stu-id="a2c19-172">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="a2c19-173">Como configurar e monitorar redes virtuais no Azure</span><span class="sxs-lookup"><span data-stu-id="a2c19-173">How to configure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="a2c19-174">Pré-requisitos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2c19-174">PowerShell prerequisites</span></span>
<span data-ttu-id="a2c19-175">Verifique se você tem o PowerShell do Azure pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="a2c19-175">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="a2c19-176">Se você já estiver usando o PowerShell, precisará atualizar para a versão 0.8.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a2c19-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="a2c19-177">Para obter mais informações sobre como configurar o PowerShell, confira o [Guia de instalação e de configuração do Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a2c19-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="a2c19-178">Depois de instalar e configurar o PowerShell, você poderá exibir todos os cmdlets disponíveis para o serviço [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2c19-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="a2c19-179">Para obter dicas que podem ajudar você a usar os cmdlets, como valores de parâmetro, entradas e saídas, que normalmente são tratados no Azure PowerShell, confira [Introdução aos cmdlets do Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a2c19-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="a2c19-180">Etapa 1: definir a assinatura</span><span class="sxs-lookup"><span data-stu-id="a2c19-180">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="a2c19-181">No Azure PowerShell, faça logon na conta do Azure usando os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="a2c19-181">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="a2c19-182">Obtenha uma lista das suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="a2c19-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="a2c19-183">Essa lista também incluirá as IDs de assinatura de cada uma das assinaturas.</span><span class="sxs-lookup"><span data-stu-id="a2c19-183">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="a2c19-184">Anote a ID da assinatura na qual você quer criar o cofre dos serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="a2c19-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="a2c19-185">Defina a assinatura na qual o cofre dos serviços de recuperação deverá ser criado mencionando a ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="a2c19-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="a2c19-186">Etapa 2: Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="a2c19-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="a2c19-187">Crie um grupo de recursos no Azure Resource Manager se você ainda não tiver um</span><span class="sxs-lookup"><span data-stu-id="a2c19-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="a2c19-188">Crie um novo cofre de Serviços de Recuperação e salve o objeto de cofre ASR criado em uma variável (será usado posteriormente).</span><span class="sxs-lookup"><span data-stu-id="a2c19-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="a2c19-189">Você também pode recuperar o objeto de cofre ASR pós-criação usando o cmdlet Get-AzureRMRecoveryServicesVault:-</span><span class="sxs-lookup"><span data-stu-id="a2c19-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="a2c19-190">Etapa 3: Configurar o contexto do Cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="a2c19-190">Step 3: Set the Recovery Services Vault context</span></span>

<span data-ttu-id="a2c19-191">Defina o contexto de cofre, executando o comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="a2c19-191">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="a2c19-192">Etapa 4: instalar o Provedor do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a2c19-192">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="a2c19-193">Na máquina da VMM, crie um diretório executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-193">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="a2c19-194">Extraia os arquivos usando o provedor baixado, executando o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="a2c19-194">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="a2c19-195">Instale o provedor usando os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2c19-195">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="a2c19-196">Aguarde a conclusão da instalação.</span><span class="sxs-lookup"><span data-stu-id="a2c19-196">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="a2c19-197">Registre o servidor no cofre usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-197">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="a2c19-198">Etapa 5: criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a2c19-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="a2c19-199">Se você não tiver uma conta de armazenamento do Azure, crie uma conta habilitada para replicação geográfica na mesma região que o cofre executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="a2c19-200">Observe que a conta de armazenamento precisa estar na mesma região que o serviço Azure Site Recovery e associada à mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="a2c19-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="a2c19-201">Etapa 6: instalar o agente dos Serviços de Recuperação do Azure</span><span class="sxs-lookup"><span data-stu-id="a2c19-201">Step 6: Install the Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="a2c19-202">Baixe o agente dos Serviços de Recuperação do Azure em [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e instale-o em cada servidor host Hyper-V localizado nas nuvens VMM que quer proteger.</span><span class="sxs-lookup"><span data-stu-id="a2c19-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>
2. <span data-ttu-id="a2c19-203">Execute o comando a seguir em todos os hosts VMM:</span><span class="sxs-lookup"><span data-stu-id="a2c19-203">Run the following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="a2c19-204">Etapa 7: definir as configurações da proteção de nuvem</span><span class="sxs-lookup"><span data-stu-id="a2c19-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="a2c19-205">Crie uma política de replicação no Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-205">Create a replication policy to Azure by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="a2c19-206">Obtenha um contêiner de proteção executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a2c19-206">Get a protection container by running the following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="a2c19-207">Obtenha os detalhes da política para uma variável usando o trabalho que foi criado e mencionando o nome amigável da política:</span><span class="sxs-lookup"><span data-stu-id="a2c19-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="a2c19-208">Inicie a associação do contêiner de proteção à política de replicação:</span><span class="sxs-lookup"><span data-stu-id="a2c19-208">Start the association of the protection container with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="a2c19-209">Após a conclusão do trabalho, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-209">After the job has finished, run the following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="a2c19-210">Após a conclusão do processamento do trabalho, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-210">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="a2c19-211">Para verificar a conclusão da operação, execute as etapas em [Monitorar a Atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a2c19-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="a2c19-212">Etapa 8: configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="a2c19-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="a2c19-213">Antes de começar o mapeamento de rede, verifique se as máquinas virtuais no servidor VMM de origem estão conectadas a uma rede VM.</span><span class="sxs-lookup"><span data-stu-id="a2c19-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="a2c19-214">Além disso, crie uma ou mais redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="a2c19-215">Saiba mais sobre como criar uma rede virtual usando o Azure Resource Manager e o PowerShell, em [Criar uma rede virtual com uma conexão VPN site a site usando o Azure Resource Manager e o PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a2c19-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="a2c19-216">Observe que várias redes de máquina virtual podem ser mapeadas para uma única rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span></span> <span data-ttu-id="a2c19-217">Se a rede de destino tiver várias sub-redes e uma dessas sub-redes tiver o mesmo nome que a sub-rede em que a máquina virtual de origem está localizada, a máquina virtual de réplica será conectada à sub-rede de destino após o failover.</span><span class="sxs-lookup"><span data-stu-id="a2c19-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span></span> <span data-ttu-id="a2c19-218">Se não houver uma sub-rede de destino com um nome correspondente, a máquina virtual será conectada à primeira sub-rede na rede.</span><span class="sxs-lookup"><span data-stu-id="a2c19-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

1. <span data-ttu-id="a2c19-219">O primeiro comando obtém servidores para o cofre atual do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a2c19-219">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="a2c19-220">O comando armazena os servidores do Microsoft Azure Site Recovery na variável de matriz $Servers.</span><span class="sxs-lookup"><span data-stu-id="a2c19-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="a2c19-221">O segundo comando obtém a rede de recuperação de site para o primeiro servidor na matriz $Servers.</span><span class="sxs-lookup"><span data-stu-id="a2c19-221">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="a2c19-222">O comando armazena as redes na variável $Networks.</span><span class="sxs-lookup"><span data-stu-id="a2c19-222">The command stores the networks in the $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="a2c19-223">O terceiro comando obtém redes virtuais do Azure e, em seguida, esse valor na variável $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="a2c19-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="a2c19-224">O cmdlet final cria um mapeamento entre a rede principal e a rede de máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="a2c19-225">O cmdlet especifica a rede principal como o primeiro elemento de $Networks.</span><span class="sxs-lookup"><span data-stu-id="a2c19-225">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="a2c19-226">O cmdlet especifica uma rede de máquina virtual como o primeiro elemento de $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="a2c19-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="a2c19-227">Etapa 9: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="a2c19-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="a2c19-228">Depois que os servidores, nuvens e redes estiverem configurados corretamente, você poderá habilitar a proteção para máquinas virtuais na nuvem.</span><span class="sxs-lookup"><span data-stu-id="a2c19-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

 <span data-ttu-id="a2c19-229">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a2c19-229">Note the following:</span></span>

* <span data-ttu-id="a2c19-230">As máquinas virtuais devem cumprir os requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="a2c19-231">Verifique os [pré-requisitos e suporte](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) no guia de planejamento.</span><span class="sxs-lookup"><span data-stu-id="a2c19-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span></span>
* <span data-ttu-id="a2c19-232">Para habilitar a proteção, o sistema operacional e as propriedades do disco do sistema operacional devem estar definidos para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a2c19-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="a2c19-233">Ao criar uma máquina virtual no VMM usando um modelo de máquina virtual, é possível definir a propriedade.</span><span class="sxs-lookup"><span data-stu-id="a2c19-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="a2c19-234">Você também pode definir essas propriedades para máquinas virtuais existentes nas guias **Geral** e **Configuração de Hardware** das propriedades da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a2c19-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="a2c19-235">Se você não definir essas propriedades no VMM, poderá configurá-las no portal de Recuperação de Site do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2c19-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="a2c19-236">Para habilitar a proteção, execute o seguinte comando para obter o contêiner de proteção:</span><span class="sxs-lookup"><span data-stu-id="a2c19-236">To enable protection, run the following command to get the protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="a2c19-237">Obtenha a entidade de proteção (VM) executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-237">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="a2c19-238">Habilite o DR para a VM executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-238">Enable the DR for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="a2c19-239">Testar a implantação</span><span class="sxs-lookup"><span data-stu-id="a2c19-239">Test your deployment</span></span>
<span data-ttu-id="a2c19-240">Para testar sua implantação, você pode executar um failover de teste em uma única máquina virtual ou criar um plano de recuperação com várias máquinas virtuais e executar um failover de teste para o plano.</span><span class="sxs-lookup"><span data-stu-id="a2c19-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span></span> <span data-ttu-id="a2c19-241">O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.</span><span class="sxs-lookup"><span data-stu-id="a2c19-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="a2c19-242">Observe que:</span><span class="sxs-lookup"><span data-stu-id="a2c19-242">Note that:</span></span>

* <span data-ttu-id="a2c19-243">Se você quiser se conectar à máquina virtual no Azure usando a Área de Trabalho Remota após o failover, habilite a Conexão de Área de Trabalho Remota na máquina virtual antes de executar o failover de teste.</span><span class="sxs-lookup"><span data-stu-id="a2c19-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="a2c19-244">Após o failover, você usará um endereço IP público para se conectar à máquina virtual no Azure usando a Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="a2c19-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="a2c19-245">Se você quiser fazer isso, verifique se não tem nenhuma política de domínio que o impeça de se conectar a uma máquina virtual usando um endereço público.</span><span class="sxs-lookup"><span data-stu-id="a2c19-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="a2c19-246">Para verificar a conclusão da operação, execute as etapas em [Monitorar a Atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="a2c19-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="a2c19-247">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="a2c19-247">Run a test failover</span></span>
- <span data-ttu-id="a2c19-248">Inicie o teste de failover executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-248">Start the test failover by running the following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="a2c19-249">Executar um failover planejado</span><span class="sxs-lookup"><span data-stu-id="a2c19-249">Run a planned failover</span></span>
- <span data-ttu-id="a2c19-250">Inicie o failover planejado executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-250">Start the planned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="a2c19-251">Executar um failover não planejado</span><span class="sxs-lookup"><span data-stu-id="a2c19-251">Run an unplanned failover</span></span>
- <span data-ttu-id="a2c19-252">Inicie o failover não planejado executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a2c19-252">Start the unplanned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="a2c19-253"><a name=monitor></a> Monitorar a atividade</span><span class="sxs-lookup"><span data-stu-id="a2c19-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="a2c19-254">Use os seguintes comandos para monitorar a atividade.</span><span class="sxs-lookup"><span data-stu-id="a2c19-254">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="a2c19-255">Observe que é necessário aguardar a conclusão do processamento entre os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a2c19-255">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="a2c19-256">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2c19-256">Next steps</span></span>
<span data-ttu-id="a2c19-257">[Leia mais](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a2c19-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
