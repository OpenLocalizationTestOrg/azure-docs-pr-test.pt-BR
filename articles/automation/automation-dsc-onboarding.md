---
title: "aaaOnboarding máquinas para o gerenciamento de DSC de automação do Azure | Microsoft Docs"
description: "Como toosetup máquinas para o gerenciamento com DSC de automação do Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Por que gerenciar máquinas com o DSC de Automação do Azure?

Como a [Configuração de Estado Desejado do PowerShell](https://technet.microsoft.com/library/dn249912.aspx), a Configuração de Estado Desejado da Automação do Azure é um serviço de gerenciamento de configuração simples, mas poderoso, para nós DSC (máquinas físicas e virtuais) em qualquer datacenter de nuvem ou no local. Ela permite a escalabilidade entre milhares de máquinas rápida e facilmente a partir de um local central e seguro. Você pode facilmente integradas máquinas, atribuir configurações declarativas, além de exibir relatórios mostrando cada máquina do estado de toohello desejado de conformidade especificado. camada de gerenciamento de DSC de automação do Azure Olá é tooDSC qual camada de gerenciamento de automação do Azure Olá é tooPowerShell script. Em outras palavras, Olá mesma forma que a automação do Azure ajuda a gerenciar scripts do PowerShell, ele também ajuda a gerenciar configurações de DSC. toolearn mais sobre os benefícios de saudação do uso de DSC de automação do Azure, consulte [visão geral de DSC de automação do Azure](automation-dsc-overview.md).

DSC de automação do Azure pode ser usado toomanage várias máquinas:

* Máquinas virtuais do Azure (clássico)
* Máquinas virtuais do Azure
* Máquinas virtuais do AWS (Amazon Web Services)
* Máquinas físicas/virtuais locais do Windows, ou em uma nuvem diferente do Azure/AWS
* Máquinas físicas/virtuais locais do Linux, no Azure, ou em uma nuvem diferente do Azure

Além disso, se você não estiver pronto toomanage a configuração de máquina da nuvem Olá, DSC de automação do Azure também pode ser usado como um ponto de extremidade somente de relatório. Isso permite a configuração desejada tooset (push) por meio do local do DSC e exibir detalhes de relatório avançados sobre a conformidade de nó com hello desejado estado na automação do Azure.

Olá seções a seguir descrevem como você pode integrar cada tipo de máquina tooAzure DSC de automação.

## <a name="azure-virtual-machines-classic"></a>Máquinas virtuais do Azure (clássico)

Com DSC de automação do Azure, você pode facilmente integradas máquinas virtuais do Azure (clássica) para gerenciamento de configuração usando Olá portal do Azure, ou o PowerShell. Bastidores hello e sem um administrador que tem tooremote em Olá VM, Olá extensão de configuração de estado desejado do Azure VM registra Olá VM com DSC de automação do Azure. Como Olá extensão de configuração de estado desejado do Azure VM executa de modo assíncrono, as etapas tootrack seu progresso ou solucionar problemas ele são fornecidas nos Olá [ **integração de máquina virtual do Azure de solução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)seção abaixo.

### <a name="azure-portal"></a>Portal do Azure

Em Olá [portal do Azure](http://portal.azure.com/), clique em **procurar** -> **máquinas virtuais (clássicas)**. Selecione Olá VM do Windows que você deseja tooonboard. Na folha de painel Olá máquina virtual, clique em **todas as configurações** -> **extensões** -> **adicionar**  ->   **DSC de automação do Azure** -> **criar**. Digite hello [valores do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para seu caso de uso, chave de registro da sua conta de automação e URL de registro e, opcionalmente, um toohello de tooassign de configuração do nó VM.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

URL de registro toofind hello e chave Olá automação conta tooonboard Olá máquina, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Máquinas virtuais do Azure

DSC de automação do Azure permite integradas facilmente máquinas virtuais do Azure para gerenciamento de configuração, usando Olá portal do Azure, modelos do Azure Resource Manager ou o PowerShell. Bastidores hello e sem um administrador que tem tooremote em Olá VM, Olá extensão de configuração de estado desejado do Azure VM registra Olá VM com DSC de automação do Azure. Como Olá extensão de configuração de estado desejado do Azure VM executa de modo assíncrono, as etapas tootrack seu progresso ou solucionar problemas ele são fornecidas nos Olá [ **integração de máquina virtual do Azure de solução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)seção abaixo.

### <a name="azure-portal"></a>Portal do Azure

Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello conta de automação do Azure onde deseja que as máquinas virtuais de tooonboard. No painel da conta de automação hello, clique em **nós DSC** -> **adicionar a máquina virtual do Azure**.

Em **selecionar máquinas virtuais tooonboard**, selecione um ou tooonboard de máquinas virtuais do Azure mais.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

Em **configurar dados de registro**, digite Olá [valores do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para seu caso de uso e, opcionalmente, um toohello de tooassign de configuração do nó VM.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Modelos do Gerenciador de Recursos do Azure

Máquinas virtuais do Azure pode ser implantadas e incorporados tooAzure DSC de automação por meio de modelos do Gerenciador de recursos do Azure. Consulte [configurar uma VM por meio da extensão de DSC e DSC de automação do Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) para um modelo de exemplo que onboards um tooAzure VM existente DSC de automação. toofind Olá chave e registro de URL de registro feito como entrada nesse modelo, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.

### <a name="powershell"></a>PowerShell

Olá [AzureRmAutomationDscNode registro](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet pode ser usado tooonboard máquinas virtuais Olá portal do Azure por meio do PowerShell.

## <a name="amazon-web-services-aws-virtual-machines"></a>Máquinas virtuais do AWS (Amazon Web Services)

Você pode facilmente integradas máquinas virtuais de Amazon Web Services para o gerenciamento de configuração DSC de automação do Azure usando Olá AWS DSC Toolkit. Você pode aprender mais sobre o Kit de ferramentas de saudação [aqui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Máquinas físicas/virtuais locais do Windows, ou em uma nuvem diferente do Azure/AWS

As máquinas do Windows local e máquinas do Windows Azure não nuvens (como Amazon Web Services) também podem ser incorporados tooAzure DSC de automação, desde que eles têm acesso de saída toohello internet, por meio de algumas etapas simples:

1. Certifique-se de que versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) está instalado nos computadores de saudação desejado tooonboard tooAzure DSC de automação.
2. Siga as instruções de saudação na seção [ **gerando DSC metaconfigurações** ](#generating-dsc-metaconfigurations) abaixo toogenerate uma pasta que contém a saudação necessário metaconfigurações de DSC.
3. Aplica remotamente as máquinas de toohello metaconfiguração PowerShell DSC Olá deseja tooonboard. **máquina de saudação este comando é executado no deve ter a versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) instalado**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Se você não pode aplicar Olá PowerShell DSC metaconfigurações remotamente, copie a pasta de metaconfigurações de saudação da etapa 2 para cada máquina tooonboard. Em seguida, chame **Set-DscLocalConfigurationManager** localmente em cada máquina tooonboard.
5. Usando Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora são mostrados como nós DSC registrado em sua conta de automação do Azure.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Máquinas físicas/virtuais locais do Linux, no Azure, ou em uma nuvem diferente do Azure

Linux local máquinas, máquinas Linux no Azure, e máquinas Linux no Azure não nuvens também podem ser incorporados tooAzure DSC de automação, desde que eles têm acesso de saída toohello internet, por meio de algumas etapas simples:

1. Certifique-se de que versão mais recente de saudação do [configuração de estado desejado do PowerShell para Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) está instalado nos computadores de saudação desejado tooonboard tooAzure DSC de automação.
2. Se hello [padrões do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) diferenciar maiusculas de minúsculas seu uso e você desejar tooonboard máquinas tal que elas **ambos** por pull e relatar tooAzure DSC de automação:

   + Em cada Linux máquina tooonboard tooAzure DSC de automação, use tooonboard Register.py usando Olá padrões do Gerenciador de configurações de Local de DSC do PowerShell:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind Olá chave e registro de URL de registro para sua conta de automação, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.

     Padrões do Gerenciador de configuração Local do PowerShell DSC se hello **fazer** **não** diferenciar maiusculas de minúsculas seu uso, ou se desejar tooonboard máquinas, de modo que eles só tooAzure DSC de automação de relatório, mas não pull configuração ou módulos do PowerShell, execute as etapas 3 a 6. Caso contrário, vá diretamente toostep 6.

3. Siga as instruções de Olá Olá [ **gerando DSC metaconfigurações** ](#generating-dsc-metaconfigurations) seção abaixo toogenerate uma pasta que contém a saudação necessário metaconfigurações de DSC.
4. Aplicam-se remotamente as máquinas de toohello metaconfiguração PowerShell DSC Olá deseja tooonboard:

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

máquina de saudação este comando é executado no deve ter a versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) instalado.

1. Se você não pode aplicar Olá PowerShell DSC metaconfigurações remotamente, para cada tooonboard de máquina do Linux, copie máquina de toothat Olá metaconfiguração correspondente da pasta de saudação na etapa 5 no computador do Linux hello. Em seguida, chame `SetDscLocalConfigurationManager.py` localmente em cada computador Linux, você deseja tooonboard tooAzure DSC de automação:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Usando Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora são mostrados como nós DSC registrado em sua conta de automação do Azure.

## <a name="generating-dsc-metaconfigurations"></a>Gerando metaconfigurações DSC

toogenerically integrar qualquer máquina tooAzure DSC de automação, um [metaconfiguração do DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) pode ser gerado que, quando aplicada, informa ao agente Olá DSC no hello máquina toopull de e/ou reportar tooAzure DSC de automação. DSC metaconfigurações para DSC de automação do Azure podem ser geradas usando uma configuração de DSC do PowerShell ou cmdlets do PowerShell do Azure Automation hello.

> [!NOTE]
> Metaconfigurações de DSC contêm Olá segredos necessário tooonboard um tooan conta de automação de gerenciamento do computador. Verifique se tooproperly proteger qualquer metaconfigurações de DSC que você criar ou excluí-los após o uso.

### <a name="using-a-dsc-configuration"></a>Usando uma Configuração de DSC

1. Abra Olá ISE do PowerShell como administrador em um computador no seu ambiente local. máquina de saudação deve ter a versão mais recente de saudação do [WMF 5](http://aka.ms/wmf5latest) instalado.
2. Saudação de cópia localmente o script a seguir. Esse script contém uma configuração de DSC do PowerShell para criar metaconfigurações e tookick um comando desativar a criação de metaconfiguração hello.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Preencha chave de registro hello e URL para sua conta de automação, bem como os nomes de saudação do hello máquinas tooonboard. Todos os outros parâmetros são opcionais. toofind Olá chave e registro de URL de registro para sua conta de automação, consulte Olá [ **proteger o registro** ](#secure-registration) seção abaixo.
4. Se você quiser Olá máquinas tooreport DSC status informações tooAzure DSC de automação, mas não pull de configuração ou módulos do PowerShell, defina Olá **ReportOnly** tootrue de parâmetro.
5. Execute o script hello. Agora você deve ter uma pasta chamada **DscMetaConfigs** no diretório de trabalho, contendo Olá metaconfigurações de DSC do PowerShell para Olá máquinas tooonboard (como administrador):

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Usando os cmdlets de automação do Azure Olá

Se os padrões do Gerenciador de configuração Local do PowerShell DSC Olá corresponderem seu caso de uso, e você deseja que as máquinas de tooonboard, de modo que eles tanto por pull e relatam tooAzure DSC de automação, Olá cmdlets de automação do Azure fornecem um método simplificado de geração de saudação DSC metaconfigurações necessário:

1. Abra o console do PowerShell hello ou ISE do PowerShell como administrador em uma máquina no seu ambiente local.
2. Conecte-se usando o Gerenciador de recursos tooAzure **AzureRmAccount adicionar**
3. Baixe Olá DSC do PowerShell metaconfigurações para máquinas Olá deseja tooonboard de saudação automação conta toowhich que você deseja que os nós de tooonboard:

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. Agora você deve ter uma pasta chamada ***DscMetaConfigs***, que contém a saudação metaconfigurações de DSC do PowerShell para Olá máquinas tooonboard (como administrador):
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Proteger o registro

Máquinas podem tooan com segurança integrada conta de automação do Azure por meio do protocolo de registro do WMF 5 DSC saudação, que permite que um nó tooauthenticate tooa PowerShell DSC V2 Pull ou relatórios servidor DSC (incluindo DSC de automação do Azure). nó Olá registra toohello server em uma **URL de registro**, autenticação usando um **chave de registro**. Durante o registro, o nó Olá DSC e servidor de Pull de DSC/relatórios negociam um certificado exclusivo para este toouse de nó para pós-registro de autenticação toohello servidor. Esse processo impede que nós integrados representem um ao outro, por exemplo, se um nó for comprometido e estiver se comportando de maneira mal-intencionada. Após o registro, a chave de registro de saudação não é usado para autenticação novamente e é excluído do nó de saudação.

Você pode obter informações de saudação necessárias para o protocolo de registro de saudação DSC da saudação **gerenciar chaves** folha no portal de visualização do Azure hello. Abrir esta folha clicando ícone chave Olá Olá **Essentials** painel para Olá conta de automação.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* URL de registro é o campo de URL de saudação na folha de gerenciamento de chaves de saudação.
* Chave de registro é Olá chave de acesso primária ou chave de acesso secundária na folha de gerenciamento de chaves de saudação. Qualquer chave pode ser usada.

Para maior segurança, as chaves de acesso primária e secundária saudação de uma conta de automação podem ser regeneradas a qualquer momento (em Olá **gerenciar chaves** folha) tooprevent registros de nó futuro usando chaves anteriores.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Solução de problemas de integração de máquina virtual do Azure

O DSC de Automação do Azure permite a fácil integração de VMs do Microsoft Azure ao gerenciamento de configuração. Bastidores Olá, Olá extensão de configuração de estado desejado do Azure VM é usada tooregister Olá VM com DSC de automação do Azure. Como Olá extensão de configuração de estado desejado do Azure VM executa de modo assíncrono, controle o progresso e execução de solução de problemas podem ser importantes.

> [!NOTE]
> Qualquer método de integração tooAzure uma VM do Windows Azure DSC de automação que usa a extensão de configuração de estado desejado do Azure VM Olá pode levar até tooan horas para Olá nó tooshow backup registrados na automação do Azure. Isso é devido a instalação de toohello do Windows Management Framework 5.0 no hello VM pela extensão de DSC de VM do Azure hello, que é necessário tooonboard Olá VM tooAzure DSC de automação.

status de Olá tootroubleshoot ou modo de exibição de extensão de configuração de estado desejado do Azure VM, no portal do Azure de saudação do hello navegue toohello VM sendo integrados, em seguida, clique em -> **todas as configurações** -> **extensões**   ->  **DSC**. Para obter mais detalhes, você pode clicar em **Exibir status detalhado**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Expiração do certificado e um novo registro

Depois de registrar um computador como um nó de DSC no DSC de automação do Azure, há várias razões por que talvez seja necessário tooreregister nesse nó no hello futura:

* Após o registro, cada nó negocia automaticamente um certificado exclusivo para autenticação, que expira depois de um ano. Atualmente, Olá protocolo de registro de DSC do PowerShell não é possível renovar automaticamente certificados quando eles estão se aproximando da expiração, portanto, você precisa nós de saudação tooreregister após a hora de um ano. Antes de registrar novamente, certifique-se de que cada nó está executando o Windows Management Framework 5.0 RTM. Se certificado de autenticação de um nó irá expirar e não for registrado novamente o nó de saudação, nó hello serão toocommunicate não é possível com a automação do Azure e será marcado como 'Sem resposta.' Um novo registro executadas 90 dias ou menos de tempo de expiração do certificado hello, ou a qualquer momento após a hora de expiração do certificado hello, resultará em um novo certificado que está sendo gerado e usado.
* toochange qualquer [valores do Gerenciador de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) que foram definidas durante o registro inicial do nó de saudação, como ConfigurationMode. Atualmente, esses valores de agente do DSC só podem ser alterados por meio de um novo registro. uma exceção de Olá Olá configuração de nó atribuída nó toohello--isso pode ser alterado no DSC de automação do Azure diretamente.

Um novo registro pode ser executado em Olá mesmo maneira registrado nó Olá inicialmente, usando qualquer um dos métodos de integração de saudação descrita neste documento. Não é necessário toounregister um nó do DSC de automação do Azure antes registrando-lo novamente.

## <a name="related-articles"></a>Artigos relacionados

* [Visão geral do DSC de Automação do Azure](automation-dsc-overview.md)
* [cmdlets da DSC de Automação do Azure](/powershell/module/azurerm.automation/#automation)
* [preço da DSC de Automação do Azure](https://azure.microsoft.com/pricing/details/automation/)
