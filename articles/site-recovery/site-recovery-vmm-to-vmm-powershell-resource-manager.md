---
title: "aaaReplicate VMs Hyper-V no site secundário do VMM tooa com o PowerShell (Gerenciador de recursos do Azure) | Microsoft Docs"
description: "Descreve como a replicação de tooorchestrate do Azure Site Recovery toodeploy, failover e recuperação de máquinas virtuais do Hyper-V no VMM nuvens tooa site do VMM secundário usando o PowerShell (Gerenciador de recursos)"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="29e11-103">Replicar máquinas virtuais de Hyper-V no VMM nuvens tooa site VMM secundário usando o PowerShell (Gerenciador de recursos)</span><span class="sxs-lookup"><span data-stu-id="29e11-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29e11-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="29e11-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="29e11-105">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="29e11-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="29e11-106">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29e11-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="29e11-107">Bem-vindo tooAzure recuperação de Site!</span><span class="sxs-lookup"><span data-stu-id="29e11-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="29e11-108">Use este artigo se você quiser tooreplicate máquinas virtuais de Hyper-V gerenciados no site secundário do System Center Virtual Machine Manager (VMM) nuvens tooa local.</span><span class="sxs-lookup"><span data-stu-id="29e11-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="29e11-109">Este artigo mostra como as tarefas comuns do toouse PowerShell tooautomate precisar tooperform ao configurar máquinas virtuais do Azure Site Recovery tooreplicate Hyper-V nas nuvens VMM do System Center VMM nuvens tooSystem Center no site secundário.</span><span class="sxs-lookup"><span data-stu-id="29e11-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="29e11-110">Olá artigo inclui os pré-requisitos para o cenário de saudação e mostra</span><span class="sxs-lookup"><span data-stu-id="29e11-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="29e11-111">Como tooset um cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="29e11-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="29e11-112">Instalar Olá provedor Azure Site Recovery no servidor do VMM de origem de saudação e o servidor do VMM de destino Olá</span><span class="sxs-lookup"><span data-stu-id="29e11-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="29e11-113">Registrar servidores do VMM Olá no cofre Olá</span><span class="sxs-lookup"><span data-stu-id="29e11-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="29e11-114">Configure a política de replicação para Olá nuvem do VMM.</span><span class="sxs-lookup"><span data-stu-id="29e11-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="29e11-115">as configurações de replicação de saudação na política de saudação será máquinas virtuais de tooall aplicada protegido</span><span class="sxs-lookup"><span data-stu-id="29e11-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="29e11-116">Habilite a proteção para máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="29e11-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="29e11-117">Olá failover de máquinas virtuais de teste individualmente ou como parte de um toomake de plano de recuperação se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="29e11-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="29e11-118">Execute um planejado ou um failover não planejado de máquinas virtuais, individualmente ou como parte de um toomake de plano de recuperação se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="29e11-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="29e11-119">Se você tiver problemas para configurar esse cenário, publique suas perguntas sobre Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="29e11-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="29e11-120">O Azure tem dois [modelos de implantação](../azure-resource-manager/resource-manager-deployment-model.md) diferentes para criar e trabalhar com recursos: Azure Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="29e11-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="29e11-121">Azure também tem dois portais – Olá portal clássico do Azure que dá suporte ao modelo de implantação clássico hello e Olá portal do Azure com suporte para ambos os modelos de implantação.</span><span class="sxs-lookup"><span data-stu-id="29e11-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="29e11-122">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="29e11-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="29e11-123">Pré-requisitos do local</span><span class="sxs-lookup"><span data-stu-id="29e11-123">On-premises prerequisites</span></span>
<span data-ttu-id="29e11-124">Aqui está o que você precisará no hello primário e secundário local sites toodeploy neste cenário:</span><span class="sxs-lookup"><span data-stu-id="29e11-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="29e11-125">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="29e11-125">**Prerequisites**</span></span> | <span data-ttu-id="29e11-126">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="29e11-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="29e11-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="29e11-127">**VMM**</span></span> |<span data-ttu-id="29e11-128">Recomendamos que você implantar um servidor do VMM no site primário hello e um servidor do VMM no site secundário hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="29e11-129">Você também pode [replicar entre nuvens em um único servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="29e11-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="29e11-130">toodo isso você precisará de pelo menos duas nuvens configuradas no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="29e11-131">Servidores do VMM devem estar executando pelo menos System Center 2012 SP1 com atualizações mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="29e11-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="29e11-132">Cada servidor do VMM deve ter em um ou mais nuvens configuradas e todas as nuvens devem ter perfil de capacidade do Hyper-V Olá definida.</span><span class="sxs-lookup"><span data-stu-id="29e11-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="29e11-133">As nuvens devem conter um ou mais grupos de hosts do VMM.</span><span class="sxs-lookup"><span data-stu-id="29e11-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="29e11-134">Saiba mais sobre como configurar nuvens do VMM em [Configurando Olá VMM malha de nuvem](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), e [passo a passo: Criando nuvens privadas com o System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e11-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="29e11-135">Os servidores VMM devem ter acesso à internet.</span><span class="sxs-lookup"><span data-stu-id="29e11-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="29e11-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="29e11-136">**Hyper-V**</span></span> |<span data-ttu-id="29e11-137">Servidores Hyper-V devem estar executando pelo menos o Windows Server 2012 com a função hello Hyper-V e ter Olá as últimas atualizações instaladas.</span><span class="sxs-lookup"><span data-stu-id="29e11-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="29e11-138">Um servidor Hyper-V deve conter uma ou mais VMs.</span><span class="sxs-lookup"><span data-stu-id="29e11-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="29e11-139">Servidores de host Hyper-V devem estar localizados em grupos de host em nuvens do VMM Olá primários e secundários.</span><span class="sxs-lookup"><span data-stu-id="29e11-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="29e11-140">Se você estiver executando o Hyper-V em um cluster no Windows Server 2012 R2, instale a [atualização 2961977](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="29e11-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="29e11-141">Se estiver executando o Hyper-V em um cluster no Windows Server 2012, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="29e11-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="29e11-142">Você precisará agente do cluster Olá tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="29e11-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="29e11-143">[Leia mais](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="29e11-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="29e11-144">**Provedor**</span><span class="sxs-lookup"><span data-stu-id="29e11-144">**Provider**</span></span> |<span data-ttu-id="29e11-145">Durante a implantação da recuperação de Site você instalar Olá provedor Azure Site Recovery em servidores do VMM.</span><span class="sxs-lookup"><span data-stu-id="29e11-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="29e11-146">Olá provedor se comunica com a recuperação de Site sobre HTTPS 443 tooorchestrate replicação.</span><span class="sxs-lookup"><span data-stu-id="29e11-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="29e11-147">Replicação de dados ocorre entre servidores de Hyper-V primário e secundário de saudação sobre Olá LAN ou uma conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="29e11-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="29e11-148">Olá provedor em execução no servidor do VMM Olá precisa acessar toothese URLs: *. c o m; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. n e t; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="29e11-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="29e11-149">Além de permitir a comunicação de firewall de saudação do VMM servidores toohello [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e permitir o protocolo HTTPS (443) de saudação.</span><span class="sxs-lookup"><span data-stu-id="29e11-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="29e11-150">Pré-requisitos de mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="29e11-150">Network mapping prerequisites</span></span>
<span data-ttu-id="29e11-151">Mapas de mapeamento de rede entre redes de VM do VMM nos servidores VMM primários e secundários de saudação para:</span><span class="sxs-lookup"><span data-stu-id="29e11-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="29e11-152">Colocar de maneira ideal VMs de réplica em hosts secundários do Hyper-V após o failover.</span><span class="sxs-lookup"><span data-stu-id="29e11-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="29e11-153">Conecte a redes VM de tooappropriate de máquinas virtuais de réplica.</span><span class="sxs-lookup"><span data-stu-id="29e11-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="29e11-154">Se você não configurar a rede mapeamento réplica VMs não será conectada tooany rede após o failover.</span><span class="sxs-lookup"><span data-stu-id="29e11-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="29e11-155">Se você quiser tooset rede mapeamento durante a recuperação de Site implantação aqui é o que será necessário:</span><span class="sxs-lookup"><span data-stu-id="29e11-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="29e11-156">Certifique-se de que as VMs no servidor host Hyper-V de origem de saudação são conectado tooa rede VM do VMM.</span><span class="sxs-lookup"><span data-stu-id="29e11-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="29e11-157">Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="29e11-158">Verifica se a nuvem secundária de saudação que você usará para a recuperação tem uma rede VM correspondente configurada.</span><span class="sxs-lookup"><span data-stu-id="29e11-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="29e11-159">Essa rede VM deve ser vinculado tooa rede lógica associada com a nuvem secundária hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="29e11-160">Saiba mais sobre como configurar redes do VMM no hello artigos abaixo</span><span class="sxs-lookup"><span data-stu-id="29e11-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="29e11-161">Como tooconfigure de redes lógicas no VMM</span><span class="sxs-lookup"><span data-stu-id="29e11-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="29e11-162">Como tooconfigure VM redes e gateways no VMM</span><span class="sxs-lookup"><span data-stu-id="29e11-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="29e11-163">[Saiba mais](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sobre o funcionamento do mapeamento de rede.</span><span class="sxs-lookup"><span data-stu-id="29e11-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="29e11-164">Pré-requisitos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="29e11-164">PowerShell prerequisites</span></span>
<span data-ttu-id="29e11-165">Certifique-se de que ter toogo pronto do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="29e11-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="29e11-166">Se você já estiver usando o PowerShell, você precisará tooupgrade tooversion 0.8.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="29e11-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="29e11-167">Para obter informações sobre como configurar o PowerShell, consulte Olá [guia tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="29e11-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="29e11-168">Depois de você ter instalado e configurado o PowerShell, você pode exibir todos os cmdlets de saudação disponíveis para o serviço de saudação [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29e11-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="29e11-169">toolearn sobre dicas que podem ajudá-lo a usar os cmdlets de saudação, como como valores de parâmetro, as entradas e saídas são tratadas normalmente no Azure PowerShell, consulte Olá [guia de Introdução aos Cmdlets do Azure de tooget](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="29e11-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="29e11-170">Etapa 1: Definir a assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="29e11-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="29e11-171">Do powershell do Azure, logon tooyour conta do Azure: usando Olá cmdlets a seguir</span><span class="sxs-lookup"><span data-stu-id="29e11-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="29e11-172">Obtenha uma lista das suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="29e11-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="29e11-173">Isso também listará Olá subscriptionIDs para cada uma das assinaturas hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="29e11-174">Anote a subscriptionID Olá de assinatura Olá no qual você deseja que o Cofre de serviços de recuperação de saudação toocreate</span><span class="sxs-lookup"><span data-stu-id="29e11-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="29e11-175">Assinatura de saudação conjunto no qual Olá Cofre de serviços de recuperação é toobe criado pelo mencionar Olá ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="29e11-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="29e11-176">Etapa 2: Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="29e11-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="29e11-177">Se você ainda não tiver um, crie um grupo de recursos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29e11-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="29e11-178">Criar um novo cofre de serviços de recuperação e salve Olá criada o objeto de Cofre de recuperação automatizada do sistema em uma variável (será usada posteriormente).</span><span class="sxs-lookup"><span data-stu-id="29e11-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="29e11-179">Você também pode recuperar Olá ASR cofre post criação do objeto usando o cmdlet Get-AzureRMRecoveryServicesVault de saudação:-</span><span class="sxs-lookup"><span data-stu-id="29e11-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="29e11-180">Etapa 3: Definir o contexto de Cofre de serviços de recuperação de saudação</span><span class="sxs-lookup"><span data-stu-id="29e11-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="29e11-181">Se você tiver um cofre já criado, execute Olá abaixo comando tooget saudação do cofre.</span><span class="sxs-lookup"><span data-stu-id="29e11-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="29e11-182">Definir o contexto de Cofre de saudação executando Olá comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="29e11-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="29e11-183">Etapa 4: Instalar Olá provedor Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="29e11-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="29e11-184">Na máquina do VMM hello, crie um diretório executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="29e11-185">Extrair arquivos hello usando o provedor de saudação baixada executando o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="29e11-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="29e11-186">Instale o provedor de saudação usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-186">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="29e11-187">Aguarde Olá toofinish de instalação.</span><span class="sxs-lookup"><span data-stu-id="29e11-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="29e11-188">Registre o servidor de saudação no cofre de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="29e11-189">Etapa 5: Criar e associar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="29e11-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="29e11-190">Crie uma política de replicação do Hyper-V 2012 R2 executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="29e11-191">Olá nuvem do VMM pode conter hosts Hyper-V executando diferentes versões do Windows Server (conforme mencionado nos pré-requisitos do Hyper-V Olá), mas a política de replicação de saudação é a versão do sistema operacional específica.</span><span class="sxs-lookup"><span data-stu-id="29e11-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="29e11-192">Se você tiver hosts diferentes em execução em versões diferentes do sistema operacional, crie políticas de replicação separadas para cada tipo de versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="29e11-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="29e11-193">Por exemplo: se você tiver cinco hosts em execução no Windows Server 2012 e três no Windows Server 2012 R2, crie duas políticas de replicação – uma para cada tipo de versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="29e11-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="29e11-194">Obter contêiner de proteção primária hello (nuvem VMM primária) e o contêiner de proteção de recuperação (recuperação de nuvem do VMM), executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="29e11-195">Recuperar política Olá que você criou na etapa 1 usando nome amigável de saudação da política de saudação</span><span class="sxs-lookup"><span data-stu-id="29e11-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="29e11-196">Inicie associação de saudação do recipiente de proteção da saudação (nuvem do VMM) com a política de replicação hello:</span><span class="sxs-lookup"><span data-stu-id="29e11-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="29e11-197">Aguarde Olá toocomplete de trabalho de associação de política.</span><span class="sxs-lookup"><span data-stu-id="29e11-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="29e11-198">Você pode verificar se o trabalho de saudação foi concluído usando Olá trecho do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="29e11-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="29e11-199">Depois que o trabalho de saudação concluiu o processamento, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="29e11-200">conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="29e11-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="29e11-201">Etapa 6: Configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="29e11-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="29e11-202">Olá primeiro comando obtém servidores para o Cofre de recuperação de Site do Azure atual hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="29e11-203">comando Olá armazena servidores do Microsoft Azure Site Recovery Olá na variável de matriz de saudação $Servers.</span><span class="sxs-lookup"><span data-stu-id="29e11-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="29e11-204">Olá abaixo comandos obter rede de recuperação de site Olá para o servidor do VMM de origem de saudação e o servidor do VMM de destino hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="29e11-205">servidor do VMM de origem Olá pode ser Olá primeira ou segunda matriz de servidores de saudação em uma saudação.</span><span class="sxs-lookup"><span data-stu-id="29e11-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="29e11-206">Verificar nomes Olá dos servidores do VMM hello e obter redes Olá adequadamente</span><span class="sxs-lookup"><span data-stu-id="29e11-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="29e11-207">Olá final cria um mapeamento entre Olá primário e rede Olá recuperação.</span><span class="sxs-lookup"><span data-stu-id="29e11-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="29e11-208">Olá cmdlet especifica a rede primária Olá como primeiro elemento de saudação da rede de recuperação $PrimaryNetworks e hello como o primeiro elemento de saudação do $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="29e11-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="29e11-209">Etapa 7: Configurar mapeamento de armazenamento</span><span class="sxs-lookup"><span data-stu-id="29e11-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="29e11-210">Olá abaixo comando obtém a lista de saudação de classificações de armazenamento em $storageclassifications variável.</span><span class="sxs-lookup"><span data-stu-id="29e11-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="29e11-211">Olá abaixo comandos obter a classificação de origem Olá na variável $SourceClassificaion e classificação de destino em $TargetClassification variável.</span><span class="sxs-lookup"><span data-stu-id="29e11-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="29e11-212">classificações de origem e destino Olá podem ser qualquer elemento na matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="29e11-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="29e11-213">Consulte a saída toohello Olá abaixo índice de saudação do comando toofigure de classificações de origem e de destino na matriz $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="29e11-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="29e11-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="29e11-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="29e11-215">Olá abaixo cmdlet cria um mapeamento entre a classificação de origem hello e classificação de destino hello.</span><span class="sxs-lookup"><span data-stu-id="29e11-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="29e11-216">Etapa 8: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="29e11-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="29e11-217">Depois de redes, nuvens e servidores Olá estão configurados corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="29e11-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="29e11-218">proteção de tooenable executar Olá contêiner de proteção do comando tooget Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="29e11-219">Obtenha a entidade de proteção de saudação (VM) executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="29e11-220">Habilite a replicação para Olá VM executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29e11-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="29e11-221">Testar a implantação</span><span class="sxs-lookup"><span data-stu-id="29e11-221">Test your deployment</span></span>
<span data-ttu-id="29e11-222">planejar a sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar um failover de teste para Olá tootest.</span><span class="sxs-lookup"><span data-stu-id="29e11-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="29e11-223">O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.</span><span class="sxs-lookup"><span data-stu-id="29e11-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="29e11-224">Você pode criar um plano de recuperação para seu aplicativo no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29e11-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="29e11-225">conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="29e11-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="29e11-226">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="29e11-226">Run a test failover</span></span>
1. <span data-ttu-id="29e11-227">Execute Olá abaixo cmdlets tooget Olá VM rede toowhich que deseja tootest failover suas VMs.</span><span class="sxs-lookup"><span data-stu-id="29e11-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="29e11-228">Execute um failover de teste de uma VM fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="29e11-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="29e11-229">Execute um failover de teste de um plano de recuperação fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="29e11-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="29e11-230">Executar um failover planejado</span><span class="sxs-lookup"><span data-stu-id="29e11-230">Run a planned failover</span></span>
1. <span data-ttu-id="29e11-231">Execute um failover planejado de máquina virtual fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="29e11-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="29e11-232">Execute um failover planejado de um plano de recuperação fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="29e11-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="29e11-233">Executar um failover não planejado</span><span class="sxs-lookup"><span data-stu-id="29e11-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="29e11-234">Execute um failover não planejado de máquina virtual fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="29e11-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="29e11-235">2. Execute um failover não planejado de um plano de recuperação fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="29e11-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="29e11-236"><a name=monitor></a> Monitorar a atividade</span><span class="sxs-lookup"><span data-stu-id="29e11-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="29e11-237">Use hello atividade de saudação toomonitor comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="29e11-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="29e11-238">Observe que você tenha toowait entre trabalhos de saudação toofinish de processamento.</span><span class="sxs-lookup"><span data-stu-id="29e11-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="29e11-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29e11-239">Next steps</span></span>
<span data-ttu-id="29e11-240">[Leia mais](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29e11-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
