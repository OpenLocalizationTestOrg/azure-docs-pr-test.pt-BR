---
title: "ativos de aaaVariable na automação do Azure | Microsoft Docs"
description: "Os ativos de variável são valores que estão disponíveis tooall runbooks e as configurações de DSC na automação do Azure.  Este artigo explica detalhes de saudação de variáveis e como toowork-los na criação de texto e gráfico."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Ativos variáveis na Automação do Azure

Os ativos de variável são valores que estão disponíveis tooall runbooks e as configurações de DSC em sua conta de automação. Eles podem ser criados, modificados e recuperados de saudação portal do Azure, Windows PowerShell e de um runbook ou a configuração DSC. Variáveis de automação são úteis para Olá os seguintes cenários:

- Compartilhe um valor entre vários runbooks ou configurações DSC.

- Compartilhar um valor entre vários trabalhos do hello mesmo runbook ou a configuração DSC.

- Gerencie um valor no portal de saudação ou na linha de comando do Windows PowerShell Olá é usada por runbooks ou configurações de DSC, como um conjunto de itens de configuração comuns como lista específica de nomes de VM, um grupo de recursos específico, um nome de domínio do AD, etc.  

Variáveis de automação são mantidas para que continuem toobe disponível mesmo se houver falha Olá runbook ou a configuração DSC.  Isso também permite que um toobe valor definido por um runbook que é usado por outro, ou é usado por Olá mesmo runbook ou saudação de configuração DSC próxima vez que ele é executado.

Quando uma variável é criada, você pode definir que ele seja armazenado criptografado.  Quando uma variável é criptografada, ela é armazenada com segurança na automação do Azure e seu valor não pode ser recuperado da saudação [AzureRmAutomationVariable Get](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet que é fornecido como parte do módulo do PowerShell do Azure hello.  Olá única maneira de recuperar um valor criptografado é de saudação **Get-AutomationVariable** atividade em um runbook ou a configuração DSC.

> [!NOTE]
> Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas. Esses ativos são criptografados e armazenados em Olá automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação. Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure. Antes de armazenar um ativo seguro, chave Olá para conta de automação de saudação é descriptografado usando certificado mestre hello e usado tooencrypt ativo de saudação.

## <a name="variable-types"></a>Tipos de variável

Quando você cria uma variável com hello portal do Azure, você deve especificar um tipo de dados na lista suspensa de saudação para que portal Olá possa exibir o controle apropriado de saudação para inserir o valor da variável hello. Olá variável não é restrito toothis dados tipo, mas você deve definir variável de saudação usando o Windows PowerShell se você quiser toospecify um valor de um tipo diferente. Se você especificar **não definido**, valor variável Olá Olá será definido muito**$null**, e você deve definir o valor de saudação com hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet ou **Set-AutomationVariable** atividade.  Não é possível criar ou alterar o valor de saudação para um tipo complexo de variável no portal de saudação, mas você pode fornecer um valor de qualquer tipo usando o Windows PowerShell. Tipos complexos serão retornados como um [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

Você pode armazenar vários valores tooa única variável criando uma matriz ou tabela de hash e salvando-o toohello variável.

Olá seguem uma lista de tipos de variáveis disponíveis na automação:

* Cadeia de caracteres
* Número inteiro
* DateTime
* Booliano
* Nulo

## <a name="cmdlets-and-workflow-activities"></a>Atividades de fluxo de trabalho e cmdlets

cmdlets Olá Olá a tabela a seguir são usada toocreate e gerenciar variáveis de automação com o Windows PowerShell. Eles são fornecidos como parte da saudação [módulo Azure PowerShell](../powershell-install-configure.md) que está disponível para uso em runbooks de automação e a configuração de DSC.

|Cmdlets|Descrição|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Recupera o valor de saudação de uma variável existente.|
|[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|Cria uma nova variável e define o seu valor.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Remove uma variável existente.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Define o valor de saudação de uma variável existente.|

atividades de fluxo de trabalho de saudação em Olá a tabela a seguir são usadas tooaccess variáveis de automação em um runbook. Eles só estão disponíveis para uso em um runbook ou a configuração DSC e não são fornecidas como parte do módulo do PowerShell do Azure hello.

|Atividades de fluxo de trabalho|Descrição|
|:---|:---|
|Get-AutomationVariable|Recupera o valor de saudação de uma variável existente.|
|Set-AutomationVariable|Define o valor de saudação de uma variável existente.|

> [!NOTE] 
> Você deve evitar usar variáveis em hello – o parâmetro Name do **Get-AutomationVariable** em um runbook ou a configuração de DSC, pois isso pode complicar a descoberta de dependências entre runbooks ou configuração de DSC e automação variáveis em tempo de design.

## <a name="creating-a-new-automation-variable"></a>Criando uma nova variável de automação

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate uma nova variável com hello portal do Azure

1. Na sua conta de automação, clique em Olá **ativos** lado a lado e, em seguida, em Olá **ativos** folha, selecione **variáveis**.
2. Em Olá **variáveis** lado a lado, selecione **adicionar uma variável**.
3. Concluir opções Olá Olá **nova variável** folha e clique em **criar** salvar Olá nova variável.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate uma nova variável com o Windows PowerShell

Olá [AzureRmAutomationVariable novo](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet cria uma nova variável e define seu valor inicial. Você pode recuperar o valor de saudação usando [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Se o valor de saudação é um tipo simples, esse mesmo tipo é retornado. Se for um tipo complexo, um **PSCustomObject** é retornado.

saudação de exemplo a seguir comandos mostram como toocreate uma variável do tipo cadeia de caracteres e, em seguida, seu valor de retorno.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

saudação de exemplo a seguir comandos mostram como toocreate uma variável com um complexo de tipo e, em seguida, retornar suas propriedades. Nesse caso, é usado um objeto máquina virtual de **Get-AzureRmVm** .

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Usando uma variável em um runbook ou configuração DSC 

Saudação de uso **Set-AutomationVariable** valor de hello atividade tooset de uma variável de automação em um runbook ou a configuração DSC e a saudação **Get-AutomationVariable** tooretrieve-lo.  Você não deve usar o hello **Set-AzureAutomationVariable** ou **Get-AzureAutomationVariable** cmdlets em um runbook ou a configuração de DSC, já que eles são menos eficientes do que as atividades de fluxo de trabalho de saudação.  Também é possível recuperar valor de saudação de variáveis seguras com **Get-AzureAutomationVariable**.  Olá toocreate de maneira somente uma nova variável de dentro de um runbook ou a configuração de DSC está Olá toouse [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.


### <a name="textual-runbook-samples"></a>Exemplos de runbook textual

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Definindo e recuperando um valor simples de uma variável

saudação de exemplo a seguir comandos mostram como tooset e recuperar uma variável em um runbook textual. Nesse exemplo, presume-se que as variáveis do tipo integer denominadas *NumberOfIterations* e *NumberOfRunnings*, além de uma variável do tipo cadeia de caracteres denominada *SampleMessage*, já foram criadas.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Definindo e recuperando um objeto complexo em uma variável

saudação de exemplo a seguir mostra código como tooupdate uma variável com um valor complexo em um runbook textual. Neste exemplo, uma máquina virtual do Azure é recuperada com **Get-AzureVM** e tooan salvo variável de automação existente.  Como explicado em [Tipos de variáveis](#variable-types), ela é armazenada como um PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


Saudação de código a seguir, valor Olá é recuperada da máquina de virtual de Olá Olá toostart variável e usado.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Definindo e recuperando uma coleção em uma variável

saudação de exemplo a seguir mostra código como toouse uma variável com uma coleção de valores complexos em um runbook textual. Neste exemplo, várias máquinas virtuais do Azure são recuperadas com **Get-AzureVM** e tooan salvo variável de automação existente.  Como explicado em [Tipos de variáveis](#variable-types), elas são armazenadas como uma coleção de PSCustomObjects.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

Na Olá código a seguir, a coleção de saudação é recuperada da variável hello e usado toostart cada máquina virtual.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Exemplos de runbook gráfico

Um runbook gráfico, você adiciona Olá **Get-AutomationVariable** ou **Set-AutomationVariable** clicando duas vezes na variável de saudação no painel de biblioteca de saudação do editor gráfico hello e selecionando Olá atividade desejada.

![Adicionar variável toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Definindo valores em uma variável
Olá imagem a seguir mostra exemplo atividades tooupdate uma variável com um valor simples em um runbook gráfico. Neste exemplo, uma única máquina virtual do Azure é recuperada com **Get-AzureRmVM** e nome do computador Olá é salvo tooan variável de automação existente com um tipo de cadeia de caracteres.  Não importa se hello [link é um pipeline ou sequência](automation-graphical-authoring-intro.md#links-and-workflow) como Esperamos que apenas um único objeto na saída de hello.

![Definir variável simples](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre como conectar atividades juntas na criação do gráfico, consulte [Links no gráfico de criação](automation-graphical-authoring-intro.md#links-and-workflow)
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md) 

