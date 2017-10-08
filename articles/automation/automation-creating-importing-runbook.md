---
title: "aaaCreating ou importar um runbook na automação do Azure"
description: "Este artigo descreve como toocreate um novo runbook na automação do Azure ou importar de um arquivo."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Criando ou importando um runbook na Automação do Azure
Você pode adicionar um tooAzure runbook automação pelo [criar um novo](#creating-a-new-runbook) ou importando um runbook existente de um arquivo ou de saudação [Galeria de Runbook](automation-runbook-gallery.md). Este artigo oferece informações sobre a criação e a importação de runbooks de um arquivo.  Você pode obter todos os detalhes de saudação sobre acesso a runbooks da comunidade e módulos no [galerias de Runbook e o módulo de automação do Azure](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Criando um novo runbook
Você pode criar um novo runbook na automação do Azure usando um hello Azure portais ou o Windows PowerShell. Quando Olá runbook tiver sido criado, você pode editá-lo usando informações em [o fluxo de trabalho do aprendizado PowerShell](automation-powershell-workflow.md) e [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate um novo runbook de automação do Azure com o portal clássico do Azure Olá
Você só pode trabalhar com [runbooks do fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) em Olá portal do Azure.

1. No portal clássico do Azure de saudação, clique em, **novo**, **serviços de aplicativos**, **automação**, **Runbook**, **criaçãorápida**.
2. Insira informações de saudação necessárias e, em seguida, clique em **criar**. nome do runbook Olá deve começar com uma letra e pode ter letras, números, sublinhados e traços.
3. Se você quiser tooedit Olá runbook agora, em seguida, clique em **Editar Runbook**. Caso contrário, clique em **OK**.
4. Seu novo runbook será exibido no hello **Runbooks** guia.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate um novo runbook de automação do Azure com hello portal do Azure
1. No portal do Azure de Olá, abra sua conta de automação.
2. Olá Hub, selecione **Runbooks** tooopen lista de saudação de runbooks.
3. Clique em Olá **adicionar um runbook** botão e, em seguida, **criar um novo runbook**.
4. Digite um **nome** runbook hello e selecione seu [tipo](automation-runbook-types.md). nome do runbook Olá deve começar com uma letra e pode ter letras, números, sublinhados e traços.
5. Clique em **criar** toocreate Olá runbook e editor Olá aberto.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate um novo runbook de automação do Azure com o Windows PowerShell
Você pode usar o hello [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) toocreate cmdlet vazio [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Você pode especificar Olá **nome** parâmetro toocreate um runbook vazio que você pode editar mais tarde ou você pode especificar Olá **caminho** parâmetro tooimport um arquivo de runbook. Olá **tipo** parâmetro também deve ser incluído toospecify um Olá quatro tipos de runbook.

saudação de exemplo a seguir comandos mostram como toocreate um novo runbook vazio.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Importando um runbook de um arquivo para a Automação do Azure
Você pode criar um novo runbook na Automação do Azure importando um script do PowerShell ou o Fluxo de Trabalho do PowerShell (extensão .ps1) ou um runbook gráfico exportado (.graphrunbook).  Você deve especificar Olá [tipo de runbook](automation-runbook-types.md) que serão criados a partir de importação de saudação considerando Olá conta as considerações a seguir.

* Um arquivo .graphrunbook só pode ser importado em um novo [runbook gráfico](automation-runbook-types.md#graphical-runbooks)e os runbooks gráficos só podem ser criados de um arquivo .graphrunbook.
* Um arquivo .ps1 com um Fluxo de Trabalho do PowerShell só poderá ser importado para um [runbook do Fluxo de Trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Se o arquivo hello contiver vários fluxos de trabalho do PowerShell, Olá importação falhará. Você deve salvar cada arquivo próprio do fluxo de trabalho tooits e importar cada um separadamente.
* Um arquivo .ps1 que não contenha um fluxo de trabalho poderá ser importado para um [runbook do PowerShell](automation-runbook-types.md#powershell-runbooks) ou para um [runbook do Fluxo de Trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Se ele for importado para um runbook de fluxo de trabalho do PowerShell, ele será convertido tooa de fluxo de trabalho e os comentários serão incluídos no runbook Olá especificando alterações Olá que foram feitas.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport um runbook a partir de um arquivo com o portal clássico do Azure Olá
Você pode usar o hello procedimento tooimport um arquivo de script a seguir para a automação do Azure.  Observe que você só poderá importar um arquivo .ps1 para um runbook do Fluxo de Trabalho do PowerShell usando este portal.  Você deve usar o hello portal do Azure para outros tipos.

1. No portal de gerenciamento do Azure hello, selecione **automação** e, em seguida, selecione uma conta de automação.
2. Clique em **Importar**.
3. Clique em **Procurar arquivo** e localize Olá tooimport de arquivo de script.
4. Se você quiser tooedit Olá runbook agora, em seguida, clique em **Editar Runbook**. Caso contrário, clique em OK.
5. Olá novo runbook será exibido no hello **Runbooks** guia Olá conta de automação.
6. Você deve [publicar Olá runbook](#publishing-a-runbook) antes de poder executá-lo.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport um runbook de um arquivo com hello portal do Azure
Você pode usar o hello procedimento tooimport um arquivo de script a seguir para a automação do Azure.  

> [!NOTE]
> Observe que você só pode importar um arquivo. ps1 em um runbook de fluxo de trabalho do PowerShell usando o portal de saudação.
> 
> 

1. No portal do Azure de Olá, abra sua conta de automação.
2. Olá Hub, selecione **Runbooks** tooopen lista de saudação de runbooks.
3. Clique em Olá **adicionar um runbook** botão e, em seguida, **importação**.
4. Clique em **arquivo de Runbook** tooselect Olá arquivo tooimport
5. Se hello **nome** campo estiver habilitado, você tem Olá opção toochange-lo.  nome do runbook Olá deve começar com uma letra e pode ter letras, números, sublinhados e traços.
6. Olá [tipo de runbook](automation-runbook-types.md) será selecionada automaticamente, mas você pode alterar o tipo de saudação após colocar restrições aplicáveis de saudação em conta. 
7. Olá novo runbook será exibido na lista de saudação de runbooks para Olá conta de automação.
8. Você deve [publicar Olá runbook](#publishing-a-runbook) antes de poder executá-lo.

> [!NOTE]
> Depois de importar um runbook gráfico ou um runbook gráfico de fluxo de trabalho do PowerShell, você tem Olá opção tooconvert toohello outro tipo se desejado. Não é possível converter tootextual.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport um runbook a partir de um arquivo de script com o Windows PowerShell
Você pode usar o hello [AzureRMAutomationRunbook importação](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport um arquivo de script como um rascunho de runbook de fluxo de trabalho do PowerShell. Se já existir um runbook Olá, a importação de saudação falhará a menos que você use Olá *-Force* parâmetro. 

Olá comandos de exemplo a seguir mostra como o arquivo de tooimport um script em um runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Publicando um runbook
Quando você criar ou importar um novo runbook, deverá publicá-lo antes de poder executá-lo.  Cada runbook na Automação tem um Rascunho e uma versão Publicada. Somente a versão do hello publicada está disponível toobe executar, e somente a versão de rascunho Olá pode ser editada. versão publicada de saudação é afetado por uma versão de rascunho toohello alterações. Quando a versão de rascunho Olá deve ficar disponível, em seguida, publicá-la que substitui a versão publicada de saudação com versão de rascunho de saudação.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish um runbook usando o portal clássico do Azure Olá
1. Abra Olá runbook no portal clássico do Azure hello.
2. Na parte superior de saudação da tela hello, clique em **autor**.
3. Na parte inferior de saudação da tela hello, clique em **publicar** e **Sim** toohello mensagem de verificação.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish um runbook usando Olá portal do Azure
1. Abra o runbook Olá no hello portal do Azure.
2. Clique em Olá **editar** botão.
3. Clique em Olá **publicar** botão e, em seguida, **Sim** toohello mensagem de verificação.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish um runbook usando o Windows PowerShell
Você pode usar o hello [AzureRmAutomationRunbook publicar](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish um runbook com o Windows PowerShell. saudação de exemplo a seguir comandos mostram como toopublish um exemplo de runbook.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como você pode se beneficiar com hello Runbook e Galeria de módulo do PowerShell, consulte [galerias de Runbook e o módulo de automação do Azure](automation-runbook-gallery.md)
* toolearn mais sobre como editar runbooks do PowerShell e fluxo de trabalho do PowerShell com um editor de texto, consulte [edição textuais runbooks na automação do Azure](automation-edit-textual-runbook.md)
* toolearn mais sobre a criação de runbook gráfico, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md)

