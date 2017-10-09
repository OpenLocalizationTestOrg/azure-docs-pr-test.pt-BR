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
# <a name="delete-a-site-recovery-vault"></a>Excluir um cofre do Site Recovery
Dependências podem impedir a exclusão de um cofre do Azure Site Recovery. Olá ações que você precisa tootake variam com base no cenário de recuperação de Site Olá: tooAzure VMware, tooAzure Hyper-V (com e sem o System Center Virtual Machine Manager) e o Backup do Azure. toodelete um cofre usado no Backup do Azure, consulte [excluir um cofre de Backup no Azure](../backup/backup-azure-delete-vault.md).

>[!Important]
>Se você estiver testando o produto hello e não estiver preocupado com a perda de dados, use Olá forçar exclusão método toorapidly remover cofre hello e todas as suas dependências.

> saudação de comando do PowerShell exclui todo o conteúdo de saudação do cofre hello e não é reversível.

## <a name="use-powershell-tooforce-delete-hello-vault"></a>Use PowerShell tooforce excluir cofre Olá 

itens protegidos de saudação toodelete Cofre de recuperação de Site mesmo se houver, usar esses comandos:

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionName "XXXXX"

    $vault = Get-AzureRmSiteRecoveryVault -Name "vaultname"

    Remove-AzureRmSiteRecoveryVault -Vault $vault


## <a name="delete-a-site-recovery-vault"></a>Excluir um cofre do Site Recovery 
Cofre de saudação toodelete, Olá siga as etapas para seu cenário recomendada.

### <a name="vmware-vms-tooazure"></a>Máquinas virtuais do VMware tooAzure

1. Excluir todos os protegidos VMs, seguindo as etapas de saudação em [desabilite a proteção de um VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Excluir todas as políticas de replicação, seguindo as etapas de saudação em [excluir uma política de replicação](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Excluir referências toovCenter por Olá seguir as etapas em [excluir um vCenter](site-recovery-vmware-to-azure-manage-vCenter.md##delete-a-vcenter-in-azure-site-recovery).

4. Excluir o servidor de configuração de saudação, seguindo as etapas de saudação em [encerrar um servidor de configuração](site-recovery-vmware-to-azure-manage-configuration-server.md##decommissioning-a-configuration-server).

5. Exclua cofre hello.


### <a name="hyper-v-vms-with-virtual-machine-manager-tooazure"></a>TooAzure de VMs Hyper-V (com o Virtual Machine Manager)
1. Excluir todos os protegidos VMs, seguindo as etapas de saudação em [desabilite a proteção para um servidor físico ou a VM do VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Excluir todas as políticas de replicação, seguindo as etapas de saudação em [excluir uma política de replicação](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3.  Excluir referências tooVirtual Machine Manager servidores seguindo as etapas de saudação em [cancelar o registro de um servidor VMM conectado](site-recovery-manage-registration-and-protection.md##unregister-a-connected-vmm-server).

4.  Exclua cofre hello.

### <a name="hyper-v-vms-without-virtual-machine-manager-tooazure"></a>TooAzure de VMs Hyper-V (do Virtual Machine Manager)
1. Excluir todos os protegidos VMs, seguindo as etapas de saudação em [desabilite a proteção para um servidor físico ou a VM do VMware](site-recovery-manage-registration-and-protection.md##disable-protection-for-a-vmware-vm-or-physical-server).

2. Excluir todas as políticas de replicação, seguindo as etapas de saudação em [excluir uma política de replicação](site-recovery-setup-replication-settings-vmware.md##delete-a-replication-policy).

3. Delete faz referência a servidores tooHyper-V, seguindo as etapas de saudação em [cancelar o registro de um host Hyper-V](/site-recovery-manage-registration-and-protection.md##unregister-a-hyper-v-host-in-a-hyper-v-site).

4. Exclua site Olá Hyper-V.

5. Exclua cofre hello.
