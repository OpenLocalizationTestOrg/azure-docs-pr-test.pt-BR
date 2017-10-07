---
title: "máquinas virtuais de aaaReplicate Hyper-V nas nuvens do VMM usando o Azure Site Recovery e PowerShell (Gerenciador de recursos) | Microsoft Docs"
description: "Replicar máquinas virtuais de Hyper-V em nuvens do VMM usando o Azure Site Recovery e PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Replicar máquinas virtuais Hyper-V no tooAzure de nuvens do VMM usando o PowerShell e o Gerenciador de recursos do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-azure.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portal clássico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - clássico](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Visão geral
O Azure Site Recovery contribui com a estratégia de recuperação (BCDR) tooyour business desastre e continuidade ao orquestrar a replicação, failover e recuperação de máquinas virtuais em vários cenários de implantação. Para obter uma lista completa de implantação de cenários consulte Olá [visão geral do Azure Site Recovery](site-recovery-overview.md).

Este artigo mostra como as tarefas comuns do toouse PowerShell tooautomate precisar tooperform ao configurar máquinas virtuais do Azure Site Recovery tooreplicate Hyper-V no armazenamento do System Center VMM nuvens tooAzure.

Olá artigo inclui os pré-requisitos para o cenário de saudação e mostra

* Como tooset um cofre de serviços de recuperação
* Instalar Olá provedor Azure Site Recovery no servidor do VMM de origem de saudação
* Registrar o servidor de saudação no cofre hello, adicione uma conta de armazenamento do Azure
* Instalar o agente de serviços de recuperação do Azure Olá nos servidores de host do Hyper-V
* Definir configurações de proteção para nuvens do VMM, que poderá ser máquinas virtuais de tooall aplicada protegido
* Habilitar a proteção para essas máquina virtuais
* Teste Olá failover toomake se que tudo está funcionando conforme o esperado.

Se você tiver problemas para configurar esse cenário, publique suas perguntas sobre Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação do Gerenciador de recursos de saudação.
>
>

## <a name="before-you-start"></a>Antes de começar
Verifique se estes pré-requisitos estão em vigor:

### <a name="azure-prerequisites"></a>Pré-requisitos do Azure
* Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Se não tiver uma, comece com uma [conta gratuita](https://azure.microsoft.com/free). Além disso, você pode ler sobre Olá [preços do Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Se você está experimentando o cenário de assinatura Olá replicação tooa CSP, você terá uma assinatura do CSP. Saiba mais sobre o programa CSP Olá no [como tooenroll no programa CSP Olá](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* Você precisará de um tooAzure de dados replicados toostore conta do Azure v2 (Gerenciador de recursos) de armazenamento. conta de saudação precisa de replicação geográfica habilitada. Deve estar no hello mesma região Olá serviço Azure Site Recovery e ser associada a saudação mesma assinatura ou Olá CSP. toolearn mais sobre como configurar o armazenamento do Azure, consulte Olá [tooMicrosoft Introdução armazenamento do Azure](../storage/common/storage-introduction.md) para referência.
* Você precisará toomake-se de que máquinas virtuais que você deseja tooprotect estejam em conformidade com hello [pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Atualmente, apenas operações no nível de VM são possíveis por meio do Powershell. Em breve, será disponibilizado o suporte para operações no nível de plano de recuperação.  Agora, você está limitado tooperforming falha renovação somente em uma granularidade de 'protected VM' e não em um nível de plano de recuperação.
>
>

### <a name="vmm-prerequisites"></a>Pré-requisitos do VMM
* Você precisará do servidor VMM em execução no System Center 2012 R2.
* Nenhum servidor VMM que contêm máquinas virtuais que você deseja tooprotect devem estar executando o hello provedor Azure Site Recovery. Isso é instalado durante a saudação implantação do Azure Site Recovery.
* Você precisará de pelo menos uma nuvem em Olá servidor VMM que você deseja tooprotect. Olá nuvem deve conter:
  * Um ou mais grupos de hosts do VMM
  * Um ou mais servidores de host do Hyper-V ou clusters em cada grupo de host.
  * Um ou mais VMs no servidor de origem Hyper-V de saudação.
* Saiba mais sobre como configurar nuvens VMM:
  * Leia mais sobre nuvens privadas do VMM no [o que há de novo na nuvem privada com o System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e em [nuvens do VMM 2012 e hello](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Saiba mais sobre [Configurando Olá VMM malha de nuvem](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Depois que os elementos de malha de nuvem estiverem em vigor, veja como criar nuvens privadas em [Criando uma nuvem privada no VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e [Passo a passo: criando de nuvens privadas com o System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Pré-requisitos do Hyper-V
* Olá servidores host Hyper-V devem estar executando pelo menos **Windows Server 2012** com a função Hyper-V ou **Microsoft Hyper-V Server 2012** e ter Olá as últimas atualizações instaladas.
* Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereços IP estáticos. Você precisará agente do cluster Olá tooconfigure manualmente. Por
* Para obter instruções, consulte [como tooConfigure agente de réplica do Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Qualquer servidor de host do Hyper-V ou cluster para o qual você deseja toomanage proteção deve ser incluído em uma nuvem VMM.

### <a name="network-mapping-prerequisites"></a>Pré-requisitos de mapeamento de rede
Quando você protege as máquinas virtuais no Azure, o mapeamento de rede Olá mapeia redes de máquina virtual Olá no servidor do VMM de origem hello e seguinte de saudação do destino redes do Azure tooenable:

* Todos os computadores que o failover em Olá mesmo rede pode se conectar a outro, independentemente do plano de recuperação que estão em tooeach.
* Se um gateway de rede estiver instalado na rede Azure de destino hello, máquinas virtuais podem se conectar a tooother em máquinas virtuais.
* Se você não configurar o mapeamento de rede, Olá somente máquinas virtuais que falhar em Olá mesmo plano de recuperação será capaz de tooconnect tooeach outros após tooAzure de failover.

Se você quiser que o mapeamento de rede toodeploy você precisará seguir hello:

* saudação de máquinas virtuais que deseja tooprotect no servidor do VMM de origem de saudação deve ser conectado tooa rede VM. Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.
* Máquinas de virtuais de toowhich replicado uma rede do Azure podem se conectar após o failover. Você selecionará essa rede no tempo de saudação do failover. rede Olá deve estar no hello mesma região que sua assinatura do Azure Site Recovery.

Saiba mais sobre mapeamento de rede em

* [Como tooconfigure de redes lógicas no VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Como tooconfigure VM redes e gateways no VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Como tooconfigure e monitorar redes virtuais no Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

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
1. Crie um grupo de recursos no Azure Resource Manager se você ainda não tiver um

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Criar um novo cofre de serviços de recuperação e salve Olá criada o objeto de Cofre de recuperação automatizada do sistema em uma variável (será usada posteriormente). Você também pode recuperar Olá ASR cofre post criação do objeto usando o cmdlet Get-AzureRMRecoveryServicesVault de saudação:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Etapa 3: Definir o contexto de Cofre de serviços de recuperação de saudação

Definir o contexto de Cofre de saudação executando Olá comando abaixo.

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

## <a name="step-5-create-an-azure-storage-account"></a>Etapa 5: criar uma conta de armazenamento do Azure

Se você não tiver uma conta de armazenamento do Azure, crie uma conta de replicação geográfica habilitada no hello mesma área geográfica como Olá cofre executando Olá comando a seguir:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Observe que a conta de armazenamento Olá deve ser Olá mesma região que o serviço do Azure Site Recovery hello e associar Olá a mesma assinatura.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Etapa 6: Instalar hello Azure Recovery Services Agent
1. Baixar o agente de serviços de recuperação do Azure Olá em [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e instale-o em cada servidor de host do Hyper-V localizado nas Olá VMM nuvens que você deseja tooprotect.
2. Execute Olá comando a seguir em todos os hosts do VMM:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Etapa 7: definir as configurações da proteção de nuvem
1. Crie um tooAzure de política de replicação executando Olá comando a seguir:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Obtenha um contêiner de proteção executando Olá comandos a seguir:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Obter Olá política detalhes tooa variável usando Olá trabalho que foi criado e mencione o nome da política amigável hello:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Inicie associação de saudação do recipiente de proteção de saudação com a política de replicação hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Após o trabalho de hello, execute Olá comando a seguir:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Depois que o trabalho de saudação concluiu o processamento, execute Olá comando a seguir:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).

## <a name="step-8-configure-network-mapping"></a>Etapa 8: configurar o mapeamento de rede
Antes de começar o mapeamento de rede Verifique se máquinas virtuais no servidor do VMM de origem de saudação tooa conectado rede VM. Além disso, crie uma ou mais redes virtuais do Azure.

Saiba mais sobre como toocreate a virtual de rede usando o Gerenciador de recursos do Azure e o PowerShell, no [criar uma rede virtual com uma conexão de VPN site a site usando o Gerenciador de recursos do Azure e o PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Observe que várias redes de máquina Virtual podem ser mapeado tooa única rede do Azure. Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.

1. Olá primeiro comando obtém servidores para o Cofre de recuperação de Site do Azure atual hello. comando Olá armazena servidores do Microsoft Azure Site Recovery Olá na variável de matriz de saudação $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Olá segundo comando obtém a rede de recuperação de site Olá para o primeiro servidor de saudação na matriz de saudação $Servers. comando Olá armazena redes Olá na variável de saudação $Networks.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. Olá terceiro comando obtém as redes virtuais do Azure e, em seguida, esse valor na variável Olá $AzureVmNetworks.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. Olá final cria um mapeamento entre Olá primário e rede Olá máquina virtual do Azure. Olá cmdlet especifica a rede primária hello como o primeiro elemento de saudação do $Networks. Olá cmdlet especifica uma rede de máquina virtual como o primeiro elemento de saudação do $AzureVmNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Etapa 9: habilitar a proteção para máquinas virtuais
Depois de redes, nuvens e servidores Olá estão configurados corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem de saudação.

 Observe o seguinte hello:

* As máquinas virtuais devem cumprir os requisitos do Azure. Verifique essas [pré-requisitos e suporte](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) no guia de planejamento de saudação.
* proteção tooenable, sistema operacional de saudação e propriedades do disco do sistema operacional devem ser definidas para a máquina virtual de saudação. Quando você cria uma máquina virtual no VMM usando um modelo de máquina virtual, você pode definir propriedade de saudação. Você também pode definir essas propriedades para máquinas virtuais existentes em Olá **geral** e **configuração de Hardware** guias de propriedades de máquina virtual de saudação. Se você não definir essas propriedades no VMM, você será capaz de tooconfigure-los no portal do Azure Site Recovery hello.

1. proteção de tooenable executar Olá contêiner de proteção do comando tooget Olá a seguir:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Obtenha a entidade de proteção de saudação (VM) executando Olá comando a seguir:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Habilite hello DR para Olá VM executando Olá comando a seguir:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Testar a implantação
tootest sua implantação, você pode executar um teste de failover em uma única máquina virtual, ou crie um plano de recuperação consiste em várias máquinas virtuais e executar um teste de failover para o plano de saudação. O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada. Observe que:

* Se você quiser tooconnect toohello VM no Azure usando a área de trabalho remota após failover hello, habilite Conexão de área de trabalho remota na máquina virtual de saudação antes de executar o failover de teste de saudação.
* Após o failover, você usará uma público IP endereço tooconnect toohello VM no Azure usando a área de trabalho remota. Se você quiser toodo isso, certifique-se de que você não tem qualquer política de domínio que impedem a máquina de virtual tooa conectar usando um endereço público.

conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).

### <a name="run-a-test-failover"></a>Execute um teste de failover
- Inicie o failover de teste Olá executando Olá comando a seguir:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Executar um failover planejado
- Saudação de iniciar o failover planejado executando o comando a seguir de saudação:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Executar um failover não planejado
- Iniciar Olá failover não planejado executando Olá comando a seguir:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
