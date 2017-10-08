---
title: "ativos de aaaConnection na automação do Azure | Microsoft Docs"
description: "Ativos de Conexão na automação do Azure contêm Olá informações necessárias tooconnect tooan serviço ou aplicativo de um runbook ou a configuração DSC. Este artigo explica detalhes de saudação de conexões e como toowork-los na criação de texto e gráfico."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Ativos de conexão na Automação do Azure

Um ativo de conexão de automação contém Olá informações necessárias tooconnect tooan serviço ou aplicativo de um runbook ou a configuração DSC. Isso pode incluir as informações necessárias para autenticação, como um nome de usuário e senha em adição tooconnection de informações como uma URL ou uma porta. valor de saudação de uma conexão é manter todas as propriedades de saudação para conectar o aplicativo específico tooa em um ativo como toocreating contrário diversas variáveis. usuário Olá pode editar valores de saudação para uma conexão em um único local, e você pode passar o nome de saudação de uma conexão tooa runbook ou a configuração DSC em um único parâmetro. Olá propriedades para uma conexão pode ser acessada no runbook hello ou configuração de DSC com hello **Get-AutomationConnection** atividade.

Ao criar uma conexão, você deve especificar um *tipo de conexão*. tipo de conexão de saudação é um modelo que define um conjunto de propriedades. conexão Olá define valores para cada propriedade definida no seu tipo de conexão. Tipos de Conexão são adicionado tooAzure automação nos módulos de integração ou criados com hello [API de automação do Azure](http://msdn.microsoft.com/library/azure/mt163818.aspx) se o módulo de integração de saudação inclui um tipo de conexão e é importado para sua conta de automação. Caso contrário, será necessário toocreate um arquivo de metadados toospecify um tipo de conexão de automação.  Para saber mais sobre isso, veja [Módulos de integração](automation-integration-modules.md).  

>[!NOTE] 
>Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas. Esses ativos são criptografados e armazenados em Olá automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação. Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure. Antes de armazenar um ativo seguro, chave Olá para conta de automação de saudação é descriptografado usando certificado mestre hello e usado tooencrypt ativo de saudação.

## <a name="windows-powershell-cmdlets"></a>Cmdlets do Windows PowerShell

cmdlets Olá Olá a tabela a seguir são usada toocreate e gerenciar conexões de automação com o Windows PowerShell. Eles são fornecidos como parte da saudação [módulo Azure PowerShell](/powershell/azure/overview) que está disponível para uso em runbooks de automação e configurações de DSC.

|Cmdlet|Descrição|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Recupera uma conexão. Inclui uma tabela de hash com valores de saudação de campos da conexão hello.|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Cria uma nova conexão.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Remove uma conexão existente.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Define o valor de saudação de um determinado campo de uma conexão existente.|

## <a name="activities"></a>Atividades

atividades Olá Olá a tabela a seguir são conexões tooaccess usado em um runbook ou a configuração DSC.

|Atividades|Descrição|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Obtém um toouse de conexão. Retorna uma tabela de hash com propriedades de saudação da conexão hello.|

>[!NOTE] 
>Evite usar variáveis com hello – o parâmetro Name do **Get - AutomationConnection** pois isso pode complicar a descoberta de dependências entre runbooks ou configurações DSC e ativos de conexão em tempo de design.

## <a name="creating-a-new-connection"></a>Criando uma nova conexão

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate uma nova conexão com hello portal do Azure

1. Na sua conta de automação, clique em Olá **ativos** parte tooopen Olá **ativos** folha.
2. Clique em Olá **conexões** parte tooopen Olá **conexões** folha.
3. Clique em **adicionar uma conexão** na parte superior de saudação da folha de saudação.
4. Em Olá **tipo** suspenso, o tipo de saudação select de conexão que você deseja toocreate. formulário de saudação apresentará propriedades Olá para esse tipo específico.
5. Preencha o formulário de saudação e clique em **criar** toosave Olá nova conexão.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate uma nova conexão com hello portal clássico do Azure

1. Na sua conta de automação, clique em **ativos** na parte superior de saudação da janela de saudação.
2. Na parte inferior de saudação da janela de saudação, clique em **Adicionar configuração**.
3. Clique em **Adicionar Conexão**.
4. Em Olá **o tipo de Conexão** suspenso, o tipo de saudação select de conexão que você deseja toocreate.  Assistente de saudação apresentará propriedades Olá para esse tipo específico.
5. Conclua o Assistente de saudação e clique em conexão nova de Olá Olá de toosave caixa de seleção.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate uma nova conexão com o Windows PowerShell

Criar uma nova conexão com o Windows PowerShell usando Olá [AzureRmAutomationConnection novo](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet. Esse cmdlet tem um parâmetro denominado **ConnectionFieldValues** que espera um [tabela de hash](http://technet.microsoft.com/library/hh847780.aspx) definir valores para cada uma das propriedades de saudação definidas pelo tipo de conexão de saudação.

Se você estiver familiarizado com hello automação [conta executar como](automation-sec-configure-azure-runas-account.md) tooauthenticate runbooks usando a entidade de serviço hello, Olá script do PowerShell, fornecido como uma alternativa toocreating Olá Olá conta executar como do portal de saudação cria um novo ativo de conexão usando Olá comandos de exemplo a seguir.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Você está ativo de conexão toouse capaz de saudação script toocreate hello, pois quando você cria sua conta de automação, ele automaticamente inclui vários módulos global por padrão junto com o tipo de conexão de saudação **AzurServicePrincipal**Olá toocreate **AzureRunAsConnection** ativo de conexão.  Isso é importante tookeep em mente, porque se você tentar toocreate um novo serviço de tooa de tooconnect de ativo de conexão ou o aplicativo com um método de autenticação diferente, ele falhará porque o tipo de conexão de saudação já não está definido na sua conta de automação.  Para obter mais informações sobre como toocreate sua própria conexão de tipo para seu módulo de saudação ou personalizado [Galeria do PowerShell](https://www.powershellgallery.com), consulte [módulos de integração](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Usando uma conexão em um runbook ou configuração DSC

Recuperar uma conexão em um runbook ou a configuração de DSC com hello **Get-AutomationConnection** cmdlet.  Você não pode usar o hello [AzureRmAutomationConnection Get](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) atividade.  Essa atividade recupera valores de saudação dos campos diferentes de saudação na conexão hello e retorna-los como um [tabela de hash](http://go.microsoft.com/fwlink/?LinkID=324844) que pode ser usado com comandos apropriados Olá Olá runbook ou a configuração DSC.

### <a name="textual-runbook-sample"></a>Exemplo de runbook textual

Olá comandos de exemplo a seguir mostram como toouse Olá conta executar como mencionado anteriormente, tooauthenticate com recursos do Azure Resource Manager em seu runbook.  Ele usa conexão Olá ativo representando Olá conta executar como, que faz referência a entidade de serviço com base em certificado hello, não as credenciais.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Exemplos de runbook gráfico

Adicionar um **Get-AutomationConnection** tooa de atividade runbook gráfico clicando na conexão de saudação no painel de biblioteca de saudação do editor gráfico hello e selecionando **adicionar toocanvas**.

![](media/automation-connections/connection-add-canvas.png)

Olá imagem a seguir mostra um exemplo do uso de uma conexão em um runbook gráfico.  Isso é hello mesmo exemplo mostrado acima para autenticar usando a conta executar como da saudação com um runbook textual.  Este exemplo usa Olá **valor constante** conjunto de dados para Olá **obter Conexão de RunAs** atividade que usa um objeto de conexão para autenticação.  Um [link de pipeline](automation-graphical-authoring-intro.md#links-and-workflow) é usado aqui, pois Olá ServicePrincipalCertificate conjunto de parâmetros está esperando um objeto único.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Próximas etapas

- Revisão [Links no gráfico de criação](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand como Olá toodirect e controle de fluxo da lógica em seus runbooks.  

- toolearn mais sobre o uso da automação do Azure dos módulos do PowerShell e as práticas recomendadas para criar seu próprio toowork de módulos do PowerShell como módulos de integração na automação do Azure, consulte [módulos de integração](automation-integration-modules.md).  
