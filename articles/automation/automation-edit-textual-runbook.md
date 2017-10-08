---
title: "runbooks de textual aaaEditing na automação do Azure"
description: "Este artigo fornece procedimentos diferentes para trabalhar com runbooks do PowerShell e fluxo de trabalho do PowerShell na automação do Azure usando o editor de texto de saudação."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Editando runbooks de texto na Automação do Azure
Olá textual editor na automação do Azure pode ser usado tooedit [runbooks do PowerShell](automation-runbook-types.md#powershell-runbooks) e [runbooks do fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Isso tem recursos típicos de saudação de outros editores de código, como intellisense e a codificação de cores com recursos especiais adicionais tooassist você acessar toorunbooks comuns de recursos.  Este artigo oferece as etapas detalhadas para a execução de funções diferentes com este editor.

editor de texto de saudação inclui um código de tooinsert de recurso para atividades, ativos e runbooks filho em um runbook. Em vez de digitar o código de saudação por conta própria, você pode selecionar em uma lista de recursos disponíveis e fazer Olá código apropriado seja inserido no runbook hello.

Cada runbook da Automação do Azure tem duas versões, Rascunho e Publicado. Editar a versão de rascunho de saudação do hello runbook e, em seguida, publicá-lo para que ele pode ser executado. versão do Hello publicada não pode ser editado. Para saber mais, consulte [Publicando um runbook](automation-creating-importing-runbook.md#publishing-a-runbook) .

toowork com [Runbooks gráficos](automation-runbook-types.md#graphical-runbooks), consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit um runbook com hello portal do Azure
Use Olá seguindo o procedimento tooopen um runbook para edição no editor de texto de saudação.

1. No portal do Azure de Olá, selecione sua conta de automação.
2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.
3. Clique em nome de saudação do runbook Olá você deseja tooedit e clique em Olá **editar** botão.
4. Execute Olá necessário editar.
5. Clique em **Salvar** quando concluir suas edições.
6. Clique em **publicar** se você quiser hello, a última versão de rascunho de saudação runbook toobe publicado.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert um cmdlet em um runbook
1. Na tela do editor de texto de saudação do hello, posicione cursor Olá onde você deseja tooplace Olá cmdlet.
2. Expanda Olá **Cmdlets** nó Olá controle da biblioteca.
3. Expanda o módulo de saudação contendo cmdlet Olá deseja toouse.
4. Olá cmdlet tooinsert clique com botão direito e selecione **adicionar toocanvas**.  Se Olá cmdlet tem mais de um parâmetro definido, a saudação padrão conjunto será adicionado.  Você também pode expandir Olá cmdlet tooselect parâmetro diferente definido.
5. código de Olá Olá cmdlet é inserido com sua lista inteira de parâmetros.
6. Forneça um valor apropriado no lugar do tipo de dados de saudação cercado por chaves <> para todos os parâmetros necessários.  Remova todos os parâmetros que não sejam necessários.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>código de tooinsert para um runbook filho em um runbook
1. Na tela do editor de texto de saudação do hello, posicione o cursor de saudação nas quais você deseja tooplace código de Olá Olá [runbook filho](automation-child-runbooks.md).
2. Expanda Olá **Runbooks** nó Olá controle da biblioteca.
3. Olá runbook tooinsert clique com botão direito e selecione **adicionar toocanvas**.
4. código de Olá Olá filho runbook é inserido com qualquer espaços reservados para os parâmetros de runbook.
5. Substitua os espaços reservados de saudação com valores apropriados para cada parâmetro.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert um ativo em um runbook
1. Na tela do editor de texto de saudação do hello, posicione cursor Olá nas quais você deseja tooplace código de Olá Olá o runbook filho.
2. Expanda Olá **ativos** nó Olá controle da biblioteca.
3. Expanda o nó de saudação para o tipo de saudação do ativo que você deseja.
4. Olá ativo tooinsert clique com botão direito e selecione **adicionar toocanvas**.  Para [ativos variável](automation-variables.md), selecione **adicionar "Obter a variável" toocanvas** ou **adicionar "Set Variable" toocanvas** dependendo se você deseja tooget ou definir variável de saudação.
5. código de saudação para ativo Olá é inserido no runbook hello.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit um runbook com hello portal do Azure
Use Olá seguindo o procedimento tooopen um runbook para edição no editor de texto de saudação.

1. No portal do Azure de Olá, selecione **automação** e, em seguida, clique em nome de saudação de uma conta de automação.
2. Selecione Olá **Runbooks** guia.
3. Clique em nome de saudação do runbook Olá você deseja tooedit e, em seguida, selecione Olá **autor** guia.
4. Clique em Olá **editar** botão Olá final da tela hello.
5. Execute Olá necessário editar.
6. Clique em **Salvar** quando concluir suas edições.
7. Clique em **publicar** se você quiser hello, a última versão de rascunho de saudação runbook toobe publicado.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert uma atividade em um Runbook
1. Na tela do editor de texto de saudação do hello, posicione o cursor Olá onde deseja que a atividade de saudação tooplace.
2. Na parte inferior de saudação da tela hello, clique em **inserir** e **atividade**.
3. Em Olá **módulo de integração** coluna, o módulo Olá select que contém a atividade de saudação.
4. Em Olá **atividade** painel, selecione uma atividade.
5. Em Olá **descrição** coluna, observe Olá descrição da atividade de saudação. Opcionalmente, você pode clicar em Exibir detalhadas ajuda toolaunch ajuda para a atividade de saudação no navegador de saudação.
6. Clique na seta direita hello.  Se hello atividade tiver parâmetros, eles serão listados para sua informação.
7. Clique o botão de seleção de saudação.  Código toorun hello atividade será inserida no runbook hello.
8. Se hello atividade exigir parâmetros, forneça um valor apropriado no lugar do tipo de dados de saudação cercado por chaves <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>código de tooinsert para um runbook filho em um runbook
1. Na tela do editor de texto de saudação do hello, posicione o cursor de Olá onde você deseja Olá tooplace [runbook filho](automation-child-runbooks.md).
2. Na parte inferior de saudação da tela hello, clique em **inserir** e **Runbook**.
3. Selecione tooinsert de runbook Olá Olá center coluna e clique na seta direita hello.
4. Se Olá runbook tiver parâmetros, eles serão listados para sua informação.
5. Clique o botão de seleção de saudação.  Código toorun Olá selecionado runbook será inserido no runbook atual hello.
6. Se Olá runbook exigir parâmetros, forneça um valor apropriado no lugar do tipo de dados de saudação cercado por chaves <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert um ativo em um runbook
1. Na tela do editor de texto de saudação do hello, posicione o cursor Olá onde você deseja que o ativo de saudação do tooplace hello atividade tooretrieve.
2. Na parte inferior de saudação da tela hello, clique em **inserir** e **configuração**.
3. Em Olá **ação de configuração** coluna, a ação Olá selecione que você deseja.
4. Selecione Olá de ativos disponíveis na coluna central de saudação.
5. Clique o botão de seleção de saudação.  Código tooget ou conjunto Olá ativo será inserido no runbook hello.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit um runbook de automação do Azure usando o Windows PowerShell
tooedit um runbook com o Windows PowerShell, você pode usar o editor de saudação de sua escolha e salvá-lo tooa. ps1 arquivo. Você pode usar o hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) cmdlet tooretrieve Olá conteúdo Olá runbook e, em seguida, [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace Olá existente rascunho de runbook com hello um modificado.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve Olá conteúdo de um Runbook usando o Windows PowerShell
Olá comandos de exemplo a seguir mostra como tooretrieve Olá script para um runbook e salvá-lo tooa arquivo de script. Neste exemplo, a versão de rascunho de saudação é recuperada. Também é publicado versão Olá tooretrieve possíveis Olá runbook Embora esta versão não pode ser alterada.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange Olá conteúdo de um Runbook usando o Windows PowerShell
Olá comandos de exemplo a seguir mostram como tooreplace Olá conteúdo existente de um runbook com o conteúdo de saudação de um arquivo de script. Observe que isso é Olá mesmo exemplo de procedimento como [tooimport um runbook a partir de um arquivo de script com o Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Artigos relacionados
* [Criando ou importando um runbook na Automação do Azure](automation-creating-importing-runbook.md)
* [Aprendendo o fluxo de trabalho do PowerShell](automation-powershell-workflow.md)
* [Criação gráfica na Automação do Azure](automation-graphical-authoring-intro.md)
* [Certificados](automation-certificates.md)
* [Conexões](automation-connections.md)
* [Credenciais](automation-credentials.md)
* [Agendas](automation-schedules.md)
* [Variáveis](automation-variables.md)
