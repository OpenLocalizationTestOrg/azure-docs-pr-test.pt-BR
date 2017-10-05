---
title: Replicar aplicativos (VMware para o Azure) | Microsoft Docs
description: "Este artigo descreve como configurar a replicação de máquinas virtuais que são executadas em uma região do Azure para outra."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="9bc26-103">Replicação de máquinas virtuais do Azure para outra região do Azure</span><span class="sxs-lookup"><span data-stu-id="9bc26-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="9bc26-104">Replicação de recuperação de site para máquinas virtuais do Azure está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="9bc26-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="9bc26-105">Este artigo descreve como configurar a replicação de máquinas virtuais que são executadas em uma região do Azure para outra.</span><span class="sxs-lookup"><span data-stu-id="9bc26-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bc26-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9bc26-106">Prerequisites</span></span>

* <span data-ttu-id="9bc26-107">O artigo supõe que você já sabe sobre o Cofre de serviços de recuperação e recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="9bc26-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="9bc26-108">Você precisa ter uma versão anterior de 'Cofre de serviços de recuperação' criada.</span><span class="sxs-lookup"><span data-stu-id="9bc26-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="9bc26-109">É recomendável que você crie o cofre de serviços de recuperação no local onde você deseja suas VMs para replicar.</span><span class="sxs-lookup"><span data-stu-id="9bc26-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="9bc26-110">Por exemplo, se o local de destino é ‘Centro dos EUA’, crie o cofre no ‘Centro dos EUA’.</span><span class="sxs-lookup"><span data-stu-id="9bc26-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="9bc26-111">Se você estiver usando Regras de Grupos de Segurança de Rede (NSG) ou proxy de firewall para controlar o acesso à conectividade de internet de saída nas VMs do Azure, certifique-se de que você permita os URLs ou o IPs necessários.</span><span class="sxs-lookup"><span data-stu-id="9bc26-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="9bc26-112">Consulte o [Documento de diretrizes de rede](./site-recovery-azure-to-azure-networking-guidance.md) para mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9bc26-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="9bc26-113">Se você tiver um ExpressRoute ou uma conexão VPN entre locais e o local de origem no Azure, siga o documento [Considerações de recuperação de Site do Azure para ExpressRoute/configuração de VPN local](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration).</span><span class="sxs-lookup"><span data-stu-id="9bc26-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="9bc26-114">Sua conta de usuário do Azure precisa ter certas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) para habilitar a replicação de uma nova máquina virtual para o Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc26-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="9bc26-115">Sua assinatura deve ser habilitada para criar VMs do Azure na região de destino que você planeja usar como a região de recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="9bc26-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="9bc26-116">Contate o suporte para habilitar a cota necessária.</span><span class="sxs-lookup"><span data-stu-id="9bc26-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="9bc26-117">Habilite a replicação do cofre Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9bc26-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="9bc26-118">Nesta ilustração, replicaremos as VMs em execução em 'Ásia Oriental' do Azure local para o local de 'Sudeste da Ásia'.</span><span class="sxs-lookup"><span data-stu-id="9bc26-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="9bc26-119">As etapas são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="9bc26-119">The steps are as follows:</span></span>

 <span data-ttu-id="9bc26-120">Clique em **+ Replicar** no cofre para habilitar a replicação para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9bc26-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="9bc26-121">**Fonte:** refere-se para o ponto de origem das máquinas que nesse caso é **Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bc26-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="9bc26-122">**Local de origem:** é a região do Azure de onde você deseja proteger suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9bc26-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="9bc26-123">Para esta ilustração, o local de origem será 'Ásia Oriental'</span><span class="sxs-lookup"><span data-stu-id="9bc26-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="9bc26-124">**Modelo de implantação:** refere-se ao modelo de implantação do Azure de computadores de origem.</span><span class="sxs-lookup"><span data-stu-id="9bc26-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="9bc26-125">Você pode selecionar qualquer clássico ou Gerenciador de recursos e computadores que pertençam a um modelo específico serão listados para a proteção na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="9bc26-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="9bc26-126">Você pode apenas replicar a máquina virtual clássica e recuperá-la como uma máquina virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="9bc26-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="9bc26-127">Você não pode recuperá-la como uma máquina virtual de gerenciamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="9bc26-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="9bc26-128">**Grupo de recursos:** é o grupo de recursos ao qual pertencem as máquinas virtuais de origem.</span><span class="sxs-lookup"><span data-stu-id="9bc26-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="9bc26-129">Todas as máquinas virtuais do grupo de recursos selecionado serão listadas para a proteção na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="9bc26-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="9bc26-131">Em **Máquinas Virtuais > Selecionar máquinas virtuais**, clique e selecione cada máquina que você deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="9bc26-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="9bc26-132">Você só pode selecionar computadores para os quais a replicação pode ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="9bc26-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="9bc26-133">Em seguida, clique em OK.</span><span class="sxs-lookup"><span data-stu-id="9bc26-133">Then click OK.</span></span>
    <span data-ttu-id="9bc26-134">![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="9bc26-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="9bc26-135">Na seção de Configurações, você pode configurar as propriedades do site de destino</span><span class="sxs-lookup"><span data-stu-id="9bc26-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="9bc26-136">**Local de destino:** Esse é o local onde seus dados de máquina virtual de origem serão replicados.</span><span class="sxs-lookup"><span data-stu-id="9bc26-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="9bc26-137">Dependendo de seu local de máquinas selecionadas, a recuperação de Site fornece a lista de regiões de destino adequado.</span><span class="sxs-lookup"><span data-stu-id="9bc26-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="9bc26-138">É recomendável manter o local de destino igual a do Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9bc26-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="9bc26-139">**Grupo de recursos de destino:** é o grupo de recursos ao qual todas as suas máquinas virtuais replicadas pertencerão. Por padrão, a ASR criará um novo grupo de recursos na região de destino com um nome com o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="9bc26-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="9bc26-140">No caso de grupo de recursos criado pelo ASR já existir, ela será reutilizada. Também é possível personalizá-lo, conforme mostrado na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="9bc26-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="9bc26-141">**Rede Virtual de Destino:** Por padrão, a ASR criará um novo grupo de recursos na região de destino com um nome com o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="9bc26-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="9bc26-142">Isso será mapeado para sua rede de origem e será usado para qualquer proteção futura.</span><span class="sxs-lookup"><span data-stu-id="9bc26-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9bc26-143">[Verifique os detalhes de rede](site-recovery-network-mapping-azure-to-azure.md) para saber mais sobre mapeamento de rede.</span><span class="sxs-lookup"><span data-stu-id="9bc26-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="9bc26-144">**Contas de Armazenamento de Destino:** Por padrão, o ASR criará a nova conta de armazenamento de destino imitando sua configuração de armazenamento de máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="9bc26-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="9bc26-145">No caso de conta de armazenamento criada por ASR já existir, ela será reutilizada.</span><span class="sxs-lookup"><span data-stu-id="9bc26-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="9bc26-146">**Contas de armazenamento de cache:** ASR precisa de conta de armazenamento extra, chamada de armazenamento em cache da região de origem.</span><span class="sxs-lookup"><span data-stu-id="9bc26-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="9bc26-147">Todas as alterações ocorrendo nas máquinas virtuais de origem são controladas e enviadas para a conta de armazenamento do cache antes de replicar para o local de destino.</span><span class="sxs-lookup"><span data-stu-id="9bc26-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="9bc26-148">**Conjunto de Disponibilidade:** Por padrão, a ASR criará um novo grupo de recursos na região de destino com um nome com o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="9bc26-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="9bc26-149">No caso de conjunto de disponibilidade criado pelo ASR já existir, ela será reutilizada.</span><span class="sxs-lookup"><span data-stu-id="9bc26-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="9bc26-150">**Política de replicação:** define as configurações para histórico de retenção de ponto de recuperação e frequência de instantâneo consistente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9bc26-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="9bc26-151">Por padrão, o ASR criará uma nova política de replicação com configurações padrão de '24 horas’ para retenção de ponto de recuperação e '60 minutos’ para a frequência do instantâneo consistente de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9bc26-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="9bc26-153">Personalizar os recursos de destino</span><span class="sxs-lookup"><span data-stu-id="9bc26-153">Customize target resources</span></span>

<span data-ttu-id="9bc26-154">No caso de você desejar alterar os padrões usados pela ASR, você pode alterar as configurações de acordo com suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9bc26-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="9bc26-155">**Personalizar:** Clique para alterar os padrões usados pela ASR.</span><span class="sxs-lookup"><span data-stu-id="9bc26-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="9bc26-156">**Grupo de recursos de destino:** Você pode selecionar o grupo de recursos da lista de todos os grupos de recursos existentes no local de destino dentro da assinatura.</span><span class="sxs-lookup"><span data-stu-id="9bc26-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="9bc26-157">**Rede Virtual de Destino:** Você pode encontrar a lista de todas as redes virtuais no local de destino.</span><span class="sxs-lookup"><span data-stu-id="9bc26-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="9bc26-158">**Conjunto de disponibilidade:** você só pode adicionar configurações de conjuntos de disponibilidade para as máquinas virtuais que fazem parte de disponibilidade na região de origem.</span><span class="sxs-lookup"><span data-stu-id="9bc26-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="9bc26-159">**Contas de Armazenamento de Destino:**</span><span class="sxs-lookup"><span data-stu-id="9bc26-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="9bc26-160">![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Clique em **Criar o recurso de destino** e Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="9bc26-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="9bc26-161">Depois que as máquinas virtuais são protegidas, você pode verificar o status de integridade de VMs em **Itens replicados**</span><span class="sxs-lookup"><span data-stu-id="9bc26-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="9bc26-162">Durante o tempo de replicação inicial existe uma possibilidade de que o status demore para atualizar e você não veja nenhum progresso por algum tempo.</span><span class="sxs-lookup"><span data-stu-id="9bc26-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="9bc26-163">Você pode clicar no botão Atualizar na parte superior da folha para obter o status mais recente.</span><span class="sxs-lookup"><span data-stu-id="9bc26-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="9bc26-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9bc26-165">Next steps</span></span>
- <span data-ttu-id="9bc26-166">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre a execução de failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="9bc26-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="9bc26-167">[Saiba mais](site-recovery-failover.md) sobre diferentes tipos de failovers e como executá-los.</span><span class="sxs-lookup"><span data-stu-id="9bc26-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="9bc26-168">Saiba mais sobre [usando planos de recuperação](site-recovery-create-recovery-plans.md) para reduzir o RTO.</span><span class="sxs-lookup"><span data-stu-id="9bc26-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="9bc26-169">Saiba mais sobre [proteger novamente as VMs do Azure](site-recovery-how-to-reprotect.md) após o failover.</span><span class="sxs-lookup"><span data-stu-id="9bc26-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
