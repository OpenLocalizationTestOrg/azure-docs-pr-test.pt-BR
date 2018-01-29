---
title: "Início Rápido do Azure - Fazer backup de uma VM com a CLI do Azure | Microsoft Docs"
description: "Saiba como fazer backup de suas máquinas virtuais com a CLI do Azure"
services: backup, virtual-machines-linux
documentationcenter: virtual-machines
author: markgalioto
manager: carmonm
editor: 
tags: azure-resource-manager, virtual-machine-backup
ms.assetid: 
ms.service: backup, virtual-machines-linux
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: vm-linux
ms.workload: storage-backup-recovery
ms.date: 1/12/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 675ebb56496846c5d00ecb5af0e4a69c092b74c6
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2018
---
# <a name="back-up-a-virtual-machine-in-azure-with-the-cli"></a>Fazer backup de uma máquina virtual no Azure com a CLI
A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts. Você pode proteger seus dados fazendo backups em intervalos regulares. O Backup do Azure cria pontos de recuperação que são armazenados em cofres de recuperação com redundância geográfica. Este artigo fornece detalhes sobre como fazer backup de uma máquina virtual (VM) no Azure com a CLI do Azure. Você também pode executar essas etapas usando o [Azure PowerShell](quick-backup-vm-powershell.md) ou o [portal do Azure](quick-backup-vm-portal.md).

Este início rápido habilita o backup em uma VM do Azure existente. Se você precisar criar uma máquina virtual, poderá [criar uma máquina virtual com a CLI do Azure](../virtual-machines/linux/quick-create-cli.md).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Para instalar e usar a CLI localmente, você deve executar a CLI do Azure versão 2.0.18 ou posterior. Para encontrar a versão da CLI, execute `az --version`. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure](/cli/azure/install-azure-cli). 


## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
Um cofre dos Serviços de Recuperação é um contêiner lógico que armazena os dados de backup para cada recurso protegido, como VMs do Azure. Quando o trabalho de backup para um recurso protegido é executado, ele cria um ponto de recuperação no cofre dos Serviços de Recuperação. Você pode usar um desses pontos de recuperação para restaurar dados para um determinado ponto no tempo.

Crie um cofre dos Serviços de Recuperação com [az backup vault create](https://docs.microsoft.com/cli/azure/backup/vault#az_backup_vault_create). Especifique o mesmo grupo de recursos e o local da VM que você deseja proteger. Se você tiver usado o [início rápido de VM](../virtual-machines/linux/quick-create-cli.md), então criou:

- um grupo de recursos denominado *myResourceGroup*,
- uma VM denominada *myVM*,
- recursos no local *eastus*.

```azurecli-interactive 
az backup vault create --resource-group myResourceGroup \
    --name myRecoveryServicesVault \
    --location eastus
```

Por padrão, o cofre dos Serviços de Recuperação é definido para o armazenamento com redundância geográfica. O armazenamento com redundância geográfica garante que os dados de backup são replicados para uma região secundária do Azure que centenas de quilômetros de distância da região primária.


## <a name="enable-backup-for-an-azure-vm"></a>Habilitar o backup para uma VM do Azure
Crie uma política de proteção para definir: quando um trabalho de backup é executado e por quanto tempo os pontos de recuperação serão armazenados. A política de proteção padrão executa um trabalho de backup a cada dia e retém pontos de recuperação por 30 dias. Você pode usar esses valores de política padrão para proteger rapidamente sua VM. Para habilitar a proteção de backup para uma VM, use [az backup protection enable-for-vm](https://docs.microsoft.com/cli/azure/backup/protection#az_backup_protection_enable_for_vm). Especifique o grupo de recursos e a VM a serem protegidos e então a política a ser usada:

```azurecli-interactive 
az backup protection enable-for-vm \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --vm myVM \
    --policy-name DefaultPolicy
```


## <a name="start-a-backup-job"></a>Iniciar um trabalho de backup
Para iniciar um backup agora em vez de aguardar a política padrão executar o trabalho no horário agendado, use [az backup protection backup-now](https://docs.microsoft.com/cli/azure/backup/protection#az_backup_protection_backup_now). O primeiro trabalho de backup cria um ponto de recuperação completa. Cada trabalho de backup depois que o backup inicial cria pontos de recuperação incremental. Os pontos de recuperação incrementais são eficientes em termos de armazenamento e de tempo, já que eles transferem somente as alterações feitas desde o último backup.

Os seguintes parâmetros são usados para fazer backup da VM:

- `--container-name`é o nome da VM
- `--item-name`é o nome da VM
- O valor `--retain-until` deve ser definido como a última data disponível, no formato de hora UTC (**dd-mm-aaaa**), em que você deseja que o ponto de recuperação esteja disponível

O exemplo a seguir faz backup da VM denominada *myVM* e define a expiração do ponto de recuperação para 18 de outubro de 2017:

```azurecli-interactive 
az backup protection backup-now \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --retain-until 18-10-2017
```


## <a name="monitor-the-backup-job"></a>Monitorar o trabalho de backup
Para monitorar o status de trabalhos de backup, use [az backup job list](https://docs.microsoft.com/cli/azure/backup/job#az_backup_job_list):

```azurecli-interactive 
az backup job list \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --output table
```

O resultado é semelhante ao exemplo a seguir, que mostra que o trabalho de backup está *InProgress*:

```
Name      Operation        Status      Item Name    Start Time UTC       Duration
--------  ---------------  ----------  -----------  -------------------  --------------
a0a8e5e6  Backup           InProgress  myvm         2017-09-19T03:09:21  0:00:48.718366
fe5d0414  ConfigureBackup  Completed   myvm         2017-09-19T03:03:57  0:00:31.191807
```

Quando o *Status* do trabalho de backup relatar *Concluído*, sua VM será protegida com os Serviços de Recuperação e terá um ponto de recuperação completo armazenado.


## <a name="clean-up-deployment"></a>Limpar implantação
Quando não for mais necessária, você poderá desabilitar a proteção na máquina virtual, remover os pontos de restauração e o cofre dos Serviços de Recuperação, então excluir o grupo de recursos e recursos associados de VM. Se você tiver usado uma VM existente, poderá ignorar o último comando [az group delete](/cli/azure/group?view=azure-cli-latest#az_group_delete) para deixar o grupo de recursos e a VM no local.

Se você quiser experimentar um tutorial de Backup que explique como restaurar dados para sua VM, vá para [Próximas etapas](#next-steps). 

```azurecli-interactive 
az backup protection disable \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --delete-backup-data true
az backup vault delete \
    --resource-group myResourceGroup \
    --name myRecoveryServicesVault \
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Próximas etapas
Neste início rápido, você criou um cofre dos Serviços de Recuperação, habilitou a proteção em uma máquina virtual e criou o ponto de recuperação inicial. Para saber mais sobre os Serviços de Recuperação e o Backup do Azure, prossiga para os tutoriais.

> [!div class="nextstepaction"]
> [Fazer backup de várias VMs do Azure](./tutorial-backup-vm-at-scale.md)
