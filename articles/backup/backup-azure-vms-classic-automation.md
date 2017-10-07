---
title: "aaaDeploy e gerenciar o backup de máquinas virtuais do Azure usando o PowerShell | Microsoft Docs"
description: Saiba como toodeploy e gerenciar o Backup do Azure usando o PowerShell.
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
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="23dea-103">Use AzureRM.Backup cmdlets tooback backup de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="23dea-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23dea-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="23dea-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="23dea-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="23dea-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="23dea-106">Este artigo mostra como toouse PowerShell do Azure para backup e recuperação de máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="23dea-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="23dea-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico.</span><span class="sxs-lookup"><span data-stu-id="23dea-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="23dea-108">Este artigo aborda o uso tooback de modelo de implantação Olá clássico o Cofre de Backup de tooa de dados.</span><span class="sxs-lookup"><span data-stu-id="23dea-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="23dea-109">Se você não tiver criado um cofre de Backup na sua assinatura, consulte a versão do Gerenciador de recursos de saudação deste artigo, [AzureRM.RecoveryServices.Backup Use cmdlets tooback backup de máquinas virtuais](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="23dea-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="23dea-110">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23dea-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23dea-111">Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="23dea-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="23dea-112">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="23dea-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="23dea-113">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="23dea-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="23dea-114">Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="23dea-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="23dea-115">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="23dea-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="23dea-116">Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="23dea-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="23dea-117">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="23dea-118">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="23dea-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="23dea-119">Conceitos</span><span class="sxs-lookup"><span data-stu-id="23dea-119">Concepts</span></span>
<span data-ttu-id="23dea-120">Este artigo fornece informações específica toohello cmdlets do PowerShell usado tooback backup de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="23dea-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="23dea-121">Para obter informações introdutórias sobre como proteger as VMs do Azure, confira [Planejar sua infraestrutura de backup de VM no Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23dea-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="23dea-122">Antes de começar, leia Olá [pré-requisitos](backup-azure-vms-prepare.md) toowork necessário com o Backup do Azure e hello [limitações](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) da solução atual de backup de VM hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="23dea-123">toouse PowerShell efetivamente, levar a uma hierarquia de saudação toounderstand do momento de objetos e de onde toostart.</span><span class="sxs-lookup"><span data-stu-id="23dea-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Hierarquia do Objeto](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="23dea-125">Olá dois fluxos mais importantes são habilitando a proteção para uma máquina virtual e restaurar dados de um ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="23dea-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="23dea-126">Olá foco deste artigo é toohelp se tornam adeptos trabalhando com tooenable de cmdlets do PowerShell Olá esses dois cenários.</span><span class="sxs-lookup"><span data-stu-id="23dea-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="23dea-127">Configuração e registro</span><span class="sxs-lookup"><span data-stu-id="23dea-127">Setup and Registration</span></span>
<span data-ttu-id="23dea-128">toobegin:</span><span class="sxs-lookup"><span data-stu-id="23dea-128">toobegin:</span></span>

1. <span data-ttu-id="23dea-129">[Baixe o PowerShell mais recente](https://github.com/Azure/azure-powershell/releases) (a versão mínima exigida é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="23dea-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="23dea-130">Localize os cmdlets do PowerShell do Azure Backup Olá disponíveis digitando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="23dea-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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

<span data-ttu-id="23dea-131">Olá tarefas de registro e configuração a seguir podem ser automatizadas com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="23dea-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="23dea-132">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="23dea-132">Create a backup vault</span></span>
* <span data-ttu-id="23dea-133">Registrando VMs Olá Olá serviço Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="23dea-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="23dea-134">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="23dea-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="23dea-135">Para clientes que usam o Backup do Azure para Olá primeira vez, você precisa tooregister hello Azure Backup provedor toobe usado com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="23dea-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="23dea-136">Isso pode ser feito executando o comando a seguir de saudação: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="23dea-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="23dea-137">Você pode criar um novo cofre de backup usando Olá **AzureRmBackupVault novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23dea-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="23dea-138">Cofre de backup Olá é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="23dea-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="23dea-139">Em um console do Azure PowerShell com privilégios elevados, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="23dea-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="23dea-140">Você pode obter uma lista de todos os cofres de backup de saudação em uma determinada assinatura usando Olá **AzureRmBackupVault Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23dea-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="23dea-141">É conveniente toostore Olá Cofre de backup objeto em uma variável.</span><span class="sxs-lookup"><span data-stu-id="23dea-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="23dea-142">objeto de cofre Olá é necessário como uma entrada para muitos cmdlets do Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="23dea-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="23dea-143">Registrando Olá VMs</span><span class="sxs-lookup"><span data-stu-id="23dea-143">Registering hello VMs</span></span>
<span data-ttu-id="23dea-144">a primeira etapa Olá para configuração de backup com o Backup do Azure é tooregister seu computador ou VM com um cofre de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="23dea-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="23dea-145">Olá **AzureRmBackupContainer registro** cmdlet obtém informações de entrada hello de uma máquina virtual IaaS do Azure e o registra cofre especificado hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="23dea-146">operação de registro Olá associa Olá máquina virtual do Azure com o Cofre de backup hello e rastreia Olá VM por meio do backup Olá de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="23dea-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="23dea-147">Registrando sua VM Olá serviço Backup do Azure cria um objeto de contêiner de nível superior.</span><span class="sxs-lookup"><span data-stu-id="23dea-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="23dea-148">Um contêiner normalmente contém vários itens que podem ser feitos, mas no caso de saudação de VMs haverá apenas um item de backup para o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="23dea-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="23dea-149">Fazer backup das VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="23dea-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="23dea-150">Crie uma política de proteção</span><span class="sxs-lookup"><span data-stu-id="23dea-150">Create a protection policy</span></span>
<span data-ttu-id="23dea-151">Não é obrigatório toocreate um novo backup de toostart de diretiva de proteção de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="23dea-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="23dea-152">cofre Olá vem com um 'política padrão' que pode ser usado tooquickly habilitar a proteção e editado posteriormente com detalhes de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="23dea-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="23dea-153">Você pode obter uma lista de políticas de saudação disponíveis no cofre hello usando Olá **AzureRmBackupProtectionPolicy Get** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="23dea-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="23dea-154">fuso horário de saudação do campo de BackupTime Olá no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="23dea-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="23dea-155">No entanto, quando o tempo de backup de saudação é mostrado no hello portal do Azure, o fuso horário de saudação é alinhado tooyour o sistema local junto com o deslocamento UTC do hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="23dea-156">Uma política de backup está associada a pelo menos uma política de retenção.</span><span class="sxs-lookup"><span data-stu-id="23dea-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="23dea-157">política de retenção Olá define quanto tempo um ponto de recuperação será mantido com o Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="23dea-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="23dea-158">Olá **AzureRmBackupRetentionPolicy novo** cria objetos do PowerShell que mantêm informações de política de retenção.</span><span class="sxs-lookup"><span data-stu-id="23dea-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="23dea-159">Esses objetos de política de retenção são usados como entradas toohello *New-AzureRmBackupProtectionPolicy* cmdlet, ou diretamente com hello *AzureRmBackupProtection habilitar* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23dea-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="23dea-160">Uma política de backup define quando e com que frequência hello de um item é feito backup.</span><span class="sxs-lookup"><span data-stu-id="23dea-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="23dea-161">Olá **AzureRmBackupProtectionPolicy novo** cmdlet cria um objeto do PowerShell que contém informações de política de backup.</span><span class="sxs-lookup"><span data-stu-id="23dea-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="23dea-162">Olá política de backup é usada como uma entrada toohello *AzureRmBackupProtection habilitar* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23dea-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="23dea-163">Habilitar proteção</span><span class="sxs-lookup"><span data-stu-id="23dea-163">Enable protection</span></span>
<span data-ttu-id="23dea-164">Habilitar a proteção envolve dois objetos - Olá Item e Olá política e ambos os toohello de toobelong necessário mesmo cofre.</span><span class="sxs-lookup"><span data-stu-id="23dea-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="23dea-165">Depois que a política Olá foi associada ao item Olá, fluxo de trabalho de backup Olá será iniciada na agenda definida hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="23dea-166">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="23dea-166">Initial backup</span></span>
<span data-ttu-id="23dea-167">agendamento de backup Olá cuidará de fazer a cópia inicial completa Olá item hello e Olá incrementais para os backups subsequentes hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="23dea-168">No entanto, se você quiser tooforce saudação inicial backup toohappen em um determinado tempo ou até mesmo imediatamente, em seguida, usar Olá **AzureRmBackupItem Backup** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="23dea-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="23dea-169">Olá fuso horário de saudação StartTime e EndTime campos mostrados no PowerShell é UTC.</span><span class="sxs-lookup"><span data-stu-id="23dea-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="23dea-170">No entanto, quando informações semelhantes Olá são exibidas no hello portal do Azure, o fuso horário de saudação é alinhado tooyour o relógio do sistema local.</span><span class="sxs-lookup"><span data-stu-id="23dea-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="23dea-171">Monitoramento de um trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="23dea-171">Monitoring a backup job</span></span>
<span data-ttu-id="23dea-172">A maioria das operações de longa duração no Backup do Azure são modeladas como um trabalho.</span><span class="sxs-lookup"><span data-stu-id="23dea-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="23dea-173">Isso torna fácil tootrack andamento sem ter que tookeep Olá Abrir portal do Azure em todos os momentos.</span><span class="sxs-lookup"><span data-stu-id="23dea-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="23dea-174">tooget Olá último status de um trabalho em andamento, use Olá **AzureRmBackupJob Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23dea-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="23dea-175">Em vez de sondagem esses trabalhos para conclusão - que é um código adicional desnecessário - é hello mais simples de toouse **AzureRmBackupJob espera** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23dea-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="23dea-176">Quando usado em um script, Olá cmdlet irá pausar execução Olá até Olá trabalho for concluído ou Olá especificado, o valor de tempo limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="23dea-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="23dea-177">Restaurar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="23dea-177">Restore an Azure VM</span></span>
<span data-ttu-id="23dea-178">Dados de pedidos toorestore backup, você precisa tooidentify Olá backup Item e Olá ponto de recuperação que contém dados de point-in-time de saudação.</span><span class="sxs-lookup"><span data-stu-id="23dea-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="23dea-179">Essas informações são fornecidas toohello AzureRmBackupItem restauração cmdlet tooinitiate uma restauração de dados de conta do cliente do hello cofre toohello.</span><span class="sxs-lookup"><span data-stu-id="23dea-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="23dea-180">Selecione Olá VM</span><span class="sxs-lookup"><span data-stu-id="23dea-180">Select hello VM</span></span>
<span data-ttu-id="23dea-181">objeto do PowerShell Olá tooget que identifica Olá direito de fazer backup do Item, você precisa toostart de saudação contêiner no cofre Olá e abaixo da hierarquia de objetos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="23dea-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="23dea-182">contêiner de saudação tooselect que representa o hello VM, use Olá **Get-AzureRmBackupContainer** cmdlet e redirecione que toohello **AzureRmBackupItem Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23dea-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="23dea-183">Escolha um ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="23dea-183">Choose a recovery point</span></span>
<span data-ttu-id="23dea-184">Agora você pode listar todos os pontos de recuperação hello para fazer backup do item hello usando Olá **AzureRmBackupRecoveryPoint Get** cmdlet e escolha Olá toorestore de ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="23dea-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="23dea-185">Normalmente os usuários escolher hello mais recente *AppConsistent* ponto na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="23dea-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="23dea-186">variável de saudação ```$rp``` é uma matriz de pontos de recuperação para Olá selecionado fazer backup do item, classificado na ordem inversa de tempo - ponto de recuperação mais recente hello está no índice 0.</span><span class="sxs-lookup"><span data-stu-id="23dea-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="23dea-187">Use o padrão matriz do PowerShell a indexação de ponto de recuperação toopick hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="23dea-188">Por exemplo: ```$rp[0]``` selecionará o último ponto de recuperação hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="23dea-189">Restaurando discos</span><span class="sxs-lookup"><span data-stu-id="23dea-189">Restoring disks</span></span>
<span data-ttu-id="23dea-190">Há uma diferença importante entre as operações de restauração de saudação feito por meio de saudação portal do Azure e do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="23dea-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="23dea-191">Com o PowerShell, a operação de restauração de saudação para a restauração de discos hello e informações de configuração de ponto de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="23dea-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="23dea-192">Ele não cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23dea-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="23dea-193">Olá AzureRmBackupItem de restauração não criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23dea-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="23dea-194">Restaura apenas os discos Olá toohello especificou a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="23dea-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="23dea-195">Isso não é Olá mesmo comportamento, você terá de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23dea-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="23dea-196">Você pode obter os detalhes de Olá Olá da operação de restauração usando Olá **AzureRmBackupJobDetails Get** cmdlet depois de concluído o trabalho de restauração hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="23dea-197">Olá *ErrorDetails* propriedade terá informações Olá necessário toorebuild Olá VM.</span><span class="sxs-lookup"><span data-stu-id="23dea-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="23dea-198">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="23dea-198">Build hello VM</span></span>
<span data-ttu-id="23dea-199">Saudação de construção VM sem discos Olá restaurado pode ser feita usando os cmdlets de PowerShell do Azure Service Management antigos hello, Olá novos modelos do Gerenciador de recursos do Azure ou por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="23dea-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="23dea-200">Um exemplo rápido, mostraremos como tooget lá usando os cmdlets de gerenciamento de serviços do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="23dea-201">Para obter mais informações sobre como toobuild uma VM de discos Olá restaurado, leia sobre Olá cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="23dea-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="23dea-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="23dea-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="23dea-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="23dea-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="23dea-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="23dea-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="23dea-205">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="23dea-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="23dea-206">1. Obter status de conclusão de saudação do trabalho subtarefas</span><span class="sxs-lookup"><span data-stu-id="23dea-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="23dea-207">status de conclusão de saudação tootrack de subtarefas individuais, você pode usar o hello **AzureRmBackupJobDetails Get** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="23dea-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="23dea-208">2. Criar um relatório diário/semanal de trabalhos de backup</span><span class="sxs-lookup"><span data-stu-id="23dea-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="23dea-209">Normalmente, os administradores querem tooknow quais trabalhos de backup foi executados no hello últimas 24 horas, o status de saudação desses trabalhos de backup.</span><span class="sxs-lookup"><span data-stu-id="23dea-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="23dea-210">Além disso, quantidade de saudação de dados transferidos oferece aos administradores uma maneira tooestimate o uso de dados mensal.</span><span class="sxs-lookup"><span data-stu-id="23dea-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="23dea-211">abaixo de script Hello extrai dados brutos de saudação do hello serviço Backup do Azure e exibe informações de saudação no console do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="23dea-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

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
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
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

<span data-ttu-id="23dea-212">Se você quiser tooadd a saída de relatório toothis recursos de criação de gráficos, saiba mais na postagem de blog do TechNet Olá [gráficos com o PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="23dea-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="23dea-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23dea-213">Next steps</span></span>
<span data-ttu-id="23dea-214">Se você preferir usar o PowerShell tooengage com os recursos do Azure, consulte artigo do PowerShell Olá para proteger o Windows Server, [implantar e gerenciar o Backup do Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="23dea-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="23dea-215">Há também um artigo do PowerShell para gerenciar os backups do DPM, [Implantar e Gerenciar o Backup do DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="23dea-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="23dea-216">Esses dois artigos têm uma versão para implantações do Gerenciador de Recursos, bem como para implantações do modelo Clássico.</span><span class="sxs-lookup"><span data-stu-id="23dea-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
