---
title: "aaaChild runbooks na automação do Azure | Microsoft Docs"
description: "Descreve métodos diferentes de saudação para iniciando um runbook na automação do Azure a partir de outro runbook e compartilhar informações entre eles."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Runbooks filhos na Automação do Azure
É uma prática recomendada no Azure toowrite reutilizáveis e modulares, os runbooks de automação com uma função discreta que pode ser usado por outros runbooks. Um runbook pai geralmente chamará um ou mais runbooks filho funcionalidade tooperform necessário. Há dois toocall de maneiras um runbook filho e cada uma tem diferenças marcantes que você deve compreender para que você possa determinar qual será a melhor para seus diferentes cenários.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Invocar um runbook filho usando a execução embutida
tooinvoke um runbook embutido de outro runbook, use nome Olá Olá runbook e forneça valores para os parâmetros exatamente como você usaria uma atividade ou cmdlet.  Olá a todos os runbooks na mesma conta de automação está disponível tooall outros toobe usados dessa maneira. Olá o runbook pai aguardará Olá filho runbook toocomplete antes de mover toohello próxima linha e nenhuma saída é retornada diretamente toohello pai.

Quando você invoca um runbook embutido, ele é executado no hello mesmo trabalho como Olá o runbook pai. Não haverá nenhuma indicação no histórico do trabalho de saudação do runbook filho Olá que ele foi executado. Todas as exceções e qualquer fluxo de saída do runbook filho de saudação será associados ao pai de saudação. Isso resulta em menos trabalhos e torna mais fácil tootrack e tootroubleshoot desde as exceções geradas pelo runbook filho de saudação e qualquer uma das suas saídas de fluxo são associadas com hello pai trabalho.

Quando um runbook é publicado, todos os runbooks filhos que ele chamar já devem ter sido publicados. Isso ocorre porque a Automação do Azure cria uma associação com os runbooks filhos quando um runbook é compilado. Se não forem, o runbook pai Olá aparecerá toopublish corretamente, mas gerará uma exceção quando ele for iniciado. Se isso acontecer, poderá republicar o runbook pai Olá em ordem tooproperly Referência Olá filho runbooks. Não é necessário o runbook pai toorepublish Olá se qualquer Olá eventuais runbooks filho forem alterados, porque associação Olá já terá sido criada.

parâmetros de saudação de um runbook filho chamado embutido podem ser qualquer tipo de dados, incluindo objetos complexos e não há nenhum [serialização JSON](automation-starting-a-runbook.md#runbook-parameters) que haja ao iniciar o runbook hello usando Olá Portal de gerenciamento ou com hello Cmdlet Start-AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Tipos de runbook
Quais tipos podem chamar um ao outro:

* Um [runbook do PowerShell ](automation-runbook-types.md#powershell-runbooks) e os [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) podem chamar uns aos outros em linha (ambos são baseados no PowerShell).
* Um [runbook do Fluxo de Trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) e runbooks gráficos do Fluxo de Trabalho do PowerShell podem chamar uns aos outros de forma embutida (ambos são baseados no Fluxo de Trabalho do PowerShell)
* Olá PowerShell tipos e Olá que tipos de fluxo de trabalho do PowerShell não é possível chamar embutido entre si e deve usar AzureRmAutomationRunbook de início.

Quando a ordem de publicação é importante:

* Olá publicar ordem de assuntos somente runbooks para runbooks do fluxo de trabalho do PowerShell gráfica e de fluxo de trabalho do PowerShell.

Quando você chamar um runbook filho do gráfico ou fluxo de trabalho do PowerShell usando a execução embutida, você apenas usar nome de saudação do runbook hello.  Quando você chamar um runbook filho do PowerShell, você deve precedido seu nome com *.\\*  toospecify que Olá script está localizado no diretório local de saudação. 

### <a name="example"></a>Exemplo
saudação de exemplo a seguir invoca um runbook filho de teste que aceita três parâmetros, um objeto complexo, um número inteiro e um valor booleano. saída de saudação do runbook filho de saudação é atribuída tooa variável.  Nesse caso, o runbook filho Olá é um runbook de fluxo de trabalho do PowerShell

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

A seguir é hello mesmo exemplo usando um runbook do PowerShell como filho de saudação.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Iniciar um runbook filho usando cmdlet
Você pode usar o hello [início AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart cmdlet um runbook, conforme descrito em [toostart um runbook com o Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Há dois modos de uso para esse cmdlet.  No modo, Olá cmdlet retorna id do trabalho Olá assim que o trabalho de filho Olá é criado para o runbook filho hello.  Em Olá outro modo, que permitem especificando Olá **-Aguarde** parâmetro, aguarda até que filho Olá Olá cmdlet trabalho concluído e retornará a saída de saudação do runbook filho de saudação.

trabalho de saudação de um runbook filho iniciado com um cmdlet será executado em um trabalho separado de saudação o runbook pai. Isso resulta em mais trabalhos do que chamar hello runbook embutido e torna mais difícil tootrack. pai de saudação pode iniciar vários runbooks filho assíncrona sem esperar que cada toocomplete. Para esse mesmo tipo de execução paralela chamando os runbooks do hello filho embutido, Olá o runbook pai precisaria Olá toouse [palavra-chave paralela](automation-powershell-workflow.md#parallel-processing).

Parâmetros de um runbook filho iniciados com um cmdlet são fornecidos como uma tabela de hash, conforme descrito em [Parâmetros de Runbook](automation-starting-a-runbook.md#runbook-parameters). Somente tipos de dados simples podem ser usados. Se o runbook Olá tem um parâmetro com um tipo de dados complexos, em seguida, ele deve ser chamado embutido.

### <a name="example"></a>Exemplo
Olá exemplo a seguir inicia um runbook filho com parâmetros e, em seguida, aguarda para ele toocomplete usando Olá AzureRmAutomationRunbook início-espera o parâmetro. Depois de concluído, a saída é coletada do runbook filho de saudação.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Comparação de métodos para chamar um runbook filho
Olá tabela a seguir resume as diferenças de saudação entre Olá dois métodos para chamar um runbook de outro runbook.

|  | Embutido | Cmdlet |
|:--- |:--- |:--- |
| Trabalho |Runbooks filho são executados em hello como pai de saudação do mesmo trabalho. |Um trabalho separado é criado para o runbook filho hello. |
| Execução |Runbook pai aguarda Olá filho runbook toocomplete antes de continuar. |Runbook pai continua imediatamente após o runbook filho ser iniciado *ou* runbook pai aguarda Olá toofinish de trabalho de filho. |
| Saída |O runbook pai pode obter saída diretamente do runbook filho. |O runbook pai deve recuperar a saída do trabalho do runbook filho *ou* o runbook pai pode obter a saída diretamente do runbook filho. |
| parâmetros |Valores para parâmetros de runbook Olá filho são especificados separadamente e podem usar qualquer tipo de dados. |Valores para o runbook filho Olá parâmetros devem ser combinados em uma única tabela de hash e só podem incluir simples, de matriz e tipos de dados que aproveitam a serialização JSON do objeto. |
| Conta de Automação |Runbook pai só pode usar o runbook filho Olá mesma conta de automação. |Runbook pai pode usar o runbook filho de qualquer conta de automação de saudação mesma assinatura do Azure e até mesmo uma assinatura diferente se você tiver um tooit de conexão. |
| Publicação |O runbook filho deve ser publicado antes da publicação do runbook pai. |O runbook filho deve ser publicado antes da inicialização do runbook pai. |

## <a name="next-steps"></a>Próximas etapas
* [Como iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md)
* [Saída de runbook e mensagens na Automação do Azure](automation-runbook-output-and-messages.md)

