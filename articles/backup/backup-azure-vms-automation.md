---
title: Implantar e gerenciar backups para VMs implantadas com o Gerenciador de Recursos usando o PowerShell | Microsoft Docs
description: Use o PowerShell para implantar e gerenciar backups no Azure para VMs implantadas com o Gerenciador de Recursos
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="7f387-103">Usar os cmdlets AzureRM.RecoveryServices.Backup para fazer backup de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="7f387-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f387-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="7f387-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="7f387-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="7f387-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="7f387-106">Este artigo mostra como usar os cmdlets do Azure PowerShell para fazer backup e recuperar uma VM (máquina virtual) do Azure de um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="7f387-107">Um cofre dos Serviços de Recuperação é um recurso do Azure Resource Manager usado para proteger dados e ativos nos serviços de Backup do Azure e do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7f387-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="7f387-108">Você pode usar um cofre dos Serviços de Recuperação para proteger as VMs implantadas no Azure Service Manager, bem como as VMs implantadas no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f387-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="7f387-109">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7f387-110">Este artigo destina-se a VMs criadas usando o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f387-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="7f387-111">Ele guiará você sobre como usar o PowerShell para proteger uma VM e como restaurar dados de um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="7f387-112">Conceitos</span><span class="sxs-lookup"><span data-stu-id="7f387-112">Concepts</span></span>
<span data-ttu-id="7f387-113">Se você não estiver familiarizado com o serviço de Backup do Azure, para ter uma visão geral do serviço, confira [O que é o Backup do Azure?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="7f387-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="7f387-114">Antes de começar, é importante ter noções básicas sobre os pré-requisitos necessários para trabalhar com o Backup do Azure e as limitações da atual solução de backup de VM.</span><span class="sxs-lookup"><span data-stu-id="7f387-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="7f387-115">Para usar efetivamente o PowerShell, é necessário compreender a hierarquia de objetos e de onde começar.</span><span class="sxs-lookup"><span data-stu-id="7f387-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![Hierarquia de objetos dos Serviços de Recuperação](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="7f387-117">Para exibir a referência do cmdlet AzureRm.RecoveryServices.Backup do PowerShell, veja [Backup do Azure – cmdlets dos Serviços de Recuperação](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) na biblioteca do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f387-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="7f387-118">Configuração e registro</span><span class="sxs-lookup"><span data-stu-id="7f387-118">Setup and Registration</span></span>
<span data-ttu-id="7f387-119">Para começar:</span><span class="sxs-lookup"><span data-stu-id="7f387-119">To begin:</span></span>

1. <span data-ttu-id="7f387-120">[Baixe a versão mais recente do PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (a versão mínima necessária é: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="7f387-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="7f387-121">Localize os cmdlets do PowerShell do Backup do Azure disponíveis digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f387-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


<span data-ttu-id="7f387-122">As seguintes tarefas podem ser automatizadas com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7f387-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="7f387-123">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="7f387-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="7f387-124">Fazer backup de VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="7f387-124">Back up Azure VMs</span></span>
* <span data-ttu-id="7f387-125">Disparar um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="7f387-125">Trigger a backup job</span></span>
* <span data-ttu-id="7f387-126">Monitorar um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="7f387-126">Monitor a backup job</span></span>
* <span data-ttu-id="7f387-127">Restaurar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="7f387-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="7f387-128">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="7f387-128">Create a recovery services vault</span></span>
<span data-ttu-id="7f387-129">As etapas a seguir orientarão você durante a criação de um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="7f387-130">Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="7f387-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="7f387-131">Se você estiver usando um Backup do Azure pela primeira vez, deverá usar o cmdlet **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** para registrar o provedor do Serviço de Recuperação do Azure com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7f387-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="7f387-132">O cofre dos Serviços de Recuperação é um recurso do Resource Manager e, portanto, você precisará colocá-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f387-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="7f387-133">Você pode usar um grupo de recursos existente ou criar um grupo de recursos com o cmdlet **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**.</span><span class="sxs-lookup"><span data-stu-id="7f387-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="7f387-134">Ao criar um grupo de recursos, especifique o nome e o local para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f387-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="7f387-135">Use o cmdlet **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** para criar um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="7f387-136">Lembre-se de especificar o mesmo local para o cofre usado para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f387-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="7f387-137">Especifique o tipo de redundância de armazenamento a usar. Você pode usar o [Armazenamento com Redundância Local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou o [Armazenamento com Redundância Geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="7f387-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="7f387-138">O exemplo a seguir mostra que a opção BackupStorageRedundancy para o testvault está definida como GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="7f387-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="7f387-139">Muitos cmdlets do Backup do Azure exigem o objeto do cofre dos Serviços de Recuperação como entrada.</span><span class="sxs-lookup"><span data-stu-id="7f387-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="7f387-140">Por esse motivo, pode ser útil armazenar o objeto do cofre dos Serviços de Recuperação de backup em uma variável.</span><span class="sxs-lookup"><span data-stu-id="7f387-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="7f387-141">Exibir os cofres em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="7f387-141">View the vaults in a subscription</span></span>
<span data-ttu-id="7f387-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** para exibir a lista de todos os cofres da assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="7f387-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="7f387-143">Você pode usar esse comando para verificar se um novo cofre foi criado ou para ver quais cofres estão disponíveis na assinatura.</span><span class="sxs-lookup"><span data-stu-id="7f387-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="7f387-144">Execute o comando Get-AzureRmRecoveryServicesVault para exibir todos os cofres na assinatura.</span><span class="sxs-lookup"><span data-stu-id="7f387-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="7f387-145">O exemplo a seguir mostra as informações exibidas para cada cofre.</span><span class="sxs-lookup"><span data-stu-id="7f387-145">The following example shows the information displayed for each vault.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a><span data-ttu-id="7f387-146">Fazer backup de VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="7f387-146">Back up Azure VMs</span></span>
<span data-ttu-id="7f387-147">Use um cofre dos Serviços de Recuperação para proteger as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7f387-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="7f387-148">Antes de aplicar a proteção, defina o contexto de cofre (o tipo de dados protegidos no cofre) e verifique a política de proteção.</span><span class="sxs-lookup"><span data-stu-id="7f387-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="7f387-149">A política de proteção é a agenda de quando o trabalho de backup é executado e de quanto tempo cada instantâneo de backup é mantido.</span><span class="sxs-lookup"><span data-stu-id="7f387-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="7f387-150">Definir o contexto de cofre</span><span class="sxs-lookup"><span data-stu-id="7f387-150">Set vault context</span></span>
<span data-ttu-id="7f387-151">Antes de habilitar a proteção em uma VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** para definir o contexto de cofre.</span><span class="sxs-lookup"><span data-stu-id="7f387-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="7f387-152">Depois que o contexto de cofre é definido, ele se aplica a todos os cmdlets subsequentes.</span><span class="sxs-lookup"><span data-stu-id="7f387-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="7f387-153">O exemplo a seguir define o contexto de cofre para o cofre, *testvault*.</span><span class="sxs-lookup"><span data-stu-id="7f387-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="7f387-154">Crie uma política de proteção</span><span class="sxs-lookup"><span data-stu-id="7f387-154">Create a protection policy</span></span>
<span data-ttu-id="7f387-155">Quando você cria um cofre dos Serviços de Recuperação, ele vem com proteção e políticas de retenção padrão.</span><span class="sxs-lookup"><span data-stu-id="7f387-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="7f387-156">A política de proteção padrão dispara um trabalho de backup diariamente em um horário especificado.</span><span class="sxs-lookup"><span data-stu-id="7f387-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="7f387-157">A política de retenção padrão retém o ponto de recuperação diário por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="7f387-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="7f387-158">Você pode usar a política padrão para proteger rapidamente sua VM e editá-la posteriormente com detalhes diferentes.</span><span class="sxs-lookup"><span data-stu-id="7f387-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="7f387-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** para exibir as políticas de proteção disponíveis no cofre.</span><span class="sxs-lookup"><span data-stu-id="7f387-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="7f387-160">Você pode usar este cmdlet para obter uma política específica ou para exibir as políticas associadas a um tipo de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7f387-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="7f387-161">O exemplo a seguir obtém as políticas para o tipo de carga de trabalho, AzureVM.</span><span class="sxs-lookup"><span data-stu-id="7f387-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="7f387-162">O fuso horário do campo BackupTime no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="7f387-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="7f387-163">No entanto, quando o tempo de backup é mostrado no Portal do Azure, o horário é ajustado para seu fuso horário local.</span><span class="sxs-lookup"><span data-stu-id="7f387-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="7f387-164">Uma política de proteção de backup está associada a pelo menos uma política de retenção.</span><span class="sxs-lookup"><span data-stu-id="7f387-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="7f387-165">A política de retenção define por quanto tempo um ponto de recuperação é mantido até ser excluído.</span><span class="sxs-lookup"><span data-stu-id="7f387-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="7f387-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** para exibir a política de retenção padrão.</span><span class="sxs-lookup"><span data-stu-id="7f387-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="7f387-167">Da mesma forma, você pode usar **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** para obter a política de agendamento padrão.</span><span class="sxs-lookup"><span data-stu-id="7f387-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="7f387-168">O cmdlet **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cria um objeto do PowerShell que mantém as informações da política de backup.</span><span class="sxs-lookup"><span data-stu-id="7f387-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="7f387-169">Os objetos de política de retenção e agendamento são usados como entradas para o cmdlet **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**.</span><span class="sxs-lookup"><span data-stu-id="7f387-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="7f387-170">O exemplo a seguir armazena a política de agendamento e a política de retenção em variáveis.</span><span class="sxs-lookup"><span data-stu-id="7f387-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="7f387-171">O exemplo usa essas variáveis para definir os parâmetros ao criar uma política de proteção, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="7f387-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="7f387-172">Habilitar proteção</span><span class="sxs-lookup"><span data-stu-id="7f387-172">Enable protection</span></span>
<span data-ttu-id="7f387-173">Depois de definir a política de proteção de backup, você deve habilitar a política para um item.</span><span class="sxs-lookup"><span data-stu-id="7f387-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="7f387-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** para habilitar a proteção.</span><span class="sxs-lookup"><span data-stu-id="7f387-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="7f387-175">Habilitar a proteção envolve dois objetos – o item e a política.</span><span class="sxs-lookup"><span data-stu-id="7f387-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="7f387-176">Depois de a política ter sido associada ao cofre, o fluxo de trabalho de backup será disparado no momento definido no agendamento da política.</span><span class="sxs-lookup"><span data-stu-id="7f387-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="7f387-177">O exemplo a seguir habilita a proteção para o item, V2VM, usando a política, NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="7f387-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="7f387-178">Para habilitar a proteção em VMs do Resource Manager não criptografadas</span><span class="sxs-lookup"><span data-stu-id="7f387-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="7f387-179">Para habilitar a proteção em VMs criptografadas (criptografadas usando BEK e KEK), você precisa conceder permissão para o serviço de Backup do Azure ler as chaves e os segredos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="7f387-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="7f387-180">Para habilitar a proteção em VMs criptografadas (criptografadas usando apenas BEK), você precisa dar permissão de serviço de Backup do Azure para ler segredos do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="7f387-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="7f387-181">Se você estiver usando a nuvem do Azure Governamental, use o valor ff281ffe-705c-4f53-9f37-a40e6f2c68f3 para o parâmetro **-ServicePrincipalName** no cmdlet [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy).</span><span class="sxs-lookup"><span data-stu-id="7f387-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="7f387-182">Para VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="7f387-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="7f387-183">Modificar uma política de proteção</span><span class="sxs-lookup"><span data-stu-id="7f387-183">Modify a protection policy</span></span>
<span data-ttu-id="7f387-184">Para modificar a política de proteção, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) para modificar os objetos SchedulePolicy ou RetentionPolicy.</span><span class="sxs-lookup"><span data-stu-id="7f387-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="7f387-185">O exemplo a seguir altera retenção de ponto de recuperação para 365 dias.</span><span class="sxs-lookup"><span data-stu-id="7f387-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="7f387-186">Disparar um backup</span><span class="sxs-lookup"><span data-stu-id="7f387-186">Trigger a backup</span></span>
<span data-ttu-id="7f387-187">Você pode usar **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** para disparar um trabalho de backup.</span><span class="sxs-lookup"><span data-stu-id="7f387-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="7f387-188">Se esse é o backup inicial, ele é um backup completo.</span><span class="sxs-lookup"><span data-stu-id="7f387-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="7f387-189">Os backups posteriores fazem uma cópia incremental.</span><span class="sxs-lookup"><span data-stu-id="7f387-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="7f387-190">Você deve usar **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** para definir o contexto de cofre antes de disparar o trabalho de backup.</span><span class="sxs-lookup"><span data-stu-id="7f387-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="7f387-191">O exemplo a seguir pressupõe que o contexto de cofre foi definido.</span><span class="sxs-lookup"><span data-stu-id="7f387-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="7f387-192">O fuso horário dos campos StartTime e EndTime mostrado no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="7f387-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="7f387-193">No entanto, quando a hora é exibida no Portal do Azure, ela é ajustada para seu fuso horário local.</span><span class="sxs-lookup"><span data-stu-id="7f387-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="7f387-194">Monitoramento de um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="7f387-194">Monitoring a backup job</span></span>
<span data-ttu-id="7f387-195">Você pode monitorar operações de longa duração, como trabalhos de backup, sem usar o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f387-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="7f387-196">Para obter o status de um trabalho em andamento, use o cmdlet **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="7f387-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="7f387-197">Esse cmdlet obtém os trabalhos de backup para um cofre específico, o qual está especificado no contexto de cofre.</span><span class="sxs-lookup"><span data-stu-id="7f387-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="7f387-198">O exemplo a seguir obtém o status de um trabalho em andamento como uma matriz e armazena o status na variável $joblist.</span><span class="sxs-lookup"><span data-stu-id="7f387-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="7f387-199">Em vez de sondar esses trabalhos para conclusão (o que é um código adicional desnecessário), é mais simples usar o cmdlet **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="7f387-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="7f387-200">Esse cmdlet pausa a execução até que o trabalho seja concluído ou o valor de tempo limite especificado seja atingido.</span><span class="sxs-lookup"><span data-stu-id="7f387-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="7f387-201">Restaurar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="7f387-201">Restore an Azure VM</span></span>
<span data-ttu-id="7f387-202">Há uma diferença importante entre a restauração de uma máquina virtual usando o portal do Azure e a restauração de uma máquina virtual usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f387-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="7f387-203">Com o PowerShell, a operação de restauração é concluída quando são criadas as informações dos discos e de configuração do ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="7f387-204">A operação de restauração não cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f387-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="7f387-205">Para criar uma máquina virtual do disco, consulte a seção [Criar a VM de discos armazenados](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="7f387-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="7f387-206">As etapas básicas para restaurar uma VM do Azure são:</span><span class="sxs-lookup"><span data-stu-id="7f387-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="7f387-207">Selecione a VM</span><span class="sxs-lookup"><span data-stu-id="7f387-207">Select the VM</span></span>
* <span data-ttu-id="7f387-208">Escolha um ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="7f387-208">Choose a recovery point</span></span>
* <span data-ttu-id="7f387-209">Restaure os discos</span><span class="sxs-lookup"><span data-stu-id="7f387-209">Restore the disks</span></span>
* <span data-ttu-id="7f387-210">Crie a VM de discos armazenados</span><span class="sxs-lookup"><span data-stu-id="7f387-210">Create the VM from stored disks</span></span>

<span data-ttu-id="7f387-211">O gráfico a seguir mostra a hierarquia de objetos do RecoveryServicesVault até o BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="7f387-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![Hierarquia de objetos dos Serviços de Recuperação mostrando BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="7f387-213">Para restaurar dados de backup, identifique o item de backup e o ponto de recuperação que mantém os dados pontuais.</span><span class="sxs-lookup"><span data-stu-id="7f387-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="7f387-214">Use o cmdlet **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** para restaurar dados do cofre para a conta do cliente.</span><span class="sxs-lookup"><span data-stu-id="7f387-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="7f387-215">Selecione a VM</span><span class="sxs-lookup"><span data-stu-id="7f387-215">Select the VM</span></span>
<span data-ttu-id="7f387-216">Para obter o objeto do PowerShell que identifica o item correto de backup, comece do contêiner no cofre e desça progressivamente na hierarquia de objetos.</span><span class="sxs-lookup"><span data-stu-id="7f387-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="7f387-217">Para selecionar o contêiner que representa a VM, use o cmdlet **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** e o redirecione para o cmdlet **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**.</span><span class="sxs-lookup"><span data-stu-id="7f387-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="7f387-218">Escolha um ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="7f387-218">Choose a recovery point</span></span>
<span data-ttu-id="7f387-219">Use o cmdlet **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** para listar todos os pontos de recuperação para o item de backup.</span><span class="sxs-lookup"><span data-stu-id="7f387-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="7f387-220">Em seguida, escolha o ponto de recuperação a ser restaurado.</span><span class="sxs-lookup"><span data-stu-id="7f387-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="7f387-221">Se você não tiver certeza de qual ponto de recuperação será usado, é uma boa prática escolher o mais recente ponto RecoveryPointType = AppConsistent na lista.</span><span class="sxs-lookup"><span data-stu-id="7f387-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="7f387-222">No script a seguir, a variável **$rp** é uma matriz de pontos de recuperação dos últimos sete dias para o item de backup selecionado.</span><span class="sxs-lookup"><span data-stu-id="7f387-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="7f387-223">A matriz é classificada em ordem inversa de tempo com o último ponto de recuperação no índice 0.</span><span class="sxs-lookup"><span data-stu-id="7f387-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="7f387-224">Use a indexação de matriz padrão do PowerShell para selecionar o ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="7f387-225">No exemplo, $rp[0] seleciona o último ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-225">In the example, $rp[0] selects the latest recovery point.</span></span>

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-the-disks"></a><span data-ttu-id="7f387-226">Restaure os discos</span><span class="sxs-lookup"><span data-stu-id="7f387-226">Restore the disks</span></span>
<span data-ttu-id="7f387-227">Use o cmdlet **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** para restaurar os dados de backup e a configuração de um item de backup para um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="7f387-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="7f387-228">Depois de ter identificado um ponto de recuperação, use-o como o valor do parâmetro **-RecoveryPoint**.</span><span class="sxs-lookup"><span data-stu-id="7f387-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="7f387-229">No código de exemplo anterior, **$rp [0]** foi o ponto de recuperação a ser usado.</span><span class="sxs-lookup"><span data-stu-id="7f387-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="7f387-230">No código de exemplo abaixo, **$rp [0]** é o ponto de recuperação a ser usado para a restauração do disco.</span><span class="sxs-lookup"><span data-stu-id="7f387-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="7f387-231">Para restaurar as informações de discos e de configuração:</span><span class="sxs-lookup"><span data-stu-id="7f387-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="7f387-232">Use o cmdlet **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** para aguardar a conclusão do trabalho de Restauração.</span><span class="sxs-lookup"><span data-stu-id="7f387-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="7f387-233">Após a conclusão do trabalho de Restauração, use o cmdlet **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** para obter os detalhes da operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="7f387-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="7f387-234">A propriedade JobDetails tem as informações necessárias para recompilar a VM.</span><span class="sxs-lookup"><span data-stu-id="7f387-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="7f387-235">Depois de restaurar os discos, vá para a próxima seção para criar a VM.</span><span class="sxs-lookup"><span data-stu-id="7f387-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="7f387-236">Criar uma máquina virtual de discos restaurados</span><span class="sxs-lookup"><span data-stu-id="7f387-236">Create a VM from restored disks</span></span>
<span data-ttu-id="7f387-237">Depois de ter restaurado os discos, use estas etapas para criar e configurar uma máquina virtual do disco.</span><span class="sxs-lookup"><span data-stu-id="7f387-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="7f387-238">Para criar VMs criptografadas de discos restaurados, a função do Azure deverá ter permissão para executar a ação **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="7f387-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="7f387-239">Se sua função não tem essa permissão, crie uma função personalizada com esta ação.</span><span class="sxs-lookup"><span data-stu-id="7f387-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="7f387-240">Para obter mais informações, veja [Funções personalizadas no RBAC do Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="7f387-241">Consulte as propriedades do disco restaurado para obter os detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="7f387-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="7f387-242">Defina o contexto do armazenamento do Azure e restaure o arquivo de configuração JSON.</span><span class="sxs-lookup"><span data-stu-id="7f387-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="7f387-243">Use o arquivo de configuração JSON para criar a configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="7f387-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="7f387-244">Anexe o disco do sistema operacional e os discos de dados.</span><span class="sxs-lookup"><span data-stu-id="7f387-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="7f387-245">Dependendo da configuração de suas VMs, clique no link para exibir os cmdlets do respectivos relevante:</span><span class="sxs-lookup"><span data-stu-id="7f387-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="7f387-246">Máquinas virtuais não gerenciados, não criptografado</span><span class="sxs-lookup"><span data-stu-id="7f387-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="7f387-247">Máquinas virtuais não gerenciados, criptografados (BEK)</span><span class="sxs-lookup"><span data-stu-id="7f387-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="7f387-248">Máquinas virtuais não gerenciados, criptografados (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="7f387-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="7f387-249">Máquinas virtuais gerenciados, não criptografado</span><span class="sxs-lookup"><span data-stu-id="7f387-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="7f387-250">Máquinas virtuais gerenciadas, criptografados (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="7f387-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="7f387-251">VMs não criptografadas não gerenciadas</span><span class="sxs-lookup"><span data-stu-id="7f387-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="7f387-252">Use a amostra a seguir para VMs não criptografadas não gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="7f387-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="7f387-253">VMs criptografadas e não gerenciadas (apenas BEK)</span><span class="sxs-lookup"><span data-stu-id="7f387-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="7f387-254">Para VMs criptografadas e não gerenciadas (criptografadas usando apenas BEK), você precisa restaurar o segredo para o cofre de chaves para poder anexar discos.</span><span class="sxs-lookup"><span data-stu-id="7f387-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="7f387-255">Para obter mais informações, consulte o artigo [Restaurar uma máquina virtual criptografada de um ponto de recuperação do Backup do Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="7f387-256">O exemplo a seguir mostra como anexar discos de dados e de SO a VMs criptografadas.</span><span class="sxs-lookup"><span data-stu-id="7f387-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="7f387-257">VMs criptografadas e não gerenciadas (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="7f387-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="7f387-258">Para VMs criptografadas e não gerenciadas (criptografadas usando BEK e KEK), você precisa restaurar a chave e o segredo para o cofre de chaves para poder anexar discos.</span><span class="sxs-lookup"><span data-stu-id="7f387-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="7f387-259">Para obter mais informações, consulte o artigo [Restaurar uma máquina virtual criptografada de um ponto de recuperação do Backup do Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="7f387-260">O exemplo a seguir mostra como anexar discos de dados e de SO a VMs criptografadas.</span><span class="sxs-lookup"><span data-stu-id="7f387-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="7f387-261">VMs não criptografadas gerenciadas</span><span class="sxs-lookup"><span data-stu-id="7f387-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="7f387-262">Para VMs não criptografadas gerenciadas, você precisará criar discos gerenciados no armazenamento de blobs e, em seguida, anexar os discos.</span><span class="sxs-lookup"><span data-stu-id="7f387-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="7f387-263">Para obter informações detalhadas, consulte o artigo [Anexar um disco de dados a uma VM do Windows usando o PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="7f387-264">O código de exemplo a seguir mostra como anexar os discos de dados a VMs não criptografadas gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="7f387-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="7f387-265">VMs criptografadas e gerenciadas (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="7f387-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="7f387-266">Para VMs criptografadas e gerenciadas (criptografadas usando BEK e KEK), você precisará criar discos gerenciados do armazenamento de blobs e, em seguida, anexar os discos.</span><span class="sxs-lookup"><span data-stu-id="7f387-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="7f387-267">Para obter informações detalhadas, consulte o artigo [Anexar um disco de dados a uma VM do Windows usando o PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="7f387-268">O código de exemplo a seguir mostra como anexar os discos de dados a VMs criptografadas gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="7f387-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. <span data-ttu-id="7f387-269">Defina as configurações de Rede.</span><span class="sxs-lookup"><span data-stu-id="7f387-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="7f387-270">Crie a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7f387-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="7f387-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f387-271">Next steps</span></span>
<span data-ttu-id="7f387-272">Se você preferir usar o PowerShell para interagir com os recursos do Azure, confira o artigo do PowerShell, [Implantar e gerenciar Backup do Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="7f387-273">Se você gerencia backups do DPM, consulte o artigo [Implantar e gerenciar o backup do DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="7f387-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="7f387-274">Esses dois artigos têm uma versão para implantações do Resource Manager, bem como para implantações do modelo Clássico.</span><span class="sxs-lookup"><span data-stu-id="7f387-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
