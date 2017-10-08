---
title: "aaaStarting um runbook na automação do Azure | Microsoft Docs"
description: "Resume Olá métodos diferentes que podem ser usado toostart um runbook na automação do Azure e fornece detalhes sobre o uso de ambos Olá portal do Azure e o Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Como iniciar um Runbook na Automação do Azure
Olá, a tabela a seguir ajudará você a determinar Olá método toostart um runbook na automação do Azure que é mais adequado tooyour cenário em particular. Este artigo inclui detalhes sobre como iniciar um runbook com hello portal do Azure e com o Windows PowerShell. Detalhes no hello outros métodos são fornecidos em outra documentação que você pode acessar de links de saudação abaixo.

| **MÉTODO** | **CARACTERÍSTICAS** |
| --- | --- |
| [Portal do Azure](#starting-a-runbook-with-the-azure-portal) |<li>Método mais simples com interface do usuário interativa.<br> <li>Valores de parâmetro simples de tooprovide do formulário.<br> <li>Controle facilmente o estado do trabalho.<br> <li>Acesso autenticado com o logon do Azure. |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Chame da linha de comando com os cmdlets do Windows PowerShell.<br> <li>Pode ser incluído em uma solução automatizada com várias etapas.<br> <li>A solicitação é autenticada com certificado ou entidade de usuário/entidade de serviço OAuth.<br> <li>Fornece valores de parâmetro simples e complexos.<br> <li>Acompanhe o estado do trabalho.<br> <li>Cliente necessário toosupport cmdlets do PowerShell. |
| [API de Automação do Azure](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>Método mais flexível, mas também o mais complexo.<br> <li>Chame de qualquer código personalizado que possa fazer solicitações HTTP.<br> <li>A solicitação autenticada com certificado ou entidade de usuário/entidade de serviço OAuth.<br> <li>Fornece valores de parâmetro simples e complexos.<br> <li>Acompanhe o estado do trabalho. |
| [Webhooks](automation-webhooks.md) |<li>Inicie o runbook de uma solicitação HTTP única.<br> <li>Autenticado com token de segurança na URL.<br> <li>O cliente não pode substituir valores de parâmetro especificados quando o webhook foi criado. Runbook pode definir um único parâmetro que é preenchido com os detalhes da solicitação HTTP hello.<br> <li>Nenhum estado de trabalho tootrack de capacidade por meio de URL de webhook. |
| [Responder tooAzure alerta](../log-analytics/log-analytics-alerts.md) |<li>Inicie um runbook no alerta de tooAzure de resposta.<br> <li>Configurar um webhook de runbook e vincular tooalert.<br> <li>Autenticado com token de segurança na URL. |
| [Agenda](automation-schedules.md) |<li>Inicie automaticamente o runbook em um cronograma horário, diário, semanal ou mensal.<br> <li>Manipule a agenda pelo portal do Azure, por cmdlets do PowerShell ou pela a API do Azure.<br> <li>Fornece toobe de valores de parâmetro usado com a agenda. |
| [De Outro Runbook](automation-child-runbooks.md) |<li>Use um runbook como uma atividade em outro runbook.<br> <li>É útil para funcionalidades usadas por vários runbooks.<br> <li>Forneça o runbook de toochild de valores de parâmetro e use a saída no runbook pai. |

Olá imagem a seguir ilustra processo passo a passo detalhado Olá ciclo de vida de um runbook. Ele inclui formas diferentes que um runbook for iniciado na automação do Azure, os componentes necessários para runbooks de automação do Azure tooexecute Hybrid Runbook Worker e as interações entre diferentes componentes. toolearn sobre a execução de runbooks de automação em seu data center, consulte muito[operadores de runbook híbrido](automation-hybrid-runbook-worker.md)

![Arquitetura do runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Iniciando um runbook com hello portal do Azure
1. No portal do Azure de Olá, selecione **automação** e, em seguida, clique em nome de saudação de uma conta de automação.
2. No menu de Hub hello, selecione **Runbooks**.
3. Em Olá **Runbooks** folha, selecione um runbook e, em seguida, clique em **iniciar**.
4. Se Olá runbook tiver parâmetros, será solicitado tooprovide valores com uma caixa de texto para cada parâmetro. Confira [Parâmetros de runbook](#Runbook-parameters) abaixo para mais detalhes sobre os parâmetros.
5. Em Olá **trabalho** folha, você pode exibir o status de Olá Olá do trabalho de runbook.

## <a name="starting-a-runbook-with-windows-powershell"></a>Iniciando um runbook com o Windows PowerShell
Você pode usar o hello [AzureRmAutomationRunbook início](https://msdn.microsoft.com/library/mt603661.aspx) toostart um runbook com o Windows PowerShell. Olá, código de exemplo seguinte inicia um runbook chamado Test-Runbook.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

Retorna AzureRmAutomationRunbook iniciar um trabalho do objeto que você pode usar tootrack seu status depois Olá runbook for iniciado. Você pode usar esse objeto de trabalho com [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine status de saudação do trabalho hello e [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget sua saída. Olá, código de exemplo a seguir inicia um runbook chamado Test-Runbook, aguarda até que ele seja concluído e exibe seu resultado.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Se Olá runbook exigir parâmetros, você deve fornecê-los como um [hashtable](http://technet.microsoft.com/library/hh847780.aspx) onde correspondências de chave de saudação da tabela de hash Olá Olá parâmetro e valor Olá são o valor do parâmetro hello. Olá exemplo a seguir mostra como toostart um runbook com dois parâmetros de cadeia de caracteres chamado FirstName e LastName, um número inteiro denominado RepeatCount e um parâmetro booleano denominado Show. Para saber mais sobre parâmetros, confira [Parâmetros de runbook](#Runbook-parameters) abaixo.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Parâmetros de runbook
Quando você inicia um runbook de saudação Portal do Azure ou o Windows PowerShell, a instrução de saudação é enviada pelo Olá serviço da web de automação do Azure. Esse serviço não dá suporte a parâmetros com tipos de dados complexos. Se você precisar tooprovide um valor para um parâmetro complexo, é necessário chamá-lo embutido de outro runbook conforme descrito em [filho runbooks na automação do Azure](automation-child-runbooks.md).

saudação de serviço da web de automação do Azure fornecerá uma funcionalidade especial para parâmetros usando certos tipos de dados, conforme descrito nas seções a seguir de saudação.

### <a name="named-values"></a>Valores nomeados
Se parâmetro hello é do tipo de dados [object], você pode usar o hello após toosend do formato JSON ele uma lista de valores nomeados: *{Nome1: 'Valor1', Name2: 'Value2', nome3: 'Value3'}*. Esses valores devem ser tipos simples. Olá runbook receberá o parâmetro hello como um [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) com propriedades que correspondem a tooeach valor nomeado.

Considere Olá runbook de teste que aceita um parâmetro chamado de usuário a seguir.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

Olá seguinte texto pode ser usado para o parâmetro de saudação do usuário.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Isso resulta em Olá saída a seguir.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Matrizes
Se o parâmetro hello é uma matriz, como [matriz] ou [string []], em seguida, você pode usar Olá toosend do formato JSON a seguir ele uma lista de valores: *[Value1, Value2, Value3]*. Esses valores devem ser tipos simples.

Considere Olá seguinte runbook de teste que aceita um parâmetro chamado *usuário*.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

Olá seguinte texto pode ser usado para o parâmetro de saudação do usuário.

```
["Joe","Smith",2,true]
```

Isso resulta em Olá saída a seguir.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Credenciais
Se o parâmetro hello é o tipo de dados **PSCredential**, em seguida, você pode fornecer o nome de saudação de um objeto de automação do Azure [ativo de credencial](automation-credentials.md). Olá runbook recuperará credencial Olá com nome hello que você especificar.

Considere Olá runbook de teste que aceita um parâmetro chamado credencial a seguir.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Olá seguinte texto pode ser usado para o parâmetro de usuário Olá supondo que havia um ativo de credencial chamado *minhas credenciais*.

```
My Credential
```

Supondo que tenha sido Olá nome de usuário na credencial Olá *jsmith*, isso resulta em Olá saída a seguir.

```
jsmith
```

## <a name="next-steps"></a>Próximas etapas
* arquitetura de runbook Olá no artigo atual fornece uma visão geral do gerenciamento de recursos no Azure e local com hello Hybrid Runbook Worker runbooks.  toolearn sobre a execução de runbooks de automação em seu data center, consulte muito[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).
* toolearn mais sobre Olá criar runbooks modular toobe usada por outros runbooks para funções específicas ou comuns, consulte muito[Runbooks filho](automation-child-runbooks.md).

