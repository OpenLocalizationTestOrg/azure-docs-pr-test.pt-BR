---
title: "Olá aaaDeploy serviço de mobilidade de recuperação de Site com DSC de automação do Azure | Microsoft Docs"
description: "Descreve como toouse DSC de automação do Azure tooautomatically implantar o serviço de mobilidade do Azure Site Recovery hello e agente do Azure para VM do VMware e tooAzure de replicação de servidor físico"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>Implantar o serviço de mobilidade Olá com DSC de automação do Azure para a replicação de VM
No Operations Management Suite, oferecemos uma solução abrangente de backup e recuperação de desastre que pode ser usada como parte de seu plano de continuidade de negócios.

Começamos esta jornada com o Hyper-V, usando a Réplica do Hyper-V. Mas, temos toosupport expandida de uma instalação heterogênea porque os clientes têm vários hipervisores e plataformas em suas nuvens.

Se você estiver executando cargas de trabalho do VMware e/ou servidores físicos hoje, um servidor de gerenciamento executa todos os Olá componentes do Azure Site Recovery em seu ambiente toohandle Olá comunicação e replicação de dados com o Azure, quando o Azure é o destino.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Implantar o serviço de mobilidade de recuperação de Site hello usando DSC de automação
Vamos começar fazendo uma análise rápida do que este servidor de gerenciamento faz.

servidor de gerenciamento Olá executa várias funções de servidor. Uma dessas funções é a de *configuração*, que coordena a comunicação e gerencia os processos de replicação e recuperação de dados.

Além disso, Olá *processo* função atua como um gateway de replicação. Essa função recebe dados de replicação das máquinas de origem protegido, otimizá-lo com o cache, a compactação e criptografia e, em seguida, envia tooan conta de armazenamento do Azure. Uma das funções de saudação para a função do processo de saudação também é toopush instalação de máquinas de tooprotected de serviço de mobilidade hello e executar a descoberta automática de máquinas virtuais do VMware.

Se houver um failback do Azure, Olá *destino mestre* função manipulará os dados de replicação de saudação como parte dessa operação.

Para máquinas de saudação protegida, contamos com hello *serviço de mobilidade*. Esse componente é implantado tooevery máquina (VM VMware ou servidor físico) que você deseja tooreplicate tooAzure. Ele captura gravações de dados na máquina de saudação e encaminha-servidor de gerenciamento toohello (função de processo).

Quando você está lidando com continuidade dos negócios, é importante toounderstand suas cargas de trabalho, sua infraestrutura e Olá componentes envolvidos. Em seguida, você pode atender aos requisitos de saudação para seu objetivo de tempo de recuperação (RTO) e o objetivo de ponto de recuperação (RPO). Nesse contexto, Olá serviço de mobilidade está tooensuring chave suas cargas de trabalho protegidos conforme o esperado.

Sendo assim, como você pode assegurar, de forma otimizada, que tem uma configuração protegida confiável com a ajuda de alguns componentes do Operations Management Suite?

Este artigo fornece um exemplo de como você pode usar o Azure Automation desejado configuração de estado (DSC), junto com a recuperação de Site, tooensure que:

* serviço de mobilidade Hello e agente de VM do Azure são implantados toohello máquinas do Windows que você deseja tooprotect.
* serviço de mobilidade Hello e agente de VM do Azure sempre em execução quando o Azure é o destino de replicação hello.

## <a name="prerequisites"></a>Pré-requisitos
* Uma configuração do repositório toostore Olá necessária
* Uma frase secreta tooregister do repositório toostore Olá necessário com o servidor de gerenciamento Olá

  > [!NOTE]
  > Uma senha exclusiva é gerada para cada servidor de gerenciamento. Se você for toodeploy vários servidores de gerenciamento, você tem tooensure que Olá correto de senha é armazenada no arquivo de passphrase.txt de saudação.
  >
  >
* WMF Windows Management Framework () 5.0 instalado nos computadores de saudação que você deseja tooenable para proteção (um requisito para DSC de automação)

  > [!NOTE]
  > Se você quiser toouse máquinas de DSC do Windows que tem o WMF 4.0 instalado, consulte a seção de saudação [DSC de uso em ambientes desconectados](## Use DSC in disconnected environments).
  

serviço de mobilidade Olá pode ser instalado por meio da linha de comando hello e aceita vários argumentos. É por isso que você precisa de binários de saudação toohave (depois de extrai-los da sua configuração) e armazená-los em um local onde você pode recuperá-los usando uma configuração DSC.

## <a name="step-1-extract-binaries"></a>Etapa 1: Extrair os binários
1. arquivos de saudação tooextract que você precisa para esta instalação, navegue toohello directory a seguir no servidor de gerenciamento:

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    Nessa pasta, você verá um arquivo MSI chamado:

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    Use Olá instalador de saudação do tooextract de comando a seguir:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Selecione todos os arquivos e enviá-los a pasta compactada (zipada) da tooa.

Agora você tem binários Olá que você precisa a instalação do serviço de mobilidade de saudação Olá tooautomate usando DSC de automação.

### <a name="passphrase"></a>Senha
Em seguida, você precisa toodetermine onde você deseja tooplace essa pasta compactada. Você pode usar uma conta de armazenamento do Azure, como mostrado posteriormente, toostore Olá frase secreta que você precisa para a instalação de saudação. agente Olá, em seguida, será registrado no servidor de gerenciamento hello como parte do processo de saudação.

Olá frase secreta que você obteve quando você implantou o servidor de gerenciamento Olá pode ser salvo o arquivo de texto tooa como passphrase.txt.

Coloca pasta compactada hello e a frase secreta de saudação em um contêiner dedicado em Olá conta de armazenamento do Azure.

![Localização da pasta](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Se você preferir tookeep esses arquivos em um compartilhamento na rede, você pode fazer isso. Basta tooensure que recursos Olá DSC que você usará mais tarde tem acesso e podem obter a senha e a instalação de saudação.

## <a name="step-2-create-hello-dsc-configuration"></a>Etapa 2: Criar configuração Olá DSC
instalação de saudação depende do WMF 5.0. Para Olá máquina toosuccessfully aplicar configuração Olá por meio da DSC de automação, WMF 5.0 precisa toobe presente.

ambiente de saudação usa Olá exemplo de configuração de DSC a seguir:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
configuração de saudação fará a seguir hello:

* variáveis de saudação informará configuração Olá onde tooget Olá binários para o serviço de mobilidade hello e agente de VM do Azure hello, onde tooget Olá frase secreta, e toostore Olá de saída.
* Olá configuração vai importar recurso de xPSDesiredStateConfiguration DSC Olá, para que você possa usar `xRemoteFile` arquivos de saudação toodownload do repositório de saudação.
* configuração de saudação criará um diretório onde você deseja que os binários de saudação toostore.
* recursos de arquivo Hello extrairá os arquivos de saudação da pasta compactada hello.
* recurso de instalação do pacote de saudação instalará o serviço de mobilidade de saudação do hello UNIFIEDAGENT. Instalador do EXE com argumentos de saudação específico. (variáveis Olá construir argumentos Olá necessário tooreflect toobe alterado seu ambiente.)
* pacote de saudação AzureAgent recurso instalará hello Azure VM agent, que é recomendado em cada VM que é executado no Azure. Agente de VM do Azure Olá também torna possível tooadd extensões toohello VM após o failover.
* Olá recurso de serviço ou recursos garantirá que Olá relacionados a serviços de mobilidade e hello serviços do Azure sempre estão em execução.

Salvar configuração hello como **ASRMobilityService**.

> [!NOTE]
> Lembre-se tooreplace Olá CSIP no servidor de gerenciamento real de configuração tooreflect hello, para que hello agente será conectado corretamente e usará a senha correta da saudação.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>Etapa 3: Carregar tooAutomation DSC
Como configuração Olá DSC feitas importará um módulo de recurso de DSC necessário (xPSDesiredStateConfiguration), é necessário tooimport que o módulo de automação antes de carregar a configuração de saudação DSC.

Entrar tooyour conta de automação, procurar muito**ativos** > **módulos**e clique em **procurar galeria**.

Aqui você pode pesquisar Olá módulo e importá-lo tooyour conta.

![Importar módulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

Quando você terminar, vá tooyour máquina onde você tenha instalados os módulos do Azure Resource Manager hello e continuar a configuração de DSC tooimport Olá recém-criado.

### <a name="import-cmdlets"></a>Importar cmdlets
No PowerShell, entrar tooyour assinatura do Azure. Modificar Olá cmdlets tooreflect seu ambiente e capturar informações de sua conta de automação em uma variável:

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Carregar Olá configuração tooAutomation DSC usando Olá cmdlet a seguir:

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Compilar a configuração de saudação no DSC de automação
Em seguida, você precisa toocompile configuração de saudação no DSC de automação, para que você possa iniciar tooregister nós tooit. Para fazer isso executando Olá cmdlet a seguir:

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

Isso pode levar alguns minutos, porque você basicamente estiver implantando o serviço de pull de DSC do hello configuração toohello hospedado.

Depois de compilar a configuração de saudação, você pode recuperar informações de trabalho de hello usando o PowerShell (Get-AzureRmAutomationDscCompilationJob) ou usando Olá [portal do Azure](https://portal.azure.com/).

![Recuperar trabalho](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

Você agora com êxito publicado e carregar sua configuração de DSC tooAutomation DSC.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>Etapa 4: Carregar máquinas tooAutomation DSC
> [!NOTE]
> Um dos pré-requisitos Olá para concluir este cenário é que as máquinas do Windows são atualizadas com a versão mais recente de saudação do WMF. Você pode baixar e instalar a versão correta do hello para sua plataforma de saudação [Centro de Download](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

Agora, você criará um metaconfig para que você aplicará tooyour nós de DSC. toosucceed com isso, você precisa tooretrieve Olá ponto de extremidade URL e hello chave primária para sua conta de automação selecionada no Azure. Você pode encontrar esses valores em **chaves** em Olá **todas as configurações** folha para Olá conta de automação.

![Valores da chave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

Neste exemplo, você tem um servidor físico do Windows Server 2012 R2 que você deseja tooprotect usando a recuperação de Site.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Verificar as operações de renomeação de arquivo no registro Olá pendentes
Antes de você iniciar o servidor de saudação do tooassociate com o ponto de extremidade do hello DSC de automação, recomendamos que você verifique as operações de renomeação de arquivo no registro Olá pendentes. Eles podem Proibir instalação Olá Concluindo devido tooa uma reinicialização pendente.

Execute Olá tooverify cmdlet que não há nenhuma reinicialização pendente no servidor de saudação a seguir:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Se isso mostra vazio, você será tooproceed Okey. Caso contrário, você deve resolver isso, a reinicialização do servidor de saudação durante uma janela de manutenção.

configuração de saudação tooapply no servidor de saudação, inicie Olá ambiente de script integrado do PowerShell (ISE) e execute Olá script a seguir. Isso é essencialmente uma configuração local do DSC que instruem Olá tooregister de mecanismo de Gerenciador de configurações Local com hello service de DSC de automação e recuperar a configuração específica da saudação (ASRMobilityService.localhost).

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Essa configuração causará Olá Gerenciador de configurações Local tooregister mecanismo próprio com DSC de automação. Ele também determina como o mecanismo de saudação deve operar, que ele deve fazer se houver uma dessincronização da configuração (ApplyAndAutoCorrect) e como ele deve prosseguir com a configuração de saudação se uma reinicialização é necessária.

Depois de executar esse script, o nó Olá deve começar tooregister com DSC de automação.

![Registro de nó em andamento](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Se você voltar toohello portal do Azure, você pode ver o nó recém-registrados Olá agora aparece no portal de saudação.

![Nó registrado no portal de saudação](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

No servidor de saudação, você pode executar Olá PowerShell cmdlet tooverify que Olá nó foi registrado corretamente a seguir:

```powershell
Get-DscLocalConfigurationManager
```

Após a configuração Olá foi desconectado e aplicadas toohello server, você pode verificar isso executando Olá cmdlet a seguir:

```powershell
Get-DscConfigurationStatus
```

saída de Hello mostra que servidor Olá foi extraída com êxito sua configuração:

![Saída](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

Além disso, a instalação de serviço de mobilidade Olá tem seu próprio log que pode ser encontrado em *SystemDrive*\ProgramData\ASRSetupLogs.

É isso. Você agora com êxito implantados e registrados de serviço de mobilidade Olá na máquina de saudação que você deseja tooprotect usando a recuperação de Site. DSC garantirá que serviços Olá necessárias sempre estão em execução.

![Implantação bem-sucedida](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Depois que o servidor de gerenciamento de saudação detecta uma implantação bem-sucedida Olá, você pode configurar a proteção e habilitar a replicação na máquina hello usando recuperação de Site.

## <a name="use-dsc-in-disconnected-environments"></a>Usar o DSC em ambientes desconectados
Se seus computadores não toohello conectado à Internet, ainda dependem toodeploy DSC e configurar o serviço de mobilidade Olá em cargas de trabalho de saudação que você deseja tooprotect.

Você pode instanciar seu próprio servidor de pull de DSC em seu ambiente tooessentially fornecer Olá mesmos recursos que você obteve de DSC de automação. Ou seja, clientes Olá extrairá configuração hello (depois de registrado) toohello DSC de ponto de extremidade. No entanto, outra opção é máquinas toomanually push Olá DSC configuração tooyour, localmente ou remotamente.

Observe que neste exemplo, há um parâmetro adicional para o nome do computador hello. arquivos remotos Olá agora estão localizados em um compartilhamento remoto deve ser acessível por máquinas de saudação que você deseja tooprotect. fim de saudação do script hello aplica configuração hello e, em seguida, inicia o computador de destino tooapply Olá DSC configuração toohello.

### <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que Olá xPSDesiredStateConfiguration PowerShell o módulo está instalado. Para máquinas do Windows onde o WMF 5.0 está instalado, você pode instalar o módulo xPSDesiredStateConfiguration de saudação executando Olá cmdlet a seguir em computadores de destino hello:

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

Você também pode baixar e salvar o módulo Olá caso você precise toodistribute-tooWindows máquinas que tem o WMF 4.0. Execute este cmdlet em um computador em que o PowerShellGet (WMF 5.0) está presente:

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

Para o WMF 4.0, assegure-se também que Olá [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) esteja instalado nos computadores de saudação.

Olá configuração a seguir pode ser enviada tooWindows máquinas que têm o WMF 5.0 e WMF 4.0:

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Se você quiser tooinstantiate seu próprio servidor de pull de DSC em seus recursos Olá toomimic de rede corporativa que você pode obter de DSC de automação, consulte [Configurando um servidor de pull da web de DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>Opcional: implantar uma configuração de DSC usando um modelo do Azure Resource Manager
Este artigo concentra-se em como você pode criar seu próprios tooautomatically de configuração DSC implantar o serviço de mobilidade hello e hello Azure VM Agent – e certifique-se de que eles sejam executados em máquinas de saudação que você deseja tooprotect. Também temos um modelo de Gerenciador de recursos do Azure que irá implantar essa DSC configuração tooa nova ou existente do Azure conta de automação. modelo de saudação usará ativos de automação de toocreate de parâmetros de entrada que contém variáveis Olá para o seu ambiente.

Depois de implantar o modelo hello, você pode simplesmente consultar toostep 4 no tooonboard neste guia suas máquinas.

modelo de saudação fará a seguir hello:

1. Usar uma conta existente ou criar uma nova conta de Automação
2. Obter parâmetros de entrada para:
   * ASRRemoteFile – local Olá onde você armazenou a instalação do serviço de mobilidade Olá
   * ASRPassphrase – local Olá onde você armazenou o arquivo de passphrase.txt Olá
   * ASRCSEndpoint - endereço IP de saudação do servidor de gerenciamento
3. Importe o módulo do PowerShell xPSDesiredStateConfiguration Olá
4. Criar e compilar a configuração de DSC Olá

Saudação de todas as etapas anteriores ocorrerá na ordem correta do hello, para que você pode iniciar a integração de suas máquinas para proteção.

modelo de Hello, com instruções para implantação, está localizado em [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

Implante o modelo de saudação usando o PowerShell:

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Próximas etapas
Depois de implantar os agentes de serviço de mobilidade hello, você pode [habilitar replicação](site-recovery-vmware-to-azure.md) para máquinas virtuais de saudação.
