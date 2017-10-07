---
title: "aaaReplicate uma implantação de várias camada Citrix XenDesktop e XenApp usando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como implantações tooprotect e recupere o Citrix XenDesktop e XenApp usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="e2f15-103">Replicar uma implantação do Citrix XenApp e XenDesktop de várias camadas usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e2f15-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="e2f15-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e2f15-104">Overview</span></span>

<span data-ttu-id="e2f15-105">Citrix XenDesktop é uma solução de virtualização de área de trabalho que a entrega de aplicativos e áreas de trabalho como um ondemand tooany usuário do serviço, em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="e2f15-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="e2f15-106">Com tecnologia de entrega FlexCast XenDesktop pode rapidamente e com segurança fornecer aplicativos e áreas de trabalho toousers.</span><span class="sxs-lookup"><span data-stu-id="e2f15-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="e2f15-107">Hoje, o Citrix XenApp não fornece qualquer capacidade de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="e2f15-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="e2f15-108">Uma solução de recuperação de desastres BOM, deve permitir modelagem de planos de recuperação em torno de saudação acima arquiteturas de aplicativos complexos e também ter Olá capacidade tooadd personalizado etapas toohandle aplicativo mapeamentos entre várias camadas, portanto, fornecendo um Clique se captura solução no evento de saudação de um desastre esquerda tooa reduzir o RTO.</span><span class="sxs-lookup"><span data-stu-id="e2f15-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="e2f15-109">Este documento fornece uma orientação passo a passo para a criação de uma solução de recuperação de desastre para suas implantações locais do Citrix XenApp em plataformas do Hyper-V e VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="e2f15-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="e2f15-110">Este documento descreve também como tooperform um failover de teste (análise de recuperação de desastres) e o failover não planejado tooAzure usando planos de recuperação, configurações de saudação com suporte e os pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="e2f15-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e2f15-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e2f15-111">Prerequisites</span></span>

<span data-ttu-id="e2f15-112">Antes de começar, certifique-se de que compreender o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e2f15-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="e2f15-113">Replicando tooAzure uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e2f15-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="e2f15-114">Como muito[criar uma rede de recuperação](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="e2f15-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="e2f15-115">Fazer um tooAzure de failover de teste</span><span class="sxs-lookup"><span data-stu-id="e2f15-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="e2f15-116">Fazer um failover tooAzure</span><span class="sxs-lookup"><span data-stu-id="e2f15-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="e2f15-117">Como muito[replicar um controlador de domínio](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="e2f15-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="e2f15-118">Como muito[replicar do SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="e2f15-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="e2f15-119">Padrões de implantação</span><span class="sxs-lookup"><span data-stu-id="e2f15-119">Deployment patterns</span></span>

<span data-ttu-id="e2f15-120">Um farm do Citrix XenApp e XenDesktop normalmente tem saudação padrão de implantação a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2f15-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="e2f15-121">**Padrão de implantação**</span><span class="sxs-lookup"><span data-stu-id="e2f15-121">**Deployment pattern**</span></span>

<span data-ttu-id="e2f15-122">A implantação do Citrix XenApp e XenDesktop com servidor DNS AD, servidor de banco de dados SQL, Controlador de entrega Citrix, servidor StoreFront, XenApp Master (VDA), servidor de licenças do Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="e2f15-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Padrão de Implantação 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="e2f15-124">Suporte do Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e2f15-124">Site Recovery support</span></span>

<span data-ttu-id="e2f15-125">Para fins de saudação deste artigo, Citrix implantações em máquinas virtuais VMware gerenciadas por vSphere 6.0 / System Center VMM 2012 R2 foram usado toosetup DR.</span><span class="sxs-lookup"><span data-stu-id="e2f15-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="e2f15-126">Origem e destino</span><span class="sxs-lookup"><span data-stu-id="e2f15-126">Source and target</span></span>

<span data-ttu-id="e2f15-127">**Cenário**</span><span class="sxs-lookup"><span data-stu-id="e2f15-127">**Scenario**</span></span> | <span data-ttu-id="e2f15-128">**site secundário tooa**</span><span class="sxs-lookup"><span data-stu-id="e2f15-128">**tooa secondary site**</span></span> | <span data-ttu-id="e2f15-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="e2f15-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="e2f15-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="e2f15-130">**Hyper-V**</span></span> | <span data-ttu-id="e2f15-131">Não está no escopo</span><span class="sxs-lookup"><span data-stu-id="e2f15-131">Not in scope</span></span> | <span data-ttu-id="e2f15-132">Sim</span><span class="sxs-lookup"><span data-stu-id="e2f15-132">Yes</span></span>
<span data-ttu-id="e2f15-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="e2f15-133">**VMware**</span></span> | <span data-ttu-id="e2f15-134">Não está no escopo</span><span class="sxs-lookup"><span data-stu-id="e2f15-134">Not in scope</span></span> | <span data-ttu-id="e2f15-135">Sim</span><span class="sxs-lookup"><span data-stu-id="e2f15-135">Yes</span></span>
<span data-ttu-id="e2f15-136">**Servidor físico**</span><span class="sxs-lookup"><span data-stu-id="e2f15-136">**Physical server**</span></span> | <span data-ttu-id="e2f15-137">Não está no escopo</span><span class="sxs-lookup"><span data-stu-id="e2f15-137">Not in scope</span></span> | <span data-ttu-id="e2f15-138">Sim</span><span class="sxs-lookup"><span data-stu-id="e2f15-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="e2f15-139">Versões</span><span class="sxs-lookup"><span data-stu-id="e2f15-139">Versions</span></span>
<span data-ttu-id="e2f15-140">Os clientes podem implantar componentes do XenApp como máquinas virtuais em execução no Hyper-V ou VMware, ou como servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="e2f15-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="e2f15-141">Recuperação de Site do Azure pode proteger tooAzure ambas as implantações físicas e virtuais.</span><span class="sxs-lookup"><span data-stu-id="e2f15-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="e2f15-142">Como XenApp 7,7 ou posterior tem suporte no Azure, somente implantações com essas versões podem sofrer failover tooAzure para recuperação de desastres ou migração.</span><span class="sxs-lookup"><span data-stu-id="e2f15-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="e2f15-143">Tookeep coisas em mente</span><span class="sxs-lookup"><span data-stu-id="e2f15-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="e2f15-144">Proteção e recuperação de local há suporte para implantações usando o sistema operacional Server máquinas toodeliver XenApp aplicativos publicados e XenApp publicado áreas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e2f15-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="e2f15-145">Não há suporte para a proteção e recuperação de implantações de local usando toodeliver de máquinas de SO da área de trabalho VDI de área de trabalho cliente áreas de trabalho virtuais, incluindo Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e2f15-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="e2f15-146">Isso ocorre porque a ASR não oferece suporte à recuperação de saudação de computadores com área de trabalho OS'es.</span><span class="sxs-lookup"><span data-stu-id="e2f15-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="e2f15-147">Além disso, alguns tipos de área de trabalho virtual do cliente (por exemplo,</span><span class="sxs-lookup"><span data-stu-id="e2f15-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="e2f15-148">Windows 7) ainda não têm suporte para licenciamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="e2f15-149">[Saiba mais](https://azure.microsoft.com/pricing/licensing-faq/) sobre licenciamento para áreas de trabalho de cliente/servidor no Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="e2f15-150">O Azure Site Recovery não pode replicar e proteger clones MCS ou PVS locais existentes.</span><span class="sxs-lookup"><span data-stu-id="e2f15-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="e2f15-151">É necessário toorecreate esses clones usando o Azure RM provisionamento do controlador de entrega.</span><span class="sxs-lookup"><span data-stu-id="e2f15-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="e2f15-152">O NetScaler não pode ser protegido usando o Azure Site Recovery conforme o NetScaler baseia-se em FreeBSD e o Azure Site Recovery não oferece suporte a proteção do sistema operacional do FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="e2f15-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="e2f15-153">Você precisa toodeploy e configurar um novo dispositivo NetScaler de mercado Azure após o failover tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="e2f15-154">Replicação de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e2f15-154">Replicating virtual machines</span></span>

<span data-ttu-id="e2f15-155">Olá seguintes componentes do hello Citrix XenApp implantação necessário toobe protegido tooenable replicação e a recuperação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="e2f15-156">Proteção do servidor DNS AD</span><span class="sxs-lookup"><span data-stu-id="e2f15-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="e2f15-157">Proteção do servidor de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="e2f15-157">Protection of SQL database server</span></span>
* <span data-ttu-id="e2f15-158">Proteção do Controlador de entrega do Citrix</span><span class="sxs-lookup"><span data-stu-id="e2f15-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="e2f15-159">Proteção do servidor StoreFront.</span><span class="sxs-lookup"><span data-stu-id="e2f15-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="e2f15-160">Proteção do XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="e2f15-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="e2f15-161">Proteção do servidor de licença do Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="e2f15-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="e2f15-162">**Replicação do servidor DNS AD**</span><span class="sxs-lookup"><span data-stu-id="e2f15-162">**AD DNS server replication**</span></span>

<span data-ttu-id="e2f15-163">Consulte também[proteger o Active Directory e DNS com o Azure Site Recovery](site-recovery-active-directory.md) na orientação para a replicação e configurar um controlador de domínio no Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="e2f15-164">**Replicação do servidor de banco de dados SQL**</span><span class="sxs-lookup"><span data-stu-id="e2f15-164">**SQL database Server replication**</span></span>

<span data-ttu-id="e2f15-165">Consulte também[proteger o SQL Server com a recuperação de desastres do SQL Server e o Azure Site Recovery](site-recovery-sql.md) para orientações técnicas detalhadas sobre Olá recomendado opções para proteger os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="e2f15-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="e2f15-166">Execute [neste guia](site-recovery-vmware-to-azure.md) toostart replicando Olá outros tooAzure de máquinas virtuais do componente.</span><span class="sxs-lookup"><span data-stu-id="e2f15-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![Proteção dos componentes do XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="e2f15-168">**Configurações de rede e de computação**</span><span class="sxs-lookup"><span data-stu-id="e2f15-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="e2f15-169">Depois de máquinas Olá protegidas (status mostra como "Protected" em itens replicados), Olá computação e as configurações de rede necessário toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="e2f15-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="e2f15-170">Em computação e rede > computação propriedades, você pode especificar o tamanho de destino e o nome de VM do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e2f15-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="e2f15-171">Se for necessário, modifique Olá nome toocomply com os requisitos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="e2f15-172">Você também pode exibir e adicionar informações sobre a rede de destino hello, sub-rede e endereço IP que será atribuído toohello VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="e2f15-173">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e2f15-173">Note hello following:</span></span>

* <span data-ttu-id="e2f15-174">Você pode definir o endereço IP de destino hello.</span><span class="sxs-lookup"><span data-stu-id="e2f15-174">You can set hello target IP address.</span></span> <span data-ttu-id="e2f15-175">Se você não fornecer um endereço, Olá failover máquina usará o DHCP.</span><span class="sxs-lookup"><span data-stu-id="e2f15-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="e2f15-176">Se você definir um endereço que não está disponível em failover, o failover de saudação não funcionará.</span><span class="sxs-lookup"><span data-stu-id="e2f15-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="e2f15-177">saudação do mesmo endereço IP de destino pode ser usado para failover de teste se o endereço de saudação está disponível na rede de failover de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="e2f15-178">Para o servidor de AD/DNS hello, reter Olá local permite endereço que especificar Olá mesmo endereço como servidor DNS Olá para rede Virtual do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e2f15-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="e2f15-179">número de saudação de adaptadores de rede é determinado pelo tamanho de saudação especificado para a máquina de virtual de destino Olá, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e2f15-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="e2f15-180">Se Olá vários adaptadores de rede no computador de origem de saudação é menor ou igual toohello número de adaptadores permitido para o tamanho de máquina de destino Olá, então terá destino Olá Olá o mesmo número de adaptadores de fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="e2f15-181">Se número Olá dos adaptadores de saudação da máquina virtual de origem exceder o número de saudação permitido para o tamanho de destino hello e tamanho máximo da saudação destino será usado.</span><span class="sxs-lookup"><span data-stu-id="e2f15-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="e2f15-182">Por exemplo, se um computador de origem tem dois adaptadores de rede e o tamanho de máquina de destino Olá oferece suporte a quatro, computador de destino Olá terá dois adaptadores.</span><span class="sxs-lookup"><span data-stu-id="e2f15-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="e2f15-183">Se o computador de origem Olá tem dois adaptadores, mas hello tamanho de destino com suporte apenas oferece suporte a um computador de destino Olá terá apenas um adaptador.</span><span class="sxs-lookup"><span data-stu-id="e2f15-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="e2f15-184">Se a máquina virtual de saudação tem vários adaptadores de rede conectará todos toohello mesma rede.</span><span class="sxs-lookup"><span data-stu-id="e2f15-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="e2f15-185">Se a máquina virtual de saudação tem vários adaptadores de rede, hello primeiro aquele mostrado na lista de saudação torna-se adaptador de rede saudação padrão em Olá máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="e2f15-186">Criar um plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="e2f15-186">Creating a recovery plan</span></span>

<span data-ttu-id="e2f15-187">Após a replicação está habilitada para Olá XenApp componente VMs, Olá próxima etapa é toocreate um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="e2f15-188">Uma plano de recuperação agrupa as máquinas virtuais com requisitos semelhantes para failover e recuperação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="e2f15-189">**Etapas toocreate um plano de recuperação**</span><span class="sxs-lookup"><span data-stu-id="e2f15-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="e2f15-190">Adicione máquinas virtuais do hello XenApp componente no plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="e2f15-191">Clique em Planos de Recuperação -> + Plano de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="e2f15-192">Forneça um nome intuitivo para o plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="e2f15-193">Para máquinas virtuais do VMware: selecione a origem como o servidor de processo do VMware, o destino como o Microsoft Azure e o modelo de implantação como o Gerenciador de Recursos, e clique em Selecionar itens.</span><span class="sxs-lookup"><span data-stu-id="e2f15-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="e2f15-194">Para máquinas virtuais Hyper-V: Selecionar origem como o servidor do VMM, como o Microsoft Azure e o modelo de implantação como o Gerenciador de recursos de destino e clique em selecionar itens e selecione máquinas virtuais de implantação XenApp hello.</span><span class="sxs-lookup"><span data-stu-id="e2f15-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="e2f15-195">A adição de grupos de toofailover de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e2f15-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="e2f15-196">Planos de recuperação podem ser personalizado tooadd failover grupos para ações de manual, a ordem ou scripts de inicialização específica.</span><span class="sxs-lookup"><span data-stu-id="e2f15-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="e2f15-197">Olá grupos a seguir precisa de plano de recuperação toobe toohello adicionado.</span><span class="sxs-lookup"><span data-stu-id="e2f15-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="e2f15-198">Grupo de failover 1: DNS AD</span><span class="sxs-lookup"><span data-stu-id="e2f15-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="e2f15-199">Grupo de failover 2: VMs do SQL Server</span><span class="sxs-lookup"><span data-stu-id="e2f15-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="e2f15-200">Grupo de failover 3: VM de imagem do VDA Master</span><span class="sxs-lookup"><span data-stu-id="e2f15-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="e2f15-201">Grupo de failover 4: controlador de entrega e VMs do servidor StoreFront</span><span class="sxs-lookup"><span data-stu-id="e2f15-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="e2f15-202">Adicionar plano de recuperação de toohello de scripts</span><span class="sxs-lookup"><span data-stu-id="e2f15-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="e2f15-203">Os scripts podem ser executados antes ou depois de um grupo específico em um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e2f15-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="e2f15-204">Ações manuais podem ser também incluídas e executadas durante o failover.</span><span class="sxs-lookup"><span data-stu-id="e2f15-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="e2f15-205">plano de recuperação personalizada Olá aparência Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="e2f15-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="e2f15-206">Grupo de failover 1: DNS AD</span><span class="sxs-lookup"><span data-stu-id="e2f15-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="e2f15-207">Grupo de failover 2: VMs do SQL Server</span><span class="sxs-lookup"><span data-stu-id="e2f15-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="e2f15-208">Grupo de failover 3: VM de imagem do VDA Master</span><span class="sxs-lookup"><span data-stu-id="e2f15-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="e2f15-209">As etapas 4, 6 e 7, que contém ações manuais ou de script são aplicável tooonly um XenApp local > ambiente com catálogos MCS/PVS.</span><span class="sxs-lookup"><span data-stu-id="e2f15-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="e2f15-210">Ação Manual ou script do grupo 3: Olá de VM VDA mestre desligamento mestre VDA VM quando o failover tooAzure estará em um estado de execução.</span><span class="sxs-lookup"><span data-stu-id="e2f15-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="e2f15-211">toocreate novos catálogos MCS usando o Azure ARM de hospedagem, mestre de Olá VDA VM é necessário toobe em parado (de alocada) estado.</span><span class="sxs-lookup"><span data-stu-id="e2f15-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="e2f15-212">Saudação de desligamento VM a partir do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="e2f15-213">Grupo de failover 4: controlador de entrega e VMs do servidor StoreFront</span><span class="sxs-lookup"><span data-stu-id="e2f15-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="e2f15-214">Ação manual ou de script do grupo 3 1:</span><span class="sxs-lookup"><span data-stu-id="e2f15-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="e2f15-215">***Adicionar conexão do host do Azure RM***</span><span class="sxs-lookup"><span data-stu-id="e2f15-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="e2f15-216">Crie conexão de host do Azure ARM no controlador de entrega máquina tooprovision novos catálogos MCS no Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="e2f15-217">Execute as etapas de saudação conforme explicado neste [artigo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="e2f15-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="e2f15-218">Ação manual ou de script do grupo 3 2:</span><span class="sxs-lookup"><span data-stu-id="e2f15-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="e2f15-219">***Recriar os catálogos MCS no Azure***</span><span class="sxs-lookup"><span data-stu-id="e2f15-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="e2f15-220">Olá existente MCS ou PVS clones no site primário Olá não será replicada tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="e2f15-221">É necessário toorecreate esses clones usando Olá replicado VDA mestre e ARM Azure provisionamento do controlador de entrega. Execute as etapas de saudação conforme explicado neste [artigo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catálogos no Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f15-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![Plano de recuperação para componentes do XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="e2f15-223">Você pode usar scripts em [local](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate Olá DNS com hello novos IPs de saudação failover > máquinas virtuais ou tooattach um balanceador de carga Olá falha pela máquina virtual, se necessário.</span><span class="sxs-lookup"><span data-stu-id="e2f15-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="e2f15-224">Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="e2f15-224">Doing a test failover</span></span>

<span data-ttu-id="e2f15-225">Execute [neste guia](site-recovery-test-failover-to-azure.md) toodo um failover de teste.</span><span class="sxs-lookup"><span data-stu-id="e2f15-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![Plano de Recuperação](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="e2f15-227">Executar um failover</span><span class="sxs-lookup"><span data-stu-id="e2f15-227">Doing a failover</span></span>

<span data-ttu-id="e2f15-228">Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.</span><span class="sxs-lookup"><span data-stu-id="e2f15-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2f15-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2f15-229">Next steps</span></span>

<span data-ttu-id="e2f15-230">Você pode [saber mais](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sobre replicação de implantações do Citrix XenApp e XenDesktop neste white paper.</span><span class="sxs-lookup"><span data-stu-id="e2f15-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="e2f15-231">Examinar a orientação de saudação muito[replicar outros aplicativos](site-recovery-workload.md) com a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="e2f15-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
