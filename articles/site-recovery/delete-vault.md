---
title: "aaaDelete um cofre de recuperação de Site"
description: "Saiba como toodelete um cofre do Azure Site Recovery, com base no cenário de recuperação de Site hello."
service: site-recovery
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
ms.date: 07/04/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: 36db202d8b790bb5d31d1348fb72f51acb5d559c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="de79a-103">Excluir um cofre do Site Recovery</span><span class="sxs-lookup"><span data-stu-id="de79a-103">Delete a Site Recovery vault</span></span>
<span data-ttu-id="de79a-104">Dependências podem impedir a exclusão de um cofre do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="de79a-104">Dependencies can prevent you from deleting an Azure Site Recovery vault.</span></span> <span data-ttu-id="de79a-105">Olá ações que você precisa tootake variam com base no cenário de recuperação de Site Olá: tooAzure VMware, tooAzure Hyper-V (com e sem o System Center Virtual Machine Manager) e o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="de79a-105">hello actions you need tootake vary based on hello Site Recovery scenario: VMware tooAzure, Hyper-V (with and without System Center Virtual Machine Manager) tooAzure, and Azure Backup.</span></span> <span data-ttu-id="de79a-106">toodelete um cofre usado no Backup do Azure, consulte [excluir um cofre de Backup no Azure](../backup/backup-azure-delete-vault.md).</span><span class="sxs-lookup"><span data-stu-id="de79a-106">toodelete a vault used in Azure Backup, see [Delete a Backup vault in Azure](../backup/backup-azure-delete-vault.md).</span></span>

>[!Important]
><span data-ttu-id="de79a-107">Se você estiver testando o produto hello e não estiver preocupado com a perda de dados, use Olá forçar exclusão método toorapidly remover cofre hello e todas as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="de79a-107">If you're testing hello product and aren't concerned about data loss, use hello force delete method toorapidly remove hello vault and all its dependencies.</span></span>

> <span data-ttu-id="de79a-108">saudação de comando do PowerShell exclui todo o conteúdo de saudação do cofre hello e não é reversível.</span><span class="sxs-lookup"><span data-stu-id="de79a-108">hello PowerShell command deletes all hello contents of hello vault and is not reversible.</span></span>

## <a name="use-powershell-tooforce-delete-hello-vault"></a><span data-ttu-id="de79a-109">Use PowerShell tooforce excluir cofre Olá</span><span class="sxs-lookup"><span data-stu-id="de79a-109">Use PowerShell tooforce delete hello vault</span></span> 

<span data-ttu-id="de79a-110">itens protegidos de saudação toodelete Cofre de recuperação de Site mesmo se houver, usar esses comandos:</span><span class="sxs-lookup"><span data-stu-id="de79a-110">toodelete hello Site Recovery vault even if there are protected items, use these commands:</span></span>

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a><span data-ttu-id="de79a-111">Excluir um cofre do Site Recovery</span><span class="sxs-lookup"><span data-stu-id="de79a-111">Delete a Site Recovery vault</span></span> 
<span data-ttu-id="de79a-112">Cofre de saudação toodelete, Olá siga as etapas para seu cenário recomendada.</span><span class="sxs-lookup"><span data-stu-id="de79a-112">toodelete hello vault, follow hello recommended steps for your scenario.</span></span>

### <a name="vmware-vms-tooazure"></a><span data-ttu-id="de79a-113">Máquinas virtuais do VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="de79a-113">VMware VMs tooAzure</span></span>

1. <span data-ttu-id="de79a-114">Excluir todos os protegidos VMs, seguindo as etapas de saudação em [desabilite a proteção de um VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="de79a-114">Delete all protected VMs by following hello steps in [Disable protection for a VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="de79a-115">Excluir todas as políticas de replicação, seguindo as etapas de saudação em [excluir uma política de replicação](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="de79a-115">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="de79a-116">Excluir referências toovCenter por Olá seguir as etapas em [excluir um vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="de79a-116">Delete references toovCenter by following hello steps in [Delete a vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).</span></span>

4. <span data-ttu-id="de79a-117">Excluir o servidor de configuração de saudação, seguindo as etapas de saudação em [encerrar um servidor de configuração](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="de79a-117">Delete hello configuration server by following hello steps in [Decommission a configuration server](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).</span></span>

5. <span data-ttu-id="de79a-118">Exclua cofre hello.</span><span class="sxs-lookup"><span data-stu-id="de79a-118">Delete hello vault.</span></span>


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a><span data-ttu-id="de79a-119">TooAzure de VMs Hyper-V (com o Virtual Machine Manager)</span><span class="sxs-lookup"><span data-stu-id="de79a-119">Hyper-V VMs (with Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="de79a-120">Excluir todos os protegidos VMs, seguindo as etapas de saudação em [desabilite a proteção para um servidor físico ou a VM do VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="de79a-120">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="de79a-121">Excluir todas as políticas de replicação, seguindo as etapas de saudação em [excluir uma política de replicação](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="de79a-121">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3.  <span data-ttu-id="de79a-122">Excluir referências tooVirtual Machine Manager servidores seguindo as etapas de saudação em [cancelar o registro de um servidor VMM conectado](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span><span class="sxs-lookup"><span data-stu-id="de79a-122">Delete references tooVirtual Machine Manager servers by following hello steps in [Unregister a connected VMM server](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).</span></span>

4.  <span data-ttu-id="de79a-123">Exclua cofre hello.</span><span class="sxs-lookup"><span data-stu-id="de79a-123">Delete hello vault.</span></span>

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a><span data-ttu-id="de79a-124">TooAzure de VMs Hyper-V (do Virtual Machine Manager)</span><span class="sxs-lookup"><span data-stu-id="de79a-124">Hyper-V VMs (without Virtual Machine Manager) tooAzure</span></span>
1. <span data-ttu-id="de79a-125">Excluir todos os protegidos VMs, seguindo as etapas de saudação em [desabilite a proteção para um servidor físico ou a VM do VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span><span class="sxs-lookup"><span data-stu-id="de79a-125">Delete all protected VMs by following hello steps in [Disable protection for a VMware VM or physical server](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).</span></span>

2. <span data-ttu-id="de79a-126">Excluir todas as políticas de replicação, seguindo as etapas de saudação em [excluir uma política de replicação](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span><span class="sxs-lookup"><span data-stu-id="de79a-126">Delete all replication policies by following hello steps in [Delete a replication policy](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).</span></span>

3. <span data-ttu-id="de79a-127">Delete faz referência a servidores tooHyper-V, seguindo as etapas de saudação em [cancelar o registro de um host Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span><span class="sxs-lookup"><span data-stu-id="de79a-127">Delete references tooHyper-V servers by following hello steps in [Unregister a Hyper-V host](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).</span></span>

4. <span data-ttu-id="de79a-128">Exclua site Olá Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="de79a-128">Delete hello Hyper-V site.</span></span>

5. <span data-ttu-id="de79a-129">Exclua cofre hello.</span><span class="sxs-lookup"><span data-stu-id="de79a-129">Delete hello vault.</span></span>
