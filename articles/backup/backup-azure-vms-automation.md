---
title: aaaDeploy e gerenciar backups para VMs implantadas pelo Gerenciador de recursos usando o PowerShell | Microsoft Docs
description: Use o PowerShell toodeploy e gerenciar backups no Azure para VMs implantadas pelo Gerenciador de recursos
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
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="2fca3-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback backup de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="2fca3-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2fca3-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="2fca3-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="2fca3-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="2fca3-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="2fca3-106">Este artigo mostra como toouse tooback de cmdlets do PowerShell do Azure backup e recuperar uma máquina virtual (VM) do Azure de serviços de recuperação de um cofre.</span><span class="sxs-lookup"><span data-stu-id="2fca3-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="2fca3-107">Um cofre de serviços de recuperação é um recurso do Gerenciador de recursos do Azure e é usado tooprotect dados e ativos nos serviços de Backup do Azure e o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2fca3-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="2fca3-108">Você pode usar um cofre de serviços de recuperação tooprotect VMs implantadas pelo Gerenciador de serviço do Azure e máquinas virtuais implantadas pelo Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fca3-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="2fca3-109">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2fca3-110">Este artigo é para uso com máquinas virtuais criadas usando o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="2fca3-111">Este artigo orienta você a usar PowerShell tooprotect uma VM e restaurar dados de um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="2fca3-112">Conceitos</span><span class="sxs-lookup"><span data-stu-id="2fca3-112">Concepts</span></span>
<span data-ttu-id="2fca3-113">Se você não estiver familiarizado com hello serviço Backup do Azure, para obter uma visão geral do serviço Olá, confira [o que é o Backup do Azure?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="2fca3-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="2fca3-114">Antes de começar, certifique-se de que abrangem essentials Olá sobre Olá pré-requisitos necessários toowork com o Backup do Azure e Olá limitações da solução atual de backup de VM hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="2fca3-115">toouse PowerShell efetivamente, é necessário toounderstand Olá hierarquia de objetos e de onde toostart.</span><span class="sxs-lookup"><span data-stu-id="2fca3-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Hierarquia de objetos dos Serviços de Recuperação](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="2fca3-117">Olá tooview Referência de cmdlet do AzureRm.RecoveryServices.Backup PowerShell, consulte Olá [Backup do Azure - Cmdlets dos serviços de recuperação](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) em Olá biblioteca do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fca3-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="2fca3-118">Configuração e registro</span><span class="sxs-lookup"><span data-stu-id="2fca3-118">Setup and Registration</span></span>
<span data-ttu-id="2fca3-119">toobegin:</span><span class="sxs-lookup"><span data-stu-id="2fca3-119">toobegin:</span></span>

1. <span data-ttu-id="2fca3-120">[Baixar a versão mais recente de saudação do PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (Olá versão mínima necessária é: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="2fca3-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="2fca3-121">Localize os cmdlets do PowerShell do Azure Backup Olá disponíveis digitando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="2fca3-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="2fca3-122">Olá tarefas a seguir pode ser automatizada com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2fca3-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="2fca3-123">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="2fca3-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="2fca3-124">Fazer backup de VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="2fca3-124">Back up Azure VMs</span></span>
* <span data-ttu-id="2fca3-125">Disparar um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="2fca3-125">Trigger a backup job</span></span>
* <span data-ttu-id="2fca3-126">Monitorar um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="2fca3-126">Monitor a backup job</span></span>
* <span data-ttu-id="2fca3-127">Restaurar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="2fca3-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="2fca3-128">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="2fca3-128">Create a recovery services vault</span></span>
<span data-ttu-id="2fca3-129">Olá etapas levá-lo na criação de um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="2fca3-130">Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="2fca3-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="2fca3-131">Se você estiver usando o Backup do Azure para Olá primeira vez, você deve usar o hello  **[registro AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  provedor de serviço de recuperação do Azure do cmdlet tooregister Olá com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="2fca3-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="2fca3-132">Olá Cofre de serviços de recuperação é um recurso do Gerenciador de recursos, portanto, você precisa tooplace-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2fca3-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="2fca3-133">Você pode usar um grupo de recursos existente ou criar um grupo de recursos com hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fca3-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="2fca3-134">Ao criar um grupo de recursos, especifique o nome de saudação e local para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="2fca3-135">Saudação de uso  **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate Olá Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="2fca3-136">Certifique-se de que toospecify Olá mesmo local para o cofre Olá que foi usada para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="2fca3-137">Especificar o tipo de saudação do toouse de redundância de armazenamento; Você pode usar [armazenamento localmente redundante (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [Geo redundante GRS (armazenamento)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="2fca3-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="2fca3-138">Olá exemplo a seguir mostra Olá - BackupStorageRedundancy opção testvault é definida tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="2fca3-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="2fca3-139">Muitos cmdlets do Backup do Azure exigem Olá objeto de Cofre de serviços de recuperação como entrada.</span><span class="sxs-lookup"><span data-stu-id="2fca3-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="2fca3-140">Por esse motivo, é conveniente toostore Olá serviços de recuperação de Backup cofre objeto em uma variável.</span><span class="sxs-lookup"><span data-stu-id="2fca3-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="2fca3-141">Exibição Olá cofres em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="2fca3-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="2fca3-142">Use  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview lista de saudação de todos os cofres na assinatura atual hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="2fca3-143">Você pode usar este toocheck de comando que foi criado um novo cofre ou toosee Olá cofres disponíveis na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="2fca3-144">Execute o comando hello, Get-AzureRmRecoveryServicesVault tooview todos os cofres na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="2fca3-145">Olá exemplo a seguir mostra informações de saudação exibidas para cada compartimento.</span><span class="sxs-lookup"><span data-stu-id="2fca3-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="2fca3-146">Fazer backup de VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="2fca3-146">Back up Azure VMs</span></span>
<span data-ttu-id="2fca3-147">Use um tooprotect de Cofre de serviços de recuperação de suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="2fca3-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="2fca3-148">Antes de aplicar proteção Olá, definir o contexto de Cofre de saudação (tipo de saudação dos dados protegidos no cofre Olá) e verifique se a diretiva de proteção de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="2fca3-149">diretiva de proteção de saudação é agendar Olá executar trabalhos de backup hello e quanto tempo cada instantâneo de backup é mantido.</span><span class="sxs-lookup"><span data-stu-id="2fca3-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="2fca3-150">Definir o contexto de cofre</span><span class="sxs-lookup"><span data-stu-id="2fca3-150">Set vault context</span></span>
<span data-ttu-id="2fca3-151">Antes de habilitar a proteção em uma máquina virtual, use  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexto de Cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="2fca3-152">Depois que o contexto de cofre Olá for definido, ela se aplica a cmdlets subsequentes tooall.</span><span class="sxs-lookup"><span data-stu-id="2fca3-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="2fca3-153">Olá, exemplo a seguir define Olá contexto de cofre para o cofre hello, *testvault*.</span><span class="sxs-lookup"><span data-stu-id="2fca3-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="2fca3-154">Crie uma política de proteção</span><span class="sxs-lookup"><span data-stu-id="2fca3-154">Create a protection policy</span></span>
<span data-ttu-id="2fca3-155">Quando você cria um cofre dos Serviços de Recuperação, ele vem com proteção e políticas de retenção padrão.</span><span class="sxs-lookup"><span data-stu-id="2fca3-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="2fca3-156">política de proteção padrão Olá dispara um trabalho de backup diariamente em um horário especificado.</span><span class="sxs-lookup"><span data-stu-id="2fca3-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="2fca3-157">política de retenção padrão Olá retém o ponto de recuperação diário Olá por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="2fca3-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="2fca3-158">Você pode usar o padrão de saudação política tooquickly proteger sua VM e Editar política de hello mais tarde com detalhes diferentes.</span><span class="sxs-lookup"><span data-stu-id="2fca3-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="2fca3-159">Use  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview políticas de proteção de saudação no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="2fca3-160">Você pode usar este cmdlet tooget uma política específica ou políticas de saudação tooview associadas com um tipo de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2fca3-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="2fca3-161">saudação de exemplo a seguir obtém as políticas para o tipo de carga de trabalho, AzureVM.</span><span class="sxs-lookup"><span data-stu-id="2fca3-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="2fca3-162">fuso horário de saudação do campo de BackupTime Olá no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="2fca3-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="2fca3-163">No entanto, quando o tempo de backup de saudação é mostrado no hello portal do Azure, o tempo de saudação é fuso horário local do tooyour ajustada.</span><span class="sxs-lookup"><span data-stu-id="2fca3-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="2fca3-164">Uma política de proteção de backup está associada a pelo menos uma política de retenção.</span><span class="sxs-lookup"><span data-stu-id="2fca3-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="2fca3-165">A política de retenção define por quanto tempo um ponto de recuperação é mantido até ser excluído.</span><span class="sxs-lookup"><span data-stu-id="2fca3-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="2fca3-166">Use  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  política de retenção tooview saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="2fca3-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="2fca3-167">Da mesma forma, você pode usar  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  política ao agendar tooobtain saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="2fca3-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="2fca3-168">Olá  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet cria um objeto do PowerShell que contém informações de política de backup.</span><span class="sxs-lookup"><span data-stu-id="2fca3-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="2fca3-169">Olá objetos de política de retenção e agendamento são usados como entradas toohello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fca3-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="2fca3-170">Olá exemplo a seguir armazena política ao agendar hello e política de retenção de saudação em variáveis.</span><span class="sxs-lookup"><span data-stu-id="2fca3-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="2fca3-171">exemplo Hello usa esses parâmetros de saudação toodefine variáveis ao criar uma política de proteção, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="2fca3-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="2fca3-172">Habilitar proteção</span><span class="sxs-lookup"><span data-stu-id="2fca3-172">Enable protection</span></span>
<span data-ttu-id="2fca3-173">Depois que você definiu a diretiva de proteção de backup hello, você deve habilitar política de saudação para um item.</span><span class="sxs-lookup"><span data-stu-id="2fca3-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="2fca3-174">Use  **[habilitar AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable proteção.</span><span class="sxs-lookup"><span data-stu-id="2fca3-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="2fca3-175">Habilitar a proteção requer dois objetos - item hello e política de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="2fca3-176">Depois que a política Olá foi associada ao Cofre hello, fluxo de trabalho de backup Olá é acionado em tempo de saudação definido na agenda de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="2fca3-177">Olá exemplo habilita proteção Olá item, V2VM, usando a política de hello, NewPolicy a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fca3-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="2fca3-178">proteção de saudação tooenable em VMs do Gerenciador de recursos não criptografado</span><span class="sxs-lookup"><span data-stu-id="2fca3-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="2fca3-179">proteção Olá tooenable criptografado VMs (criptografadas usando BEK e KEK), chaves de tooread permissão do serviço de Backup do Azure de saudação toogive e segredos do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="2fca3-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="2fca3-180">proteção Olá tooenable criptografado VMs (criptografadas usando apenas o BEK), toogive hello Azure Backup service permissão tooread segredos do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="2fca3-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="2fca3-181">Se você estiver usando a nuvem do Azure Government hello, use Olá ff281ffe-705c-4f53-9f37-a40e6f2c68f3 de valor para o parâmetro hello **- ServicePrincipalName** na [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .</span><span class="sxs-lookup"><span data-stu-id="2fca3-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="2fca3-182">Para VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="2fca3-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="2fca3-183">Modificar uma política de proteção</span><span class="sxs-lookup"><span data-stu-id="2fca3-183">Modify a protection policy</span></span>
<span data-ttu-id="2fca3-184">política de proteção Olá toomodify, use [AzureRmRecoveryServicesBackupProtectionPolicy conjunto](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify Olá SchedulePolicy ou política de retenção objetos.</span><span class="sxs-lookup"><span data-stu-id="2fca3-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="2fca3-185">Olá, exemplo a seguir altera dias de too365 retenção do ponto de recuperação hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="2fca3-186">Disparar um backup</span><span class="sxs-lookup"><span data-stu-id="2fca3-186">Trigger a backup</span></span>
<span data-ttu-id="2fca3-187">Você pode usar  **[Backup AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger um trabalho de backup.</span><span class="sxs-lookup"><span data-stu-id="2fca3-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="2fca3-188">Se for backup inicial Olá, é um backup completo.</span><span class="sxs-lookup"><span data-stu-id="2fca3-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="2fca3-189">Os backups posteriores fazem uma cópia incremental.</span><span class="sxs-lookup"><span data-stu-id="2fca3-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="2fca3-190">Ser toouse se  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexto de cofre Olá antes de disparar o trabalho de backup hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="2fca3-191">saudação de exemplo a seguir pressupõe que o cofre contexto foi definido.</span><span class="sxs-lookup"><span data-stu-id="2fca3-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="2fca3-192">fuso horário de saudação de campos de StartTime e EndTime Olá no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="2fca3-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="2fca3-193">No entanto, quando o tempo de saudação é mostrado no portal do Azure de saudação, tempo de saudação é fuso horário local do tooyour ajustada.</span><span class="sxs-lookup"><span data-stu-id="2fca3-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="2fca3-194">Monitoramento de um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="2fca3-194">Monitoring a backup job</span></span>
<span data-ttu-id="2fca3-195">Você pode monitorar as operações de execução longa, como trabalhos de backup, sem usar Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fca3-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="2fca3-196">status de saudação tooget de um trabalho em andamento, use Olá  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fca3-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="2fca3-197">Esse cmdlet obtém os trabalhos de backup da saudação para um cofre específico e que os está especificado no contexto de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="2fca3-198">Olá exemplo a seguir obtém o status de saudação de um trabalho em andamento como uma matriz e armazena status Olá na Olá $joblist variável.</span><span class="sxs-lookup"><span data-stu-id="2fca3-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="2fca3-199">Em vez de sondagem esses trabalhos para conclusão - que é desnecessário código adicional - use Olá  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fca3-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="2fca3-200">Esse cmdlet pausa a execução de saudação até Olá trabalho for concluído ou Olá especificado, o valor de tempo limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="2fca3-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="2fca3-201">Restaurar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="2fca3-201">Restore an Azure VM</span></span>
<span data-ttu-id="2fca3-202">Há uma diferença importante entre hello restaurar uma máquina virtual usando Olá portal do Azure e restaurar uma máquina virtual usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fca3-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="2fca3-203">Com o PowerShell, operação de restauração de saudação é concluída após a criação de discos de saudação e informações de configuração de ponto de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="2fca3-204">operação de restauração Olá não cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2fca3-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="2fca3-205">toocreate uma máquina virtual do disco, consulte a seção Olá [criar hello VM dos discos armazenados](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="2fca3-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="2fca3-206">as etapas básicas de saudação toorestore uma VM do Azure são:</span><span class="sxs-lookup"><span data-stu-id="2fca3-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="2fca3-207">Selecione Olá VM</span><span class="sxs-lookup"><span data-stu-id="2fca3-207">Select hello VM</span></span>
* <span data-ttu-id="2fca3-208">Escolha um ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="2fca3-208">Choose a recovery point</span></span>
* <span data-ttu-id="2fca3-209">Restaurar discos Olá</span><span class="sxs-lookup"><span data-stu-id="2fca3-209">Restore hello disks</span></span>
* <span data-ttu-id="2fca3-210">Criar hello VM de discos armazenados</span><span class="sxs-lookup"><span data-stu-id="2fca3-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="2fca3-211">Olá gráfico a seguir mostra hierarquia de objetos de saudação do hello RecoveryServicesVault para baixo toohello BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="2fca3-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Hierarquia de objetos dos Serviços de Recuperação mostrando BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="2fca3-213">toorestore os dados de backup, identificar o item de backup hello e ponto de recuperação de saudação que contém dados de point-in-time de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="2fca3-214">Saudação de uso  **[restauração AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore dados Olá cofre conta toohello do cliente.</span><span class="sxs-lookup"><span data-stu-id="2fca3-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="2fca3-215">Selecione Olá VM</span><span class="sxs-lookup"><span data-stu-id="2fca3-215">Select hello VM</span></span>
<span data-ttu-id="2fca3-216">objeto do PowerShell Olá tooget que identifica o direito de saudação item de backup, iniciar do contêiner de saudação no cofre hello e trabalhar abaixo da hierarquia de objetos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="2fca3-217">contêiner de saudação tooselect que representa o hello VM, use Olá  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet e redirecione que toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fca3-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="2fca3-218">Escolha um ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="2fca3-218">Choose a recovery point</span></span>
<span data-ttu-id="2fca3-219">Saudação de uso  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist cmdlet pontos de recuperação todos para fazer backup do item hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="2fca3-220">Em seguida, escolha Olá toorestore de ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="2fca3-221">Se você não tiver certeza de qual toouse de ponto de recuperação, é uma boa prática toochoose hello mais recente RecoveryPointType = AppConsistent ponto na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="2fca3-222">Em Olá script a seguir, Olá variável, **$rp**, é uma matriz de pontos de recuperação para fazer backup do item selecionado Olá da saudação últimos sete dias.</span><span class="sxs-lookup"><span data-stu-id="2fca3-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="2fca3-223">matriz de saudação é classificada em ordem inversa de tempo com o último ponto de recuperação Olá no índice 0.</span><span class="sxs-lookup"><span data-stu-id="2fca3-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="2fca3-224">Use o padrão matriz do PowerShell a indexação de ponto de recuperação toopick hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="2fca3-225">No exemplo hello, $rp [0] seleciona o último ponto de recuperação hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="2fca3-226">Restaurar discos Olá</span><span class="sxs-lookup"><span data-stu-id="2fca3-226">Restore hello disks</span></span>
<span data-ttu-id="2fca3-227">Saudação de uso  **[restauração AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore cmdlet dados do item de um backup e configuração tooa ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="2fca3-228">Depois de ter identificado um ponto de recuperação, usá-lo como valor Olá para Olá **- RecoveryPoint** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2fca3-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="2fca3-229">No código de exemplo anterior hello, **$rp [0]** foi Olá toouse de ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="2fca3-230">Em Olá código de exemplo a seguir **$rp [0]** é Olá toouse de ponto de recuperação para restaurar o disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="2fca3-231">discos de saudação toorestore e informações de configuração:</span><span class="sxs-lookup"><span data-stu-id="2fca3-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="2fca3-232">Saudação de uso  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait cmdlet para Olá toocomplete de trabalho de restauração.</span><span class="sxs-lookup"><span data-stu-id="2fca3-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="2fca3-233">Depois de concluído o trabalho de restauração hello, use Olá  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  detalhes de saudação do cmdlet tooget de saudação de operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="2fca3-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="2fca3-234">Olá JobDetails propriedade tem Olá toorebuild necessário de informações Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2fca3-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="2fca3-235">Depois que você restaurar discos hello, vá Olá de toocreate de seção próximo do toohello VM.</span><span class="sxs-lookup"><span data-stu-id="2fca3-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="2fca3-236">Criar uma máquina virtual de discos restaurados</span><span class="sxs-lookup"><span data-stu-id="2fca3-236">Create a VM from restored disks</span></span>
<span data-ttu-id="2fca3-237">Depois de ter restaurado os discos Olá, use essas etapas toocreate e configurar a máquina virtual de saudação do disco.</span><span class="sxs-lookup"><span data-stu-id="2fca3-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="2fca3-238">toocreate criptografados VMs de discos restaurados, a função do Azure deve ter a ação de saudação do tooperform de permissão, **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="2fca3-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="2fca3-239">Se sua função não tem essa permissão, crie uma função personalizada com esta ação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="2fca3-240">Para obter mais informações, veja [Funções personalizadas no RBAC do Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="2fca3-241">Saudação de consulta restaurado propriedades do disco para obter detalhes do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="2fca3-242">Definir contexto do armazenamento do Azure hello e restaurar o arquivo de configuração JSON hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="2fca3-243">Use configuração de VM Olá JSON configuração arquivo toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="2fca3-244">Anexe o disco do sistema operacional hello e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="2fca3-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="2fca3-245">Dependendo da configuração de saudação das suas máquinas virtuais, clique nos cmdlets do respectivos de tooview Olá link relevante:</span><span class="sxs-lookup"><span data-stu-id="2fca3-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="2fca3-246">Máquinas virtuais não gerenciados, não criptografado</span><span class="sxs-lookup"><span data-stu-id="2fca3-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="2fca3-247">Máquinas virtuais não gerenciados, criptografados (BEK)</span><span class="sxs-lookup"><span data-stu-id="2fca3-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="2fca3-248">Máquinas virtuais não gerenciados, criptografados (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="2fca3-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="2fca3-249">Máquinas virtuais gerenciados, não criptografado</span><span class="sxs-lookup"><span data-stu-id="2fca3-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="2fca3-250">Máquinas virtuais gerenciadas, criptografados (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="2fca3-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="2fca3-251">VMs não criptografadas não gerenciadas</span><span class="sxs-lookup"><span data-stu-id="2fca3-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="2fca3-252">Use Olá exemplo a seguir para VMs não gerenciado, não criptografado.</span><span class="sxs-lookup"><span data-stu-id="2fca3-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="2fca3-253">VMs criptografadas e não gerenciadas (apenas BEK)</span><span class="sxs-lookup"><span data-stu-id="2fca3-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="2fca3-254">Para VMs não gerenciados, criptografadas (criptografadas usando apenas o BEK), você precisa cofre da chave secreta toohello toorestore Olá antes de você pode anexar discos.</span><span class="sxs-lookup"><span data-stu-id="2fca3-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="2fca3-255">Para obter mais informações, consulte o artigo Olá [restaurar uma máquina virtual criptografada de um ponto de recuperação de Backup do Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="2fca3-256">saudação de exemplo a seguir mostra como tooattach SO e discos de dados para criptografada VMs.</span><span class="sxs-lookup"><span data-stu-id="2fca3-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="2fca3-257">VMs criptografadas e não gerenciadas (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="2fca3-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="2fca3-258">Para VMs não gerenciados, criptografadas (criptografadas usando BEK e KEK), você precisa toorestore chave de saudação e cofre da chave secreta toohello antes de você pode anexar discos.</span><span class="sxs-lookup"><span data-stu-id="2fca3-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="2fca3-259">Para obter mais informações, consulte o artigo Olá [restaurar uma máquina virtual criptografada de um ponto de recuperação de Backup do Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="2fca3-260">saudação de exemplo a seguir mostra como tooattach SO e discos de dados para criptografada VMs.</span><span class="sxs-lookup"><span data-stu-id="2fca3-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="2fca3-261">VMs não criptografadas gerenciadas</span><span class="sxs-lookup"><span data-stu-id="2fca3-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="2fca3-262">Para VMs gerenciadas não criptografado, você precisa toocreate gerenciado discos do armazenamento de blob e, em seguida, anexar discos hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="2fca3-263">Para obter informações detalhadas, consulte o artigo Olá [anexar um disco de dados tooa VM do Windows usando o PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="2fca3-264">Olá, código de exemplo a seguir mostra como tooattach Olá discos de dados para VMs gerenciadas não criptografado.</span><span class="sxs-lookup"><span data-stu-id="2fca3-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="2fca3-265">VMs criptografadas e gerenciadas (BEK e KEK)</span><span class="sxs-lookup"><span data-stu-id="2fca3-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="2fca3-266">Para VMs criptografadas gerenciadas (criptografadas usando BEK e KEK), você precisa toocreate gerenciado discos do armazenamento de blob e, em seguida, anexar discos hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="2fca3-267">Para obter informações detalhadas, consulte o artigo Olá [anexar um disco de dados tooa VM do Windows usando o PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="2fca3-268">Olá código exemplo a seguir mostra como tooattach Olá discos de dados para VMs criptografadas gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="2fca3-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="2fca3-269">Defina as configurações de rede hello.</span><span class="sxs-lookup"><span data-stu-id="2fca3-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="2fca3-270">Crie a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fca3-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="2fca3-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fca3-271">Next steps</span></span>
<span data-ttu-id="2fca3-272">Se você preferir toouse PowerShell tooengage com os recursos do Azure, consulte o artigo do PowerShell hello, [implantar e gerenciar o Backup do Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="2fca3-273">Se você gerenciar backups do DPM, consulte o artigo Olá [implantar e gerenciar o Backup do DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="2fca3-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="2fca3-274">Esses dois artigos têm uma versão para implantações do Resource Manager, bem como para implantações do modelo Clássico.</span><span class="sxs-lookup"><span data-stu-id="2fca3-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
