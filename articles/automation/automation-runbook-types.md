---
title: "aaaAzure tipos de Runbook de automação | Microsoft Docs"
description: "Descreve tipos diferentes de saudação de runbooks que você pode usar na automação do Azure e as considerações que você deve levar em consideração ao determinar quais toouse de tipo. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Tipos de runbook da Automação do Azure
Automação do Azure oferece suporte a quatro tipos de runbooks que são descritos brevemente Olá a tabela a seguir.  Olá, seções a seguir fornecem informações adicionais sobre cada tipo, incluindo considerações sobre quando toouse cada.

| Tipo | Descrição |
|:--- |:--- |
| [Gráfico](#graphical-runbooks) |Com base no Windows PowerShell e criado e editado completamente no editor gráfico do portal do Azure. |
| [Fluxo de Trabalho Gráfico do PowerShell](#graphical-runbooks) |Com base no fluxo de trabalho do Windows PowerShell e editor gráfico de saudação criados e editados completamente no portal do Azure. |
| [PowerShell](#powershell-runbooks) |Runbook de texto com base no script do Windows PowerShell. |
| [Fluxo de Trabalho do PowerShell](#powershell-workflow-runbooks) |Runbook de texto com base no Fluxo de Trabalho do Windows PowerShell. |

## <a name="graphical-runbooks"></a>Runbooks gráficos
[Gráfico](automation-runbook-types.md#graphical-runbooks) e fluxo de trabalho do PowerShell gráfica runbooks são criados e editados com o editor gráfico de saudação em Olá portal do Azure.  Você pode exportá-los tooa arquivo e, em seguida, importá-los para outra conta de automação, mas você não pode criar ou editá-los com outra ferramenta.  Runbooks gráficos gerar código do PowerShell, mas você não pode exibir ou modificar o código de saudação diretamente. Runbooks gráficos não pode ser convertido tooone de saudação [formatos de texto](automation-runbook-types.md), nem pode ser de um runbook no texto de formato toographical convertido. Runbooks gráficos pode ser convertido tooGraphical runbooks do fluxo de trabalho do PowerShell durante a importação e vice-versa.

### <a name="advantages"></a>Vantagens
* Modelo visual de criação para configurar link de inserção  
* Se concentrar em como os dados fluem pelo processo de saudação  
* Representar visualmente os processos de gerenciamento  
* Incluir outros runbooks filho runbooks toocreate alto nível fluxos de trabalho  
* Incentiva a programação modular  


### <a name="limitations"></a>Limitações
* Não é possível editar um runbook fora do portal do Azure.
* Pode exigir uma atividade de código que contém a lógica complexa de tooperform de código do PowerShell.
* Não é possível exibir ou editar diretamente o código do PowerShell Olá criado pelo fluxo de trabalho gráfico hello. Observe que você pode exibir o código de saudação que criar em todas as atividades de código.

## <a name="powershell-runbooks"></a>Runbooks do PowerShell
Os runbooks do PowerShell se baseiam no Windows PowerShell.  Você editar diretamente o código Olá Olá runbook usando o editor de texto de saudação em Olá portal do Azure.  Você também pode usar qualquer editor de texto offline e [importar runbook Olá](http://msdn.microsoft.com/library/azure/dn643637.aspx) na automação do Azure.

### <a name="advantages"></a>Vantagens
* Implemente toda a lógica complexa com o código do PowerShell sem complexidades adicionais de saudação do fluxo de trabalho do PowerShell. 
* Runbook inicia o mais rápido do que o fluxo de trabalho do PowerShell runbooks desde que ela não precisa toobe compilado antes de executar.

### <a name="limitations"></a>Limitações
* Exige familiarização com a criação de script do PowerShell.
* Não é possível usar [processamento paralelo](automation-powershell-workflow.md#parallel-processing) tooperform várias ações em paralelo.
* Não é possível usar [pontos de verificação](automation-powershell-workflow.md#checkpoints) tooresume runbook no caso de erro.
* Runbooks de fluxo de trabalho do PowerShell e runbooks gráficos podem ser incluídos apenas como runbooks filho usando o cmdlet Start-AzureAutomationRunbook de saudação que cria um novo trabalho.

### <a name="known-issues"></a>Problemas conhecidos
Veja a seguir problemas conhecidos atuais com os runbooks do PowerShell.

* Os runbooks do PowerShell não podem recuperar um [ativo variável](automation-variables.md) não criptografado com um valor nulo.
* Runbooks do PowerShell não é possível recuperar um [ativo variável](automation-variables.md) com  *~*  no nome da saudação.
* Get-Process em um loop em um runbook do PowerShell pode falhar após cerca de 80 iterações. 
* Um runbook do PowerShell poderá falhar se tentar toowrite uma grande quantidade de dados toohello do fluxo de saída de uma vez.   Normalmente você pode contornar esse problema por meio da geração apenas informações de saudação que é necessário ao trabalhar com objetos grandes.  Por exemplo, em vez de saída algo como *Get-Process*, você pode extrair apenas os campos de saudação necessárias com *Get-Process | Selecione ProcessName, CPU*.

## <a name="powershell-workflow-runbooks"></a>Runbooks do Fluxo de Trabalho do PowerShell
Os runbooks do Fluxo de Trabalho do PowerShell são runbooks de texto baseados no [Fluxo de Trabalho do Windows PowerShell](automation-powershell-workflow.md).  Você editar diretamente o código Olá Olá runbook usando o editor de texto de saudação em Olá portal do Azure.  Você também pode usar qualquer editor de texto offline e [importar runbook Olá](http://msdn.microsoft.com/library/azure/dn643637.aspx) na automação do Azure.

### <a name="advantages"></a>Vantagens
* Implemente toda a lógica complexa com o código do Fluxo de Trabalho do PowerShell.
* Use [pontos de verificação](automation-powershell-workflow.md#checkpoints) tooresume runbook no caso de erro.
* Use [processamento paralelo](automation-powershell-workflow.md#parallel-processing) tooperform várias ações em paralelo.
* Pode incluir outros runbooks de fluxo de trabalho do PowerShell e runbooks gráficos como filho runbooks toocreate alto nível fluxos de trabalho.

### <a name="limitations"></a>Limitações
* O autor deve estar familiarizado com o Fluxo de Trabalho do PowerShell.
* Runbook deve lidar com complexidade adicional de saudação do fluxo de trabalho do PowerShell como [desserializar objetos](automation-powershell-workflow.md#code-changes).
* Runbook leva toostart mais tempo que os runbooks do PowerShell, desde que ele precisa toobe compilado antes de executar.
* Runbooks do PowerShell só pode ser incluído como runbooks filho usando o cmdlet Start-AzureAutomationRunbook de saudação que cria um novo trabalho.

## <a name="considerations"></a>Considerações
Você deve considerar Olá conta considerações adicionais a seguir para determinar qual toouse de tipo de um runbook específico.

* Você não pode converter runbooks do tipo de gráfico tootextual ou vice-versa.
* Há limitações ao usar runbooks de tipos diferentes, como um runbook filho.  Veja [Runbooks filho na Automação do Azure](automation-child-runbooks.md) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre a criação de runbook gráfico, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md)
* Olá toounderstand as diferenças entre o PowerShell e o PowerShell, fluxos de trabalho de runbooks, consulte [fluxo de trabalho do aprendizado de Windows PowerShell](automation-powershell-workflow.md)
* Para obter mais informações sobre como toocreate ou importar um Runbook, consulte [criar ou importar um Runbook](automation-creating-importing-runbook.md)

