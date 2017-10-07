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
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Use AzureRM.Backup cmdlets tooback backup de máquinas virtuais
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](backup-azure-vms-automation.md)
> * [Clássico](backup-azure-vms-classic-automation.md)
>
>

Este artigo mostra como toouse PowerShell do Azure para backup e recuperação de máquinas virtuais do Azure. O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: Resource Manager e Clássico. Este artigo aborda o uso tooback de modelo de implantação Olá clássico o Cofre de Backup de tooa de dados. Se você não tiver criado um cofre de Backup na sua assinatura, consulte a versão do Gerenciador de recursos de saudação deste artigo, [AzureRM.RecoveryServices.Backup Use cmdlets tooback backup de máquinas virtuais](backup-azure-vms-automation.md). A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

> [!IMPORTANT]
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup. **Em 1º de novembro de 2017**:
>- Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

## <a name="concepts"></a>Conceitos
Este artigo fornece informações específica toohello cmdlets do PowerShell usado tooback backup de máquinas virtuais. Para obter informações introdutórias sobre como proteger as VMs do Azure, confira [Planejar sua infraestrutura de backup de VM no Azure](backup-azure-vms-introduction.md).

> [!NOTE]
> Antes de começar, leia Olá [pré-requisitos](backup-azure-vms-prepare.md) toowork necessário com o Backup do Azure e hello [limitações](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) da solução atual de backup de VM hello.
>
>

toouse PowerShell efetivamente, levar a uma hierarquia de saudação toounderstand do momento de objetos e de onde toostart.

![Hierarquia do Objeto](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Olá dois fluxos mais importantes são habilitando a proteção para uma máquina virtual e restaurar dados de um ponto de recuperação. Olá foco deste artigo é toohelp se tornam adeptos trabalhando com tooenable de cmdlets do PowerShell Olá esses dois cenários.

## <a name="setup-and-registration"></a>Configuração e registro
toobegin:

1. [Baixe o PowerShell mais recente](https://github.com/Azure/azure-powershell/releases) (a versão mínima exigida é: 1.0.0)
2. Localize os cmdlets do PowerShell do Azure Backup Olá disponíveis digitando o comando a seguir de saudação:

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

Olá tarefas de registro e configuração a seguir podem ser automatizadas com o PowerShell:

* Criar um cofre de backup
* Registrando VMs Olá Olá serviço Backup do Azure

### <a name="create-a-backup-vault"></a>Criar um cofre de backup
> [!WARNING]
> Para clientes que usam o Backup do Azure para Olá primeira vez, você precisa tooregister hello Azure Backup provedor toobe usado com sua assinatura. Isso pode ser feito executando o comando a seguir de saudação: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"
>
>

Você pode criar um novo cofre de backup usando Olá **AzureRmBackupVault novo** cmdlet. Cofre de backup Olá é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos. Em um console do Azure PowerShell com privilégios elevados, execute Olá comandos a seguir:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Você pode obter uma lista de todos os cofres de backup de saudação em uma determinada assinatura usando Olá **AzureRmBackupVault Get** cmdlet.

> [!NOTE]
> É conveniente toostore Olá Cofre de backup objeto em uma variável. objeto de cofre Olá é necessário como uma entrada para muitos cmdlets do Backup do Azure.
>
>

### <a name="registering-hello-vms"></a>Registrando Olá VMs
a primeira etapa Olá para configuração de backup com o Backup do Azure é tooregister seu computador ou VM com um cofre de Backup do Azure. Olá **AzureRmBackupContainer registro** cmdlet obtém informações de entrada hello de uma máquina virtual IaaS do Azure e o registra cofre especificado hello. operação de registro Olá associa Olá máquina virtual do Azure com o Cofre de backup hello e rastreia Olá VM por meio do backup Olá de ciclo de vida.

Registrando sua VM Olá serviço Backup do Azure cria um objeto de contêiner de nível superior. Um contêiner normalmente contém vários itens que podem ser feitos, mas no caso de saudação de VMs haverá apenas um item de backup para o contêiner de saudação.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Fazer backup das VMs do Azure
### <a name="create-a-protection-policy"></a>Crie uma política de proteção
Não é obrigatório toocreate um novo backup de toostart de diretiva de proteção de suas VMs. cofre Olá vem com um 'política padrão' que pode ser usado tooquickly habilitar a proteção e editado posteriormente com detalhes de saudação à direita. Você pode obter uma lista de políticas de saudação disponíveis no cofre hello usando Olá **AzureRmBackupProtectionPolicy Get** cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> fuso horário de saudação do campo de BackupTime Olá no PowerShell é UTC. No entanto, quando o tempo de backup de saudação é mostrado no hello portal do Azure, o fuso horário de saudação é alinhado tooyour o sistema local junto com o deslocamento UTC do hello.
>
>

Uma política de backup está associada a pelo menos uma política de retenção. política de retenção Olá define quanto tempo um ponto de recuperação será mantido com o Azure Backup. Olá **AzureRmBackupRetentionPolicy novo** cria objetos do PowerShell que mantêm informações de política de retenção. Esses objetos de política de retenção são usados como entradas toohello *New-AzureRmBackupProtectionPolicy* cmdlet, ou diretamente com hello *AzureRmBackupProtection habilitar* cmdlet.

Uma política de backup define quando e com que frequência hello de um item é feito backup. Olá **AzureRmBackupProtectionPolicy novo** cmdlet cria um objeto do PowerShell que contém informações de política de backup. Olá política de backup é usada como uma entrada toohello *AzureRmBackupProtection habilitar* cmdlet.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Habilitar proteção
Habilitar a proteção envolve dois objetos - Olá Item e Olá política e ambos os toohello de toobelong necessário mesmo cofre. Depois que a política Olá foi associada ao item Olá, fluxo de trabalho de backup Olá será iniciada na agenda definida hello.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>Backup inicial
agendamento de backup Olá cuidará de fazer a cópia inicial completa Olá item hello e Olá incrementais para os backups subsequentes hello. No entanto, se você quiser tooforce saudação inicial backup toohappen em um determinado tempo ou até mesmo imediatamente, em seguida, usar Olá **AzureRmBackupItem Backup** cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> Olá fuso horário de saudação StartTime e EndTime campos mostrados no PowerShell é UTC. No entanto, quando informações semelhantes Olá são exibidas no hello portal do Azure, o fuso horário de saudação é alinhado tooyour o relógio do sistema local.
>
>

### <a name="monitoring-a-backup-job"></a>Monitoramento de um trabalho de backup
A maioria das operações de longa duração no Backup do Azure são modeladas como um trabalho. Isso torna fácil tootrack andamento sem ter que tookeep Olá Abrir portal do Azure em todos os momentos.

tooget Olá último status de um trabalho em andamento, use Olá **AzureRmBackupJob Get** cmdlet.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

Em vez de sondagem esses trabalhos para conclusão - que é um código adicional desnecessário - é hello mais simples de toouse **AzureRmBackupJob espera** cmdlet. Quando usado em um script, Olá cmdlet irá pausar execução Olá até Olá trabalho for concluído ou Olá especificado, o valor de tempo limite é atingido.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Restaurar uma VM do Azure
Dados de pedidos toorestore backup, você precisa tooidentify Olá backup Item e Olá ponto de recuperação que contém dados de point-in-time de saudação. Essas informações são fornecidas toohello AzureRmBackupItem restauração cmdlet tooinitiate uma restauração de dados de conta do cliente do hello cofre toohello.

### <a name="select-hello-vm"></a>Selecione Olá VM
objeto do PowerShell Olá tooget que identifica Olá direito de fazer backup do Item, você precisa toostart de saudação contêiner no cofre Olá e abaixo da hierarquia de objetos de trabalho. contêiner de saudação tooselect que representa o hello VM, use Olá **Get-AzureRmBackupContainer** cmdlet e redirecione que toohello **AzureRmBackupItem Get** cmdlet.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Escolha um ponto de recuperação
Agora você pode listar todos os pontos de recuperação hello para fazer backup do item hello usando Olá **AzureRmBackupRecoveryPoint Get** cmdlet e escolha Olá toorestore de ponto de recuperação. Normalmente os usuários escolher hello mais recente *AppConsistent* ponto na lista de saudação.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

variável de saudação ```$rp``` é uma matriz de pontos de recuperação para Olá selecionado fazer backup do item, classificado na ordem inversa de tempo - ponto de recuperação mais recente hello está no índice 0. Use o padrão matriz do PowerShell a indexação de ponto de recuperação toopick hello. Por exemplo: ```$rp[0]``` selecionará o último ponto de recuperação hello.

### <a name="restoring-disks"></a>Restaurando discos
Há uma diferença importante entre as operações de restauração de saudação feito por meio de saudação portal do Azure e do PowerShell do Azure. Com o PowerShell, a operação de restauração de saudação para a restauração de discos hello e informações de configuração de ponto de recuperação de saudação. Ele não cria uma máquina virtual.

> [!WARNING]
> Olá AzureRmBackupItem de restauração não criar uma máquina virtual. Restaura apenas os discos Olá toohello especificou a conta de armazenamento. Isso não é Olá mesmo comportamento, você terá de saudação portal do Azure.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

Você pode obter os detalhes de Olá Olá da operação de restauração usando Olá **AzureRmBackupJobDetails Get** cmdlet depois de concluído o trabalho de restauração hello. Olá *ErrorDetails* propriedade terá informações Olá necessário toorebuild Olá VM.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Criar hello VM
Saudação de construção VM sem discos Olá restaurado pode ser feita usando os cmdlets de PowerShell do Azure Service Management antigos hello, Olá novos modelos do Gerenciador de recursos do Azure ou por meio de saudação portal do Azure. Um exemplo rápido, mostraremos como tooget lá usando os cmdlets de gerenciamento de serviços do Azure hello.

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

Para obter mais informações sobre como toobuild uma VM de discos Olá restaurado, leia sobre Olá cmdlets a seguir:

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Exemplos de código
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. Obter status de conclusão de saudação do trabalho subtarefas
status de conclusão de saudação tootrack de subtarefas individuais, você pode usar o hello **AzureRmBackupJobDetails Get** cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Criar um relatório diário/semanal de trabalhos de backup
Normalmente, os administradores querem tooknow quais trabalhos de backup foi executados no hello últimas 24 horas, o status de saudação desses trabalhos de backup. Além disso, quantidade de saudação de dados transferidos oferece aos administradores uma maneira tooestimate o uso de dados mensal. abaixo de script Hello extrai dados brutos de saudação do hello serviço Backup do Azure e exibe informações de saudação no console do PowerShell hello.

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

Se você quiser tooadd a saída de relatório toothis recursos de criação de gráficos, saiba mais na postagem de blog do TechNet Olá [gráficos com o PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Próximas etapas
Se você preferir usar o PowerShell tooengage com os recursos do Azure, consulte artigo do PowerShell Olá para proteger o Windows Server, [implantar e gerenciar o Backup do Windows Server](backup-client-automation-classic.md). Há também um artigo do PowerShell para gerenciar os backups do DPM, [Implantar e Gerenciar o Backup do DPM](backup-dpm-automation-classic.md). Esses dois artigos têm uma versão para implantações do Gerenciador de Recursos, bem como para implantações do modelo Clássico.
