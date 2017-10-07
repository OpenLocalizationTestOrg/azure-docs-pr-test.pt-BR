---
title: "aaaReplicate VMs Hyper-V no site secundário do VMM tooa com o PowerShell (Gerenciador de recursos do Azure) | Microsoft Docs"
description: "Descreve como a replicação de tooorchestrate do Azure Site Recovery toodeploy, failover e recuperação de máquinas virtuais do Hyper-V no VMM nuvens tooa site do VMM secundário usando o PowerShell (Gerenciador de recursos)"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Replicar máquinas virtuais de Hyper-V no VMM nuvens tooa site VMM secundário usando o PowerShell (Gerenciador de recursos)
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clássico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Bem-vindo tooAzure recuperação de Site! Use este artigo se você quiser tooreplicate máquinas virtuais de Hyper-V gerenciados no site secundário do System Center Virtual Machine Manager (VMM) nuvens tooa local.

Este artigo mostra como as tarefas comuns do toouse PowerShell tooautomate precisar tooperform ao configurar máquinas virtuais do Azure Site Recovery tooreplicate Hyper-V nas nuvens VMM do System Center VMM nuvens tooSystem Center no site secundário.

Olá artigo inclui os pré-requisitos para o cenário de saudação e mostra

* Como tooset um cofre de serviços de recuperação
* Instalar Olá provedor Azure Site Recovery no servidor do VMM de origem de saudação e o servidor do VMM de destino Olá
* Registrar servidores do VMM Olá no cofre Olá
* Configure a política de replicação para Olá nuvem do VMM. as configurações de replicação de saudação na política de saudação será máquinas virtuais de tooall aplicada protegido
* Habilite a proteção para máquinas virtuais de saudação.
* Olá failover de máquinas virtuais de teste individualmente ou como parte de um toomake de plano de recuperação se que tudo está funcionando conforme o esperado.
* Execute um planejado ou um failover não planejado de máquinas virtuais, individualmente ou como parte de um toomake de plano de recuperação se que tudo está funcionando conforme o esperado.

Se você tiver problemas para configurar esse cenário, publique suas perguntas sobre Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> O Azure tem dois [modelos de implantação](../azure-resource-manager/resource-manager-deployment-model.md) diferentes para criar e trabalhar com recursos: Azure Resource Manager e Clássico. Azure também tem dois portais – Olá portal clássico do Azure que dá suporte ao modelo de implantação clássico hello e Olá portal do Azure com suporte para ambos os modelos de implantação. Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.
>
>

## <a name="on-premises-prerequisites"></a>Pré-requisitos do local
Aqui está o que você precisará no hello primário e secundário local sites toodeploy neste cenário:

| **Pré-requisitos** | **Detalhes** |
| --- | --- |
| **VMM** |Recomendamos que você implantar um servidor do VMM no site primário hello e um servidor do VMM no site secundário hello.<br/><br/> Você também pode [replicar entre nuvens em um único servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo isso você precisará de pelo menos duas nuvens configuradas no servidor do VMM hello.<br/><br/> Servidores do VMM devem estar executando pelo menos System Center 2012 SP1 com atualizações mais recentes de saudação.<br/><br/> Cada servidor do VMM deve ter em um ou mais nuvens configuradas e todas as nuvens devem ter perfil de capacidade do Hyper-V Olá definida. <br/><br/>As nuvens devem conter um ou mais grupos de hosts do VMM.<br/><br/>Saiba mais sobre como configurar nuvens do VMM em [Configurando Olá VMM malha de nuvem](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), e [passo a passo: Criando nuvens privadas com o System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> Os servidores VMM devem ter acesso à internet. |
| **Hyper-V** |Servidores Hyper-V devem estar executando pelo menos o Windows Server 2012 com a função hello Hyper-V e ter Olá as últimas atualizações instaladas.<br/><br/> Um servidor Hyper-V deve conter uma ou mais VMs.<br/><br/>  Servidores de host Hyper-V devem estar localizados em grupos de host em nuvens do VMM Olá primários e secundários.<br/><br/> Se você estiver executando o Hyper-V em um cluster no Windows Server 2012 R2, instale a [atualização 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se estiver executando o Hyper-V em um cluster no Windows Server 2012, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereço IP estático. Você precisará agente do cluster Olá tooconfigure manualmente. [Leia mais](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Provedor** |Durante a implantação da recuperação de Site você instalar Olá provedor Azure Site Recovery em servidores do VMM. Olá provedor se comunica com a recuperação de Site sobre HTTPS 443 tooorchestrate replicação. Replicação de dados ocorre entre servidores de Hyper-V primário e secundário de saudação sobre Olá LAN ou uma conexão VPN.<br/><br/> Olá provedor em execução no servidor do VMM Olá precisa acessar toothese URLs: *. c o m; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. n e t; *. store.core.windows.net.<br/><br/> Além de permitir a comunicação de firewall de saudação do VMM servidores toohello [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e permitir o protocolo HTTPS (443) de saudação. |

### <a name="network-mapping-prerequisites"></a>Pré-requisitos de mapeamento de rede
Mapas de mapeamento de rede entre redes de VM do VMM nos servidores VMM primários e secundários de saudação para:

* Colocar de maneira ideal VMs de réplica em hosts secundários do Hyper-V após o failover.
* Conecte a redes VM de tooappropriate de máquinas virtuais de réplica.
* Se você não configurar a rede mapeamento réplica VMs não será conectada tooany rede após o failover.
* Se você quiser tooset rede mapeamento durante a recuperação de Site implantação aqui é o que será necessário:

  * Certifique-se de que as VMs no servidor host Hyper-V de origem de saudação são conectado tooa rede VM do VMM. Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.
  * Verifica se a nuvem secundária de saudação que você usará para a recuperação tem uma rede VM correspondente configurada. Essa rede VM deve ser vinculado tooa rede lógica associada com a nuvem secundária hello.

Saiba mais sobre como configurar redes do VMM no hello artigos abaixo

* [Como tooconfigure de redes lógicas no VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Como tooconfigure VM redes e gateways no VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[Saiba mais](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sobre o funcionamento do mapeamento de rede.

### <a name="powershell-prerequisites"></a>Pré-requisitos do PowerShell
Certifique-se de que ter toogo pronto do PowerShell do Azure. Se você já estiver usando o PowerShell, você precisará tooupgrade tooversion 0.8.10 ou posterior. Para obter informações sobre como configurar o PowerShell, consulte Olá [guia tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs). Depois de você ter instalado e configurado o PowerShell, você pode exibir todos os cmdlets de saudação disponíveis para o serviço de saudação [aqui](/powershell/azure/overview).

toolearn sobre dicas que podem ajudá-lo a usar os cmdlets de saudação, como como valores de parâmetro, as entradas e saídas são tratadas normalmente no Azure PowerShell, consulte Olá [guia de Introdução aos Cmdlets do Azure de tooget](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Etapa 1: Definir a assinatura de saudação
1. Do powershell do Azure, logon tooyour conta do Azure: usando Olá cmdlets a seguir

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Obtenha uma lista das suas assinaturas. Isso também listará Olá subscriptionIDs para cada uma das assinaturas hello. Anote a subscriptionID Olá de assinatura Olá no qual você deseja que o Cofre de serviços de recuperação de saudação toocreate    

        Get-AzureRmSubscription
3. Assinatura de saudação conjunto no qual Olá Cofre de serviços de recuperação é toobe criado pelo mencionar Olá ID da assinatura

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Etapa 2: Criar um cofre dos Serviços de Recuperação
1. Se você ainda não tiver um, crie um grupo de recursos do Azure Resource Manager

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Criar um novo cofre de serviços de recuperação e salve Olá criada o objeto de Cofre de recuperação automatizada do sistema em uma variável (será usada posteriormente). Você também pode recuperar Olá ASR cofre post criação do objeto usando o cmdlet Get-AzureRMRecoveryServicesVault de saudação:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Etapa 3: Definir o contexto de Cofre de serviços de recuperação de saudação
1. Se você tiver um cofre já criado, execute Olá abaixo comando tooget saudação do cofre.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Definir o contexto de Cofre de saudação executando Olá comando abaixo.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Etapa 4: Instalar Olá provedor Azure Site Recovery
1. Na máquina do VMM hello, crie um diretório executando Olá comando a seguir:

       New-Item c:\ASR -type directory
2. Extrair arquivos hello usando o provedor de saudação baixada executando o comando a seguir de saudação

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Instale o provedor de saudação usando Olá comandos a seguir:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Aguarde Olá toofinish de instalação.
4. Registre o servidor de saudação no cofre de saudação usando Olá comando a seguir:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a>Etapa 5: Criar e associar uma política de replicação
1. Crie uma política de replicação do Hyper-V 2012 R2 executando Olá comando a seguir:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Olá nuvem do VMM pode conter hosts Hyper-V executando diferentes versões do Windows Server (conforme mencionado nos pré-requisitos do Hyper-V Olá), mas a política de replicação de saudação é a versão do sistema operacional específica. Se você tiver hosts diferentes em execução em versões diferentes do sistema operacional, crie políticas de replicação separadas para cada tipo de versão do sistema operacional. Por exemplo: se você tiver cinco hosts em execução no Windows Server 2012 e três no Windows Server 2012 R2, crie duas políticas de replicação – uma para cada tipo de versão do sistema operacional.

1. Obter contêiner de proteção primária hello (nuvem VMM primária) e o contêiner de proteção de recuperação (recuperação de nuvem do VMM), executando Olá comandos a seguir:

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Recuperar política Olá que você criou na etapa 1 usando nome amigável de saudação da política de saudação

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Inicie associação de saudação do recipiente de proteção da saudação (nuvem do VMM) com a política de replicação hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Aguarde Olá toocomplete de trabalho de associação de política. Você pode verificar se o trabalho de saudação foi concluído usando Olá trecho do PowerShell a seguir.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Depois que o trabalho de saudação concluiu o processamento, execute Olá comando a seguir:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).

## <a name="step-6-configure-network-mapping"></a>Etapa 6: Configurar o mapeamento de rede
1. Olá primeiro comando obtém servidores para o Cofre de recuperação de Site do Azure atual hello. comando Olá armazena servidores do Microsoft Azure Site Recovery Olá na variável de matriz de saudação $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Olá abaixo comandos obter rede de recuperação de site Olá para o servidor do VMM de origem de saudação e o servidor do VMM de destino hello.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > servidor do VMM de origem Olá pode ser Olá primeira ou segunda matriz de servidores de saudação em uma saudação. Verificar nomes Olá dos servidores do VMM hello e obter redes Olá adequadamente


1. Olá final cria um mapeamento entre Olá primário e rede Olá recuperação. Olá cmdlet especifica a rede primária Olá como primeiro elemento de saudação da rede de recuperação $PrimaryNetworks e hello como o primeiro elemento de saudação do $RecoveryNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Etapa 7: Configurar mapeamento de armazenamento
1. Olá abaixo comando obtém a lista de saudação de classificações de armazenamento em $storageclassifications variável.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Olá abaixo comandos obter a classificação de origem Olá na variável $SourceClassificaion e classificação de destino em $TargetClassification variável.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > classificações de origem e destino Olá podem ser qualquer elemento na matriz de saudação. Consulte a saída toohello Olá abaixo índice de saudação do comando toofigure de classificações de origem e de destino na matriz $storageclassifications.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. Olá abaixo cmdlet cria um mapeamento entre a classificação de origem hello e classificação de destino hello.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Etapa 8: habilitar a proteção para máquinas virtuais
Depois de redes, nuvens e servidores Olá estão configurados corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem de saudação.

1. proteção de tooenable executar Olá contêiner de proteção do comando tooget Olá a seguir:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Obtenha a entidade de proteção de saudação (VM) executando Olá comando a seguir:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Habilite a replicação para Olá VM executando Olá comando a seguir:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Testar a implantação
planejar a sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar um failover de teste para Olá tootest. O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.

> [!NOTE]
> Você pode criar um plano de recuperação para seu aplicativo no Portal do Azure.
>
>

conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).

### <a name="run-a-test-failover"></a>Execute um teste de failover
1. Execute Olá abaixo cmdlets tooget Olá VM rede toowhich que deseja tootest failover suas VMs.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Execute um failover de teste de uma VM fazendo Olá seguinte:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Execute um failover de teste de um plano de recuperação fazendo Olá seguinte:

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Executar um failover planejado
1. Execute um failover planejado de máquina virtual fazendo Olá seguinte:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Execute um failover planejado de um plano de recuperação fazendo Olá seguinte:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Executar um failover não planejado
1. Execute um failover não planejado de máquina virtual fazendo Olá seguinte:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. Execute um failover não planejado de um plano de recuperação fazendo Olá seguinte:

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <a name=monitor></a> Monitorar a atividade
Use hello atividade de saudação toomonitor comandos a seguir. Observe que você tenha toowait entre trabalhos de saudação toofinish de processamento.

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Próximas etapas
[Leia mais](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.
