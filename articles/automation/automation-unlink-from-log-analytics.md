---
title: "aaaUnlink conta de automação do Azure da análise de Log | Microsoft Docs"
description: "Este artigo fornece uma visão geral de como toounlink à automação do Azure a conta de um espaço de trabalho do OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>Como toounlink a automação da conta de um espaço de trabalho de análise de Log

Automação do Azure integra-se com a análise de Log toonot somente suporte o monitoramento proativo de seus trabalhos de runbook em todas as suas contas de automação, mas também é necessária quando você importar Olá soluções que são dependentes de análise de Log a seguir:

* [Gerenciamento de atualizações](../operations-management-suite/oms-solution-update-management.md)
* [Controle de alterações](../log-analytics/log-analytics-change-tracking.md)
* [Iniciar/parar VMs durante os horários fora de pico](automation-solution-vm-management.md)
 
Se você decidir que não deseja mais toointegrate sua conta de automação com análise de Log, você pode desvincular sua conta diretamente da saudação portal do Azure.  Antes de prosseguir, você precisará primeiro tooremove soluções de saudação mencionadas anteriormente, caso contrário, esse processo será impedido de continuar.  Tópico de saudação de revisão para solução em particular Olá importou etapas de saudação toounderstand necessárias tooremove-lo.  

Após a remoção dessas soluções pode executar Olá toounlink as etapas a seguir sua conta de automação.

## <a name="unlink-workspace"></a>Desvincular o espaço de trabalho

1. Em Olá portal do Azure, abra sua conta de automação e, na folha de conta de automação hello, na folha de conta hello, selecione **desvincular o espaço de trabalho**.<br><br> ![Opção Desvincular espaço de trabalho](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. Na folha de espaço de trabalho de desvinculação hello, clique em **desvincular o espaço de trabalho**.<br><br> ![Folha Desvincular espaço de trabalho](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Você receberá um aviso verificando que desejar tooproceed.<br><br>
3. Enquanto a automação do Azure tenta conta de saudação toounlink seu espaço de trabalho de análise de Log, você pode acompanhar o progresso de saudação em **notificações** menu hello.

Se você usou a solução de gerenciamento de atualizações de Olá, opcionalmente, convém Olá tooremove itens que não são mais necessárias após remover solução Olá a seguir.

* Agendas de atualizações.  Cada uma terá nomes que correspondam às implantações de atualização de saudação criado)

* Grupos de trabalho híbrida criados para solução de saudação.  Cada uma será nomeada da mesma forma muito machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

Se você usou Olá iniciar/parar VMs durante a solução de fora do horário comercial, opcionalmente, convém Olá tooremove itens que não são mais necessárias após remover solução Olá a seguir.

* Iniciar e parar agendas de runbook da VM 
* Iniciar e parar runbooks da VM
* variáveis   

## <a name="next-steps"></a>Próximas etapas

tooreconfigure seu toointegrate de conta de automação com análise de logs do OMS, consulte [encaminhar o status do trabalho e fluxos de trabalho de automação tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md). 
