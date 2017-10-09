---
title: "aaaUser ação iniciada pelo Azure automação de Runbook na análise de Log | Microsoft Docs"
description: "Este artigo descreve como toorun um runbook de automação de uma análise de Log Pesquisar resultados sob demanda."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Realizar uma ação com um Runbook de Automação de um resultado de pesquisa do Log Analytics

Em um resultado de pesquisa de log na análise de Log do Azure, agora você pode selecionar **agir** toorun um runbook de automação.  Olá runbook pode ser usado tooremediate Olá problema ou executar alguma outra ação, como coletar informações de solução de problemas, envie um email ou criar uma solicitação de serviço. 

## <a name="components-and-features-used"></a>Componentes e recursos usados
* [Conta de Automação do Azure](../automation/automation-offering-get-started.md)
* [Espaço de trabalho do Log Analytics](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>runbook tooinitiate de pesquisa de log

ação tootake em um evento e iniciar um runbook a partir de resultados de pesquisa de log, comece criando uma pesquisa de log e de resultados hello, você pode chamar uma runbook sob demanda.  Isso pode ser obtido do recurso de pesquisa de log de saudação do hello Azure ou [portal do OMS](../log-analytics/log-analytics-log-searches.md).  Neste exemplo, podemos executar uma pesquisa de log de saudação portal do Azure com uma demonstração básica desse recurso.

1. Olá portal do Azure, no menu de Hub Olá em **mais serviços** e selecione **análise de Log**.  
2. Na folha de análise de Log hello, selecione seu espaço de trabalho de análise de Log e na folha de espaço de trabalho Olá selecione **pesquisa de Log**.  
3. Na folha de pesquisa de Log hello, execute uma pesquisa de log.  
4. Olá log dos resultados da pesquisa, clique em esquerda de toohello Olá elipse de um dos campos de saudação e de saudação pop-up, selecione **agir em**.<br><br> ![Selecione a opção Agir do resultado da pesquisa](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Na folha de ação de Take hello, selecione **executar um runbook**e em Olá **executar um runbook** folha, você pode selecionar um toorun de runbook.  Você pode selecionar qualquer runbook no hello conta de automação é o espaço de trabalho de análise de Log toohello vinculado.  Observe o seguinte hello:

    * Os runbooks são organizados por marcas
    * Valores de parâmetro de entrada do runbook podem ser selecionados diretamente em campos de saudação do resultado da pesquisa hello.  Uma lista suspensa aparecerá exibindo todos os campos disponíveis do hello de tooselect de resultado de saudação do.  
    * Você pode escolher toorun Olá runbook em um [hybrid runbook worker de](../automation/automation-hybrid-runbook-worker.md) que você instalou no computador de saudação que tem o problema de saudação se você tiver um grupo do Hybrid Runbook Worker correspondente que contenha apenas como um membro.  Se nome de saudação do grupo do Hybrid Worker Olá corresponder a nome de saudação do computador Olá no resultado de pesquisa de log de saudação, grupo de saudação é selecionado automaticamente.    

6. Depois de clicar em **executar**, folha de trabalho de runbook Olá abrirá tooallow você tooreview Olá status do trabalho de saudação.   

Se você selecionar um runbook que foi configurado toobe [chamado a partir de um alerta de análise de Log](../automation/automation-invoke-runbook-from-omsla-alert.md), ele tem um parâmetro de entrada chamado **WebhookData** que é **objeto** tipo.  Se o parâmetro de entrada hello é obrigatório, você precisa toopass Olá pesquisa resultados toohello runbook para que ele pode converter cadeia de caracteres formatada em JSON de saudação em um tipo de objeto, permitindo que você toofilter em itens específicos que você irá referenciar nas atividades de runbook.  Você faz isso selecionando **(Object) do resultado da pesquisa** da lista suspensa de saudação.<br><br> ![Selecione o objeto de dados de Webhook para o parâmetro do runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Próximas etapas

* Saudação de revisão [referência de pesquisa de log de análise de Log](log-analytics-search-reference.md) tooview todos Olá Pesquisar campos e facetas disponíveis na análise de Log.
* toolearn como tooinvoke um runbook de automação automaticamente, examine [chamar um runbook de automação do Azure de um alerta de análise de logs do OMS](../automation/automation-invoke-runbook-from-omsla-alert.md).  
