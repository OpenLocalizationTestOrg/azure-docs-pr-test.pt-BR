---
title: "aaaScheduling um runbook na automação do Azure | Microsoft Docs"
description: "Descreve como toocreate uma agenda na automação do Azure para que você pode iniciar um runbook automaticamente em um horário específico ou em um agendamento recorrente."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Agendando um runbook na Automação do Azure
tooschedule um runbook na automação do Azure toostart em um horário especificado, você vinculá-lo tooone ou mais agendas. Uma agenda pode ser configurado tooeither executado uma vez ou em um recorrente por hora ou diariamente agendamento para runbooks Olá portal clássico do Azure e runbooks em Olá portal do Azure, você pode adicionalmente agendá-los para semanais, mensais, específicos dias da semana de saudação ou os dias da mês Hello, ou um dia específico do mês de saudação.  Um runbook pode ser vinculado toomultiple agendamentos e um agendamento pode ter vários tooit de runbooks vinculados.

## <a name="creating-a-schedule"></a>Criando uma agenda
Você pode criar uma nova agenda de runbooks em Olá portal do Azure, no portal clássico do hello, ou com o Windows PowerShell. Você também tem a opção de saudação de criação de uma nova agenda quando você vincular um agendamento de tooa runbook usando Olá clássico do Azure ou o portal do Azure.

> [!NOTE]
> Quando você associa uma agenda com um runbook, automação armazena as versões atuais dos módulos Olá Olá em sua conta e links-los toothat agendamento.  Isso significa que, se você tinha um módulo com a versão 1.0 em sua conta ao criar uma agenda e, em seguida, atualizar Olá módulo tooversion 2.0, agenda Olá continuará toouse 1.0.  Na versão de módulo atualizado do pedido toouse hello, você deve criar uma nova agenda. 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate uma nova agenda em Olá portal clássico do Azure
1. Em Olá portal clássico do Azure, selecione a automação e, em seguida, selecione Olá nome de uma conta de automação.
2. Selecione Olá **ativos** guia.
3. Na parte inferior de saudação da janela de saudação, clique em **Adicionar configuração**.
4. Clique em **Adicionar Agenda**.
5. Digite um **nome** e, opcionalmente, um **descrição** para schedule.your novo Olá agenda será executada **uma vez**, **por hora**, **Diário**, **semanal**, ou **mensal**.
6. Especifique um **Start Time** e outras opções, dependendo do tipo de saudação de agenda que você selecionou.

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate uma nova agenda em Olá portal do Azure
1. No portal do Azure, na sua conta de automação de saudação, clique em Olá **ativos** bloco tooopen Olá **ativos** folha.
2. Clique em Olá **agendas** bloco tooopen Olá **agendas** folha.
3. Clique em **adicionar uma agenda** na parte superior de saudação da folha de saudação.
4. Em Olá **nova agenda** folha, digite um **nome** e, opcionalmente, um **descrição** para nova agenda de saudação.
5. Selecione se a agenda de saudação será executada uma vez ou em uma agenda recorrente de **uma vez** ou **recorrência**.  Se você selecionar **Uma vez**, especifique uma **Hora de início** e clique em **Criar**.  Se você selecionar **recorrência**, especifique um **hora de início** e a frequência de saudação de frequência você deseja Olá runbook toorepeat - por **hora**, **dia**, **semana**, ou **mês**.  Se você selecionar **semana** ou **mês** da lista suspensa de hello, Olá **opção de recorrência** aparecerá na folha de saudação e após a seleção, hello **recorrência opção** folha será exibida e você pode selecionar dia Olá da semana se você selecionou **semana**.  Se você selecionou **mês**, você pode optar por **dias da semana** ou dias específicos do mês de saudação em Olá calendário e, finalmente, você deseja toorun-Olá último dia do mês de saudação ou não e, em seguida, clique em **Okey **.   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate uma nova agenda com o Windows PowerShell
Você pode usar o hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) toocreate cmdlet uma nova agenda na automação do Azure para runbooks clássico, ou [AzureRmAutomationSchedule novo](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet para runbooks na saudação do Azure Portal. Você deve especificar a hora de início de Olá para agendamento hello e a frequência de saudação que deve ser executado.

Olá comandos de exemplo a seguir mostra como toocreate uma nova agenda que executa cada dia às 3:30 PM começando em 20 de janeiro de 2015, com um cmdlet de gerenciamento de serviços do Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Olá exemplo a seguir comandos mostra como toocreate uma agenda para Olá 15 e 30 de cada mês usando um cmdlet do Gerenciador de recursos do Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>Vinculando um runbook tooa de agenda
Um runbook pode ser vinculado toomultiple agendamentos e um agendamento pode ter vários tooit de runbooks vinculados. Se um runbook tiver parâmetros, você pode fornecer valores para eles. Você deve fornecer valores para todos os parâmetros obrigatórios e pode fornecer valores para os opcionais.  Esses valores serão usados sempre Olá runbook for iniciado por essa agenda.  Você pode anexar Olá mesmo runbook tooanother agendamento e especificar valores de parâmetros diferentes.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink um runbook de tooa agenda com hello portal clássico do Azure
1. No portal clássico do Azure do hello, selecione **automação** e, em seguida, clique em nome de saudação de uma conta de automação.
2. Selecione Olá **Runbooks** guia.
3. Clique no nome de saudação do hello runbook tooschedule.
4. Clique em Olá **agenda** guia.
5. Se Olá runbook não está vinculado atualmente tooa agenda, você terá a opção de saudação muito**Link tooa nova agenda** ou **Link tooan agendamento existente**.  Se o runbook Olá agenda tooa vinculadas no momento, clique em **Link** em Olá inferior da saudação janela tooaccess essas opções.
6. Se Olá runbook tiver parâmetros, você será solicitado para seus valores.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink um runbook de tooa agenda com hello portal do Azure
1. No portal do Azure, na sua conta de automação de saudação, clique em Olá **Runbooks** bloco tooopen Olá **Runbooks** folha.
2. Clique no nome de saudação do hello runbook tooschedule.
3. Se Olá runbook não estiver atualmente vinculado tooa agenda, você será ser Olá determinada opção toocreate uma nova agenda ou vincular tooan existente agenda.  
4. Se Olá runbook tiver parâmetros, você pode selecionar a opção de saudação **modificar configurações de execução (padrão: Azure)** e hello **parâmetros** folha é apresentada onde você pode inserir informações de saudação adequadamente.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink um runbook tooa de agenda com o Windows PowerShell
Você pode usar o hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink um runbook clássico do agendamento tooa ou [AzureRmAutomationScheduledRunbook registro](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet para runbooks na Olá portal do Azure.  Você pode especificar valores para parâmetros de runbook Olá com o parâmetro hello parâmetros. Confira [Como iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md) para saber mais sobre como especificar valores de parâmetro.

saudação de exemplo a seguir comandos mostram como toolink uma agenda usando um cmdlet de gerenciamento de serviços do Azure com parâmetros.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

saudação de exemplo a seguir comandos mostram como toolink um runbook de tooa agenda usando um cmdlet do Gerenciador de recursos do Azure com parâmetros.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Desabilitando uma agenda
Quando você desabilita uma agenda, qualquer tooit runbooks vinculados não serão mais executados na agenda. Você pode desabilitar manualmente uma agenda ou definir uma hora de expiração para agendas com uma frequência ao criá-las. Quando é atingido o tempo de expiração hello, Olá agenda será desabilitada.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable uma agenda de saudação portal clássico do Azure
Você pode desabilitar uma agenda no hello portal clássico do Azure na página de detalhes da agenda Olá para agendamento de saudação.

1. Em Olá portal clássico do Azure, selecione a automação e, em seguida, clique em nome de saudação de uma conta de automação.
2. Selecione a guia de ativos de saudação.
3. Clique em nome de saudação do tooopen agenda sua página de detalhes.
4. Alterar **habilitado** muito**não**.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable uma agenda de saudação portal do Azure
1. No portal do Azure, na sua conta de automação de saudação, clique em Olá **ativos** bloco tooopen Olá **ativos** folha.
2. Clique em Olá **agendas** bloco tooopen Olá **agendas** folha.
3. Clique em nome de saudação de uma folha de detalhes do agendamento tooopen hello.
4. Alterar **habilitado** muito**não**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable uma agenda com o Windows PowerShell
Você pode usar o hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) propriedades de saudação do cmdlet toochange de uma agenda existente para um runbook clássico ou [AzureRmAutomationSchedule conjunto](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet para runbooks na saudação do Azure Portal. Olá toodisable agendar, especifique **false** para Olá **IsEnabled** parâmetro.

Olá comandos de exemplo a seguir mostra como toodisable um agendamento usando Olá cmdlets de gerenciamento de serviços do Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

saudação de exemplo a seguir comandos mostram como toodisable uma agenda para um runbook usando um cmdlet do Gerenciador de recursos do Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre como trabalhar com agendas, consulte [ativos de agenda na automação do Azure](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* tooget iniciado com runbooks na automação do Azure, consulte [iniciando um Runbook na automação do Azure](automation-starting-a-runbook.md) 

