---
title: "Replicar VMs do Hyper-V no VMM para um site secundário com o PowerShell (Azure Resource Manager) | Microsoft Docs"
description: "Descreve como implantar o Azure Site Recovery para orquestrar a replicação, o failover e a recuperação de VMs do Hyper-V em nuvens do VMM para um local de VMM secundário usando o PowerShell (Resource Manager)"
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
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="bbe40-103">Replicar máquinas virtuais do Hyper-V em nuvens de VMM para um site de VMM secundário usando PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="bbe40-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bbe40-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bbe40-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="bbe40-105">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="bbe40-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="bbe40-106">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bbe40-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="bbe40-107">Bem-vindo ao Azure Site Recovery!</span><span class="sxs-lookup"><span data-stu-id="bbe40-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="bbe40-108">Use este artigo se desejar replicar máquinas virtuais Hyper-V locais gerenciadas em nuvens do System Center VMM (Virtual Machine Manager) para um site secundário.</span><span class="sxs-lookup"><span data-stu-id="bbe40-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="bbe40-109">Este artigo mostra como usar o PowerShell para automatizar tarefas comuns que você precisa executar quando você configura o Azure Site Recovery para replicar máquinas virtuais Hyper-V em nuvens do System Center VMM para nuvens do VMM do System Center no site secundário.</span><span class="sxs-lookup"><span data-stu-id="bbe40-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="bbe40-110">O artigo inclui pré-requisitos para o cenário e mostra a você como:</span><span class="sxs-lookup"><span data-stu-id="bbe40-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="bbe40-111">Configurar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="bbe40-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="bbe40-112">Instalar o Provedor do Azure Site Recovery no servidor VMM de origem e de destino</span><span class="sxs-lookup"><span data-stu-id="bbe40-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="bbe40-113">Registrar os servidores do VMM no cofre</span><span class="sxs-lookup"><span data-stu-id="bbe40-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="bbe40-114">Configurar a política de replicação para a nuvem do VMM.</span><span class="sxs-lookup"><span data-stu-id="bbe40-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="bbe40-115">As configurações de replicação na política serão aplicadas a todas as máquinas virtuais protegidas</span><span class="sxs-lookup"><span data-stu-id="bbe40-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="bbe40-116">Habilitar a proteção para as máquina virtuais.</span><span class="sxs-lookup"><span data-stu-id="bbe40-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="bbe40-117">Testar o failover de VMs, individualmente ou como parte de um plano de recuperação para verificar se tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="bbe40-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="bbe40-118">Executar um failover planejado ou não planejado de VMs, individualmente ou como parte de um plano de recuperação para verificar se tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="bbe40-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="bbe40-119">Se você enfrentar problemas ao configurar esse cenário, publique suas perguntas no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bbe40-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="bbe40-120">O Azure tem dois [modelos de implantação](../azure-resource-manager/resource-manager-deployment-model.md) diferentes para criar e trabalhar com recursos: Azure Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="bbe40-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="bbe40-121">O Azure também tem dois portais – o portal clássico do Azure, que dá suporte ao modelo de implantação clássica, e o portal do Azure, com suporte para ambos os modelos de implantação.</span><span class="sxs-lookup"><span data-stu-id="bbe40-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="bbe40-122">Este artigo aborda o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="bbe40-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="bbe40-123">Pré-requisitos do local</span><span class="sxs-lookup"><span data-stu-id="bbe40-123">On-premises prerequisites</span></span>
<span data-ttu-id="bbe40-124">Aqui está o que será necessário nos sites primário e secundário locais para implantar este cenário:</span><span class="sxs-lookup"><span data-stu-id="bbe40-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="bbe40-125">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="bbe40-125">**Prerequisites**</span></span> | <span data-ttu-id="bbe40-126">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="bbe40-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="bbe40-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="bbe40-127">**VMM**</span></span> |<span data-ttu-id="bbe40-128">Recomendamos a implantação com um servidor VMM no site primário e de um servidor VMM no site secundário.</span><span class="sxs-lookup"><span data-stu-id="bbe40-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="bbe40-129">Você também pode [replicar entre nuvens em um único servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="bbe40-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="bbe40-130">Para fazer isso, você precisará de pelo menos duas nuvens configuradas no servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="bbe40-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="bbe40-131">Os servidores VMM devem estar executando pelo menos o System Center 2012 SP1 com as atualizações mais recentes.</span><span class="sxs-lookup"><span data-stu-id="bbe40-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="bbe40-132">Cada servidor VMM deve ter uma ou mais nuvens configuradas, e todas as nuvens devem ter o perfil de Capacidade do Hyper-V definido.</span><span class="sxs-lookup"><span data-stu-id="bbe40-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="bbe40-133">As nuvens devem conter um ou mais grupos de hosts do VMM.</span><span class="sxs-lookup"><span data-stu-id="bbe40-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="bbe40-134">Saiba mais sobre como configurar nuvens VMM em [Configurando a malha de nuvem VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric) e [Passo a passo: criando nuvens privadas com o VMM do System Center 2012 SP1](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbe40-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="bbe40-135">Os servidores VMM devem ter acesso à internet.</span><span class="sxs-lookup"><span data-stu-id="bbe40-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="bbe40-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="bbe40-136">**Hyper-V**</span></span> |<span data-ttu-id="bbe40-137">Os servidores Hyper-V devem estar executando pelo menos o Windows Server 2012 com a função Hyper-V e ter as últimas atualizações instaladas.</span><span class="sxs-lookup"><span data-stu-id="bbe40-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="bbe40-138">Um servidor Hyper-V deve conter uma ou mais VMs.</span><span class="sxs-lookup"><span data-stu-id="bbe40-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="bbe40-139">Os servidores host Hyper-V devem estar localizados em grupos de hosts nas nuvens VMM primárias e secundárias.</span><span class="sxs-lookup"><span data-stu-id="bbe40-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="bbe40-140">Se você estiver executando o Hyper-V em um cluster no Windows Server 2012 R2, instale a [atualização 2961977](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="bbe40-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="bbe40-141">Se estiver executando o Hyper-V em um cluster no Windows Server 2012, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="bbe40-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="bbe40-142">Você precisará configurar o agente de cluster manualmente.</span><span class="sxs-lookup"><span data-stu-id="bbe40-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="bbe40-143">[Leia mais](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbe40-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="bbe40-144">**Provedor**</span><span class="sxs-lookup"><span data-stu-id="bbe40-144">**Provider**</span></span> |<span data-ttu-id="bbe40-145">Durante a implantação de Recuperação de Site, você instala o Provedor do Azure Site Recovery em servidores VMM.</span><span class="sxs-lookup"><span data-stu-id="bbe40-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="bbe40-146">O Provedor se comunica com a Recuperação de Site por HTTPS 443 para orquestrar a replicação.</span><span class="sxs-lookup"><span data-stu-id="bbe40-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="bbe40-147">A replicação de dados ocorre entre os servidores Hyper-V primário e secundário sobre a LAN ou uma conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="bbe40-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="bbe40-148">O Provedor em execução no servidor VMM precisa de acesso a estas URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="bbe40-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="bbe40-149">Além disso, permita a comunicação de firewall de servidores VMM para os [Intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e permita o protocolo HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="bbe40-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="bbe40-150">Pré-requisitos de mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="bbe40-150">Network mapping prerequisites</span></span>
<span data-ttu-id="bbe40-151">Mapeamento de rede mapeiam entre redes de VM do VMM nos servidores primário e secundário do VMM para:</span><span class="sxs-lookup"><span data-stu-id="bbe40-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="bbe40-152">Colocar de maneira ideal VMs de réplica em hosts secundários do Hyper-V após o failover.</span><span class="sxs-lookup"><span data-stu-id="bbe40-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="bbe40-153">Conecte VMs de réplica às redes de VM apropriadas.</span><span class="sxs-lookup"><span data-stu-id="bbe40-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="bbe40-154">Se você não configurar o mapeamento de rede, as VMs de réplica não serão conectadas a nenhuma rede após o failover.</span><span class="sxs-lookup"><span data-stu-id="bbe40-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="bbe40-155">Se você quiser configurar o mapeamento de rede durante a implantação de Recuperação de Site, você precisará disto:</span><span class="sxs-lookup"><span data-stu-id="bbe40-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="bbe40-156">Verifique se as VMs do servidor host de origem do Hyper-V estão conectadas a uma rede de VMs do VMM.</span><span class="sxs-lookup"><span data-stu-id="bbe40-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="bbe40-157">Essa rede deve ser vinculada a uma rede lógica que esteja associada à nuvem.</span><span class="sxs-lookup"><span data-stu-id="bbe40-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="bbe40-158">Verifique se a nuvem secundária que você usará para recuperação tem uma rede VM correspondente configurada.</span><span class="sxs-lookup"><span data-stu-id="bbe40-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="bbe40-159">Essa rede de VM deverá ser vinculada a uma rede lógica associada à nuvem secundária.</span><span class="sxs-lookup"><span data-stu-id="bbe40-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="bbe40-160">Saiba mais sobre como configurar redes VMM nos artigos abaixo</span><span class="sxs-lookup"><span data-stu-id="bbe40-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="bbe40-161">Como configurar redes lógicas no VMM</span><span class="sxs-lookup"><span data-stu-id="bbe40-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="bbe40-162">Como configurar redes e gateways de VMs no VMM</span><span class="sxs-lookup"><span data-stu-id="bbe40-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="bbe40-163">[Saiba mais](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sobre o funcionamento do mapeamento de rede.</span><span class="sxs-lookup"><span data-stu-id="bbe40-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="bbe40-164">Pré-requisitos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="bbe40-164">PowerShell prerequisites</span></span>
<span data-ttu-id="bbe40-165">Verifique se você tem o PowerShell do Azure pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="bbe40-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="bbe40-166">Se você já estiver usando o PowerShell, precisará atualizar para a versão 0.8.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bbe40-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="bbe40-167">Para obter mais informações sobre como configurar o PowerShell, confira o [Guia de instalação e de configuração do Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="bbe40-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="bbe40-168">Depois de instalar e configurar o PowerShell, você poderá exibir todos os cmdlets disponíveis para o serviço [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bbe40-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="bbe40-169">Para obter dicas que podem ajudar você a usar os cmdlets, como valores de parâmetro, entradas e saídas, que normalmente são tratados no Azure PowerShell, confira [Introdução aos cmdlets do Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="bbe40-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="bbe40-170">Etapa 1: definir a assinatura</span><span class="sxs-lookup"><span data-stu-id="bbe40-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="bbe40-171">No Azure PowerShell, faça logon na conta do Azure usando os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="bbe40-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="bbe40-172">Obtenha uma lista das suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="bbe40-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="bbe40-173">Essa lista também incluirá as IDs de assinatura de cada uma das assinaturas.</span><span class="sxs-lookup"><span data-stu-id="bbe40-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="bbe40-174">Anote a ID da assinatura na qual você quer criar o cofre dos serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="bbe40-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="bbe40-175">Defina a assinatura na qual o cofre dos serviços de recuperação deverá ser criado mencionando a ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="bbe40-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="bbe40-176">Etapa 2: Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="bbe40-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="bbe40-177">Se você ainda não tiver um, crie um grupo de recursos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bbe40-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="bbe40-178">Crie um novo cofre de Serviços de Recuperação e salve o objeto de cofre ASR criado em uma variável (será usado posteriormente).</span><span class="sxs-lookup"><span data-stu-id="bbe40-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="bbe40-179">Você também pode recuperar o objeto de cofre ASR pós-criação usando o cmdlet Get-AzureRMRecoveryServicesVault:-</span><span class="sxs-lookup"><span data-stu-id="bbe40-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="bbe40-180">Etapa 3: Configurar o contexto do Cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="bbe40-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="bbe40-181">Se já houver um cofre criado, execute o comando abaixo para obter o cofre.</span><span class="sxs-lookup"><span data-stu-id="bbe40-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="bbe40-182">Defina o contexto de cofre, executando o comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="bbe40-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="bbe40-183">Etapa 4: instalar o Provedor do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bbe40-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="bbe40-184">Na máquina da VMM, crie um diretório executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bbe40-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="bbe40-185">Extraia os arquivos usando o provedor baixado, executando o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="bbe40-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="bbe40-186">Instale o provedor usando os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbe40-186">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="bbe40-187">Aguarde a conclusão da instalação.</span><span class="sxs-lookup"><span data-stu-id="bbe40-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="bbe40-188">Registre o servidor no cofre usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bbe40-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="bbe40-189">Etapa 5: Criar e associar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="bbe40-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="bbe40-190">Crie uma política de replicação do Hyper-V 2012 R2 executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbe40-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="bbe40-191">A nuvem do VMM pode conter hosts Hyper-V executando versões diferentes do Windows Server (conforme mencionado nos pré-requisitos do Hyper-V), mas a política de replicação é específica à versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="bbe40-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="bbe40-192">Se você tiver hosts diferentes em execução em versões diferentes do sistema operacional, crie políticas de replicação separadas para cada tipo de versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="bbe40-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="bbe40-193">Por exemplo: se você tiver cinco hosts em execução no Windows Server 2012 e três no Windows Server 2012 R2, crie duas políticas de replicação – uma para cada tipo de versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="bbe40-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="bbe40-194">Obtenha o contêiner de proteção principal (nuvem VMM principal) e o contêiner de proteção de recuperação (nuvem do VMM de recuperação) executando os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbe40-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="bbe40-195">Recuperar a política que você criou na etapa 1 usando o nome amigável da política</span><span class="sxs-lookup"><span data-stu-id="bbe40-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="bbe40-196">Inicie a associação do contêiner de proteção (Nuvem do VMM) com a política de replicação:</span><span class="sxs-lookup"><span data-stu-id="bbe40-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="bbe40-197">Aguarde o conclusão do trabalho de associação da política.</span><span class="sxs-lookup"><span data-stu-id="bbe40-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="bbe40-198">Você pode verificar se o trabalho foi concluído usando o seguinte trecho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bbe40-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="bbe40-199">Após a conclusão do processamento do trabalho, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bbe40-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="bbe40-200">Para verificar a conclusão da operação, execute as etapas em [Monitorar a Atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bbe40-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="bbe40-201">Etapa 6: Configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="bbe40-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="bbe40-202">O primeiro comando obtém servidores para o cofre atual do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bbe40-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="bbe40-203">O comando armazena os servidores do Microsoft Azure Site Recovery na variável de matriz $Servers.</span><span class="sxs-lookup"><span data-stu-id="bbe40-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="bbe40-204">Os comandos a seguir obtêm a rede de recuperação de site para o servidor VMM de origem e o servidor VMM de destino.</span><span class="sxs-lookup"><span data-stu-id="bbe40-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="bbe40-205">O servidor VMM de origem pode ser o primeiro ou o segundo na matriz de servidores.</span><span class="sxs-lookup"><span data-stu-id="bbe40-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="bbe40-206">Verifique os nomes dos servidores VMM e obtenha as redes adequadamente</span><span class="sxs-lookup"><span data-stu-id="bbe40-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="bbe40-207">O cmdlet final cria um mapeamento entre a rede principal e a rede de recuperação.</span><span class="sxs-lookup"><span data-stu-id="bbe40-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="bbe40-208">O cmdlet especifica a rede principal como o primeiro elemento da $PrimaryNetworks e a rede de recuperação como o primeiro elemento da $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="bbe40-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="bbe40-209">Etapa 7: Configurar mapeamento de armazenamento</span><span class="sxs-lookup"><span data-stu-id="bbe40-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="bbe40-210">O comando abaixo coloca a lista de classificações de armazenamento na variável $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="bbe40-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="bbe40-211">Os comandos a seguir colocam a classificação de origem na variável $SourceClassificaion e a classificação de destino na variável $TargetClassification.</span><span class="sxs-lookup"><span data-stu-id="bbe40-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="bbe40-212">As classificações de origem e de destino podem ser qualquer elemento na matriz.</span><span class="sxs-lookup"><span data-stu-id="bbe40-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="bbe40-213">Consulte a saída do comando abaixo para identificar o índice das classificações de origem e destino na matriz $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="bbe40-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="bbe40-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="bbe40-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="bbe40-215">O cmdlet a seguir cria um mapeamento entre a classificação de origem e a classificação de destino.</span><span class="sxs-lookup"><span data-stu-id="bbe40-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="bbe40-216">Etapa 8: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="bbe40-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="bbe40-217">Depois que os servidores, nuvens e redes estiverem configurados corretamente, você poderá habilitar a proteção para máquinas virtuais na nuvem.</span><span class="sxs-lookup"><span data-stu-id="bbe40-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="bbe40-218">Para habilitar a proteção, execute o seguinte comando para obter o contêiner de proteção:</span><span class="sxs-lookup"><span data-stu-id="bbe40-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="bbe40-219">Obtenha a entidade de proteção (VM) executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bbe40-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="bbe40-220">Habilite a replicação para a VM executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bbe40-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="bbe40-221">Testar a implantação</span><span class="sxs-lookup"><span data-stu-id="bbe40-221">Test your deployment</span></span>
<span data-ttu-id="bbe40-222">Para testar sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consistente de várias máquinas virtuais e executar um failover de teste para o plano.</span><span class="sxs-lookup"><span data-stu-id="bbe40-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="bbe40-223">O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.</span><span class="sxs-lookup"><span data-stu-id="bbe40-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="bbe40-224">Você pode criar um plano de recuperação para seu aplicativo no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe40-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="bbe40-225">Para verificar a conclusão da operação, execute as etapas em [Monitorar a Atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bbe40-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="bbe40-226">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="bbe40-226">Run a test failover</span></span>
1. <span data-ttu-id="bbe40-227">Execute os cmdlets abaixo para obter a rede de VM na qual você deseja testar o failover de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="bbe40-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="bbe40-228">Execute um teste de failover de uma VM fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bbe40-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="bbe40-229">Execute um teste de failover de um plano de recuperação fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bbe40-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="bbe40-230">Executar um failover planejado</span><span class="sxs-lookup"><span data-stu-id="bbe40-230">Run a planned failover</span></span>
1. <span data-ttu-id="bbe40-231">Execute um failover planejado de uma VM fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bbe40-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="bbe40-232">Execute um failover planejado de um plano de recuperação fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bbe40-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="bbe40-233">Executar um failover não planejado</span><span class="sxs-lookup"><span data-stu-id="bbe40-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="bbe40-234">Execute um failover não planejado de uma VM fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bbe40-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="bbe40-235">2. Execute um failover não planejado de um plano de recuperação fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bbe40-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="bbe40-236"><a name=monitor></a> Monitorar a atividade</span><span class="sxs-lookup"><span data-stu-id="bbe40-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="bbe40-237">Use os seguintes comandos para monitorar a atividade.</span><span class="sxs-lookup"><span data-stu-id="bbe40-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="bbe40-238">Observe que é necessário aguardar a conclusão do processamento entre os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="bbe40-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="bbe40-239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bbe40-239">Next steps</span></span>
<span data-ttu-id="bbe40-240">[Leia mais](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bbe40-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
