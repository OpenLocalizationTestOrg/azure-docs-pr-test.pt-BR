---
title: Implantar e gerenciar o backup das VMs do Azure usando o PowerShell | Microsoft Docs
description: Saiba como implantar e gerenciar o Backup do Azure usando o PowerShell.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f0f06adb8177ce2d17aa0b40666470279c04e22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="03296-103">Usar cmdlets AzureRM.Backup para fazer backup de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="03296-103">Use AzureRM.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03296-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="03296-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="03296-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="03296-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="03296-106">Este artigo mostra como usar o Azure PowerShell para backup e recuperação de VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="03296-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="03296-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="03296-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="03296-108">Este artigo aborda o uso do modelo de implantação Clássico para fazer backup de dados em um Cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="03296-108">This article covers using the Classic deployment model to back up data to a Backup vault.</span></span> <span data-ttu-id="03296-109">Se você ainda não criou um Cofre de backup em sua assinatura, consulte a versão do Resource Manager deste artigo [Usar os cmdlets AzureRM.RecoveryServices.Backup para fazer backup de máquinas virtuais](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="03296-109">If you have not created a Backup vault in your subscription, see the Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="03296-110">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="03296-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03296-111">Agora você pode atualizar os cofres de Backup para cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-111">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="03296-112">Para obter detalhes, veja o artigo [Atualizar um cofre de Backup para um cofre dos Serviços de Recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="03296-112">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="03296-113">A Microsoft incentiva você a atualizar os cofres de Backup para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-113">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="03296-114">Após 15 de outubro de 2017, você não poderá usar o PowerShell para criar os Cofres do Backup.</span><span class="sxs-lookup"><span data-stu-id="03296-114">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="03296-115">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="03296-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="03296-116">Todos os Cofres do Backup restantes serão atualizados automaticamente para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-116">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="03296-117">Você não poderá acessar os dados de backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="03296-117">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="03296-118">Em vez disso, use o portal do Azure para acessar os dados de backup nos cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-118">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="03296-119">Conceitos</span><span class="sxs-lookup"><span data-stu-id="03296-119">Concepts</span></span>
<span data-ttu-id="03296-120">Este artigo fornece informações específicas para os cmdlets do PowerShell usados para fazer backup de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="03296-120">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span></span> <span data-ttu-id="03296-121">Para obter informações introdutórias sobre como proteger as VMs do Azure, confira [Planejar sua infraestrutura de backup de VM no Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03296-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="03296-122">Antes de começar, leia os [pré-requisitos](backup-azure-vms-prepare.md) necessários para trabalhar com o Backup do Azure e as [limitações](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) da solução de backup da VM atual.</span><span class="sxs-lookup"><span data-stu-id="03296-122">Before you start, read the [prerequisites](backup-azure-vms-prepare.md) required to work with Azure Backup, and the [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of the current VM backup solution.</span></span>
>
>

<span data-ttu-id="03296-123">Para usar efetivamente o PowerShell, reserve algum tempo para entender a hierarquia de objetos e de onde começar.</span><span class="sxs-lookup"><span data-stu-id="03296-123">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span></span>

![Hierarquia do Objeto](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="03296-125">Os dois fluxos mais importantes são habilitar a proteção para uma VM e restaurar dados de um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-125">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="03296-126">O foco deste artigo é ajudar você a se tornar um especialista em trabalhar com os cmdlets do PowerShell para habilitar esses dois cenários.</span><span class="sxs-lookup"><span data-stu-id="03296-126">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="03296-127">Configuração e registro</span><span class="sxs-lookup"><span data-stu-id="03296-127">Setup and Registration</span></span>
<span data-ttu-id="03296-128">Para começar:</span><span class="sxs-lookup"><span data-stu-id="03296-128">To begin:</span></span>

1. <span data-ttu-id="03296-129">[Baixe o PowerShell mais recente](https://github.com/Azure/azure-powershell/releases) (a versão mínima exigida é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="03296-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="03296-130">Localize os cmdlets do PowerShell do Backup do Azure disponíveis digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="03296-130">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

<span data-ttu-id="03296-131">As seguintes tarefas de configuração e de registro podem ser automatizadas com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="03296-131">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="03296-132">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="03296-132">Create a backup vault</span></span>
* <span data-ttu-id="03296-133">Registrando as VMs no serviço de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="03296-133">Registering the VMs with the Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="03296-134">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="03296-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="03296-135">Para clientes usando o Backup do Azure pela primeira vez, você precisa registrar o provedor de Backup do Azure para ser usado com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="03296-135">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="03296-136">Isso pode ser feito com a execução do seguinte comando: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="03296-136">This can be done by running the following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="03296-137">Você pode criar um novo cofre de backup usando o cmdlet **New-AzureRmBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="03296-137">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="03296-138">O cofre de backup é um recurso do ARM e, portanto, você precisará colocá-lo em um Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="03296-138">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="03296-139">Em um console do Azure PowerShell com privilégios elevados, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="03296-139">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="03296-140">É possível obter uma lista de todos os cofres de backup em uma determinada assinatura usando o cmdlet **Get-AzureRmBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="03296-140">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="03296-141">É conveniente armazenar o objeto cofre de backup em uma variável.</span><span class="sxs-lookup"><span data-stu-id="03296-141">It is convenient to store the backup vault object into a variable.</span></span> <span data-ttu-id="03296-142">O objeto cofre é necessário como uma entrada para vários cmdlets do Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="03296-142">The vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-the-vms"></a><span data-ttu-id="03296-143">Registrando as VMs</span><span class="sxs-lookup"><span data-stu-id="03296-143">Registering the VMs</span></span>
<span data-ttu-id="03296-144">A primeira etapa para configurar o backup com o Backup do Azure é registrar seu computador ou VM em um cofre de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="03296-144">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="03296-145">O cmdlet **Register-AzureRmBackupContainer** usa as informações de entrada de uma máquina virtual IaaS do Azure e as registra no cofre especificado.</span><span class="sxs-lookup"><span data-stu-id="03296-145">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span></span> <span data-ttu-id="03296-146">A operação de registro associa a máquina virtual do Azure com o Cofre de backup e controla a VM por meio do ciclo de vida do backup.</span><span class="sxs-lookup"><span data-stu-id="03296-146">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span></span>

<span data-ttu-id="03296-147">Registrar sua VM com o serviço de Backup do Azure cria um objeto de contêiner de nível superior.</span><span class="sxs-lookup"><span data-stu-id="03296-147">Registering your VM with the Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="03296-148">Um contêiner normalmente contém vários itens que podem ser copiados, mas no caso de VMs haverá apenas um item de backup para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="03296-148">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="03296-149">Fazer backup das VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="03296-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="03296-150">Crie uma política de proteção</span><span class="sxs-lookup"><span data-stu-id="03296-150">Create a protection policy</span></span>
<span data-ttu-id="03296-151">Não é obrigatório criar uma nova política de proteção para iniciar o backup das suas VMs.</span><span class="sxs-lookup"><span data-stu-id="03296-151">It is not mandatory to create a new protection policy to start backup of your VMs.</span></span> <span data-ttu-id="03296-152">O cofre vem com uma 'Política Padrão' que pode ser usado para habilitar a proteção rapidamente e editada posteriormente com os detalhes à direita.</span><span class="sxs-lookup"><span data-stu-id="03296-152">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span></span> <span data-ttu-id="03296-153">Você pode obter uma lista das políticas disponíveis no cofre usando o cmdlet **Get-AzureRmBackupProtectionPolicy** :</span><span class="sxs-lookup"><span data-stu-id="03296-153">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="03296-154">O fuso horário do campo BackupTime no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="03296-154">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="03296-155">No entanto, quando o tempo de backup é mostrado no portal do Azure, o fuso horário é alinhado ao sistema local com a diferença UTC.</span><span class="sxs-lookup"><span data-stu-id="03296-155">However, when the backup time is shown in the Azure portal, the timezone is aligned to your local system along with the UTC offset.</span></span>
>
>

<span data-ttu-id="03296-156">Uma política de backup está associada a pelo menos uma política de retenção.</span><span class="sxs-lookup"><span data-stu-id="03296-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="03296-157">A política de retenção define quanto tempo um ponto de recuperação é mantido pelo Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="03296-157">The retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="03296-158">O cmdlet **New-AzureRmBackupRetentionPolicy** cria objetos do PowerShell que armazenam informações da política de retenção.</span><span class="sxs-lookup"><span data-stu-id="03296-158">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="03296-159">Esses objetos da política de retenção são usados como entradas para o cmdlet *New-AzureRmBackupProtectionPolicy* ou diretamente com o cmdlet *Enable AzureRmBackupProtection*.</span><span class="sxs-lookup"><span data-stu-id="03296-159">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="03296-160">Uma política de backup define quando e com que frequência será feito o backup de um item.</span><span class="sxs-lookup"><span data-stu-id="03296-160">A backup policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="03296-161">O cmdlet **New-AzureRmBackupProtectionPolicy** cria um objeto do PowerShell que mantém as informações da política de backup.</span><span class="sxs-lookup"><span data-stu-id="03296-161">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="03296-162">A política de backup é usada como entrada para o cmdlet *Enable-AzureRmBackupProtection* .</span><span class="sxs-lookup"><span data-stu-id="03296-162">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="03296-163">Habilitar proteção</span><span class="sxs-lookup"><span data-stu-id="03296-163">Enable protection</span></span>
<span data-ttu-id="03296-164">Habilitar a proteção envolve dois objetos - o Item e a Política, e ambos precisam pertencer ao mesmo cofre.</span><span class="sxs-lookup"><span data-stu-id="03296-164">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span></span> <span data-ttu-id="03296-165">Depois que a política é associada ao item, o fluxo de trabalho de backup será iniciado no agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="03296-165">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="03296-166">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="03296-166">Initial backup</span></span>
<span data-ttu-id="03296-167">O agendamento de backup se encarregará de fazer a cópia inicial completa do item e a cópia incremental para os backups subsequentes.</span><span class="sxs-lookup"><span data-stu-id="03296-167">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span></span> <span data-ttu-id="03296-168">No entanto, se desejar forçar o backup inicial para que ele ocorra em um determinado momento ou até mesmo imediatamente, use o cmdlet **Backup-AzureRmBackupItem** :</span><span class="sxs-lookup"><span data-stu-id="03296-168">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="03296-169">O fuso horário dos campos StartTime e EndTime mostrado no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="03296-169">The timezone of the StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="03296-170">No entanto, quando as informações semelhantes são mostradas no portal do Azure, o fuso horário é alinhado ao relógio do seu sistema local.</span><span class="sxs-lookup"><span data-stu-id="03296-170">However, when the similar information is shown in the Azure portal, the timezone is aligned to your local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="03296-171">Monitoramento de um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="03296-171">Monitoring a backup job</span></span>
<span data-ttu-id="03296-172">A maioria das operações de longa duração no Backup do Azure são modeladas como um trabalho.</span><span class="sxs-lookup"><span data-stu-id="03296-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="03296-173">Isso facilita acompanhar o andamento sem a necessidade de manter o portal do Azure aberto em todos os momentos.</span><span class="sxs-lookup"><span data-stu-id="03296-173">This makes it easy to track progress without having to keep the Azure portal open at all times.</span></span>

<span data-ttu-id="03296-174">Para obter o último status de um trabalho em andamento, use o cmdlet **Get-AzureRmBackupJob** .</span><span class="sxs-lookup"><span data-stu-id="03296-174">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="03296-175">Em vez de sondar esses trabalhos para conclusão – o que é um código adicional desnecessário - é mais simples usar o cmdlet **Wait-AzureRmBackupJob** .</span><span class="sxs-lookup"><span data-stu-id="03296-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="03296-176">Quando usado em um script, o cmdlet fará uma pausa na execução até que o trabalho seja concluído ou o valor de tempo limite especificado seja atingido.</span><span class="sxs-lookup"><span data-stu-id="03296-176">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="03296-177">Restaurar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="03296-177">Restore an Azure VM</span></span>
<span data-ttu-id="03296-178">Para restaurar dados de backup, é necessário identificar o Item de backup e o ponto de recuperação que mantém os dados pontuais.</span><span class="sxs-lookup"><span data-stu-id="03296-178">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span></span> <span data-ttu-id="03296-179">Essas informações são fornecidas pelo cmdlet Restore-AzureRmBackupItem para iniciar uma restauração de dados do cofre para a conta do cliente.</span><span class="sxs-lookup"><span data-stu-id="03296-179">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="03296-180">Selecione a VM</span><span class="sxs-lookup"><span data-stu-id="03296-180">Select the VM</span></span>
<span data-ttu-id="03296-181">Para obter o objeto do PowerShell que identifica o item correto de backup, você precisa começar do contêiner no cofre e descer para baixo na hierarquia de objetos.</span><span class="sxs-lookup"><span data-stu-id="03296-181">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="03296-182">Para selecionar o contêiner que representa a VM, use o cmdlet **Get-AzureRmBackupContainer** e redirecione para o cmdlet **Get-AzureRmBackupItem**.</span><span class="sxs-lookup"><span data-stu-id="03296-182">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="03296-183">Escolha um ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="03296-183">Choose a recovery point</span></span>
<span data-ttu-id="03296-184">Agora você pode listar todos os pontos de recuperação para o item de backup usando o cmdlet **Get-AzureRmBackupRecoveryPoint** e escolher o ponto de recuperação para restaurar.</span><span class="sxs-lookup"><span data-stu-id="03296-184">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span></span> <span data-ttu-id="03296-185">Normalmente, os usuários escolhem o ponto *AppConsistent* mais recente na lista.</span><span class="sxs-lookup"><span data-stu-id="03296-185">Typically users pick the most recent *AppConsistent* point in the list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="03296-186">A variável ```$rp``` é uma matriz de pontos de recuperação para o item de backup selecionado, classificados na ordem inversa de tempo - o último ponto de recuperação está no índice 0.</span><span class="sxs-lookup"><span data-stu-id="03296-186">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span></span> <span data-ttu-id="03296-187">Use a indexação de matriz padrão do PowerShell para selecionar o ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-187">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="03296-188">Por exemplo: ```$rp[0]``` selecionará o último ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-188">For example: ```$rp[0]``` will select the latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="03296-189">Restaurando discos</span><span class="sxs-lookup"><span data-stu-id="03296-189">Restoring disks</span></span>
<span data-ttu-id="03296-190">Há uma diferença importante entre as operações de restauração feitas por meio do portal do Azure e por meio do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03296-190">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="03296-191">Com o PowerShell, a operação de restauração para na restauração de discos e configura as informações do ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="03296-191">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span></span> <span data-ttu-id="03296-192">Ele não cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03296-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="03296-193">O Restore-AzureRmBackupItem não cria uma VM.</span><span class="sxs-lookup"><span data-stu-id="03296-193">The Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="03296-194">Ele restaura apenas os discos para a conta de armazenamento especificada.</span><span class="sxs-lookup"><span data-stu-id="03296-194">It only restores the disks to the specified storage account.</span></span> <span data-ttu-id="03296-195">Este não é o mesmo comportamento que você verá no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="03296-195">This is not the same behavior you will experience in the Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="03296-196">Você pode obter os detalhes da operação de restauração usando o cmdlet **Get-AzureRmBackupJobDetails** depois que o trabalho de restauração for concluído.</span><span class="sxs-lookup"><span data-stu-id="03296-196">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span></span> <span data-ttu-id="03296-197">A propriedade *ErrorDetails* terá as informações necessárias para recompilar a VM.</span><span class="sxs-lookup"><span data-stu-id="03296-197">The *ErrorDetails* property will have the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a><span data-ttu-id="03296-198">Compilar a VM</span><span class="sxs-lookup"><span data-stu-id="03296-198">Build the VM</span></span>
<span data-ttu-id="03296-199">A criação da VM por meio dos discos restaurados pode ser realizada com os cmdlets do PowerShell do Azure Service Manager mais antigos, os novos modelos de Azure Resource Manager, ou até mesmo usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="03296-199">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span></span> <span data-ttu-id="03296-200">Em um exemplo rápido, mostraremos como chegar lá usando os cmdlets do Azure Service Manager.</span><span class="sxs-lookup"><span data-stu-id="03296-200">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span></span>

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

<span data-ttu-id="03296-201">Para saber mais sobre como criar uma VM por meio dos discos restaurados, leia sobre os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="03296-201">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span></span>

* [<span data-ttu-id="03296-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="03296-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="03296-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="03296-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="03296-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="03296-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="03296-205">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="03296-205">Code samples</span></span>
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a><span data-ttu-id="03296-206">1. Obter o status de conclusão das subtarefas do trabalho</span><span class="sxs-lookup"><span data-stu-id="03296-206">1. Get the completion status of job sub-tasks</span></span>
<span data-ttu-id="03296-207">Para acompanhar o status de conclusão de subtarefas individuais, é possível usar o cmdlet **Get-AzureRmBackupJobDetails** :</span><span class="sxs-lookup"><span data-stu-id="03296-207">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="03296-208">2. Criar um relatório diário/semanal de trabalhos de backup</span><span class="sxs-lookup"><span data-stu-id="03296-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="03296-209">Os administradores geralmente querem saber se os trabalhos de backup foram executados nas últimas 24 horas, o status desses trabalhos de backup.</span><span class="sxs-lookup"><span data-stu-id="03296-209">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span></span> <span data-ttu-id="03296-210">Além disso, a quantidade de dados transferidos fornece aos administradores uma maneira de estimar sua utilização mensal de dados.</span><span class="sxs-lookup"><span data-stu-id="03296-210">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span></span> <span data-ttu-id="03296-211">O script a seguir extrai os dados brutos do serviço do Azure Backup e exibe as informações no console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03296-211">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span></span>

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -To $enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for the last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract the information for the reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

<span data-ttu-id="03296-212">Se você deseja adicionar recursos de gráficos à saída do relatório, saiba mais na postagem do blog do TechNet em [Gráficos com o PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="03296-212">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="03296-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03296-213">Next steps</span></span>
<span data-ttu-id="03296-214">Se você preferir usar o PowerShell para interagir com os recursos do Azure, confira o artigo do PowerShell para proteger o Windows Server, [Implantar e Gerenciar o Backup do Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="03296-214">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="03296-215">Há também um artigo do PowerShell para gerenciar os backups do DPM, [Implantar e Gerenciar o Backup do DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="03296-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="03296-216">Esses dois artigos têm uma versão para implantações do Gerenciador de Recursos, bem como para implantações do modelo Clássico.</span><span class="sxs-lookup"><span data-stu-id="03296-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
