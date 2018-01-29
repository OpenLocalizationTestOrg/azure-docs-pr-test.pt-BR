---
title: Replicar VMs do Hyper-V com PowerShell e o Azure Resource Manager | Microsoft Docs
description: "Automatize a replicação de VMs do Hyper-V no Azure com o Azure Site Recovery usando o PowerShell e o Azure Resource Manager."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 10/19/2017
ms.author: bsiva
ms.openlocfilehash: d93be3b958f85cd2892f92d84ed68996909a5d6b
ms.sourcegitcommit: 76a3cbac40337ce88f41f9c21a388e21bbd9c13f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2017
---
# <a name="set-up-disaster-recovery-to-azure-for-hyper-v-vms-using-powershell-and-azure-resource-manager"></a>Configurar a recuperação de desastres para o Azure para máquinas virtuais do Hyper-V usando o PowerShell e o Azure Resource Manager

O [Azure Site Recovery](site-recovery-overview.md) contribui para sua estratégia de BCDR (continuidade de negócios e recuperação de desastre) gerenciando replicação, failover e recuperação de máquinas virtuais (VMs) do Azure e servidores físicos e VMs locais.

Este artigo descreve como usar o Windows PowerShell, junto com o Azure Resource Manager para replicar máquinas virtuais do Hyper-V no Azure. O exemplo usado neste artigo mostra como replicar uma única VM em execução em um host Hyper-V no Azure.

## <a name="overview"></a>Visão geral

O Azure PowerShell fornece cmdlets para gerenciar o Azure usando o Windows PowerShell. Os cmdlets do PowerShell da Recuperação de Site disponíveis com o Azure PowerShell para o Azure Resource Manager permitem que você proteja e recupere seus servidores no Azure.

Não é preciso ser um especialista no PowerShell para usar este artigo, mas é necessário entender os conceitos básicos, como módulos, cmdlets e sessões. Leia [Introdução ao Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx) e [Uso do Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> Os parceiros da Microsoft no programa CSP (Provedor de Solução na Nuvem) podem configurar e gerenciar a proteção dos servidores de clientes em suas respectivas assinaturas de CSP (assinaturas de locatário).
>
>

## <a name="before-you-start"></a>Antes de começar
Verifique se estes pré-requisitos estão em vigor:

* Uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). Além disso, você pode ler sobre [preços do Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Para obter informações sobre essa versão e como instalá-la, confira [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Os módulos [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/). É possível obter as versões mais recentes desses módulos na [Galeria do PowerShell](https://www.powershellgallery.com/)

Além disso, o exemplo específico descrito neste artigo tem os seguintes pré-requisitos:

* Um host Hyper-V que executa o Windows Server 2012 R2 ou o Microsoft Hyper-V Server 2012 R2 contendo uma ou mais máquinas virtuais. Os servidores Hyper-V devem estar conectados à Internet, diretamente ou por meio de um proxy.
* As máquinas virtuais que você deseja replicar devem estar em conformidade com [esses pré-requisitos](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-to-your-azure-account"></a>Etapa 1: Entrar em sua conta do Azure

1. Abra um console do PowerShell e execute este comando para entrar em sua conta do Azure. O cmdlet abre uma página da Web que solicitará suas credenciais de conta: **Login-AzureRmAccount**.
    - Como alternativa, você pode incluir as credenciais de conta como um parâmetro no cmdlet **Login-AzureRmAccount**, usando o parâmetro **-Credential**.
    - Se você é um parceiro CSP trabalhando em nome de um locatário, especifique o cliente como um locatário usando sua tenantID ou o nome de domínio primário do locatário. Por exemplo: **Login-AzureRmAccount -Tenant "fabrikam.com"**
2. Associe a assinatura que deseja usar com a conta, uma vez que uma conta pode ter várias assinaturas:

    `Select-AzureRmSubscription -SubscriptionName $SubscriptionName`

3. Verifique se sua assinatura está registrada para usar os provedores do Azure para os Serviços de Recuperação e o Site Recovery usando os seguintes comandos:

    `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

4. Se, na saída de comando, o **RegistrationState** estiver definido como **Registrado**, você poderá prosseguir para a Etapa 2. Caso contrário, você deverá registrar o provedor ausente em sua assinatura executando estes comandos:

    `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery` `Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices`

5. Verifique se os provedores foram registrados com êxito usando os seguintes comandos:

    `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-the-vault"></a>Etapa 2: configurar o cofre

1. Crie um grupo de recursos do Azure Resource Manager no qual você criará o cofre ou use um grupo de recursos existente. Crie um novo grupo de recursos da seguinte maneira. A variável $ResourceGroupName contém o nome do grupo de recursos que você deseja criar e a variável $Geo contém a região do Azure na qual o grupo de recursos será criado (por exemplo, “Sul do Brasil”).

    `New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo` 

2. Para obter uma lista de grupos de recursos em sua assinatura, use o cmdlet **Get-AzureRmResourceGroup**.
2. Crie um novo cofre dos Serviços de Recuperação do Azure da seguinte maneira:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Você pode recuperar uma lista de cofres existentes com o cmdlet **Get-AzureRmRecoveryServicesVault**.


## <a name="step-3-set-the-recovery-services-vault-context"></a>Etapa 3: Configurar o contexto do Cofre dos Serviços de Recuperação

Defina o contexto do cofre da seguinte maneira:

`Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault`

## <a name="step-4-create-a-hyper-v-site"></a>Etapa 4: criar um site do Hyper-V

1. Crie um novo site do Hyper-V da seguinte maneira:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

2. Este cmdlet inicia um trabalho da Recuperação de Site para a criação do site e retorna um objeto de trabalho da Recuperação de Site. Aguarde a conclusão do trabalho e verifique se ele foi concluído com êxito.
3. Use o cmdlet **Get-AzureRmSiteRecoveryJob cmdlet** para recuperar o objeto de trabalho e verificar o status atual do trabalho.
4. Gere e baixe uma chave de registro para o site da seguinte maneira:

    ```
    $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path
    ```

5. Copie a chave baixada no host Hyper-V. Você precisa da chave para registrar o host Hyper-V no site.

## <a name="step-5-install-the-provider-and-agent"></a>Etapa 5: instalar o Provedor e o agente

1. Baixe o instalador para obter a versão mais recente do provedor na [Microsoft](https://aka.ms/downloaddra).
2. Execute o instalador no host Hyper-V.
3. No final da instalação, vá para a etapa de registro.
4. Quando solicitado, forneça a chave baixada e conclua o registro do host Hyper-V.
5. Verifique se o host Hyper-V foi registrado no site da seguinte maneira:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy"></a>Etapa 6: criar uma política de replicação

Antes de iniciar, observe que a conta de armazenamento especificada deve estar na mesma região do Azure que o cofre e deve ter a replicação geográfica habilitada.

1. Crie uma política de replicação da seguinte maneira:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

2. Verifique o trabalho retornado para garantir que a criação da política de replicação foi bem-sucedida.

3. Recupere o contêiner de proteção corresponde ao site da seguinte maneira:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Associe o contêiner de proteção à política de replicação da seguinte maneira:

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer

4. Aguarde o conclusão bem-sucedida do trabalho de associação.

## <a name="step-7-enable-vm-protection"></a>Etapa 7: habilitar a proteção de VM

1. Recupere a entidade de proteção correspondente à VM que você deseja proteger, da seguinte maneira:

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Proteja a VM. Se a VM que você estiver protegendo tiver mais de um disco anexado, será necessário especificar o disco do sistema operacional usando o parâmetro *OSDiskName* .

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

3. Aguarde até que as máquinas virtuais atinjam um estado protegido após a replicação inicial. Isso pode demorar um pouco, dependendo de fatores como a quantidade de dados a serem replicados e a largura de banda upstream disponível no Azure. Quando um estado protegido estiver implantado, o State e StateDescription do trabalho são atualizados da seguinte maneira: 

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Atualize as propriedades de recuperação (como o tamanho da função VM) e a rede do Azure à qual o NIC da VM será anexado após o failover.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update the virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Etapa 8: executar um failover de teste
1. Execute o failover de teste da seguinte maneira:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Verifique se a VM de teste foi criada no Azure. O trabalho de failover de teste é suspenso após a criação da VM de teste no Azure.
3. Para limpar e concluir o failover de teste, execute:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Próximas etapas
[Saiba mais](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.
