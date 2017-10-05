---
title: "Atualizar um cofre do Site Recovery para um cofre dos Serviços de Recuperação do Azure"
description: "Saiba como atualizar um cofre do Azure Site Recovery para um cofre dos Serviços de Recuperação"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: fdb33ea0d08353b491f2934fcf885fcb6910b9a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-site-recovery-vault-to-an-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="01baa-103">Atualizar um cofre do Site Recovery para um cofre dos Serviços de Recuperação com base no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01baa-103">Upgrade a Site Recovery vault to an Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="01baa-104">Este artigo descreve como atualizar cofres do Azure Site Recovery para cofres dos Serviços de Recuperação com base no Azure Resource Manager sem afetar a replicação em andamento.</span><span class="sxs-lookup"><span data-stu-id="01baa-104">This article describes how to upgrade Azure Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="01baa-105">Para saber mais sobre os recursos e benefícios do Azure Resource Manager, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="01baa-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="01baa-106">Introduction</span></span>
<span data-ttu-id="01baa-107">Um cofre dos Serviços de Recuperação é um recurso do Azure Resource Manager para gerenciar backup e recuperação de desastre de forma nativa na nuvem.</span><span class="sxs-lookup"><span data-stu-id="01baa-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in the cloud.</span></span> <span data-ttu-id="01baa-108">É um cofre unificado que você pode usar no novo Portal do Azure e ele substitui o backup clássico e os cofres do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="01baa-108">It is a unified vault that you can use in the new Azure portal, and it replaces the classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="01baa-109">Os cofres dos Serviços de Recuperação oferecem uma matriz de recursos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="01baa-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="01baa-110">Suporte do Azure Resource Manager: você pode proteger e realizar o failover de suas máquinas virtuais e computadores físicos em uma pilha do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01baa-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="01baa-111">Excluir disco: se você tem arquivos temporários ou dados com uma variação alta, com os quais você não deseja gastar sua largura de banda, exclua os volumes da replicação.</span><span class="sxs-lookup"><span data-stu-id="01baa-111">Exclude disk: If you have temp files or high churn data that you don’t want to use all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="01baa-112">Essa capacidade está atualmente habilitada em *VMware para Azure* e *Hyper-V para Azure* e está estendido para outros cenários também.</span><span class="sxs-lookup"><span data-stu-id="01baa-112">This capability has been enabled currently in *VMware to Azure* and *Hyper-V to Azure* and is extended to other scenarios as well.</span></span>

* <span data-ttu-id="01baa-113">Suporte para armazenamento Premium e armazenamento com redundância local: agora você pode proteger servidores em contas de armazenamento Premium que permitem aos clientes proteger aplicativos com mais operações de entrada/saída por segundo (IOPS).</span><span class="sxs-lookup"><span data-stu-id="01baa-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers to protect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="01baa-114">Essa capacidade está atualmente habilitada em *VMware para o Azure*.</span><span class="sxs-lookup"><span data-stu-id="01baa-114">This capability is currently enabled in *VMware to Azure*.</span></span>

* <span data-ttu-id="01baa-115">Experiência de introdução simplificada: a experiência aprimorada de introdução foi projetada para facilitar a configuração da recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="01baa-115">Streamlined getting-started experience: The enhanced getting-started experience has been designed to make disaster-recovery setup easy.</span></span>

* <span data-ttu-id="01baa-116">Gerenciamento de Backup e Site Recovery por meio do mesmo cofre: agora você pode proteger servidores para recuperação de desastre ou realização de backup por meio do mesmo cofre, o que reduz consideravelmente a sobrecarga de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="01baa-116">Backup and Site Recovery management from the same vault: You can now protect servers for disaster recovery or perform backup from the same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="01baa-117">Para obter mais informações sobre a experiência e os recursos atualizados, consulte o [Blog de Armazenamento, Backup e Recuperação](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="01baa-117">For more information about the upgraded experience and features, see the [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="01baa-118">Principais recursos</span><span class="sxs-lookup"><span data-stu-id="01baa-118">Salient features</span></span>

* <span data-ttu-id="01baa-119">Sem impacto na replicação em andamento: as replicações em andamento continuam sem qualquer interrupção durante e após a atualização.</span><span class="sxs-lookup"><span data-stu-id="01baa-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="01baa-120">Sem custo adicional: obtenha um conjunto completo de recursos atualizados sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="01baa-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="01baa-121">Sem perda de dados: como esse processo é uma atualização e não uma migração, os pontos de recuperação e as configurações de replicação existentes permanecem intactas durante e após a atualização.</span><span class="sxs-lookup"><span data-stu-id="01baa-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after the upgrade.</span></span>


## <a name="what-happens-during-the-vault-upgrade"></a><span data-ttu-id="01baa-122">O que acontece durante a atualização do cofre?</span><span class="sxs-lookup"><span data-stu-id="01baa-122">What happens during the vault upgrade?</span></span>

<span data-ttu-id="01baa-123">Durante a atualização, você não pode realizar operações como registrar um novo servidor ou habilitar a replicação para uma VM (máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="01baa-123">During the upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="01baa-124">As operações que envolvem a leitura ou gravação de dados no cofre, como a replicação em andamento de itens protegidos no cofre, continuam sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="01baa-124">Operations that involve reading data from or writing data to the vault, such as ongoing replication of protected items to the vault, continue uninterrupted.</span></span>

### <a name="changes-to-automation-and-tooling-after-the-upgrade"></a><span data-ttu-id="01baa-125">Alterações na automação e nas ferramentas depois da atualização</span><span class="sxs-lookup"><span data-stu-id="01baa-125">Changes to automation and tooling after the upgrade</span></span>
<span data-ttu-id="01baa-126">Ao atualizar o tipo de cofre do modelo de implantação clássico para o modelo de implantação do Resource Manager, atualize a automação ou as ferramentas existentes para garantir que continuem funcionando após a atualização.</span><span class="sxs-lookup"><span data-stu-id="01baa-126">As you upgrade the vault type from the classic deployment model to the Resource Manager deployment model, update the existing automation or tooling to ensure that it continues to work after the upgrade.</span></span>

### <a name="prepare-your-environment-for-the-upgrade"></a><span data-ttu-id="01baa-127">Preparar o ambiente para a atualização</span><span class="sxs-lookup"><span data-stu-id="01baa-127">Prepare your environment for the upgrade</span></span>

* [<span data-ttu-id="01baa-128">Instale o PowerShell ou atualize-o para a versão 5 ou posterior</span><span class="sxs-lookup"><span data-stu-id="01baa-128">Install PowerShell or upgrade it to version 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="01baa-129">Instale a versão mais recente do MSI do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="01baa-129">Install the latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="01baa-130">Baixe o script de atualização do cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="01baa-130">Download the Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="01baa-131">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="01baa-131">Prerequisites</span></span>
<span data-ttu-id="01baa-132">Para atualizar de cofres do Site Recovery para cofres do Serviço de Recuperação com base no Azure Resource Manager, você deve atender aos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="01baa-132">To upgrade from Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults, you must meet the following requirements:</span></span>

* <span data-ttu-id="01baa-133">Versão mínima do agente: a versão do Provedor do Azure Site Recovery instalado em seu servidor deve ser a 5.1.1700.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="01baa-133">Minimum agent version: The version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="01baa-134">Configuração com suporte: não é possível configurar o cofre com a rede SAN (rede de área de armazenamento ) ou Grupos de Disponibilidade AlwaysOn do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="01baa-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="01baa-135">Há suporte para todas as outras configurações.</span><span class="sxs-lookup"><span data-stu-id="01baa-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="01baa-136">Após a atualização, você pode gerenciar o mapeamento de armazenamento somente por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01baa-136">After the upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="01baa-137">Cenário de implantação com suporte: seu cofre não deve ser do modelo de implantação herdado *VMware para Azure*.</span><span class="sxs-lookup"><span data-stu-id="01baa-137">Supported deployment scenario: Your vault shouldn’t be the *VMware to Azure* legacy deployment model.</span></span> <span data-ttu-id="01baa-138">Antes de prosseguir, primeiro mude para o modelo de implantação avançado.</span><span class="sxs-lookup"><span data-stu-id="01baa-138">Before you proceed, first move to the enhanced deployment model.</span></span>

* <span data-ttu-id="01baa-139">Nenhum trabalho ativo iniciado pelo usuário que envolva operações do plano de gerenciamento: como o acesso ao plano de gerenciamento é restrito durante a atualização, conclua todas as ações do plano de gerenciamento antes de disparar a atualização.</span><span class="sxs-lookup"><span data-stu-id="01baa-139">No active user-initiated jobs that involve management plane operations: Because access to the management plane is restricted during upgrade, complete all your management plane actions before you trigger the upgrade.</span></span> <span data-ttu-id="01baa-140">Esse processo não inclui a replicação em andamento.</span><span class="sxs-lookup"><span data-stu-id="01baa-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="01baa-141">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="01baa-141">Frequently asked questions</span></span>

<span data-ttu-id="01baa-142">**Essa atualização afeta minha replicação em andamento?**</span><span class="sxs-lookup"><span data-stu-id="01baa-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="01baa-143">Não.</span><span class="sxs-lookup"><span data-stu-id="01baa-143">No.</span></span> <span data-ttu-id="01baa-144">A replicação em andamento continuará sem interrupção durante e após a atualização.</span><span class="sxs-lookup"><span data-stu-id="01baa-144">Your ongoing replication continues uninterrupted during and after the upgrade.</span></span>

<span data-ttu-id="01baa-145">**O que acontece com as configurações de rede, como configurações de IP e VPN site a site?**</span><span class="sxs-lookup"><span data-stu-id="01baa-145">**What happens to network settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="01baa-146">A atualização não afeta as configurações de rede.</span><span class="sxs-lookup"><span data-stu-id="01baa-146">The upgrade doesn't affect the network settings.</span></span> <span data-ttu-id="01baa-147">Todas as conexões Azure para local permanecem intactas.</span><span class="sxs-lookup"><span data-stu-id="01baa-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="01baa-148">**O que acontece com meus cofres se eu não planejo atualizar em breve?**</span><span class="sxs-lookup"><span data-stu-id="01baa-148">**What happens to my vaults if I don’t plan to upgrade in the near future?**</span></span>

<span data-ttu-id="01baa-149">O suporte para o cofre do Site Recovery no Portal do Azure antigo será preterido a partir de setembro de 2017.</span><span class="sxs-lookup"><span data-stu-id="01baa-149">Support for Site Recovery vault in the old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="01baa-150">É altamente recomendável que você use o recurso de atualização para mudar para o novo portal.</span><span class="sxs-lookup"><span data-stu-id="01baa-150">We strongly recommend that you use the upgrade feature to move to the new portal.</span></span>

<span data-ttu-id="01baa-151">**O que este plano de migração significa para minhas ferramentas existentes?**</span><span class="sxs-lookup"><span data-stu-id="01baa-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="01baa-152">Atualizar suas ferramentas para o modelo de implantação do Resource Manager é uma das alterações mais importantes que você deve considerar em seus planos de atualização.</span><span class="sxs-lookup"><span data-stu-id="01baa-152">Updating your tooling to the Resource Manager deployment model is one of the most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="01baa-153">Os cofres dos Serviços de Recuperação são baseados no modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01baa-153">The Recovery Services vaults are based on the Resource Manager deployment model.</span></span> 

<span data-ttu-id="01baa-154">**Qual será o tempo de inatividade do plano de gerenciamento?**</span><span class="sxs-lookup"><span data-stu-id="01baa-154">**How long does the management-plane downtime last?**</span></span>

<span data-ttu-id="01baa-155">A atualização normalmente leva cerca de 15 a 30 minutos e poderá levar, no máximo, uma hora.</span><span class="sxs-lookup"><span data-stu-id="01baa-155">The upgrade ordinarily takes about 15 to 30 minutes, and it could take up to a maximum of one hour.</span></span>

<span data-ttu-id="01baa-156">**Posso reverter após a atualização?**</span><span class="sxs-lookup"><span data-stu-id="01baa-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="01baa-157">Não.</span><span class="sxs-lookup"><span data-stu-id="01baa-157">No.</span></span> <span data-ttu-id="01baa-158">Não há suporte para reversão após os recursos terem sido atualizados com êxito.</span><span class="sxs-lookup"><span data-stu-id="01baa-158">Rollback is not supported after the resources have been successfully upgraded.</span></span>

<span data-ttu-id="01baa-159">**Posso validar minha assinatura ou meus recursos para ver se eles podem ser atualizados?**</span><span class="sxs-lookup"><span data-stu-id="01baa-159">**Can I validate my subscription or resources to see whether they can be upgraded?**</span></span>

<span data-ttu-id="01baa-160">Sim.</span><span class="sxs-lookup"><span data-stu-id="01baa-160">Yes.</span></span> <span data-ttu-id="01baa-161">Na opção de atualização com suporte da plataforma, a primeira etapa é validar se os recursos podem ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="01baa-161">In the platform-supported upgrade option, the first step in the upgrade is to validate that the resources are capable of an upgrade.</span></span> <span data-ttu-id="01baa-162">Se a validação falhar, você receberá mensagens de erro ou avisos apropriados.</span><span class="sxs-lookup"><span data-stu-id="01baa-162">If the validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="01baa-163">**Como faço para relatar um problema com a atualização?**</span><span class="sxs-lookup"><span data-stu-id="01baa-163">**How do I report an issue with the upgrade?**</span></span>

<span data-ttu-id="01baa-164">Se você enfrentar falhas durante a atualização, observe a ID da operação que estará listada no erro.</span><span class="sxs-lookup"><span data-stu-id="01baa-164">If you experience any failures during the upgrade, note the operation ID that's listed in the error.</span></span> <span data-ttu-id="01baa-165">O Suporte da Microsoft trabalhará proativamente para resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="01baa-165">Microsoft Support will proactively work on resolving the issue.</span></span> <span data-ttu-id="01baa-166">Também é possível entrar em contato com a equipe do Suporte, informando sua ID de assinatura, o nome do cofre e a ID da operação.</span><span class="sxs-lookup"><span data-stu-id="01baa-166">You can also contact the Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="01baa-167">O suporte trabalhará para resolver o problema o mais rápido possível.</span><span class="sxs-lookup"><span data-stu-id="01baa-167">Support will work to resolve the issue as quickly as possible.</span></span> <span data-ttu-id="01baa-168">Não repita a operação, a menos que seja explicitamente instruído a fazer isso pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01baa-168">Do not retry the operation unless you are explicitly instructed to do so by Microsoft.</span></span>

## <a name="run-the-script"></a><span data-ttu-id="01baa-169">Execute o script</span><span class="sxs-lookup"><span data-stu-id="01baa-169">Run the script</span></span>

<span data-ttu-id="01baa-170">No PowerShell, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="01baa-170">In PowerShell, run the following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="01baa-171">SubscriptionID: a ID da assinatura associada ao cofre que você está atualizando.</span><span class="sxs-lookup"><span data-stu-id="01baa-171">SubscriptionID: The subscription ID that's associated with the vault that you're upgrading.</span></span>

* <span data-ttu-id="01baa-172">VaultName: o nome do cofre que você está atualizando.</span><span class="sxs-lookup"><span data-stu-id="01baa-172">VaultName: The name of the vault that you're upgrading.</span></span>

* <span data-ttu-id="01baa-173">Localização: a localização do cofre que você está atualizando.</span><span class="sxs-lookup"><span data-stu-id="01baa-173">Location: The location of the vault that you're upgrading.</span></span>

* <span data-ttu-id="01baa-174">ResourceType: HyperVRecoveryManagerVault para cofres do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="01baa-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="01baa-175">TargetResourceGroupName: o grupo de recursos no qual você deseja que o cofre atualizado seja colocado.</span><span class="sxs-lookup"><span data-stu-id="01baa-175">TargetResourceGroupName: The resource group into which you want the upgraded vault to be placed.</span></span> <span data-ttu-id="01baa-176">O TargetResourceGroupName pode ser de um grupo de recursos existente no Azure Resource Manager ou um novo.</span><span class="sxs-lookup"><span data-stu-id="01baa-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="01baa-177">Se o TargetResourceGroupName fornecido não existir, ele será criado como parte da atualização no mesmo local que o cofre.</span><span class="sxs-lookup"><span data-stu-id="01baa-177">If the TargetResourceGroupName that's supplied does not exist, it is created as part of the upgrade in the same location as the vault.</span></span> <span data-ttu-id="01baa-178">Para obter mais informações, consulte a seção "Grupos de recursos" da [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="01baa-178">For more information, see the "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="01baa-179">A nomenclatura do grupo de recursos está sujeita a determinadas restrições.</span><span class="sxs-lookup"><span data-stu-id="01baa-179">Resource group naming is subject to certain constraints.</span></span> <span data-ttu-id="01baa-180">Para evitar a falha na atualização do cofre, certifique-se de observar a convenção de nomenclatura com cuidado.</span><span class="sxs-lookup"><span data-stu-id="01baa-180">To prevent vault upgrade failure, be sure to observe the naming convention carefully.</span></span>
    >
    ><span data-ttu-id="01baa-181">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="01baa-181">For example:</span></span>
    >
    ><span data-ttu-id="01baa-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="01baa-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="01baa-183">Como alternativa, você pode executar o seguinte script.</span><span class="sxs-lookup"><span data-stu-id="01baa-183">Alternatively, you can run the following script.</span></span> <span data-ttu-id="01baa-184">Insira os valores dos parâmetros necessários.</span><span class="sxs-lookup"><span data-stu-id="01baa-184">Enter the values for the required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for the following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="01baa-185">O script do PowerShell solicita que você insira suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="01baa-185">The PowerShell script prompts you to enter your credentials.</span></span> <span data-ttu-id="01baa-186">Digite-as duas vezes, uma vez para a conta do modelo de implantação clássico e outra para a conta do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01baa-186">Enter them twice, once for the classic deployment model account and once for the Azure Resource Manager account.</span></span>

2. <span data-ttu-id="01baa-187">Depois de inserir suas credenciais, o script executará uma verificação para determinar se a sua configuração de infraestrutura atende aos requisitos mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="01baa-187">After you've entered your credentials, the script runs a check to determine whether your infrastructure setup meets the previously mentioned requirements.</span></span>

3. <span data-ttu-id="01baa-188">Depois que os pré-requisitos foram verificados e confirmados, você será solicitado a continuar com a atualização do cofre.</span><span class="sxs-lookup"><span data-stu-id="01baa-188">After the prerequisites have been checked and confirmed, you are prompted to proceed with the vault upgrade.</span></span> <span data-ttu-id="01baa-189">O processo de atualização começará a atualizar seu cofre.</span><span class="sxs-lookup"><span data-stu-id="01baa-189">The upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="01baa-190">Toda a atualização pode levar de 15 a 30 minutos para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="01baa-190">The entire upgrade can take 15 to 30 minutes to complete.</span></span>

4. <span data-ttu-id="01baa-191">Depois que a atualização for concluída com êxito, você poderá acessar o cofre atualizado no novo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01baa-191">After the upgrade has been completed successfully, you can access the upgraded vault in the new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="01baa-192">Gerenciamento do cofre após a atualização</span><span class="sxs-lookup"><span data-stu-id="01baa-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-the-recovery-services-vault"></a><span data-ttu-id="01baa-193">Replicar usando o Azure Site Recovery no cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="01baa-193">Replicate by using Azure Site Recovery in the Recovery Services vault</span></span>

* <span data-ttu-id="01baa-194">Agora você pode proteger suas VMs do Azure de uma região para outra.</span><span class="sxs-lookup"><span data-stu-id="01baa-194">You can now protect your Azure VMs from one region to another.</span></span> <span data-ttu-id="01baa-195">Para obter mais informações, consulte [Replicar VMs do Azure entre regiões com o Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="01baa-196">Para obter mais informações sobre a replicação de VMs do VMware para o Azure, consulte [Replicar VMs do VMware no Azure com o Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-196">For more information about replicating VMware VMs to Azure, see [Replicate VMware VMs to Azure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="01baa-197">Para obter mais informações sobre a replicação de VMs do Hyper-V (sem VMM) no Azure, consulte [Replicar máquinas virtuais do Hyper-V (sem o VMM) no Azure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-197">For more information about replicating Hyper-V VMs (without VMM) to Azure, see [Replicate Hyper-V virtual machines (without VMM) to Azure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="01baa-198">Para obter mais informações sobre a replicação de VMs do Hyper-V (com o VMM) no Azure, consulte [Replicar máquinas virtuais Hyper-V em nuvens VMM no Azure usando o Site Recovery no Portal do Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-198">For more information about replicating Hyper-V VMs (with VMM) to Azure, see [Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="01baa-199">Para obter mais informações sobre a replicação de VMs do Hyper-V (com o VMM) em um site secundário, consulte [Replicar máquinas virtuais do Hyper-V em nuvens VMM para um site de VMM secundário usando o Portal do Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-199">For more information about replicating Hyper-VMs (with VMM) to a secondary site, see [Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using the Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="01baa-200">Para obter mais informações sobre a replicação de VMs do VMware para um site secundário, consulte [Replicar máquinas virtuais locais ou servidores físicos do VMware em um site secundário no Portal Clássico do Azure](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-200">For more information about replicating VMware VMs to a secondary site, see [Replicate on-premises VMware virtual machines or physical servers to a secondary site in the classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="01baa-201">Exibir seus itens replicados</span><span class="sxs-lookup"><span data-stu-id="01baa-201">View your replicated items</span></span>

<span data-ttu-id="01baa-202">A imagem abaixo mostra a página de painel do cofre dos Serviços de Recuperação que exibe as principais entidades do cofre.</span><span class="sxs-lookup"><span data-stu-id="01baa-202">The following image shows the Recovery Services vault dashboard page that displays key entities for the vault.</span></span> <span data-ttu-id="01baa-203">Para exibir uma lista de entidades protegidas no cofre, selecione **Site Recovery** > **Itens replicados**.</span><span class="sxs-lookup"><span data-stu-id="01baa-203">To view a list of protected entities in the vault, select **Site Recovery** > **Replicated items**.</span></span>


![Itens replicados](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="01baa-205">A imagem a seguir mostra o fluxo de trabalho para exibir seus itens replicados e o comando **Failover** para iniciar um failover.</span><span class="sxs-lookup"><span data-stu-id="01baa-205">The following image shows the workflow for viewing your replicated items and the **Failover** command for initiating a failover.</span></span>

![Itens replicados](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="01baa-207">Exibir suas configurações de replicação</span><span class="sxs-lookup"><span data-stu-id="01baa-207">View your replication settings</span></span>

<span data-ttu-id="01baa-208">No cofre do Site Recovery, cada grupo de proteção é definido com frequência de cópia, retenção do ponto de recuperação, frequência dos instantâneos consistentes com aplicativo e outras configurações de replicação.</span><span class="sxs-lookup"><span data-stu-id="01baa-208">In the Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="01baa-209">No cofre dos Serviços de Recuperação, essas configurações são definidas como uma política de replicação.</span><span class="sxs-lookup"><span data-stu-id="01baa-209">In the Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="01baa-210">O nome da política é o nome do grupo de proteção ou da *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="01baa-210">The name of the policy is the name of the protection group or the *primarycloud_Policy*.</span></span>

<span data-ttu-id="01baa-211">Para obter mais informações sobre a política de replicação, consulte [Gerenciar a política de replicação para VMware para Azure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="01baa-211">For more information about replication policy, see [Manage replication policy for VMware to Azure](site-recovery-setup-replication-settings-vmware.md).</span></span>
