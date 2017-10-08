---
title: "configurações de aaaCompiling no DSC de automação do Azure | Microsoft Docs"
description: "Este artigo descreve como as configurações de configuração de estado desejado (DSC) toocompile para automação do Azure."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Compilando configurações no DSC de Automação do Azure

Você pode compilar configurações de configuração de estado desejado (DSC) de duas maneiras na automação do Azure: no hello portal do Azure e com o Windows PowerShell. Olá tabela a seguir ajudam a determinar quando toouse qual método com base em características de saudação de cada um:

### <a name="azure-portal"></a>Portal do Azure

* Método mais simples com interface do usuário interativo
* Valores de parâmetro simples do formulário tooprovide
* Acompanhar facilmente o estado do trabalho
* Acesso autenticado com o logon do Azure

### <a name="windows-powershell"></a>Windows PowerShell

* Chame da linha de comando com os cmdlets do Windows PowerShell
* Pode ser incluído em uma solução automatizada com várias etapas
* Fornece valores de parâmetro simples e complexos.
* Acompanha o estado do trabalho
* Cliente necessário toosupport cmdlets do PowerShell
* Transmitir ConfigurationData
* Compilar configurações que usam credenciais

Depois de decidir sobre um método de compilação, você pode seguir os procedimentos de respectivos de saudação abaixo toostart compilação.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>Compilar uma configuração de DSC com hello portal do Azure

1. Em sua conta de Automação, clique em **Configurações DSC**.
2. Clique em uma configuração tooopen sua folha.
3. Clique em **Compilar**.
4. Se a configuração de saudação não tiver parâmetros, será tooconfirm solicitada se você deseja toocompile-lo. Se a configuração de saudação tiver parâmetros, Olá **compilar configuração** folha será aberta para que possa fornecer os valores de parâmetro. Consulte Olá [ **parâmetros básicos** ](#basic-parameters) seção abaixo para obter mais detalhes sobre os parâmetros.
5. Olá **trabalho de compilação** folha é aberta para que você pode acompanhar o status do trabalho de compilação hello e hello configurações do nó (documentos MOF de configuração) causou toobe colocada em Olá servidor de Pull de DSC do Azure Automation.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Compilando uma Configuração DSC com o Windows PowerShell

Você pode usar [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compilar com o Windows PowerShell. Olá, código de exemplo a seguir inicia a compilação de uma configuração DSC chamada **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`Retorna uma compilação que você pode usar tootrack seu status de objeto de trabalho. Você pode usar esse objeto de trabalho de compilação com [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine status de saudação do trabalho de compilação de saudação e [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview seus fluxos (saída). Olá, código de exemplo a seguir inicia a compilação de saudação **SampleConfig** configuração, aguarda até que ele foi concluído e exibe seus fluxos.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Parâmetros básicos
Declaração de parâmetro em configurações de DSC, incluindo tipos de parâmetro e propriedades, works Olá mesmo como runbooks de automação do Azure. Consulte [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md) toolearn mais informações sobre parâmetros de runbook.

Olá, exemplo a seguir usa dois parâmetros chamados **FeatureName** e **IsPresent**, valores de saudação toodetermine das propriedades Olá **ParametersExample.sample** nó configuração, gerada durante a compilação.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

Você pode compilar configurações DSC que usam parâmetros básicos no portal de DSC de automação do Azure hello, ou com o Azure PowerShell:

### <a name="portal"></a>Portal

No portal de saudação, você pode inserir valores de parâmetro depois de clicar em **compilar**.

![texto alternativo](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell requer parâmetros em um [hashtable](http://technet.microsoft.com/library/hh847780.aspx) onde chave Olá corresponde o nome do parâmetro hello e Olá valor for igual a valor do parâmetro hello.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

Para obter informações sobre como transmitir PSCredentials como parâmetros, confira <a href="#credential-assets">**Ativos de credencial**</a> abaixo.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** permite a configuração estrutural tooseparate de qualquer configuração específica do ambiente durante o uso de DSC do PowerShell. Consulte [separando "O que" de "Onde" PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn mais sobre **ConfigurationData**.

> [!NOTE]
> Você pode usar **ConfigurationData** ao compilar no DSC de automação do Azure usando o PowerShell do Azure, mas não no hello portal do Azure.

Olá exemplo DSC configuração a seguir usa **ConfigurationData** via Olá **$ConfigurationData** e **$AllNodes** palavras-chave. Você também precisará Olá [ **xWebAdministration** módulo](https://www.powershellgallery.com/packages/xWebAdministration/) para este exemplo:

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

Você pode compilar a configuração de DSC Olá acima com o PowerShell. Olá abaixo do PowerShell adiciona dois toohello de configurações de nó servidor de Pull de DSC do Azure Automation: **ConfigurationDataSample.MyVM1** e **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Ativos

Referências de ativos são Olá mesmo em runbooks e as configurações DSC de automação do Azure. Veja a seguir Olá para obter mais informações:

* [Certificados](automation-certificates.md)
* [Conexões](automation-connections.md)
* [Credenciais](automation-credentials.md)
* [Variáveis](automation-variables.md)

### <a name="credential-assets"></a>Ativos de credencial

Embora as Configurações DSC na Automação do Azure possam fazer referência aos ativos de credencial usando **Get-AzureRmAutomationCredential**, os ativos de credencial também podem ser transmitidos por meio de parâmetros, se desejado. Se uma configuração aceita um parâmetro de **PSCredential** digite, em seguida, é necessário o nome de cadeia de caracteres de saudação toopass de um ativo de credencial de automação do Azure como valores do parâmetro, em vez de um objeto PSCredential. Em segundo plano hello, ativo de credencial de automação do Azure Olá com esse nome será recuperado e passado toohello configuração.

Manter credenciais segura em configurações do nó (documentos MOF de configuração) requer a criptografia de credenciais Olá no arquivo do MOF de configuração de nó de saudação. Automação do Azure vai ainda mais e criptografa o arquivo MOF inteiro de saudação. No entanto, no momento você deve dizer DSC do PowerShell é okey para credenciais toobe enviada em texto sem formatação durante a geração do MOF de configuração de nó, porque DSC do PowerShell não sabe que automação do Azure será criptografar arquivo MOF inteiro de saudação após seu geração por meio de um trabalho de compilação.

Você pode informar DSC do PowerShell que é okey para credenciais toobe enviada em texto sem formatação na configuração de nó Olá gerado MOFs usando [ **ConfigurationData**](#configurationdata). Você deve passar `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** para o nome do bloco de cada nó que aparece na configuração de saudação DSC e usa credenciais.

Olá, exemplo a seguir mostra uma configuração de DSC que usa um ativo de credencial de automação.

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

Você pode compilar a configuração de DSC Olá acima com o PowerShell. Olá abaixo do PowerShell adiciona dois toohello de configurações de nó servidor de Pull de DSC do Azure Automation: **CredentialSample.MyVM1** e **CredentialSample.MyVM2**.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>Como importar configurações de nó

Você também pode importar configurações de nó (MOFs) que você compilou fora do Azure. Uma das vantagens disso é que as configurações de nó podem ser assinadas.
Uma configuração de nó assinado é verificada localmente em um nó gerenciado por agente Olá DSC, garantindo que a configuração hello está sendo aplicada toohello nó vem de uma origem autorizada.

> [!NOTE]
> Você pode importar configurações assinadas em sua conta de Automação do Azure, mas a Automação do Azure não oferece suporte à compilação de configurações assinadas.

> [!NOTE]
> Um arquivo de configuração do nó não deve ser maior que 1 MB tooallow-toobe importado para a automação do Azure.

Você pode aprender como configurações do nó toosign em https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Importar uma configuração de nó no hello portal do Azure

1. Em sua conta de Automação, clique em **Configurações do nó DSC**.

    ![Configurações de nó DSC](./media/automation-dsc-compile/node-config.png)
2. Em Olá **configurações do nó DSC** folha, clique em **adicionar um NodeConfiguration**.
3. Em Olá **importação** folha, clique Olá pasta ícone próximo toohello **arquivo de configuração de nó** toobrowse da caixa de texto para um arquivo de configuração de nó (MOF) em seu computador local.

    ![Procurar arquivo local](./media/automation-dsc-compile/import-browse.png)
4. Insira um nome no hello **nome da configuração** caixa de texto. Esse nome deve corresponder a saudação nome da configuração de saudação do qual a configuração do nó Olá foi compilada.
5. Clique em **OK**.

### <a name="importing-a-node-configuration-with-powershell"></a>Importar uma configuração de nó com o PowerShell

Você pode usar o hello [AzureRmAutomationDscNodeConfiguration importação](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport uma configuração de nó em sua conta de automação.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



