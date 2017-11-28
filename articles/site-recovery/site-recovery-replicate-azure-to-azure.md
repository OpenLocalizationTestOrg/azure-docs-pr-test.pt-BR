---
title: aplicativos de aaaReplicate (tooAzure do Azure) | Microsoft Docs
description: "Este artigo descreve como tooset a replicação virtual máquinas em execução em uma região do Azure muito outra região no Azure."
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
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="41a66-103">Replicar máquinas virtuais do Azure tooanother região do Azure</span><span class="sxs-lookup"><span data-stu-id="41a66-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="41a66-104">Atualmente, a replicação do Site Recovery para máquinas virtuais do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="41a66-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="41a66-105">Este artigo descreve como tooset a replicação virtual máquinas em execução em uma região do Azure tooanother região do Azure.</span><span class="sxs-lookup"><span data-stu-id="41a66-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41a66-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="41a66-106">Prerequisites</span></span>

* <span data-ttu-id="41a66-107">artigo de saudação pressupõe que você já sabe sobre o Cofre de serviços de recuperação e recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="41a66-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="41a66-108">É necessário toohave pré 'Cofre de serviços de recuperação' criado.</span><span class="sxs-lookup"><span data-stu-id="41a66-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="41a66-109">É recomendável criar hello 'Cofre de serviços de recuperação' no local de saudação onde você deseja que seu tooreplicate VMs.</span><span class="sxs-lookup"><span data-stu-id="41a66-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="41a66-110">Por exemplo, se o local de destino é ‘Centro dos EUA’, crie o cofre no ‘Centro dos EUA’.</span><span class="sxs-lookup"><span data-stu-id="41a66-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="41a66-111">Se você estiver usando regras de grupos de segurança de rede (NSG) ou conectividade de internet do firewall proxy toocontrol acesso toooutbound em Olá VMs do Azure, certifique-se de que Olá de lista branca você exigido URLs ou IPs.</span><span class="sxs-lookup"><span data-stu-id="41a66-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="41a66-112">Consulte também[documento Guia de rede](./site-recovery-azure-to-azure-networking-guidance.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="41a66-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="41a66-113">Se você tiver um ExpressRoute ou uma conexão VPN entre locais e hello local no Azure de origem, execute [considerações de recuperação de Site para o Azure tooon local ExpressRoute / configuração de VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.</span><span class="sxs-lookup"><span data-stu-id="41a66-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="41a66-114">Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="41a66-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="41a66-115">Sua assinatura do Azure deve ser habilitado toocreate VMs no local de destino Olá deseja toouse região a recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="41a66-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="41a66-116">Você pode contatar o suporte tooenable Olá necessário cota.</span><span class="sxs-lookup"><span data-stu-id="41a66-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="41a66-117">Habilite a replicação do cofre Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="41a66-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="41a66-118">Nesta ilustração, podemos replicará as VMs em execução no toohello de local do Azure Olá 'Ásia Oriental' local ' Sudeste da Ásia '.</span><span class="sxs-lookup"><span data-stu-id="41a66-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="41a66-119">etapas de saudação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="41a66-119">hello steps are as follows:</span></span>

 <span data-ttu-id="41a66-120">Clique em **+ replicar** em replicação de tooenable Olá cofre para máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="41a66-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="41a66-121">**Fonte:** refere-se o ponto de toohello de origem de máquinas de saudação que nesse caso é **Azure**.</span><span class="sxs-lookup"><span data-stu-id="41a66-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="41a66-122">**Local de origem:** é Olá região do Azure de onde você deseja tooprotect suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="41a66-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="41a66-123">Para nesta ilustração, o local de origem Olá será 'Ásia Oriental'</span><span class="sxs-lookup"><span data-stu-id="41a66-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="41a66-124">**Modelo de implantação:** refere-se o modelo de implantação do Azure toohello das máquinas de origem hello.</span><span class="sxs-lookup"><span data-stu-id="41a66-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="41a66-125">Você pode selecionar qualquer clássico ou Gerenciador de recursos e computadores que pertencem a modelo específico toohello serão listados para a proteção na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="41a66-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="41a66-126">É possível replicar apenas uma máquina virtual clássica e recuperá-la como uma máquina virtual clássica.</span><span class="sxs-lookup"><span data-stu-id="41a66-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="41a66-127">Não é possível recuperá-la como uma máquina de virtual do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="41a66-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="41a66-128">**Grupo de recursos:** -lo da saudação recurso grupo toowhich suas máquinas virtuais de origem pertence.</span><span class="sxs-lookup"><span data-stu-id="41a66-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="41a66-129">Olá todas as VMs no grupo de recursos selecionado hello serão listados para a proteção na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="41a66-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="41a66-131">Em **máquinas virtuais > Selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="41a66-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="41a66-132">Você só pode selecionar computadores para os quais a replicação pode ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="41a66-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="41a66-133">Em seguida, clique em OK.</span><span class="sxs-lookup"><span data-stu-id="41a66-133">Then click OK.</span></span>
    <span data-ttu-id="41a66-134">![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="41a66-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="41a66-135">Na seção de Configurações, você pode configurar as propriedades do site de destino</span><span class="sxs-lookup"><span data-stu-id="41a66-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="41a66-136">**Local de destino:** Olá local onde sua fonte de dados de máquina virtual serão replicados.</span><span class="sxs-lookup"><span data-stu-id="41a66-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="41a66-137">Dependendo de seu local de máquinas selecionadas, a recuperação de Site fornecerá que Olá lista de regiões de destino adequado.</span><span class="sxs-lookup"><span data-stu-id="41a66-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="41a66-138">Recomenda-se o local de destino tookeep mesmo a partir de sua recuperação o Cofre de serviços.</span><span class="sxs-lookup"><span data-stu-id="41a66-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="41a66-139">**Grupo de recursos de destino:** é Olá recurso grupo toowhich todas as suas máquinas virtuais replicadas pertencerá. Por padrão a ASR criará um novo grupo de recursos na região de destino Olá com nome com o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="41a66-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="41a66-140">No caso de grupo de recursos criado pelo ASR já existir, ela será reutilizada. Você também pode escolher toocustomize-lo, conforme mostrado na seção de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="41a66-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="41a66-141">**Rede Virtual de destino:** por padrão, ASR criará uma nova rede virtual na região de destino Olá com nome com o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="41a66-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="41a66-142">Isso será mapeada tooyour rede de origem e será usado para qualquer proteção futuras.</span><span class="sxs-lookup"><span data-stu-id="41a66-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="41a66-143">[Verifique os detalhes de rede](site-recovery-network-mapping-azure-to-azure.md) tooknow mais sobre mapeamento de rede.</span><span class="sxs-lookup"><span data-stu-id="41a66-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="41a66-144">**Contas de armazenamento de destino:** por padrão, a ASR criará Olá novo destino conta de armazenamento imitando sua configuração de armazenamento de máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="41a66-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="41a66-145">No caso de conta de armazenamento criada por ASR já existir, ela será reutilizada.</span><span class="sxs-lookup"><span data-stu-id="41a66-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="41a66-146">**Contas de armazenamento de cache:** ASR precisa chamada armazenamento em cache na região de origem de saudação de conta de armazenamento extra.</span><span class="sxs-lookup"><span data-stu-id="41a66-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="41a66-147">Todos os Olá alterações ocorrendo no hello VMs de origem são rastreadas e enviadas toocache conta de armazenamento antes de replicar esses local de destino toohello.</span><span class="sxs-lookup"><span data-stu-id="41a66-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="41a66-148">**Conjunto de disponibilidade:** por padrão, o ASR criará uma novo conjunto de disponibilidade na região de destino Olá com nome com o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="41a66-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="41a66-149">No caso de conjunto de disponibilidade criado pelo ASR já existir, ela será reutilizada.</span><span class="sxs-lookup"><span data-stu-id="41a66-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="41a66-150">**Política de replicação:** ele define as configurações de saudação para recuperação ponto retenção aplicativo e o histórico de instantâneo consistente com frequência.</span><span class="sxs-lookup"><span data-stu-id="41a66-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="41a66-151">Por padrão, o ASR criará uma nova política de replicação com configurações padrão de '24 horas’ para retenção de ponto de recuperação e '60 minutos’ para a frequência do instantâneo consistente de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41a66-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="41a66-153">Personalizar os recursos de destino</span><span class="sxs-lookup"><span data-stu-id="41a66-153">Customize target resources</span></span>

<span data-ttu-id="41a66-154">Caso você deseje toochange saudação padrão ASR, você pode alterar configurações de saudação com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="41a66-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="41a66-155">**Personalizar:** clique em toochange Olá os padrões usados pelos ASR.</span><span class="sxs-lookup"><span data-stu-id="41a66-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="41a66-156">**Grupo de recursos de destino:** você pode selecionar o grupo de recursos de saudação da lista de saudação de todos os grupos de recursos Olá existente no local de destino de saudação de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="41a66-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="41a66-157">**Rede Virtual de destino:** você pode encontrar a lista de saudação da rede virtual de saudação todos os no local de destino hello.</span><span class="sxs-lookup"><span data-stu-id="41a66-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="41a66-158">**Conjunto de disponibilidade:** você só pode adicionar disponibilidade conjuntos de configurações toohello VMs que fazem parte de disponibilidade na região de origem.</span><span class="sxs-lookup"><span data-stu-id="41a66-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="41a66-159">**Contas de Armazenamento de Destino:**</span><span class="sxs-lookup"><span data-stu-id="41a66-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="41a66-160">![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Clique em **Criar o recurso de destino** e Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="41a66-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="41a66-161">Depois que as máquinas virtuais são protegidas você pode verificar o status de saudação de integridade de VMs em **replicadas itens**</span><span class="sxs-lookup"><span data-stu-id="41a66-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="41a66-162">Durante a saudação momento da replicação inicial existe pode ser uma possibilidade de que o status leva tempo toorefresh e você não vir o andamento por algum tempo.</span><span class="sxs-lookup"><span data-stu-id="41a66-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="41a66-163">Você pode clicar em botão de atualização de saudação na parte superior da saudação de status mais recente do Olá Olá folha tooget.</span><span class="sxs-lookup"><span data-stu-id="41a66-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Habilitar a replicação](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="41a66-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41a66-165">Next steps</span></span>
- <span data-ttu-id="41a66-166">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre a execução de failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="41a66-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="41a66-167">[Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.</span><span class="sxs-lookup"><span data-stu-id="41a66-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="41a66-168">Saiba mais sobre [usando planos de recuperação](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="41a66-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="41a66-169">Saiba mais sobre [proteger novamente as VMs do Azure](site-recovery-how-to-reprotect.md) após o failover.</span><span class="sxs-lookup"><span data-stu-id="41a66-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
