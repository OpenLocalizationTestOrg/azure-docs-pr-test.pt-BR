---
title: "Cofre de serviços de recuperação do Azure tooan aaaUpgrade um cofre de recuperação de Site"
description: "Saiba como tooupgrade um cofre do Azure Site Recovery serviços de recuperação de tooa cofre"
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
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="5bab4-103">Atualizar um cofre de serviços de recuperação baseados no Gerenciador de recursos do Azure Site Recovery cofre tooan</span><span class="sxs-lookup"><span data-stu-id="5bab4-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="5bab4-104">Este artigo descreve como tooupgrade do Azure Site Recovery cofres cofres de serviços de recuperação com base em Gerenciador de recursos tooAzure sem nenhum impacto sobre replicação em andamento.</span><span class="sxs-lookup"><span data-stu-id="5bab4-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="5bab4-105">Para saber mais sobre os recursos e benefícios do Azure Resource Manager, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="5bab4-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="5bab4-106">Introduction</span></span>
<span data-ttu-id="5bab4-107">Um cofre de serviços de recuperação é um recurso do Gerenciador de recursos do Azure para o gerenciamento de backup e recuperação de desastres nativamente na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="5bab4-108">É um cofre unificado que você pode usar no novo portal do Azure Olá e substitui o backup clássico hello e cofres de recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="5bab4-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="5bab4-109">Os cofres dos Serviços de Recuperação oferecem uma matriz de recursos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="5bab4-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="5bab4-110">Suporte do Azure Resource Manager: você pode proteger e realizar o failover de suas máquinas virtuais e computadores físicos em uma pilha do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5bab4-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="5bab4-111">Excluir disco: se você tiver arquivos temporários ou alta rotatividade de dados que você não deseja toouse toda a largura de banda para, você pode excluir volumes de replicação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="5bab4-112">Esse recurso foi habilitado no momento em *VMware tooAzure* e *tooAzure Hyper-V* e são estendidos tooother cenários bem.</span><span class="sxs-lookup"><span data-stu-id="5bab4-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="5bab4-113">Suporte para premium e o armazenamento redundante localmente: agora você pode proteger servidores no armazenamento premium contas que permitem que os clientes tooprotect aplicativos com maior operações de entradam/saídam por segundo (IOPS).</span><span class="sxs-lookup"><span data-stu-id="5bab4-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="5bab4-114">Esse recurso está habilitado no momento em *tooAzure VMware*.</span><span class="sxs-lookup"><span data-stu-id="5bab4-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="5bab4-115">Simplificada de experiência do guia de Introdução: experiência de Introdução Olá Avançado foi projetada fácil da configuração de recuperação de desastres de toomake.</span><span class="sxs-lookup"><span data-stu-id="5bab4-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="5bab4-116">Backup e recuperação de Site de gerenciamento de Olá mesmo cofre: agora você pode proteger servidores para recuperação de desastres ou realizar o backup do hello mesmo cofre, que pode reduzir o gerenciamento de sobrecarga significativamente.</span><span class="sxs-lookup"><span data-stu-id="5bab4-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="5bab4-117">Para obter mais informações sobre a experiência de saudação atualizada e recursos, consulte Olá [blog de armazenamento, Backup e recuperação](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="5bab4-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="5bab4-118">Principais recursos</span><span class="sxs-lookup"><span data-stu-id="5bab4-118">Salient features</span></span>

* <span data-ttu-id="5bab4-119">Sem impacto na replicação em andamento: as replicações em andamento continuam sem qualquer interrupção durante e após a atualização.</span><span class="sxs-lookup"><span data-stu-id="5bab4-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="5bab4-120">Sem custo adicional: obtenha um conjunto completo de recursos atualizados sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="5bab4-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="5bab4-121">Sem perda de dados: como esse processo é uma atualização e não uma migração, pontos de recuperação de replicação existentes e configurações permanecem intactas durante e após a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="5bab4-122">O que acontece durante a atualização de cofre Olá?</span><span class="sxs-lookup"><span data-stu-id="5bab4-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="5bab4-123">Durante a atualização de saudação, você não pode executar operações como registrar um novo servidor ou habilitar a replicação para uma máquina virtual (VM).</span><span class="sxs-lookup"><span data-stu-id="5bab4-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="5bab4-124">As operações que envolvem ler dados de ou gravar dados toohello cofre, como replicação contínua de itens protegidos toohello cofre, continuam sem interrupções.</span><span class="sxs-lookup"><span data-stu-id="5bab4-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="5bab4-125">Alterações tooautomation e ferramentas depois da atualização de saudação</span><span class="sxs-lookup"><span data-stu-id="5bab4-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="5bab4-126">Conforme você atualiza o tipo de Cofre de saudação do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos, atualize automação existentes hello ou ferramentas tooensure que ele continue toowork após a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="5bab4-127">Preparar o ambiente para a atualização de saudação</span><span class="sxs-lookup"><span data-stu-id="5bab4-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="5bab4-128">Instale o PowerShell ou atualizá-lo tooversion 5 ou posterior</span><span class="sxs-lookup"><span data-stu-id="5bab4-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="5bab4-129">Instale a versão mais recente saudação do MSI do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab4-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="5bab4-130">Baixar o script de atualização do Cofre de serviços de recuperação de Olá</span><span class="sxs-lookup"><span data-stu-id="5bab4-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="5bab4-131">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5bab4-131">Prerequisites</span></span>
<span data-ttu-id="5bab4-132">tooupgrade do Site Recovery cofres tooAzure cofres de serviços de recuperação com base em Gerenciador de recursos, você deve cumprir Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5bab4-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="5bab4-133">Versão mínima do agente: versão de saudação do provedor Azure Site Recovery instalado em seu servidor deve ser 5.1.1700.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5bab4-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="5bab4-134">Configuração com suporte: não é possível configurar o cofre com a rede SAN (rede de área de armazenamento ) ou Grupos de Disponibilidade AlwaysOn do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5bab4-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="5bab4-135">Há suporte para todas as outras configurações.</span><span class="sxs-lookup"><span data-stu-id="5bab4-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5bab4-136">Após a atualização de saudação, você pode gerenciar o mapeamento de armazenamento somente por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5bab4-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="5bab4-137">Cenário de implantação com suporte: seu cofre não deve ser Olá *tooAzure VMware* modelo de implantação herdado.</span><span class="sxs-lookup"><span data-stu-id="5bab4-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="5bab4-138">Antes de prosseguir, primeiro mova o modelo de implantação avançada do toohello.</span><span class="sxs-lookup"><span data-stu-id="5bab4-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="5bab4-139">Nenhum trabalho ativo iniciada pelo usuário que envolvem o gerenciamento de operações de plano: porque o plano de gerenciamento de toohello de acesso é restrito durante a atualização, conclua todas as ações do plano de gerenciamento antes de disparar atualização hello.</span><span class="sxs-lookup"><span data-stu-id="5bab4-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="5bab4-140">Esse processo não inclui a replicação em andamento.</span><span class="sxs-lookup"><span data-stu-id="5bab4-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="5bab4-141">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="5bab4-141">Frequently asked questions</span></span>

<span data-ttu-id="5bab4-142">**Essa atualização afeta minha replicação em andamento?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="5bab4-143">Não.</span><span class="sxs-lookup"><span data-stu-id="5bab4-143">No.</span></span> <span data-ttu-id="5bab4-144">A replicação em andamento continuará sem interrupção durante e após a atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="5bab4-145">**O que acontece toonetwork configurações, como configurações de IP e de VPN site a site?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="5bab4-146">atualização de saudação não afeta as configurações de rede hello.</span><span class="sxs-lookup"><span data-stu-id="5bab4-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="5bab4-147">Todas as conexões Azure para local permanecem intactas.</span><span class="sxs-lookup"><span data-stu-id="5bab4-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="5bab4-148">**O que acontece cofres toomy se eu não planejar tooupgrade em Olá futuro próximo?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="5bab4-149">Suporte para o Cofre de recuperação de Site no portal do Azure antigo Olá será preterido começando em setembro de 2017.</span><span class="sxs-lookup"><span data-stu-id="5bab4-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="5bab4-150">É altamente recomendável que você use Olá recurso de atualização toomove toohello novo portal.</span><span class="sxs-lookup"><span data-stu-id="5bab4-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="5bab4-151">**O que este plano de migração significa para minhas ferramentas existentes?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="5bab4-152">A atualização de seu modelo de implantação do Gerenciador de recursos de toohello ferramentas é uma saudação alterações mais importantes que você deve considerar nos planos de atualização.</span><span class="sxs-lookup"><span data-stu-id="5bab4-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="5bab4-153">Olá cofres de serviços de recuperação são baseados no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="5bab4-154">**Quanto tempo Olá plano de gerenciamento de tempo de inatividade última?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="5bab4-155">atualização de saudação normalmente demora cerca de 15 minutos de too30 e pode levar até tooa máximo de uma hora.</span><span class="sxs-lookup"><span data-stu-id="5bab4-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="5bab4-156">**Posso reverter após a atualização?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="5bab4-157">Não.</span><span class="sxs-lookup"><span data-stu-id="5bab4-157">No.</span></span> <span data-ttu-id="5bab4-158">A reversão não tem suporte depois recursos Olá foi atualizados com êxito.</span><span class="sxs-lookup"><span data-stu-id="5bab4-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="5bab4-159">**Eu Validar minha assinatura ou toosee recursos se eles podem ser atualizados?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="5bab4-160">Sim.</span><span class="sxs-lookup"><span data-stu-id="5bab4-160">Yes.</span></span> <span data-ttu-id="5bab4-161">Opção atualização com suporte de plataforma hello, Olá primeira etapa na atualização de saudação é toovalidate que recursos Olá são capazes de fazer uma atualização.</span><span class="sxs-lookup"><span data-stu-id="5bab4-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="5bab4-162">Se a validação de saudação falhar, você receberá mensagens de erro apropriadas ou avisos.</span><span class="sxs-lookup"><span data-stu-id="5bab4-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="5bab4-163">**Como faço para relatar um problema com a atualização de Olá?**</span><span class="sxs-lookup"><span data-stu-id="5bab4-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="5bab4-164">Se ocorrerem falhas durante a atualização Olá, observe o ID da operação Olá listado no erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="5bab4-165">Microsoft Support proativamente funcionará para resolver o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="5bab4-166">Você também pode contatar a equipe de suporte de saudação com sua ID de assinatura, nome do cofre e ID da operação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="5bab4-167">Suporte funcionará problema de saudação tooresolve assim que possível.</span><span class="sxs-lookup"><span data-stu-id="5bab4-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="5bab4-168">Não tente novamente a operação Olá a menos que seja explicitamente instruções toodo caso pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5bab4-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="5bab4-169">Execute o script hello</span><span class="sxs-lookup"><span data-stu-id="5bab4-169">Run hello script</span></span>

<span data-ttu-id="5bab4-170">No PowerShell, execute o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="5bab4-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="5bab4-171">SubscriptionID: Olá ID de assinatura que está associado ao Cofre Olá que você está atualizando.</span><span class="sxs-lookup"><span data-stu-id="5bab4-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="5bab4-172">VaultName: o nome de saudação do cofre Olá que você estiver atualizando.</span><span class="sxs-lookup"><span data-stu-id="5bab4-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="5bab4-173">: Olá local do cofre Olá que você está atualizando.</span><span class="sxs-lookup"><span data-stu-id="5bab4-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="5bab4-174">ResourceType: HyperVRecoveryManagerVault para cofres do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5bab4-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="5bab4-175">TargetResourceGroupName: grupo de recursos de saudação no qual você deseja Olá atualizado toobe cofre colocado.</span><span class="sxs-lookup"><span data-stu-id="5bab4-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="5bab4-176">O TargetResourceGroupName pode ser de um grupo de recursos existente no Azure Resource Manager ou um novo.</span><span class="sxs-lookup"><span data-stu-id="5bab4-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="5bab4-177">Se não existir Olá TargetResourceGroupName for fornecido, ele é criado como parte da atualização de saudação no hello mesmo local Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="5bab4-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="5bab4-178">Para obter mais informações, consulte a seção "Grupos de recursos" hello [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="5bab4-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="5bab4-179">Nomes de grupo de recursos é restrições de toocertain de assunto.</span><span class="sxs-lookup"><span data-stu-id="5bab4-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="5bab4-180">cofre tooprevent atualização falha, ser se Olá tooobserve convenção de nomenclatura com cuidado.</span><span class="sxs-lookup"><span data-stu-id="5bab4-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="5bab4-181">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5bab4-181">For example:</span></span>
    >
    ><span data-ttu-id="5bab4-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="5bab4-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="5bab4-183">Como alternativa, você pode executar Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="5bab4-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="5bab4-184">Insira valores hello de parâmetros de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="5bab4-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="5bab4-185">Olá script do PowerShell solicitará que você tooenter suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="5bab4-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="5bab4-186">Digite-os em duas vezes, uma vez para a conta de modelo de implantação clássico hello e uma vez para Olá conta do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5bab4-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="5bab4-187">Depois de inserir suas credenciais, script hello executa toodetermine uma verificação se a saudação de atende infraestrutura instalação mencionado anteriormente requisitos.</span><span class="sxs-lookup"><span data-stu-id="5bab4-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="5bab4-188">Depois que os pré-requisitos de saudação foram verificados e confirmados, você está tooproceed solicitada com a atualização do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="5bab4-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="5bab4-189">o processo de atualização Olá inicia a atualização de seu cofre.</span><span class="sxs-lookup"><span data-stu-id="5bab4-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="5bab4-190">atualização inteira Olá pode levar 15 toocomplete minutos de too30.</span><span class="sxs-lookup"><span data-stu-id="5bab4-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="5bab4-191">Depois Olá atualização foi concluída com êxito, você pode acessar o Cofre de saudação atualizado no novo portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="5bab4-192">Gerenciamento do cofre após a atualização</span><span class="sxs-lookup"><span data-stu-id="5bab4-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="5bab4-193">Replicar usando o Azure Site Recovery no cofre de serviços de recuperação de saudação</span><span class="sxs-lookup"><span data-stu-id="5bab4-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="5bab4-194">Agora você pode proteger suas VMs do Azure de uma região tooanother.</span><span class="sxs-lookup"><span data-stu-id="5bab4-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="5bab4-195">Para obter mais informações, consulte [Replicar VMs do Azure entre regiões com o Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="5bab4-196">Para obter mais informações sobre a replicação de máquinas virtuais do VMware tooAzure, consulte [tooAzure replicar máquinas virtuais do VMware com a recuperação de Site](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="5bab4-197">Para obter mais informações sobre a replicação de máquinas virtuais do Hyper-V (sem VMM) tooAzure, consulte [tooAzure de máquinas virtuais (sem VMM) do Hyper-V replicar](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="5bab4-198">Para obter mais informações sobre a replicação de máquinas virtuais do Hyper-V (com o VMM) tooAzure, consulte [Olá de máquinas virtuais de Hyper-V replicar em tooAzure de nuvens do VMM com a recuperação de Site no portal do Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="5bab4-199">Para obter mais informações sobre a replicação de site secundário do tooa Hyper-VMs (com o VMM), consulte [Olá de máquinas virtuais de replicar Hyper-V no VMM nuvens tooa secundário do VMM site usando o portal do Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="5bab4-200">Para obter mais informações sobre a replicação de site secundário do VMs VMware tooa, consulte [replicar em máquinas virtuais VMware ou local site secundário do tooa servidores físicos no portal do Azure clássico de saudação](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="5bab4-201">Exibir seus itens replicados</span><span class="sxs-lookup"><span data-stu-id="5bab4-201">View your replicated items</span></span>

<span data-ttu-id="5bab4-202">Olá imagem a seguir mostra Olá dos serviços de recuperação cofre página do painel que exibe as principais entidades para o cofre hello.</span><span class="sxs-lookup"><span data-stu-id="5bab4-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="5bab4-203">Selecione tooview uma lista de entidades protegidas no cofre hello, **recuperação de Site** > **replicadas itens**.</span><span class="sxs-lookup"><span data-stu-id="5bab4-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Itens replicados](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="5bab4-205">Olá, imagem a seguir mostra Olá de fluxo de trabalho para exibir seus itens replicados e hello **Failover** comando para iniciar um failover.</span><span class="sxs-lookup"><span data-stu-id="5bab4-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Itens replicados](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="5bab4-207">Exibir suas configurações de replicação</span><span class="sxs-lookup"><span data-stu-id="5bab4-207">View your replication settings</span></span>

<span data-ttu-id="5bab4-208">No cofre de recuperação de Site hello, cada grupo de proteção é configurado com a frequência de cópia, retenção de ponto de recuperação, a frequência dos instantâneos consistentes por aplicativo e outras configurações de replicação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="5bab4-209">No cofre de serviços de recuperação hello, essas configurações são definidas como uma política de replicação.</span><span class="sxs-lookup"><span data-stu-id="5bab4-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="5bab4-210">nome de saudação da política de saudação é nome de saudação do grupo de proteção Olá Olá *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="5bab4-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="5bab4-211">Para obter mais informações sobre a política de replicação, consulte [Gerenciar política de replicação para VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="5bab4-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
