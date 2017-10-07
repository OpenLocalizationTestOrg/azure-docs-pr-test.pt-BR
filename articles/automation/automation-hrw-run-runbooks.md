---
title: "aaaRun runbooks no Hybrid Runbook Worker de automação do Azure | Microsoft Docs"
description: "Este artigo fornece informações sobre runbooks em execução em computadores em seu datacenter local ou o provedor de nuvem com a função de operador de Runbook híbrido hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Executar runbooks em um Hybrid Runbook Worker 
Não há nenhuma diferença na estrutura de saudação de runbooks que são executados na automação do Azure e aqueles que são executados em um trabalho de Runbook híbrido. Runbooks que você pode usar com cada provavelmente diferem significativamente embora como runbooks direcionando um Hybrid Runbook Worker normalmente gerenciar recursos no computador local de saudação em si ou a recursos no ambiente local hello, onde ele é implantado, enquanto runbooks na automação do Azure normalmente gerencie recursos em Olá nuvem do Azure.

Você pode editar um runbook para Hybrid Runbook Worker na automação do Azure, mas você pode ter problemas se você tentar tootest Olá runbook no editor de saudação.  módulos do PowerShell Olá que acessam recursos locais Olá talvez não esteja instalados em seu ambiente de automação do Azure nesse caso, o teste de saudação falhará.  Se você instalar Olá necessário módulos, em seguida, Olá runbook será executado, mas não será capaz de tooaccess recursos locais para um teste completo.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Iniciar um runbook no Hybrid Runbook Worker
[Como iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md) descreve métodos diferentes para se iniciar um runbook.  Hybrid Runbook Worker adiciona um **RunOn** opção onde você pode especificar o nome de saudação de um grupo de trabalho de Runbook híbrido.  Se um grupo for especificado, Olá runbook é recuperado e executando de trabalhadores Olá nesse grupo.  Se essa opção não for especificada, ele é executado na Automação do Azure como de costume.

Quando você iniciar um runbook no hello portal do Azure, você verá um **executados em** opção onde você pode selecionar **Azure** ou **Hybrid Worker**.  Se você selecionar **Hybrid Worker**, em seguida, você pode selecionar o grupo de saudação em uma lista suspensa.

Saudação de uso **RunOn** parâmetro.  Você pode usar o hello comando toostart um runbook chamado Test-Runbook em um grupo do Hybrid Runbook Worker denominado MyHybridGroup usando o Windows PowerShell a seguir.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Olá **RunOn** parâmetro foi adicionado toohello **Start-AzureAutomationRunbook** cmdlet na versão 0.9.1 do Microsoft Azure PowerShell.  Você deve [baixar a versão mais recente do hello](https://azure.microsoft.com/downloads/) se você tiver uma anterior instalada.  Você só precisa tooinstall esta versão em uma estação de trabalho onde você está iniciando o runbook de saudação do Windows PowerShell.  Não é necessário tooinstall-lo no computador de trabalho hello, a menos que você pretende runbooks toostart desse computador.  Atualmente você não pode iniciar um runbook em um trabalho de Runbook híbrido de outro runbook, pois isso exigiria a versão mais recente de saudação do Azure Powershell toobe instalado na sua conta de automação.  versão mais recente da saudação é atualizado automaticamente na automação do Azure e automaticamente propagada toohello trabalhadores em breve.
>
>

## <a name="runbook-permissions"></a>Permissões de runbook
Runbooks em execução em um trabalho de Runbook híbrido não é possível usar Olá mesmo método que é normalmente usado para runbooks autenticando tooAzure recursos, desde que eles acessam recursos fora do Azure.  Olá runbook pode fornecer sua própria autenticação toolocal recursos, ou você pode especificar uma conta de RunAs tooprovide um contexto de usuário para todos os runbooks.

### <a name="runbook-authentication"></a>Autenticação de runbook
Por padrão, os runbooks serão executados no contexto Olá Olá conta de sistema local no computador do local de hello, para que eles devem fornecer suas próprias tooresources de autenticação que eles acessarão.  

Você pode usar [credencial](http://msdn.microsoft.com/library/dn940015.aspx) e [certificado](http://msdn.microsoft.com/library/dn940013.aspx) ativos no seu runbook com os cmdlets que permitem que você toospecify credenciais para autenticar o toodifferent recursos.  Olá, exemplo a seguir mostra uma parte de um runbook que reinicia um computador.  Ele recupera as credenciais de um nome de ativo e hello de credencial do computador de saudação de um ativo de variável e, em seguida, usa esses valores com hello Restart-Computer cmdlet.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

Você também pode aproveitar [InlineScript](automation-powershell-workflow.md#inlinescript), que permite que você toorun blocos de código em outro computador com as credenciais especificadas pelo Olá [parâmetro comum PSCredential](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>Conta RunAs
Em vez de ter runbooks fornecer sua própria autenticação toolocal recursos, você pode especificar um **RunAs** conta para um grupo do Hybrid worker.  Você especifica um [ativo de credencial](automation-credentials.md) que tenha acesso toolocal recursos, e todos os runbooks são executados sob essas credenciais ao executar em um trabalho de Runbook híbrido em grupo hello.  

nome de usuário Olá credencial Olá deve ter uma saudação formatos a seguir:

* domínio\nome de usuário
* username@domain
* nome de usuário (para contas locais toohello, computador local)

Use Olá seguindo o procedimento toospecify uma conta executar como para um grupo do Hybrid worker:

1. Criar um [ativo de credencial](automation-credentials.md) com toolocal acessar os recursos.
2. Abra conta de automação Olá no hello portal do Azure.
3. Selecione Olá **grupos de trabalho híbrida** lado a lado e, em seguida, selecione o grupo de saudação.
4. Escolha **Todas as configurações** e **Configurações do grupo do Hybrid Worker**.
5. Alterar **executar como** de **padrão** muito**personalizado**.
6. Selecione a credencial hello e clique em **salvar**.

### <a name="automation-run-as-account"></a>Conta de automação Executar como
Como parte do processo de compilação automatizado para implantação de recursos no Azure, você pode exigir acesso local tooon sistemas toosupport uma tarefa ou um conjunto de etapas na sequência de implantação.  autenticação toosupport no Azure usando a conta executar como do hello, é necessário tooinstall Olá executar como certificado de conta.  

Olá runbook do PowerShell a seguir *RunAsCertificateToHybridWorker de exportação*, exporta Olá executar como certificado de sua conta de automação do Azure e downloads e importa-o para o repositório de certificados do computador local Olá em um Operador híbrido conectado toohello mesma conta.  Após essa etapa é concluída, ela verifica trabalho Olá pode autenticar com êxito tooAzure usando Olá a conta executar como.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Salvar Olá *RunAsCertificateToHybridWorker de exportação* runbook tooyour computador com um `.ps1` extensão.  Importe-o para sua conta de automação e editar runbook hello, alterar valor variável Olá Olá `$Password` com sua própria senha.  Publicar e, em seguida, executar runbook Olá direcionando o grupo do Hybrid Worker Olá que executam o e autenticar usando a conta executar como da saudação de runbooks.  Olá trabalho fluxo relatórios Olá tentativa tooimport Olá certificado no repositório de computador local hello e segue com várias linhas, dependendo do número de contas de automação é definido em sua assinatura e se a autenticação for bem-sucedida.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Solucionando problemas de runbooks no Hybrid Runbook Worker
Os logs são armazenados localmente em cada hybrid worker, em C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Operador híbrido também registra erros e eventos no log de eventos do Windows hello em **aplicativos e serviços Logs\Microsoft-SMA\Operational**.  Eventos relacionados toorunbooks executados no trabalho de saudação são gravados muito**aplicativos e serviços Logs\Microsoft-Automation\Operational**.  Olá **Microsoft SMA** log inclui muitos mais eventos relacionados toohello runbook trabalho toohello enviadas por push hello e trabalho processamento de runbook hello.  Durante a saudação **automação do Microsoft** log de eventos não tem muitos eventos com detalhes para ajudar com a saudação de solução de problemas de execução de runbook, pelo menos, você encontrará resultados Olá Olá do trabalho de runbook.  

[Mensagens e saída de runbook](automation-runbook-output-and-messages.md) são enviadas tooAzure automação de operadores híbrido apenas como trabalhos de runbook executados na nuvem hello.  Você também pode habilitar Olá detalhado e fluxos de andamento Olá mesma maneira que faria para outros runbooks.  

Se seus runbooks não são concluídas com êxito e o resumo do trabalho de saudação mostra um status de **suspenso**, examine o artigo de solução de problemas de saudação [Hybrid Runbook Worker: um trabalho de runbook termina com um status de Suspenso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre métodos diferentes de saudação que pode ser usado toostart um runbook, consulte [iniciando um Runbook na automação do Azure](automation-starting-a-runbook.md).  
* toounderstand Olá diferentes procedimentos para trabalhar com runbooks do PowerShell e fluxo de trabalho do PowerShell na automação do Azure usando o editor de texto hello, consulte [editando um Runbook na automação do Azure](automation-edit-textual-runbook.md)
