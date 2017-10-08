---
title: "execução de aaaRunbook na automação do Azure | Microsoft Docs"
description: "Descreve os detalhes de saudação do como um runbook na automação do Azure é processado."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Execução de runbook na Automação do Azure
Quando você inicia um runbook na Automação do Azure, um trabalho é criado. Um trabalho é uma instância única de execução de um runbook. Um objeto de automação do Azure worker é atribuído toorun cada trabalho. Enquanto os trabalhadores são compartilhados por várias contas do Azure, os trabalhos de diferentes contas de automação ficam isolados uns dos outros. Você não tem controle sobre qual solicitação do trabalho serviços Olá para seu trabalho.  Um único runbook pode ter vários trabalhos em execução ao mesmo tempo. Quando você exibir a lista de saudação de runbooks em Olá portal do Azure, ele lista o status de saudação de todos os trabalhos que foram iniciados para cada runbook. Você pode exibir a lista de saudação de trabalhos para cada runbook no status do pedido tootrack saudação de cada um. Para obter uma descrição do status de trabalho diferente do hello, consulte [status do trabalho](#job-statuses).

Olá, diagrama a seguir mostra saudação do ciclo de vida de um trabalho de runbook para [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) e [runbooks do fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Status de trabalho - Fluxo de trabalho do PowerShell](./media/automation-runbook-execution/job-statuses.png)

Olá, diagrama a seguir mostra saudação do ciclo de vida de um trabalho de runbook para [runbooks do PowerShell](automation-runbook-types.md#powershell-runbooks).

![Status de trabalho - Script do PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

Os trabalhos de tem acesso tooyour Azure recursos fazendo uma conexão tooyour assinatura do Azure. Somente tiverem acesso tooresources em seu data center se esses recursos estiverem acessíveis da nuvem pública hello.

## <a name="job-statuses"></a>Status de trabalho
Olá tabela a seguir descreve Olá diferentes status possíveis para um trabalho.

| Status | Descrição |
|:--- |:--- |
| Concluído |trabalho de saudação concluído com êxito. |
| Com falha |Para [runbooks gráfico e fluxo de trabalho do PowerShell](automation-runbook-types.md), Olá runbook falha toocompile.  Para [runbooks de Script do PowerShell](automation-runbook-types.md), Olá runbook falha toostart ou trabalho Olá encontrou uma exceção. |
| Erro, aguardando recursos |Falha no trabalho de saudação porque atingiu Olá [compartilhamento justo](#fairshare) limitar três vezes e iniciado a partir de Olá mesmo ponto de verificação ou de saudação de runbook Olá cada hora inicial. |
| Em fila |Olá trabalho está aguardando recursos em um trabalho de automação toocome disponível para que ele possa ser iniciado. |
| Iniciando |Olá trabalho foi atribuído trabalho tooa e sistema hello está em processo de saudação de iniciá-lo. |
| Continuando |sistema de saudação está no processo de saudação de retomar o trabalho Olá depois que ele foi suspenso. |
| Executando |trabalho de Hello está sendo executado. |
| Executando, aguardando recursos |Olá trabalho foi descarregado porque atingiu Olá [compartilhamento justo](#fairshare) limite. Ele será retomado em breve do seu último ponto de verificação. |
| Parada |trabalho de saudação foi interrompido pelo usuário Olá antes de ser concluída. |
| Parando |sistema de saudação está no processo de saudação de parar o trabalho de saudação. |
| Suspenso |trabalho de saudação foi suspenso pelo usuário hello, pelo sistema de saudação ou por um comando no runbook hello. Um trabalho suspenso pode ser iniciado novamente e continuar a partir de seu último ponto de verificação ou hello a partir de runbook Olá se ele não tem pontos de verificação. Olá runbook somente será suspenso pelo sistema hello quando ocorre uma exceção. Por padrão, ErrorActionPreference está definido muito**continuar**, que significa que o trabalho Olá continua em execução em um erro. Se essa variável de preferência for definida muito**parar**, em seguida, suspende o trabalho de saudação em um erro.  Aplica-se também[runbooks gráfico e fluxo de trabalho do PowerShell](automation-runbook-types.md) somente. |
| Suspensão |sistema de saudação está tentando toosuspend trabalho de saudação na solicitação de saudação do usuário hello. Olá runbook precisa atingir seu próximo ponto de verificação antes de poder ser suspenso. Se já passou de seu último ponto de verificação, ele será concluído antes de ser suspenso.  Aplica-se também[runbooks gráfico e fluxo de trabalho do PowerShell](automation-runbook-types.md) somente. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Exibindo o status do trabalho de saudação portal do Azure
Você pode exibir o status resumido de todos os trabalhos de runbook ou analisar detalhes de um trabalho específico de runbook no portal do Azure de saudação ou configurando a integração com o status de trabalho de runbook sua análise de logs do Microsoft Operations Management Suite (OMS) espaço de trabalho tooforward e fluxos de trabalho.  Para obter mais informações sobre como integrar com análise de logs do OMS, consulte [encaminhar o status do trabalho e fluxos de trabalho de automação tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Resumo dos trabalhos de runbook da Automação
Em Olá à direita da sua conta de automação selecionada, você pode ver um resumo de todos os trabalhos de runbook Olá para uma conta de automação selecionada em **estatísticas de trabalho** lado a lado.<br><br> ![Bloco Estatísticas de Trabalho](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Este bloco exibe uma contagem e a representação gráfica do status do trabalho Olá para todos os trabalhos executados.  

Clicar no bloco Olá apresenta Olá **trabalhos** folha, que inclui uma lista resumida de todos os trabalhos executados, com o status, a execução do trabalho e horas de início e conclusão.<br><br> ![Folha Trabalhos da Conta de automação](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Você pode filtrar a lista de saudação de trabalhos selecionando **filtrar trabalhos** e filtrar em um runbook específico, o status do trabalho, ou da lista suspensa de hello, Olá toosearch de intervalo de data/hora dentro.<br><br> ![Filtrar por status do trabalho](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Como alternativa, você pode exibir detalhes de resumo do trabalho para um runbook específico, selecionando esse runbook da saudação **Runbooks** folha em conta de automação e, em seguida, selecione Olá **trabalhos** lado a lado.  Isso apresenta Olá **trabalhos** folha, e de lá você pode clicar em Olá trabalho registro tooview seus detalhes e saída.<br><br> ![Folha Trabalhos da Conta de automação](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Resumo do trabalho
Você pode exibir uma lista de todos os trabalhos de saudação que foram criados para um determinado runbook e seus status mais recentes. Você pode filtrar essa lista pelo status do trabalho e intervalo de saudação de datas para Olá última alteração toohello trabalho. tooview suas informações detalhadas e saída, clique no nome de saudação de um trabalho. Olá exibição detalhada do trabalho de saudação inclui valores de Olá Olá parâmetros de runbook que foram fornecidos toothat trabalho.

Você pode usar o hello etapas tooview saudação de trabalhos para um runbook a seguir.

1. No portal do Azure de Olá, selecione **automação** e, em seguida, selecione o nome de saudação de uma conta de automação.
2. No hub hello, selecione **Runbooks** e, em seguida, em Olá **Runbooks** folha selecionar um runbook na lista de saudação.
3. Na folha de Olá runbook Olá selecionado, clique em Olá **trabalhos** lado a lado.
4. Clique em um dos trabalhos de saudação na lista de saudação e na folha de detalhes de trabalho de runbook hello, você pode exibir seus detalhes e saída.

## <a name="retrieving-job-status-using-windows-powershell"></a>Recuperando o status do trabalho usando o Windows PowerShell
Você pode usar o hello [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) tooretrieve trabalhos de saudação criados para o runbook e hello detalhes de um trabalho específico. Se você iniciar um runbook com o Windows PowerShell usando [AzureRmAutomationRunbook início](https://msdn.microsoft.com/library/mt603661.aspx), em seguida, ele retorna o trabalho resultante hello. Use [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)tooget de saída, a saída de um trabalho.

Olá comandos de exemplo a seguir recuperar o último trabalho Olá para um exemplo de runbook e exibe seu status, valores hello fornecidos para os parâmetros de runbook hello e Olá saída do trabalho de saudação.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>fração justa
Em recursos de tooshare ordem entre todos os runbooks na nuvem hello, automação do Azure serão descarregados temporariamente qualquer trabalho após sua execução por três horas.  Durante esse tempo, os trabalhos para [runbooks com base no PowerShell](automation-runbook-types.md#powershell-runbooks) são interrompidos e não serão reiniciados.  Olá trabalho status mostra **parado**.  Esse tipo de runbook sempre será reiniciado desde o início de saudação desde que não oferecem suporte a pontos de verificação.  

[Os runbooks baseados em Fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) serão retomados do seu último [ponto de verificação](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Depois de executar três horas, o trabalho de runbook Olá será suspenso pelo serviço hello e seu status mostra **em execução, aguardando recursos**.  Quando uma área restrita fica disponível, Olá runbook será reiniciado automaticamente pelo serviço de automação de saudação e reinicia a partir do último ponto de verificação de saudação.  Este é o comportamento normal do fluxo de trabalho do PowerShell para suspender/reiniciar.  Se o runbook Olá novamente exceder três horas de tempo de execução, Olá processo se repete toothree horas.  Após Olá terceira reinicialização, se Olá runbook ainda não foi concluída em três horas, em seguida, falha do trabalho de runbook hello e status do trabalho Olá mostra **falhou, aguardando recursos**.  Nesse caso, você receberá Olá a seguinte exceção com falha de saudação.

*trabalho Olá não pode continuar em execução porque ele foi removido repetidamente a partir Olá mesmo ponto de verificação. Verifique se o Runbook não executa operações demoradas sem persistir o estado.*

Este é o serviço de saudação do tooprotect de execução de runbooks indefinidamente sem concluir, porque eles não são toomake capaz de ele toohello próximo ponto de verificação sem serem descarregados novamente.

Se Olá runbook não tiver nenhum ponto de verificação ou trabalho Olá não atingiu o primeiro ponto de verificação de saudação antes de ser descarregado, em seguida, ele será reiniciado desde o início de saudação.  

Quando você cria um runbook, você deve garantir que toorun de tempo de saudação todas as atividades entre dois pontos de verificação não exceda três horas. Talvez seja necessário tooadd pontos de verificação tooyour runbook tooensure que não atingir esse limite de três horas ou dividir longa operações em execução. Por exemplo, o runbook pode executar uma reindexação em um grande banco de dados SQL. Se essa única operação não for concluída dentro de saudação razoável limite de compartilhamento, em seguida, o trabalho de saudação é descarregados e reiniciado a partir do início da saudação. Nesse caso, você deve interromper a operação de reindexação Olá em várias etapas, como reindexar uma tabela por vez e, em seguida, insira um ponto de verificação após cada operação, de modo que hello trabalho possa ser retomado após Olá última operação toocomplete.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre métodos diferentes de saudação que pode ser usado toostart um runbook na automação do Azure, consulte [iniciando um runbook na automação do Azure](automation-starting-a-runbook.md)

