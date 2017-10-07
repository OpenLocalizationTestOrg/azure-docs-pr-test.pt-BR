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
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Use AzureRM.RecoveryServices.Backup cmdlets tooback backup de máquinas virtuais
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](backup-azure-vms-automation.md)
> * [Clássico](backup-azure-vms-classic-automation.md)
>
>

Este artigo mostra como toouse tooback de cmdlets do PowerShell do Azure backup e recuperar uma máquina virtual (VM) do Azure de serviços de recuperação de um cofre. Um cofre de serviços de recuperação é um recurso do Gerenciador de recursos do Azure e é usado tooprotect dados e ativos nos serviços de Backup do Azure e o Azure Site Recovery. Você pode usar um cofre de serviços de recuperação tooprotect VMs implantadas pelo Gerenciador de serviço do Azure e máquinas virtuais implantadas pelo Gerenciador de recursos do Azure.

> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo é para uso com máquinas virtuais criadas usando o modelo do Gerenciador de recursos de saudação.
>
>

Este artigo orienta você a usar PowerShell tooprotect uma VM e restaurar dados de um ponto de recuperação.

## <a name="concepts"></a>Conceitos
Se você não estiver familiarizado com hello serviço Backup do Azure, para obter uma visão geral do serviço Olá, confira [o que é o Backup do Azure?](backup-introduction-to-azure-backup.md) Antes de começar, certifique-se de que abrangem essentials Olá sobre Olá pré-requisitos necessários toowork com o Backup do Azure e Olá limitações da solução atual de backup de VM hello.

toouse PowerShell efetivamente, é necessário toounderstand Olá hierarquia de objetos e de onde toostart.

![Hierarquia de objetos dos Serviços de Recuperação](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

Olá tooview Referência de cmdlet do AzureRm.RecoveryServices.Backup PowerShell, consulte Olá [Backup do Azure - Cmdlets dos serviços de recuperação](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) em Olá biblioteca do Azure.

## <a name="setup-and-registration"></a>Configuração e registro
toobegin:

1. [Baixar a versão mais recente de saudação do PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (Olá versão mínima necessária é: 1.4.0)
2. Localize os cmdlets do PowerShell do Azure Backup Olá disponíveis digitando o comando a seguir de saudação:

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


Olá tarefas a seguir pode ser automatizada com o PowerShell:

* Criar um cofre dos Serviços de Recuperação
* Fazer backup de VMs do Azure
* Disparar um trabalho de backup
* Monitorar um trabalho de backup
* Restaurar uma VM do Azure

## <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação
Olá etapas levá-lo na criação de um cofre de serviços de recuperação. Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.

1. Se você estiver usando o Backup do Azure para Olá primeira vez, você deve usar o hello  **[registro AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  provedor de serviço de recuperação do Azure do cmdlet tooregister Olá com sua assinatura.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Olá Cofre de serviços de recuperação é um recurso do Gerenciador de recursos, portanto, você precisa tooplace-lo em um grupo de recursos. Você pode usar um grupo de recursos existente ou criar um grupo de recursos com hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  cmdlet. Ao criar um grupo de recursos, especifique o nome de saudação e local para o grupo de recursos de saudação.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Saudação de uso  **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  cmdlet toocreate Olá Cofre de serviços de recuperação. Certifique-se de que toospecify Olá mesmo local para o cofre Olá que foi usada para o grupo de recursos de saudação.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Especificar o tipo de saudação do toouse de redundância de armazenamento; Você pode usar [armazenamento localmente redundante (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [Geo redundante GRS (armazenamento)](../storage/common/storage-redundancy.md#geo-redundant-storage). Olá exemplo a seguir mostra Olá - BackupStorageRedundancy opção testvault é definida tooGeoRedundant.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Muitos cmdlets do Backup do Azure exigem Olá objeto de Cofre de serviços de recuperação como entrada. Por esse motivo, é conveniente toostore Olá serviços de recuperação de Backup cofre objeto em uma variável.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Exibição Olá cofres em uma assinatura
Use  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview lista de saudação de todos os cofres na assinatura atual hello. Você pode usar este toocheck de comando que foi criado um novo cofre ou toosee Olá cofres disponíveis na assinatura de saudação.

Execute o comando hello, Get-AzureRmRecoveryServicesVault tooview todos os cofres na assinatura de saudação. Olá exemplo a seguir mostra informações de saudação exibidas para cada compartimento.

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


## <a name="back-up-azure-vms"></a>Fazer backup de VMs do Azure
Use um tooprotect de Cofre de serviços de recuperação de suas máquinas virtuais. Antes de aplicar proteção Olá, definir o contexto de Cofre de saudação (tipo de saudação dos dados protegidos no cofre Olá) e verifique se a diretiva de proteção de saudação. diretiva de proteção de saudação é agendar Olá executar trabalhos de backup hello e quanto tempo cada instantâneo de backup é mantido.

### <a name="set-vault-context"></a>Definir o contexto de cofre
Antes de habilitar a proteção em uma máquina virtual, use  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexto de Cofre de saudação. Depois que o contexto de cofre Olá for definido, ela se aplica a cmdlets subsequentes tooall. Olá, exemplo a seguir define Olá contexto de cofre para o cofre hello, *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Crie uma política de proteção
Quando você cria um cofre dos Serviços de Recuperação, ele vem com proteção e políticas de retenção padrão. política de proteção padrão Olá dispara um trabalho de backup diariamente em um horário especificado. política de retenção padrão Olá retém o ponto de recuperação diário Olá por 30 dias. Você pode usar o padrão de saudação política tooquickly proteger sua VM e Editar política de hello mais tarde com detalhes diferentes.

Use  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview políticas de proteção de saudação no cofre hello. Você pode usar este cmdlet tooget uma política específica ou políticas de saudação tooview associadas com um tipo de carga de trabalho. saudação de exemplo a seguir obtém as políticas para o tipo de carga de trabalho, AzureVM.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> fuso horário de saudação do campo de BackupTime Olá no PowerShell é UTC. No entanto, quando o tempo de backup de saudação é mostrado no hello portal do Azure, o tempo de saudação é fuso horário local do tooyour ajustada.
>
>

Uma política de proteção de backup está associada a pelo menos uma política de retenção. A política de retenção define por quanto tempo um ponto de recuperação é mantido até ser excluído. Use  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  política de retenção tooview saudação padrão.  Da mesma forma, você pode usar  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  política ao agendar tooobtain saudação padrão. Olá  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet cria um objeto do PowerShell que contém informações de política de backup. Olá objetos de política de retenção e agendamento são usados como entradas toohello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  cmdlet. Olá exemplo a seguir armazena política ao agendar hello e política de retenção de saudação em variáveis. exemplo Hello usa esses parâmetros de saudação toodefine variáveis ao criar uma política de proteção, *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Habilitar proteção
Depois que você definiu a diretiva de proteção de backup hello, você deve habilitar política de saudação para um item. Use  **[habilitar AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable proteção. Habilitar a proteção requer dois objetos - item hello e política de saudação. Depois que a política Olá foi associada ao Cofre hello, fluxo de trabalho de backup Olá é acionado em tempo de saudação definido na agenda de diretiva de saudação.

Olá exemplo habilita proteção Olá item, V2VM, usando a política de hello, NewPolicy a seguir. proteção de saudação tooenable em VMs do Gerenciador de recursos não criptografado

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

proteção Olá tooenable criptografado VMs (criptografadas usando BEK e KEK), chaves de tooread permissão do serviço de Backup do Azure de saudação toogive e segredos do Cofre de chaves.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

proteção Olá tooenable criptografado VMs (criptografadas usando apenas o BEK), toogive hello Azure Backup service permissão tooread segredos do Cofre de chaves.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> Se você estiver usando a nuvem do Azure Government hello, use Olá ff281ffe-705c-4f53-9f37-a40e6f2c68f3 de valor para o parâmetro hello **- ServicePrincipalName** na [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet .
>
>

Para VMs clássicas

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Modificar uma política de proteção
política de proteção Olá toomodify, use [AzureRmRecoveryServicesBackupProtectionPolicy conjunto](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify Olá SchedulePolicy ou política de retenção objetos.

Olá, exemplo a seguir altera dias de too365 retenção do ponto de recuperação hello.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Disparar um backup
Você pode usar  **[Backup AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger um trabalho de backup. Se for backup inicial Olá, é um backup completo. Os backups posteriores fazem uma cópia incremental. Ser toouse se  **[conjunto AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexto de cofre Olá antes de disparar o trabalho de backup hello. saudação de exemplo a seguir pressupõe que o cofre contexto foi definido.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> fuso horário de saudação de campos de StartTime e EndTime Olá no PowerShell é UTC. No entanto, quando o tempo de saudação é mostrado no portal do Azure de saudação, tempo de saudação é fuso horário local do tooyour ajustada.
>
>

## <a name="monitoring-a-backup-job"></a>Monitoramento de um trabalho de backup
Você pode monitorar as operações de execução longa, como trabalhos de backup, sem usar Olá portal do Azure. status de saudação tooget de um trabalho em andamento, use Olá  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  cmdlet. Esse cmdlet obtém os trabalhos de backup da saudação para um cofre específico e que os está especificado no contexto de cofre hello. Olá exemplo a seguir obtém o status de saudação de um trabalho em andamento como uma matriz e armazena status Olá na Olá $joblist variável.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Em vez de sondagem esses trabalhos para conclusão - que é desnecessário código adicional - use Olá  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  cmdlet. Esse cmdlet pausa a execução de saudação até Olá trabalho for concluído ou Olá especificado, o valor de tempo limite é atingido.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Restaurar uma VM do Azure
Há uma diferença importante entre hello restaurar uma máquina virtual usando Olá portal do Azure e restaurar uma máquina virtual usando o PowerShell. Com o PowerShell, operação de restauração de saudação é concluída após a criação de discos de saudação e informações de configuração de ponto de recuperação de saudação.

> [!NOTE]
> operação de restauração Olá não cria uma máquina virtual.
>
>

toocreate uma máquina virtual do disco, consulte a seção Olá [criar hello VM dos discos armazenados](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). as etapas básicas de saudação toorestore uma VM do Azure são:

* Selecione Olá VM
* Escolha um ponto de recuperação
* Restaurar discos Olá
* Criar hello VM de discos armazenados

Olá gráfico a seguir mostra hierarquia de objetos de saudação do hello RecoveryServicesVault para baixo toohello BackupRecoveryPoint.

![Hierarquia de objetos dos Serviços de Recuperação mostrando BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

toorestore os dados de backup, identificar o item de backup hello e ponto de recuperação de saudação que contém dados de point-in-time de saudação. Saudação de uso  **[restauração AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  cmdlet toorestore dados Olá cofre conta toohello do cliente.

### <a name="select-hello-vm"></a>Selecione Olá VM
objeto do PowerShell Olá tooget que identifica o direito de saudação item de backup, iniciar do contêiner de saudação no cofre hello e trabalhar abaixo da hierarquia de objetos de saudação. contêiner de saudação tooselect que representa o hello VM, use Olá  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  cmdlet e redirecione que toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  cmdlet.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Escolha um ponto de recuperação
Saudação de uso  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist cmdlet pontos de recuperação todos para fazer backup do item hello. Em seguida, escolha Olá toorestore de ponto de recuperação. Se você não tiver certeza de qual toouse de ponto de recuperação, é uma boa prática toochoose hello mais recente RecoveryPointType = AppConsistent ponto na lista de saudação.

Em Olá script a seguir, Olá variável, **$rp**, é uma matriz de pontos de recuperação para fazer backup do item selecionado Olá da saudação últimos sete dias. matriz de saudação é classificada em ordem inversa de tempo com o último ponto de recuperação Olá no índice 0. Use o padrão matriz do PowerShell a indexação de ponto de recuperação toopick hello. No exemplo hello, $rp [0] seleciona o último ponto de recuperação hello.

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



### <a name="restore-hello-disks"></a>Restaurar discos Olá
Saudação de uso  **[restauração AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore cmdlet dados do item de um backup e configuração tooa ponto de recuperação. Depois de ter identificado um ponto de recuperação, usá-lo como valor Olá para Olá **- RecoveryPoint** parâmetro. No código de exemplo anterior hello, **$rp [0]** foi Olá toouse de ponto de recuperação. Em Olá código de exemplo a seguir **$rp [0]** é Olá toouse de ponto de recuperação para restaurar o disco de saudação.

discos de saudação toorestore e informações de configuração:

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Saudação de uso  **[espera AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait cmdlet para Olá toocomplete de trabalho de restauração.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Depois de concluído o trabalho de restauração hello, use Olá  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  detalhes de saudação do cmdlet tooget de saudação de operação de restauração. Olá JobDetails propriedade tem Olá toorebuild necessário de informações Olá VM.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

Depois que você restaurar discos hello, vá Olá de toocreate de seção próximo do toohello VM.

## <a name="create-a-vm-from-restored-disks"></a>Criar uma máquina virtual de discos restaurados
Depois de ter restaurado os discos Olá, use essas etapas toocreate e configurar a máquina virtual de saudação do disco.

> [!NOTE]
> toocreate criptografados VMs de discos restaurados, a função do Azure deve ter a ação de saudação do tooperform de permissão, **Microsoft.KeyVault/vaults/deploy/action**. Se sua função não tem essa permissão, crie uma função personalizada com esta ação. Para obter mais informações, veja [Funções personalizadas no RBAC do Azure](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Saudação de consulta restaurado propriedades do disco para obter detalhes do trabalho hello.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Definir contexto do armazenamento do Azure hello e restaurar o arquivo de configuração JSON hello.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Use configuração de VM Olá JSON configuração arquivo toocreate hello.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Anexe o disco do sistema operacional hello e discos de dados. Dependendo da configuração de saudação das suas máquinas virtuais, clique nos cmdlets do respectivos de tooview Olá link relevante: 
    - [Máquinas virtuais não gerenciados, não criptografado](#non-managed-non-encrypted-vms)
    - [Máquinas virtuais não gerenciados, criptografados (BEK)](#non-managed-encrypted-vms-bek-only)
    - [Máquinas virtuais não gerenciados, criptografados (BEK e KEK)](#non-managed-encrypted-vms-bek-and-kek)
    - [Máquinas virtuais gerenciados, não criptografado](#managed-non-encrypted-vms)
    - [Máquinas virtuais gerenciadas, criptografados (BEK e KEK)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>VMs não criptografadas não gerenciadas

    Use Olá exemplo a seguir para VMs não gerenciado, não criptografado.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>VMs criptografadas e não gerenciadas (apenas BEK)

    Para VMs não gerenciados, criptografadas (criptografadas usando apenas o BEK), você precisa cofre da chave secreta toohello toorestore Olá antes de você pode anexar discos. Para obter mais informações, consulte o artigo Olá [restaurar uma máquina virtual criptografada de um ponto de recuperação de Backup do Azure](backup-azure-restore-key-secret.md). saudação de exemplo a seguir mostra como tooattach SO e discos de dados para criptografada VMs.

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>VMs criptografadas e não gerenciadas (BEK e KEK)

    Para VMs não gerenciados, criptografadas (criptografadas usando BEK e KEK), você precisa toorestore chave de saudação e cofre da chave secreta toohello antes de você pode anexar discos. Para obter mais informações, consulte o artigo Olá [restaurar uma máquina virtual criptografada de um ponto de recuperação de Backup do Azure](backup-azure-restore-key-secret.md). saudação de exemplo a seguir mostra como tooattach SO e discos de dados para criptografada VMs.

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

    #### <a name="managed-non-encrypted-vms"></a>VMs não criptografadas gerenciadas

    Para VMs gerenciadas não criptografado, você precisa toocreate gerenciado discos do armazenamento de blob e, em seguida, anexar discos hello. Para obter informações detalhadas, consulte o artigo Olá [anexar um disco de dados tooa VM do Windows usando o PowerShell](../virtual-machines/windows/attach-disk-ps.md). Olá, código de exemplo a seguir mostra como tooattach Olá discos de dados para VMs gerenciadas não criptografado.

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>VMs criptografadas e gerenciadas (BEK e KEK)

    Para VMs criptografadas gerenciadas (criptografadas usando BEK e KEK), você precisa toocreate gerenciado discos do armazenamento de blob e, em seguida, anexar discos hello. Para obter informações detalhadas, consulte o artigo Olá [anexar um disco de dados tooa VM do Windows usando o PowerShell](../virtual-machines/windows/attach-disk-ps.md). Olá código exemplo a seguir mostra como tooattach Olá discos de dados para VMs criptografadas gerenciadas.

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

5. Defina as configurações de rede hello.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Crie a máquina virtual de saudação.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Próximas etapas
Se você preferir toouse PowerShell tooengage com os recursos do Azure, consulte o artigo do PowerShell hello, [implantar e gerenciar o Backup do Windows Server](backup-client-automation.md). Se você gerenciar backups do DPM, consulte o artigo Olá [implantar e gerenciar o Backup do DPM](backup-dpm-automation.md). Esses dois artigos têm uma versão para implantações do Resource Manager, bem como para implantações do modelo Clássico.  
