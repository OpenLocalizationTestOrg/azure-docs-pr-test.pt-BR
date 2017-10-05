---
title: "Replicar uma implantação do Citrix XenDesktop e XenApp de várias camadas usando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como proteger e recuperar implantações do Citrix XenDesktop e XenApp usando o Azure Site Recovery."
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
ms.openlocfilehash: dc064352b1841ff346b705dc63186b12d79350b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="f7753-103">Replicar uma implantação do Citrix XenApp e XenDesktop de várias camadas usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f7753-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="f7753-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f7753-104">Overview</span></span>

<span data-ttu-id="f7753-105">O Citrix XenDesktop é uma solução de virtualização de área de trabalho que entrega aplicativos e áreas de trabalho como um serviço sob demanda a qualquer usuário, em qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="f7753-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service to any user, anywhere.</span></span> <span data-ttu-id="f7753-106">Com tecnologia de entrega FlexCast, o XenDesktop pode fornecer aplicativos e áreas de trabalho aos usuários de forma rápida e com segurança.</span><span class="sxs-lookup"><span data-stu-id="f7753-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops to users.</span></span>
<span data-ttu-id="f7753-107">Hoje, o Citrix XenApp não fornece qualquer capacidade de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="f7753-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="f7753-108">Uma boa solução de recuperação de desastres deve permitir a modelagem de planos de recuperação em torno das arquiteturas de aplicativo complexas indicadas acima, e também tem a capacidade de adicionar etapas personalizadas para lidar com mapeamentos de aplicativo entre as várias camadas, fornecendo uma solução certeira acionada com um único clique no caso de um desastre resultar em um RTO inferior.</span><span class="sxs-lookup"><span data-stu-id="f7753-108">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>

<span data-ttu-id="f7753-109">Este documento fornece uma orientação passo a passo para a criação de uma solução de recuperação de desastre para suas implantações locais do Citrix XenApp em plataformas do Hyper-V e VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="f7753-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="f7753-110">Este documento também descreve como executar um failover de teste (análise de recuperação de desastre) e o failover não planejado para o Azure usando planos de recuperação, as configurações com suporte e os pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="f7753-110">This document also describes how to perform a test failover(disaster recovery drill) and unplanned failover to Azure using recovery plans, the supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f7753-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f7753-111">Prerequisites</span></span>

<span data-ttu-id="f7753-112">Antes de começar, você precisa entender o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7753-112">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="f7753-113">Replicar uma máquina virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="f7753-113">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="f7753-114">Como [criar uma rede de recuperação](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="f7753-114">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="f7753-115">Executar um failover de teste no Azure</span><span class="sxs-lookup"><span data-stu-id="f7753-115">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="f7753-116">Executar um failover no Azure</span><span class="sxs-lookup"><span data-stu-id="f7753-116">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="f7753-117">Como [replicar um controlador de domínio](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="f7753-117">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="f7753-118">Como [replicar o SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="f7753-118">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="f7753-119">Padrões de implantação</span><span class="sxs-lookup"><span data-stu-id="f7753-119">Deployment patterns</span></span>

<span data-ttu-id="f7753-120">Um farm do Citrix XenApp e XenDesktop normalmente tem o seguinte padrão de implantação:</span><span class="sxs-lookup"><span data-stu-id="f7753-120">A Citrix XenApp and XenDesktop farm typically has the following deployment pattern:</span></span>

<span data-ttu-id="f7753-121">**Padrão de implantação**</span><span class="sxs-lookup"><span data-stu-id="f7753-121">**Deployment pattern**</span></span>

<span data-ttu-id="f7753-122">A implantação do Citrix XenApp e XenDesktop com servidor DNS AD, servidor de banco de dados SQL, Controlador de entrega Citrix, servidor StoreFront, XenApp Master (VDA), servidor de licenças do Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="f7753-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Padrão de Implantação 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="f7753-124">Suporte do Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f7753-124">Site Recovery support</span></span>

<span data-ttu-id="f7753-125">Com a finalidade deste artigo, as implantações do Citrix em máquinas virtuais VMware gerenciadas pelo vSphere 6.0/System Center VMM 2012 R2 foram usadas para configurar a recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="f7753-125">For the purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used to setup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="f7753-126">Origem e destino</span><span class="sxs-lookup"><span data-stu-id="f7753-126">Source and target</span></span>

<span data-ttu-id="f7753-127">**Cenário**</span><span class="sxs-lookup"><span data-stu-id="f7753-127">**Scenario**</span></span> | <span data-ttu-id="f7753-128">**Para um site secundário**</span><span class="sxs-lookup"><span data-stu-id="f7753-128">**To a secondary site**</span></span> | <span data-ttu-id="f7753-129">**Para o Azure**</span><span class="sxs-lookup"><span data-stu-id="f7753-129">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="f7753-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="f7753-130">**Hyper-V**</span></span> | <span data-ttu-id="f7753-131">Não está no escopo</span><span class="sxs-lookup"><span data-stu-id="f7753-131">Not in scope</span></span> | <span data-ttu-id="f7753-132">Sim</span><span class="sxs-lookup"><span data-stu-id="f7753-132">Yes</span></span>
<span data-ttu-id="f7753-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="f7753-133">**VMware**</span></span> | <span data-ttu-id="f7753-134">Não está no escopo</span><span class="sxs-lookup"><span data-stu-id="f7753-134">Not in scope</span></span> | <span data-ttu-id="f7753-135">Sim</span><span class="sxs-lookup"><span data-stu-id="f7753-135">Yes</span></span>
<span data-ttu-id="f7753-136">**Servidor físico**</span><span class="sxs-lookup"><span data-stu-id="f7753-136">**Physical server**</span></span> | <span data-ttu-id="f7753-137">Não está no escopo</span><span class="sxs-lookup"><span data-stu-id="f7753-137">Not in scope</span></span> | <span data-ttu-id="f7753-138">Sim</span><span class="sxs-lookup"><span data-stu-id="f7753-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="f7753-139">Versões</span><span class="sxs-lookup"><span data-stu-id="f7753-139">Versions</span></span>
<span data-ttu-id="f7753-140">Os clientes podem implantar componentes do XenApp como máquinas virtuais em execução no Hyper-V ou VMware, ou como servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="f7753-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="f7753-141">O Azure Site Recovery pode proteger as implantações físicas e virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-141">Azure Site Recovery can protect both physical and virtual deployments to Azure.</span></span>
<span data-ttu-id="f7753-142">Como o XenApp 7,7 ou posterior tem suporte no Azure, somente implantações com essas versões podem fazer failover no Azure para recuperação de desastre ou migração.</span><span class="sxs-lookup"><span data-stu-id="f7753-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over to Azure for Disaster Recovery or migration.</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="f7753-143">Algumas coisas que se deve manter em mente</span><span class="sxs-lookup"><span data-stu-id="f7753-143">Things to keep in mind</span></span>

1. <span data-ttu-id="f7753-144">A proteção e a recuperação de implantações locais usando os computadores com o sistema operacional de servidor para entregar aplicativos publicados do XenApp e áreas de trabalho publicadas do XenApp.</span><span class="sxs-lookup"><span data-stu-id="f7753-144">Protection and recovery of on-premises deployments using Server OS machines to deliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="f7753-145">A proteção e a recuperação de implantações locais usando os computadores com o sistema operacional de área de trabalho para entregar VDI da área de trabalho para as áreas de trabalho virtuais do cliente, incluindo o Windows 10, não é suportada.</span><span class="sxs-lookup"><span data-stu-id="f7753-145">Protection and recovery of on-premises deployments using desktop OS machines to deliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="f7753-146">Isso ocorre porque o ASR não dá suporte a recuperação de computadores com o sistema operacional de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f7753-146">This is because ASR does not support the recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="f7753-147">Além disso, alguns tipos de área de trabalho virtual do cliente (por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f7753-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="f7753-148">Windows 7) ainda não têm suporte para licenciamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="f7753-149">[Saiba mais](https://azure.microsoft.com/pricing/licensing-faq/) sobre licenciamento para áreas de trabalho de cliente/servidor no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="f7753-150">O Azure Site Recovery não pode replicar e proteger clones MCS ou PVS locais existentes.</span><span class="sxs-lookup"><span data-stu-id="f7753-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="f7753-151">Você precisa recriar esses clones usando o provisionamento do Azure RM do Controlador de entrega.</span><span class="sxs-lookup"><span data-stu-id="f7753-151">You need to recreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="f7753-152">O NetScaler não pode ser protegido usando o Azure Site Recovery conforme o NetScaler baseia-se em FreeBSD e o Azure Site Recovery não oferece suporte a proteção do sistema operacional do FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="f7753-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="f7753-153">Você precisa implantar e configurar um novo dispositivo NetScaler do Azure Marketplace após o failover no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-153">You would need to deploy and configure a new NetScaler appliance from Azure Market place after failover to Azure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="f7753-154">Replicação de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="f7753-154">Replicating virtual machines</span></span>

<span data-ttu-id="f7753-155">Os seguintes componentes da implantação do Citrix XenApp precisam ser protegidos para habilitar a replicação e a recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-155">The following components of the Citrix XenApp deployment need to be protected to enable replication and recovery.</span></span>

* <span data-ttu-id="f7753-156">Proteção do servidor DNS AD</span><span class="sxs-lookup"><span data-stu-id="f7753-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="f7753-157">Proteção do servidor de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="f7753-157">Protection of SQL database server</span></span>
* <span data-ttu-id="f7753-158">Proteção do Controlador de entrega do Citrix</span><span class="sxs-lookup"><span data-stu-id="f7753-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="f7753-159">Proteção do servidor StoreFront.</span><span class="sxs-lookup"><span data-stu-id="f7753-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="f7753-160">Proteção do XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="f7753-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="f7753-161">Proteção do servidor de licença do Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="f7753-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="f7753-162">**Replicação do servidor DNS AD**</span><span class="sxs-lookup"><span data-stu-id="f7753-162">**AD DNS server replication**</span></span>

<span data-ttu-id="f7753-163">Consulte [Proteger o Active Directory e DNS com o Azure Site Recovery](site-recovery-active-directory.md) na orientação para a replicação e configurar de um controlador de domínio no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-163">Please refer to [Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="f7753-164">**Replicação do servidor de banco de dados SQL**</span><span class="sxs-lookup"><span data-stu-id="f7753-164">**SQL database Server replication**</span></span>

<span data-ttu-id="f7753-165">Consulte [Proteger o SQL Server com a recuperação de desastre do SQL Server e o Azure Site Recovery](site-recovery-sql.md) na orientação técnica detalhada das opções recomendadas para proteger os servidores SQL.</span><span class="sxs-lookup"><span data-stu-id="f7753-165">Please refer to [Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on the recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="f7753-166">Siga [esta orientação](site-recovery-vmware-to-azure.md) para começar a replicar as outras máquinas virtuais de componente para o Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-166">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the other component virtual machines to Azure.</span></span>

![Proteção dos componentes do XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="f7753-168">**Configurações de rede e de computação**</span><span class="sxs-lookup"><span data-stu-id="f7753-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="f7753-169">Depois que os computadores estiverem protegidos (o status mostra como "Protegido" em Itens replicados), as configurações de rede e de computação precisam ser definidas.</span><span class="sxs-lookup"><span data-stu-id="f7753-169">After the machines are protected (status shows as “Protected” under Replicated Items), the Compute and Network settings need to be configured.</span></span>
<span data-ttu-id="f7753-170">Em Computação e Rede > Propriedades de Computação, você pode especificar o nome da VM do Azure e o tamanho do destino.</span><span class="sxs-lookup"><span data-stu-id="f7753-170">In Compute and Network > Compute properties, you can specify the Azure VM name and target size.</span></span>
<span data-ttu-id="f7753-171">Modifique o nome para que ele fique em conformidade com os requisitos do Azure, se for necessário.</span><span class="sxs-lookup"><span data-stu-id="f7753-171">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="f7753-172">Você também pode exibir e adicionar as informações sobre a rede de destino, a sub-rede e o endereço IP que será atribuído à VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-172">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span>

<span data-ttu-id="f7753-173">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7753-173">Note the following:</span></span>

* <span data-ttu-id="f7753-174">Você pode definir o endereço IP de destino.</span><span class="sxs-lookup"><span data-stu-id="f7753-174">You can set the target IP address.</span></span> <span data-ttu-id="f7753-175">Se você não fornecer um endereço, o computador com failover usará o DHCP.</span><span class="sxs-lookup"><span data-stu-id="f7753-175">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="f7753-176">Se você definir um endereço que não esteja disponível no failover, o failover não funcionará.</span><span class="sxs-lookup"><span data-stu-id="f7753-176">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="f7753-177">O mesmo endereço IP de destino poderá ser usado para failover de teste caso o endereço esteja disponível na rede de failover de teste.</span><span class="sxs-lookup"><span data-stu-id="f7753-177">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

* <span data-ttu-id="f7753-178">Para o servidor DNS/AD, manter o endereço local permite que você especifique o mesmo endereço como o servidor DNS para a rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-178">For the AD/DNS server, retaining the on-premises address lets you specify the same address as the DNS server for the Azure Virtual network.</span></span>

<span data-ttu-id="f7753-179">O número de adaptadores de rede é determinado pelo tamanho especificado para a máquina virtual de destino, como a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7753-179">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

*   <span data-ttu-id="f7753-180">Se o número de adaptadores de rede na máquina de origem for menor ou igual ao número de adaptadores permitido para o tamanho da máquina de destino, o destino terá o mesmo número de adaptadores que a origem.</span><span class="sxs-lookup"><span data-stu-id="f7753-180">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
*   <span data-ttu-id="f7753-181">Se o número de adaptadores para máquina virtual de origem exceder o número permitido para o tamanho de destino e o tamanho máximo de destino será usado.</span><span class="sxs-lookup"><span data-stu-id="f7753-181">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
* <span data-ttu-id="f7753-182">Por exemplo, se uma máquina de origem tiver dois adaptadores de rede e o tamanho da máquina de destino der suporte a quatro, a máquina de destino terá dois adaptadores.</span><span class="sxs-lookup"><span data-stu-id="f7753-182">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="f7753-183">Se a máquina de origem tiver dois adaptadores, mas o tamanho de destino com suporte oferecer suporte apenas a uma máquina de destino, ela terá apenas um adaptador.</span><span class="sxs-lookup"><span data-stu-id="f7753-183">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>
*   <span data-ttu-id="f7753-184">Se a máquina virtual tiver vários adaptadores de rede, todos eles se conectarão à mesma rede.</span><span class="sxs-lookup"><span data-stu-id="f7753-184">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
*   <span data-ttu-id="f7753-185">Se a máquina virtual tiver vários adaptadores de rede, o primeiro deles mostrado na lista se tornará o adaptador de rede Padrão na máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-185">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the Default network adapter in the Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="f7753-186">Criar um plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="f7753-186">Creating a recovery plan</span></span>

<span data-ttu-id="f7753-187">Após a replicação estar habilitada para as VMs de componente do XenApp, a próxima etapa é criar um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-187">After replication is enabled for the XenApp component VMs, the next step is to create a recovery plan.</span></span>
<span data-ttu-id="f7753-188">Uma plano de recuperação agrupa as máquinas virtuais com requisitos semelhantes para failover e recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="f7753-189">**Etapas para criar um plano de recuperação**</span><span class="sxs-lookup"><span data-stu-id="f7753-189">**Steps to create a recovery plan**</span></span>

1. <span data-ttu-id="f7753-190">Adicione máquinas virtuais de componente do XenApp no Plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-190">Add the XenApp component virtual machines in the Recovery Plan.</span></span>
2. <span data-ttu-id="f7753-191">Clique em Planos de Recuperação -> + Plano de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="f7753-192">Forneça um nome intuitivo para o plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-192">Provide an intuitive name for the recovery plan.</span></span>
3. <span data-ttu-id="f7753-193">Para máquinas virtuais do VMware: selecione a origem como o servidor de processo do VMware, o destino como o Microsoft Azure e o modelo de implantação como o Gerenciador de Recursos, e clique em Selecionar itens.</span><span class="sxs-lookup"><span data-stu-id="f7753-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="f7753-194">Para máquinas virtuais do Hyper-V: selecione a origem como o servidor do VMM, o destino como o Microsoft Azure e o modelo de implantação como o Gerenciador de Recursos, e clique em Selecionar itens e, em seguida, selecione as VMs de implantação do XenApp.</span><span class="sxs-lookup"><span data-stu-id="f7753-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select the XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="f7753-195">Adicionar máquinas virtuais aos grupos de failover</span><span class="sxs-lookup"><span data-stu-id="f7753-195">Adding virtual machines to failover groups</span></span>

<span data-ttu-id="f7753-196">Os planos de recuperação podem ser personalizados para adicionar grupos de failover para a ordem de inicialização específica, scripts ou ações manuais.</span><span class="sxs-lookup"><span data-stu-id="f7753-196">Recovery plans can be customized to add failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="f7753-197">Os grupos a seguir precisam ser adicionados ao plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-197">The following groups need to be added to the recovery plan.</span></span>

1. <span data-ttu-id="f7753-198">Grupo de failover 1: DNS AD</span><span class="sxs-lookup"><span data-stu-id="f7753-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="f7753-199">Grupo de failover 2: VMs do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f7753-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="f7753-200">Grupo de failover 3: VM de imagem do VDA Master</span><span class="sxs-lookup"><span data-stu-id="f7753-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="f7753-201">Grupo de failover 4: controlador de entrega e VMs do servidor StoreFront</span><span class="sxs-lookup"><span data-stu-id="f7753-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="f7753-202">Adicionar scripts ao plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="f7753-202">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="f7753-203">Os scripts podem ser executados antes ou depois de um grupo específico em um plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="f7753-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="f7753-204">Ações manuais podem ser também incluídas e executadas durante o failover.</span><span class="sxs-lookup"><span data-stu-id="f7753-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="f7753-205">O plano de recuperação personalizado parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7753-205">The customized recovery plan looks like the below:</span></span>

1. <span data-ttu-id="f7753-206">Grupo de failover 1: DNS AD</span><span class="sxs-lookup"><span data-stu-id="f7753-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="f7753-207">Grupo de failover 2: VMs do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f7753-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="f7753-208">Grupo de failover 3: VM de imagem do VDA Master</span><span class="sxs-lookup"><span data-stu-id="f7753-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="f7753-209">As etapas 4, 6 e 7, que contém ações manuais ou de script, são aplicáveis apenas a um XenApp local > ambiente com catálogos MCS/PVS.</span><span class="sxs-lookup"><span data-stu-id="f7753-209">Steps 4, 6 and 7 containing manual or script actions are applicable to only an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="f7753-210">Ação manual ou de script do grupo 3: desligamento da VM do VDA Master quando o failover para o Azure estiver em estado de execução.</span><span class="sxs-lookup"><span data-stu-id="f7753-210">Group 3 Manual or script action: Shutdown master VDA VM The Master VDA VM when failed over to Azure will be in a running state.</span></span> <span data-ttu-id="f7753-211">Para criar novos catálogos do MCS usando a hospedagem do Azure ARM, a VM do VDA mestre precisa estar com o estado Parada (alocada).</span><span class="sxs-lookup"><span data-stu-id="f7753-211">To create new MCS catalogs using Azure ARM hosting, the master VDA VM is required to be in Stopped (de allocated) state.</span></span> <span data-ttu-id="f7753-212">Desligar a VM do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-212">Shutdown the VM from Azure Portal.</span></span>

5. <span data-ttu-id="f7753-213">Grupo de failover 4: controlador de entrega e VMs do servidor StoreFront</span><span class="sxs-lookup"><span data-stu-id="f7753-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="f7753-214">Ação manual ou de script do grupo 3 1:</span><span class="sxs-lookup"><span data-stu-id="f7753-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="f7753-215">***Adicionar conexão do host do Azure RM***</span><span class="sxs-lookup"><span data-stu-id="f7753-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="f7753-216">Crie uma conexão de host do Azure ARM no computador do Controlador de entrega para provisionar novos catálogos MCS no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-216">Create Azure ARM host connection in Delivery Controller machine to provision new MCS catalogs in Azure.</span></span> <span data-ttu-id="f7753-217">Siga as etapas, conforme explicado neste [artigo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="f7753-217">Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="f7753-218">Ação manual ou de script do grupo 3 2:</span><span class="sxs-lookup"><span data-stu-id="f7753-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="f7753-219">***Recriar os catálogos MCS no Azure***</span><span class="sxs-lookup"><span data-stu-id="f7753-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="f7753-220">Os clones MCS ou PVS existentes no site primário não serão replicados para o Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-220">The existing MCS or PVS clones on the primary site will not be replicated to Azure.</span></span> <span data-ttu-id="f7753-221">Você precisa recriar esses clones usando o provisionamento do VDA Master e do Azure ARM replicados do Controlador de entrega. Siga as etapas, conforme explicado neste [artigo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) para criar catálogos MCS no Azure.</span><span class="sxs-lookup"><span data-stu-id="f7753-221">You need to recreate these clones using the replicated master VDA and Azure ARM provisioning from Delivery controller.Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) to create MCS catalogs in Azure.</span></span>

![Plano de recuperação para componentes do XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="f7753-223">Você pode usar scripts no [local](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) para atualizar o DNS com os novos IPs de failover > máquinas virtuais ou para anexar um balanceador de carga pela máquina virtual na qual o failover foi realizado, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f7753-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) to update the DNS with the new IPs of the failed over >virtual machines or to attach a load balancer on the failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="f7753-224">Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="f7753-224">Doing a test failover</span></span>

<span data-ttu-id="f7753-225">Siga [este guia](site-recovery-test-failover-to-azure.md) fazer um failover de teste.</span><span class="sxs-lookup"><span data-stu-id="f7753-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

![Plano de Recuperação](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="f7753-227">Executar um failover</span><span class="sxs-lookup"><span data-stu-id="f7753-227">Doing a failover</span></span>

<span data-ttu-id="f7753-228">Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.</span><span class="sxs-lookup"><span data-stu-id="f7753-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7753-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7753-229">Next steps</span></span>

<span data-ttu-id="f7753-230">Você pode [saber mais](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sobre replicação de implantações do Citrix XenApp e XenDesktop neste white paper.</span><span class="sxs-lookup"><span data-stu-id="f7753-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="f7753-231">Examine as orientações para [replicar outros aplicativos](site-recovery-workload.md) usando o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f7753-231">Look at the guidance to [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
