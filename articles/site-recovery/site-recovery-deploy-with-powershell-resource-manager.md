---
title: aaaReplicate VMs Hyper-V com o PowerShell e o Gerenciador de recursos do Azure | Microsoft Docs
description: "Automatize a replicação de saudação do tooAzure de VMs Hyper-V com o Azure Site Recovery usando o PowerShell e o Gerenciador de recursos do Azure."
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
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>Replicar entre máquinas virtuais locais do Hyper-V e o Azure usando o PowerShell e o Azure Resource Manager
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell – Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portal clássico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Visão geral
O Azure Site Recovery contribui com a estratégia de recuperação tooyour business desastre e continuidade ao orquestrar a replicação, failover e recuperação de máquinas virtuais em vários cenários de implantação. Para obter uma lista completa dos cenários de implantação, consulte Olá [visão geral do Azure Site Recovery](site-recovery-overview.md).

PowerShell do Azure é um módulo que fornece toomanage de cmdlets do Azure por meio do Windows PowerShell. Ele pode funcionar com dois tipos de módulos: Olá módulo de perfil do Azure ou módulo do Azure Resource Manager hello.

Os cmdlets do PowerShell da Recuperação de Site disponíveis com o Azure PowerShell para o Azure Resource Manager permitem que você proteja e recupere seus servidores no Azure.

Este artigo descreve como toouse do Windows PowerShell, junto com o Gerenciador de recursos do Azure, toodeploy tooconfigure de recuperação de Site e orquestrar tooAzure de proteção do servidor. exemplo Hello usado neste artigo mostra como tooprotect, failover e recupere máquinas virtuais em um tooAzure de host do Hyper-V, usando o PowerShell do Azure com o Gerenciador de recursos do Azure.

> [!NOTE]
> Olá cmdlets do PowerShell de recuperação de Site no momento permitem Olá tooconfigure a seguir: um tooanother de site do Virtual Machine Manager, um tooAzure de site do Virtual Machine Manager e um tooAzure de site do Hyper-V.
>
>

Você não precisa toobe um toouse especialista do PowerShell deste artigo, mas é necessário toounderstand Olá os conceitos básicos, como sessões, cmdlets e módulos. Para obter mais informações sobre o Windows PowerShell, consulte [Introdução ao PowerShell do Microsoft Azure (a página pode estar em inglês)](http://technet.microsoft.com/library/hh857337.aspx).

Leia mais sobre isso em [Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> Parceiros da Microsoft que fazem parte do programa do provedor de solução de nuvem (CSP) Olá podem configurar e gerenciar a proteção de servidores de seus clientes tootheir respectivos CSP as assinaturas dos clientes (assinaturas de locatários).
>
>

## <a name="before-you-start"></a>Antes de começar
Verifique se estes pré-requisitos estão em vigor:

* Uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). Além disso, você pode ler sobre [preços do Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Para obter informações sobre esta versão e como tooinstall, consulte [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Olá [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) módulos. Você pode obter versões mais recentes de saudação desses módulos de saudação [Galeria do PowerShell](https://www.powershellgallery.com/)

Este artigo ilustra como toouse Powershell do Azure com o Azure Resource Manager tooconfigure e gerenciar a proteção dos seus servidores. exemplo Hello usado neste artigo mostra como tooprotect uma máquina virtual, em execução em um host Hyper-V, tooAzure. Olá pré-requisitos a seguir é exemplos de toothis específico. Para um conjunto mais abrangente de requisitos para Olá vários cenários de recuperação de Site, consulte a documentação de toohello relativos toothat cenário.

* Um host Hyper-V que executa o Windows Server 2012 R2 ou o Microsoft Hyper-V Server 2012 R2 contendo uma ou mais máquinas virtuais.
* Servidores Hyper-V conectado toohello Internet, diretamente ou através de um proxy.
* Olá máquinas virtuais que você deseja tooprotect devem estar em conformidade com [pré-requisitos para a máquina Virtual](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Etapa 1: Inscrever-se em tooyour conta do Azure
1. Abrir um console do PowerShell e execute este comando toosign em tooyour conta do Azure. Olá cmdlet abre uma página da web que solicitará as credenciais de conta.

        Login-AzureRmAccount

    Como alternativa, você também pode incluir as credenciais de conta como um parâmetro toohello `Login-AzureRmAccount` cmdlet, usando Olá `-Credential` parâmetro.

    Se você estiver trabalhando em nome de um locatário de parceiro CSP, especifique Prezado cliente como um locatário usando o nome de domínio primário tenantID ou locatário.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Uma conta pode ter várias assinaturas, para que você deve associar uma assinatura Olá deseja toouse com conta hello.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Verifique se sua assinatura está registrada toouse hello Azure provedores de serviços de recuperação e recuperação de Site, usando Olá comandos a seguir:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   Na saída de hello desses comandos, se hello **RegistrationState** está definido muito**registrado**, você poderá tooStep 2. Caso contrário, você deve registrar o provedor de saudação ausente na sua assinatura.

   Olá tooregister provedor do Azure para recuperação de Site e serviços de recuperação, executar Olá comandos a seguir:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Verificar se os provedores de saudação registrado com êxito usando Olá comandos a seguir: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Etapa 2: Configurar a saudação que Cofre de serviços de recuperação
1. Crie um grupo de recursos do Gerenciador de recursos do Azure em que você criar cofre hello, ou use um grupo de recursos existente. Você pode criar um novo grupo de recursos usando o comando a seguir de saudação:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    Quando a variável de saudação $ResourceGroupName contém nome Olá Olá do grupo de recursos você deseja toocreate e variável Olá $Geo contém hello Azure região na qual grupo de recursos de saudação do toocreate (por exemplo, "Sul do Brasil").

    Você pode obter uma lista de grupos de recursos em sua assinatura usando Olá `Get-AzureRmResourceGroup` cmdlet.
2. Crie um novo cofre dos Serviços de Recuperação do Azure da seguinte maneira:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Você pode recuperar uma lista de cofres existentes usando Olá `Get-AzureRmRecoveryServicesVault` cmdlet.

> [!NOTE]
> Se você quiser tooperform operações nos cofres de recuperação de Site criados usando o portal clássico do hello ou módulo do PowerShell do Azure Service Management hello, você pode recuperar uma lista de tais cofres usando Olá `Get-AzureRmSiteRecoveryVault` cmdlet. É necessário criar um novo cofre dos Serviços de Recuperação para todas as novas operações. cofres da recuperação de Site Olá que você criou anteriormente têm suporte, mas não tem recursos mais recentes de saudação.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Etapa 3: Definir Olá contexto de Cofre de serviços de recuperação
1. Definir o contexto do cofre Olá executando Olá comando a seguir:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Etapa 4: Criar um site do Hyper-V e gerar uma nova chave de registro do cofre para o site de saudação.
1. Crie um novo site do Hyper-V da seguinte maneira:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Esse cmdlet inicia um site do Site Recovery trabalho toocreate hello e retorna um objeto de trabalho de recuperação de Site. Aguarde Olá toocomplete de trabalho e verificar que o trabalho Olá concluída com êxito.

    Você pode recuperar o objeto de trabalho hello e, assim, verificar status atual de saudação do trabalho hello, usando o cmdlet Get-AzureRmSiteRecoveryJob de saudação.
2. Gerar e baixar uma chave de registro para o site de hello, da seguinte maneira:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Saudação de cópia baixado host toohello chave Hyper-V. Precisar Olá tooregister chave Olá Hyper-V host toohello site.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Etapa 5: Instalar o provedor do Azure Site Recovery hello e Azure Recovery Services Agent em seu host do Hyper-V
1. Baixar o instalador Olá para a versão mais recente saudação do provedor de saudação do [Microsoft](https://aka.ms/downloaddra).
2. Instalador de saudação de execução no host do Hyper-V e no final de saudação da instalação de saudação continuar toohello etapa de registro.
3. Quando solicitado, forneça Olá baixado a chave de registro de site e concluir o registro do site do Hyper-V host toohello da saudação.
4. Verifique se o que host Olá Hyper-V é registrado toohello site usando o comando a seguir de saudação:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Etapa 6: Criar uma política de replicação e associe-o contêiner de proteção Olá
1. Crie uma política de replicação da seguinte maneira:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Saudação de seleção retornada tooensure de trabalho que a criação de política de replicação Olá terá êxito.

   > [!IMPORTANT]
   > Olá conta de armazenamento especificada deve ser em Olá mesma região do Azure como seu Cofre de serviços de recuperação e deve ter a replicação geográfica habilitada.
   >
   > * Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (clássico).
   > * Se Olá especificado a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Gerenciador de recursos do Azure), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (Gerenciador de recursos do Azure).
   >
   >
2. Obter Olá proteção contêiner toohello site correspondente, da seguinte maneira:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Inicie associação de saudação do recipiente de proteção de saudação com a política de replicação hello, da seguinte maneira:

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer

   Espere Olá associação trabalho toocomplete e certifique-se de que ela foi concluída com êxito.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Etapa 7: habilitar a proteção para máquinas virtuais
1. Obter Olá proteção entidade correspondente toohello VM que você deseja tooprotect, da seguinte maneira:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Inicie a proteção de máquina virtual de hello, da seguinte maneira:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Olá conta de armazenamento especificada deve ser em Olá mesma região do Azure como seu Cofre de serviços de recuperação e deve ter a replicação geográfica habilitada.
   >
   > * Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (clássico).
   > * Se Olá especificado a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Gerenciador de recursos do Azure), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (Gerenciador de recursos do Azure).
   >
   > Se Olá VM que você está protegendo tem mais de um disco anexado tooit, especifique o disco do sistema operacional hello usando Olá *OSDiskName* parâmetro.
   >
   >
3. Aguarde Olá máquinas virtuais tooreach um estado protegido após a replicação inicial hello. Isso pode demorar um pouco, dependendo de fatores como a quantidade de saudação de toobe dados replicado e Olá tooAzure upstream de largura de banda disponível. Estado do trabalho Hello e StateDescription são atualizados da seguinte maneira após Olá VM atingir um estado protegido.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Atualize propriedades de recuperação, como Olá tamanho de função VM e failover de tooupon de placas de interface de rede Olá rede Azure tooattach Olá máquina virtual.

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
        DisplayName      : Update hello virtual machine
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
1. Execute um trabalho de failover de teste, da seguinte maneira:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Verifique se esse teste Olá que VM é criada no Azure. (trabalho de failover de teste hello está suspenso, depois de criar a VM de teste Olá no Azure. Olá trabalho for concluído limpando artefatos Olá criado ao retomar o trabalho hello, conforme ilustrado na próxima etapa do hello.)
3. Olá completa testar o failover, da seguinte maneira:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Próximas etapas
[Leia mais](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.
