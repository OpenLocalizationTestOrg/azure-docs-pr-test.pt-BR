---
title: "aaaTesting um runbook na automação do Azure | Microsoft Docs"
description: "Antes de publicar um runbook na automação do Azure, você pode testar tooensure funciona conforme o esperado.  Este artigo descreve como tootest um runbook e exibir sua saída."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Testando um runbook na Automação do Azure
Quando você testar um runbook, Olá [versão de rascunho](automation-creating-importing-runbook.md#publishing-a-runbook) é executado e as ações que ele realiza são concluídas. Nenhum histórico de trabalho é criado, mas Olá [saída](automation-runbook-output-and-messages.md#output-stream) e [aviso e erro](automation-runbook-output-and-messages.md#message-streams) fluxos são exibidos no hello painel de saída do teste. Mensagens toohello [fluxo detalhado](automation-runbook-output-and-messages.md#message-streams) são exibidos no painel de saída de hello somente se hello [$VerbosePreference variável](automation-runbook-output-and-messages.md#preference-variables) é definida tooContinue.

Mesmo que a versão de rascunho hello está sendo executado, Olá runbook ainda executa normalmente o fluxo de trabalho hello e executa quaisquer ações contra recursos no ambiente de saudação. Por esse motivo, você deve testar apenas runbooks em recursos de não produção.

Olá procedimento tootest cada [tipo de runbook](automation-runbook-types.md) é Olá mesmo, e não há nenhuma diferença em testes entre o editor de texto de saudação e editor gráfico de saudação em Olá portal do Azure.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest um runbook no portal do Azure de saudação
Você pode trabalhar com qualquer [tipo de runbook](automation-runbook-types.md) em Olá portal do Azure.

1. Versão de rascunho Olá aberto de runbook hello em qualquer Olá [editor textual](automation-edit-textual-runbook.md) ou [editor gráfico](automation-graphical-authoring-intro.md).
2. Clique em Olá **teste** folha de teste do botão tooopen hello.
3. Se Olá runbook tiver parâmetros, eles serão listados no painel esquerdo hello, onde você pode fornecer valores toobe usado para teste de saudação.
4. Se você quiser teste de saudação toorun em um [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), altere **configurações de execução** muito**Hybrid Worker** e o nome de select saudação do grupo de destino de saudação.  Caso contrário, mantenha o padrão de saudação **Azure** toorun Olá teste na nuvem hello.
5. Clique em Olá **iniciar** teste de saudação do botão toostart.
6. Se o runbook Olá [fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) ou [gráfico](automation-runbook-types.md#graphical-runbooks), em seguida, você pode interromper ou suspendê-lo enquanto ele está sendo testado com os botões de saudação abaixo Olá painel de saída. Quando você suspende o runbook hello, ele conclui a atividade atual de saudação antes de ser suspenso. Depois que Olá runbook for suspenso, você pode interrompê-lo ou reiniciá-lo.
7. Inspecione a saída Olá Olá runbook no painel de saída de hello.

## <a name="next-steps"></a>Próximas etapas
* toolearn como toocreate ou importar um runbook, consulte [criando ou importando um runbook na automação do Azure](automation-creating-importing-runbook.md)
* toolearn mais sobre a criação de gráficos, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
* toolearn mais sobre como configurar mensagens de status de tooreturn runboks e erros, incluindo práticas recomendadas, consulte [Runbook mensagens na automação do Azure e saída](automation-runbook-output-and-messages.md)

