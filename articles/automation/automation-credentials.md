---
title: "ativos de aaaCredential na automação do Azure | Microsoft Docs"
description: "Ativos de credencial na automação do Azure contêm as credenciais de segurança que podem ser usados tooauthenticate tooresources acessados por runbook hello ou configuração de DSC. Este artigo descreve como toocreate ativos de credenciais e usá-los em um runbook ou a configuração DSC."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Ativos de credenciais na Automação do Azure
Um ativo da credencial de Automação tem um objeto [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) que contém as credenciais de segurança, como um nome de usuário e uma senha. Runbooks, configurações de DSC podem usar os cmdlets que aceitam um objeto PSCredential para autenticação, ou eles podem extrair Olá nome de usuário e senha de aplicativo de toosome PSCredential objeto tooprovide de hello ou serviço que requer autenticação. Propriedades de saudação de uma credencial são armazenadas com segurança na automação do Azure e podem ser acessadas no runbook hello ou configuração de DSC com hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) atividade.

> [!NOTE]
> Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas. Esses ativos são criptografados e armazenados em Olá automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação. Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure. Antes de armazenar um ativo seguro, chave Olá para conta de automação de saudação é descriptografado usando certificado mestre hello e usado tooencrypt ativo de saudação.  

## <a name="windows-powershell-cmdlets"></a>Cmdlets do Windows PowerShell
cmdlets Olá Olá a tabela a seguir são usada toocreate e gerenciar ativos de credencial de automação com o Windows PowerShell.  Eles são fornecidos como parte da saudação [módulo Azure PowerShell](/powershell/azure/overview) que está disponível para uso em runbooks de automação e configurações de DSC.

| Cmdlets | Descrição |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Recupera informações sobre um ativo de credencial. Você só pode recuperar a credencial Olá propriamente dita do **Get-AutomationPSCredential** atividade. |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Cria uma nova credencial de Automação. |
| [Remove- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Remove uma credencial de Automação. |
| [Set- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Conjuntos de Olá propriedades para uma credencial de automação existente. |

## <a name="runbook-activities"></a>Atividades de runbook
atividades Olá Olá a tabela a seguir são usados tooaccess credenciais em um runbook e configurações de DSC.

| Atividades | Descrição |
|:--- |:--- |
| Get-AutomationPSCredential |Obtém um toouse de credencial em um runbook ou a configuração DSC. Retorna um objeto [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) . |

> [!NOTE]
> Você deve evitar usar variáveis em hello – o parâmetro Name de Get-AutomationPSCredential, pois isso pode complicar a descoberta de dependências entre runbooks ou configurações DSC e ativos de credenciais em tempo de design.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Criando um novo ativo de credencial

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate um novo ativo de credencial com hello portal do Azure
1. Na sua conta de automação, clique em Olá **ativos** parte tooopen Olá **ativos** folha.
2. Clique em Olá **credenciais** parte tooopen Olá **credenciais** folha.
3. Clique em **adicionar uma credencial** na parte superior de saudação da folha de saudação.
4. Preencha o formulário de saudação e clique em **criar** toosave Olá nova credencial.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate um novo ativo de credencial com o Windows PowerShell
Olá comandos de exemplo a seguir mostram como toocreate uma automação nova credencial. Um objeto PSCredential é criado pela primeira vez com hello nome e senha e, em seguida, usado toocreate ativo de credencial de saudação. Como alternativa, você pode usar o hello **Get-Credential** toobe cmdlet solicitado tootype em um nome e uma senha.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate um novo ativo de credencial com hello portal clássico do Azure
1. Na sua conta de automação, clique em **ativos** na parte superior de saudação da janela de saudação.
2. Na parte inferior de saudação da janela de saudação, clique em **Adicionar configuração**.
3. Clique em **Adicionar Credencial**.
4. Em Olá **tipo de credencial** lista suspensa, selecione **credencial do PowerShell**.
5. Conclua o Assistente de saudação e clique em Olá caixa de seleção toosave Olá nova credencial.

## <a name="using-a-powershell-credential"></a>Usando uma credencial do PowerShell
Recuperar um ativo de credencial em um runbook ou a configuração de DSC com hello **Get-AutomationPSCredential** atividade. Isso retorna um [objeto PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) que você pode usar com uma atividade ou cmdlet que exija um parâmetro PSCredential. Você também pode recuperar propriedades de saudação do toouse de objeto de credencial Olá individualmente. Olá, objeto tem uma propriedade Olá nome de usuário e uma senha segura hello, ou você pode usar o hello **GetNetworkCredential** método tooreturn um [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) objeto que fornecerá um segura versão da senha de saudação.

### <a name="textual-runbook-sample"></a>Exemplo de runbook textual
Olá comandos de exemplo a seguir mostram como as credenciais em um runbook toouse do PowerShell. Neste exemplo, Olá credencial é recuperada e seu nome de usuário e a senha atribuída toovariables.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Exemplo de runbook gráfico
Adicionar um **Get-AutomationPSCredential** tooa de atividade runbook gráfico clicando na credencial Olá no painel de biblioteca de saudação do editor gráfico hello e selecionando **adicionar toocanvas**.

![Adicionar toocanvas de credencial](media/automation-credentials/credential-add-canvas.png)

Olá imagem a seguir mostra um exemplo do uso de uma credencial em um runbook gráfico.  Nesse caso, ele está sendo usado tooprovide autenticação para recursos de tooAzure um runbook conforme descrito em [Runbooks autenticar com a conta de usuário do AD do Azure](automation-create-aduser-account.md).  primeira atividade de saudação recupera credencial Olá que tenha acesso toohello assinatura do Azure.  Olá **Add-AzureAccount** atividade, em seguida, usa a autenticação de tooprovide de credencial para todas as atividades que vêm depois dele.  Um [link de pipeline](automation-graphical-authoring-intro.md#links-and-workflow) está disponível, já que **Get-AutomationPSCredential** está esperando um único objeto.  

![Adicionar toocanvas de credencial](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Usando uma credencial do PowerShell na DSC
Embora as Configurações DSC na Automação do Azure possam fazer referência aos ativos de credencial usando **Get-AutomationPSCredential**, os ativos de credencial também podem ser transmitidos por meio de parâmetros, se desejado. Para obter mais informações, veja [Compilando configurações na DSC de Automação do Azure](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre links na criação do gráfico, consulte [Links no gráfico de criação](automation-graphical-authoring-intro.md#links-and-workflow)
* métodos de autenticação diferentes toounderstand hello com automação, consulte [segurança da automação do Azure](automation-security-overview.md)
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md) 

