---
title: "aaaReplicate tooAzure de VMs Hyper-V no portal clássico do hello com o PowerShell | Microsoft Docs"
description: "Automatizar a replicação de saudação de máquinas virtuais de Hyper-V nas nuvens do VMM usando o PowerShell e recuperação de Site no portal clássico Olá"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Replicar tooAzure de VMs Hyper-V com o PowerShell no portal clássico Olá
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

artigo Olá inclui os pré-requisitos para o cenário de saudação e mostra a você como tooset um cofre da recuperação de Site, instale Olá provedor Azure Site Recovery no servidor do VMM de origem de saudação, registrar o servidor de saudação no cofre hello, adicione uma conta de armazenamento do Azure, instale o hello Azure Agente de serviços de recuperação em servidores de host do Hyper-V, definir configurações de proteção para nuvens do VMM que serão máquinas virtuais de tooall aplicada protegido e, em seguida, habilite a proteção para as máquinas virtuais. Concluir teste Olá failover toomake se que tudo está funcionando conforme o esperado.

Se você tiver problemas para configurar esse cenário, publique suas perguntas sobre Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello.
>
>

## <a name="before-you-start"></a>Antes de começar
Verifique se estes pré-requisitos estão em vigor:

### <a name="azure-prerequisites"></a>Pré-requisitos do Azure
* Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Você precisará de um toostore replicado dados da conta de armazenamento do Azure. conta de saudação precisa de replicação geográfica habilitada. Deve estar no hello mesma região do cofre do Azure Site Recovery hello e associar Olá a mesma assinatura. [Saiba mais sobre o Armazenamento do Azure](../storage/common/storage-introduction.md).
* Você precisará toomake-se de que máquinas virtuais que você deseja tooprotect estejam em conformidade com [pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>Pré-requisitos do VMM
* Você precisará do servidor VMM em execução no System Center 2012 R2.
* Você precisará de pelo menos uma nuvem em Olá servidor VMM que você deseja tooprotect. Olá nuvem deve conter:
  * Um ou mais grupos de hosts do VMM
  * Um ou mais servidores host Hyper-V ou clusters em cada grupo de hosts.
  * Um ou mais VMs no servidor de origem Hyper-V de saudação.

### <a name="hyper-v-prerequisites"></a>Pré-requisitos do Hyper-V
* Olá servidores host Hyper-V devem estar executando pelo menos **Windows Server 2012** com a função Hyper-V ou **Microsoft Hyper-V Server 2012** e ter Olá as últimas atualizações instaladas.
* Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereços IP estáticos. Você precisará agente do cluster Olá tooconfigure manualmente. toodo isso, no Gerenciador do servidor > Gerenciador de Cluster de Failover, conecte-se o cluster toohello, clique em **configurar função** e selecione **agente de réplica do Hyper-V** em Olá **Selecionar função**tela do Assistente para alta disponibilidade de saudação.
* Qualquer servidor de host do Hyper-V ou cluster para o qual você deseja toomanage proteção deve ser incluído em uma nuvem VMM.

### <a name="network-mapping-prerequisites"></a>Pré-requisitos de mapeamento de rede
Quando você protege máquinas virtuais no mapeamento de rede do Azure mapeia entre redes VM no servidor do VMM de origem de saudação e procedimentos de saudação do destino redes do Azure tooenable:

* Todos os computadores que o failover em Olá mesmo rede pode se conectar a outro, independentemente do plano de recuperação que estão em tooeach.
* Se um gateway de rede estiver instalado na rede Azure de destino hello, máquinas virtuais podem se conectar a tooother em máquinas virtuais.
* Se você não configurar rede mapeamento apenas as máquinas virtuais que fazem failover no hello mesmo plano de recuperação será capaz de tooconnect tooeach outros após tooAzure de failover.

Se você quiser que o mapeamento de rede toodeploy você precisará seguir hello:

* saudação de máquinas virtuais que deseja tooprotect no servidor do VMM de origem de saudação deve ser conectado tooa rede VM. Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.
* Máquinas de virtuais de toowhich replicado uma rede do Azure podem se conectar após o failover. Você selecionará essa rede no tempo de saudação de failover. rede Olá deve estar no hello mesma região que sua assinatura do Azure Site Recovery.

### <a name="powershell-prerequisites"></a>Pré-requisitos do PowerShell
Certifique-se de que ter toogo pronto do PowerShell do Azure. Se você já estiver usando o PowerShell, você precisará tooupgrade tooversion 0.8.10 ou posterior. Para obter informações sobre como configurar o PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs). Depois de você ter instalado e configurado o PowerShell, você pode exibir todos os cmdlets de saudação disponíveis para o serviço de saudação [aqui](/powershell/azure/overview).

toolearn sobre dicas que podem ajudá-lo a usar os cmdlets de saudação, como como valores de parâmetro, as entradas e saídas são tratadas normalmente no Azure PowerShell, consulte [Introdução aos Cmdlets do Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Etapa 1: Definir a assinatura de saudação
No PowerShell, execute estes cmdlets:

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Substitua elementos Olá Olá "< >" com as informações específicas.

## <a name="step-2-create-a-site-recovery-vault"></a>Etapa 2: criar um cofre da Recuperação de Site
No PowerShell, substitua elementos Olá Olá "< >" com suas informações específicas e execute estes comandos:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>Etapa 3: gerar uma chave de registro do cofre
Gere uma chave de registro no cofre de saudação. Depois de baixar Olá provedor Azure Site Recovery e instalá-lo no servidor do VMM hello, você usará esse servidor do VMM Olá tooregister chave no cofre de saudação.

1. Obter o arquivo de configuração do cofre hello e defina o contexto de saudação:

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Definir o contexto do cofre Olá executando Olá comandos a seguir:

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Etapa 4: Instalar Olá provedor Azure Site Recovery
1. Na máquina do VMM hello, crie um diretório executando Olá comando a seguir:

   ```

   pushd C:\ASR\

   ```
2. Extrair arquivos hello usando o provedor de saudação baixada executando o comando a seguir de saudação

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Instale o provedor de saudação usando Olá comandos a seguir:

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Aguarde Olá toofinish de instalação.
4. Registre o servidor de saudação no cofre de saudação usando Olá comando a seguir:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>Etapa 5: criar uma conta de armazenamento do Azure
Se você não tiver uma conta de armazenamento do Azure, crie uma conta de replicação geográfica habilitada executando Olá comando a seguir:

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Observe que a conta de armazenamento Olá deve ser Olá mesma região que o serviço do Azure Site Recovery hello e associar Olá a mesma assinatura.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Etapa 6: Instalar hello Azure Recovery Services Agent
Olá portal do Azure, o agente de serviços de recuperação do Azure Olá instalação em cada servidor de host do Hyper-V localizado nas nuvens do VMM Olá deseja tooprotect.

Execute Olá comando a seguir em todos os hosts do VMM:

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>Etapa 7: definir as configurações da proteção de nuvem
1. Crie um tooAzure de perfil de proteção de nuvem executando Olá comando a seguir:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Obtenha um contêiner de proteção executando Olá comandos a seguir:

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Inicie associação de saudação do recipiente de proteção de saudação com nuvem hello:

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Após o trabalho de hello, execute Olá comando a seguir:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Depois que o trabalho de saudação concluiu o processamento, execute Olá comando a seguir:

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



conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).

## <a name="step-8-configure-network-mapping"></a>Etapa 8: configurar o mapeamento de rede
Antes de começar o mapeamento de rede Verifique se máquinas virtuais no servidor do VMM de origem de saudação tooa conectado rede VM. Além disso, crie uma ou mais redes virtuais do Azure. Observe que várias redes VM podem ser mapeadas tooa única rede do Azure.

Observe que se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover. Se não houver uma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.

Olá primeiro comando obtém servidores para o Cofre de recuperação de Site do Azure atual hello. comando Olá armazena servidores do Microsoft Azure Site Recovery Olá na variável de matriz de saudação $Servers.

    $Servers = Get-AzureSiteRecoveryServer


Olá segundo comando obtém a rede de recuperação de site Olá para o primeiro servidor de saudação na matriz de saudação $Servers. comando Olá armazena redes Olá na variável de saudação $Networks.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

Olá terceiro comando obtém suas assinaturas do Azure usando o cmdlet Get-AzureSubscription de Olá e, em seguida, armazena esse valor na variável Olá $Subscriptions.

    $Subscriptions = Get-AzureSubscription



Olá quarto comando obtém as redes virtuais do Azure usando o cmdlet Get-AzureVNetSite de saudação e, em seguida, esse valor na variável Olá $AzureVmNetworks.

    $AzureVmNetworks = Get-AzureVNetSite



Olá final cria um mapeamento entre Olá primário e rede Olá máquina virtual do Azure. Olá cmdlet especifica a rede primária hello como o primeiro elemento de saudação do $Networks. Olá cmdlet especifica uma rede de máquina virtual como o primeiro elemento de saudação do $AzureVmNetworks usando sua ID. comando de saudação inclui sua ID de assinatura do Azure.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>Etapa 9: habilitar a proteção para máquinas virtuais
Depois de servidores, nuvens e redes configuradas corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem hello. Observe o seguinte hello:

Máquinas virtuais devem cumprir os [Pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

sistema operacional do tooenable proteção hello e propriedades do disco do sistema operacional devem ser definidas para a máquina virtual de saudação. Quando você cria uma máquina virtual no VMM usando um modelo de máquina virtual, você pode definir propriedade de saudação. Você também pode definir essas propriedades para máquinas virtuais existentes em Olá **geral** e **configuração de Hardware** guias de propriedades de máquina virtual de saudação. Se você não definir essas propriedades no VMM, você será capaz de tooconfigure-los no portal do Azure Site Recovery hello.

1. proteção de tooenable executar Olá contêiner de proteção do comando tooget Olá a seguir:

     $ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName
2. Obtenha a entidade de proteção de saudação (VM) executando Olá comando a seguir:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Habilite hello DR para Olá VM executando Olá comando a seguir:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Testar a implantação
planejar a sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar um failover de teste para Olá tootest. O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada. Observe que:

* Se você quiser tooconnect toohello VM no Azure usando a área de trabalho remota após o failover hello, habilite Conexão de área de trabalho remota na máquina virtual de saudação antes de executar o failover de teste de saudação.
* Após o failover, você usará uma público IP endereço tooconnect toohello VM no Azure usando a área de trabalho remota. Se você quiser toodo isso, certifique-se de que você não tem qualquer política de domínio que impedem a máquina de virtual tooa conectar usando um endereço público.

conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).

### <a name="create-a-recovery-plan"></a>Criar um plano de recuperação
1. Criar um arquivo. XML como um modelo para o plano de recuperação usando dados de saudação abaixo e salve-o como "C:\RPTemplatePath.xml".
2. Alterar o nó de RecoveryPlan Olá Id, nome, PrimaryServerId e SecondaryServerId.
3. Altere Olá ProtectionEntity nó PrimaryProtectionEntityId (vmid do VMM).
4. Você pode adicionar mais VMs adicionando mais nós ProtectionEntity.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Preencha dados Olá no modelo de saudação:

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Crie hello RecoveryPlan:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Execute um teste de failover
1. Obter o objeto de RecoveryPlan de saudação executando Olá comando a seguir:

     $RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;
2. Inicie o failover de teste Olá executando Olá comando a seguir:

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


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
[Leia mais](/powershell/azure/overview) sobre os cmdlets do PowerShell do Azure Site Recovery. </a>.
