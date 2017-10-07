---
title: "aaaView atividades do Azure registra em log com análise de Log | Microsoft Docs"
description: "Você pode usar o hello tooanalyze de solução de Logs de atividades do Azure e o log de atividades do Azure de saudação de pesquisa em todas as suas assinaturas do Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Exibir logs de atividade do Azure

![Símbolo dos logs de atividades do Azure](./media/log-analytics-activity/activity-log-analytics.png)

Olá solução de análise de Log de atividade ajuda você a analisar e pesquisar Olá [log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) em todas as suas assinaturas do Azure. Olá Log de atividades do Azure é um log que oferece ideias sobre Olá operações executadas em recursos em suas assinaturas. Hello atividade Log era conhecido anteriormente como *os Logs de auditoria* ou *Logs operacionais* desde que ele relata eventos de suas assinaturas.

Usando hello atividade de Log, você pode determinar Olá *que*, *que*, e *quando* para qualquer gravação operações (PUT, POST, DELETE) realizadas para recursos de saudação em sua assinatura. Você também pode saber o status de saudação de operações de saudação e outras propriedades relevantes. Olá Log de atividades não inclui operações (GET) de leitura ou de operações para recursos que usam o modelo de implantação clássico hello.

Quando você se conectar a seu logs de atividades do Azure tooLog análise, você pode:

- Analisar logs de atividade de saudação com exibições predefinidas
- Analisar e pesquisar logs de atividade de várias assinaturas do Azure
- Manter logs de atividade por mais de 90 dias<sup>1</sup>
- Correlacionar os logs de atividade com outra plataforma do Azure e dados do aplicativo
- Consultar atividades operacionais agregadas por status
- Exibir tendências de atividades que acontecem em cada serviço do Azure
- Relatar alterações de autorização em todos os recursos do Azure
- Identificar problemas de integridade ou interrupção de serviço que afetam os recursos
- Use atividades de usuário de toocorrelate de pesquisa de Log, operações de dimensionamento automático, alterações de autorização e logs de tooother de integridade do serviço ou métricas do seu ambiente

<sup>1</sup>por padrão, a análise de Log mantém seus logs de atividades do Azure por 90 dias, mesmo se você estiver na camada gratuita hello. Ou, se você tiver uma configuração de retenção de espaço de trabalho inferior a 90 dias. Se o seu espaço de trabalho tem retenção mais de 90 dias, hello atividade logs são mantidos por período de retenção de saudação do espaço de trabalho.

Análise de log coleta logs de atividade gratuitamente e armazena os logs de saudação por 90 dias gratuitos. Se você armazenar logs por mais de 90 dias, incorrerá em encargos de retenção de dados para dados de saudação armazenados mais de 90 dias.

Quando você estiver no hello livre de preço, logs de atividade não se aplicam a tooyour diário consumo de dados.

## <a name="connected-sources"></a>Fontes conectadas

Ao contrário da maioria das outras soluções do Log Analytics, dados não são coletados para logs de atividade por agentes. Todos os dados usados pela solução de saudação vem diretamente do Azure.

| Fonte Conectada | Suportado | Descrição |
| --- | --- | --- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Não | solução de saudação não coletará informações de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não | solução de saudação não coletará informações de agentes do Linux. |
| [Grupo de gerenciamento do SCOM](log-analytics-om-agents.md) | Não | solução de saudação não coletará informações de agentes em um grupo de gerenciamento do SCOM conectado. |
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | solução de saudação não coleta informações do armazenamento do Azure. |

## <a name="prerequisites"></a>Pré-requisitos

- tooaccess informações do log de atividades do Azure, você deve ter uma assinatura do Azure.

## <a name="configuration"></a>Configuração

Execute Olá solução de análise de Log de atividade de saudação etapas tooconfigure para seus espaços de trabalho a seguir.

1. Habilitar a solução de análise de Log de atividade de saudação da saudação [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. Configure o espaço de trabalho de atividade logs toogo tooyour análise de Log.
    1. Olá portal do Azure, selecione o espaço de trabalho e, em seguida, clique em **log de atividades do Azure**.
    2. Para cada assinatura, clique no nome de assinatura de saudação.  
        ![adicionar assinatura](./media/log-analytics-activity/add-subscription.png)
    3. Em Olá *SubscriptionName* folha, clique em **conectar**.  
        ![conectar assinatura](./media/log-analytics-activity/subscription-connect.png)

Se você adicionar a solução hello usando o portal do OMS Olá, você verá a seguir Olá lado a lado. Entrar toohello tooconnect portal do Azure um espaço de trabalho de tooyour de assinatura do Azure.  
![executar avaliação](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Usando a solução de saudação

Quando você adiciona o espaço de trabalho tooyour solução de análise de Log de atividade de hello, Olá **os Logs de atividade do Azure** bloco é adicionado o painel de visão geral de tooyour. Este bloco exibe uma contagem do número de saudação de registros de atividades do Azure para hello assinaturas do Azure que Olá solução tem acessem.

![Bloco de logs de atividade do Azure](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Exibir logs de atividade do Azure

Clique em hello **os Logs de atividade do Azure** bloco tooopen Olá **Logs de atividade do Azure** painel. painel Olá inclui folhas Olá Olá a tabela a seguir. Cada folha lista os itens too10 correspondência critérios da folha de saudação especificado escopo e tempo de intervalo. Você pode executar uma pesquisa de log que retorna todos os registros clicando **ver todos os** na parte inferior da folha de saudação ou clicando o cabeçalho de folha de saudação do hello.

Dados de log de atividade aparecem somente *depois* você configurou sua solução de toohello de toogo de logs de atividade, para que você não pode exibir dados antes disso.

| Folha | Descrição |
| --- | --- |
| Entradas de log de atividades do Azure | Mostra um gráfico de barras da superior Olá entrada de log de atividades do Azure registros totais Olá intervalo de datas selecionado e mostra uma lista de saudação chamadores de atividade 10 principais. Clique em Olá toorun de gráfico de barras de uma pesquisa de log para <code>Type=AzureActivity</code>. Clique em um toorun de item do chamador uma pesquisa de log retornando todas as entradas de log de atividade para aquele item. |
| Logs de atividade por status | Mostra um gráfico de rosca para status do log de atividades do Azure para o intervalo de datas de saudação que você selecionou. Também mostra uma lista de uma lista de registros de status dez principais da saudação. Clique em Olá gráfico toorun uma pesquisa de log para <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Clique em um toorun de item de status retornando todas as entradas de log de atividade para esse registro de status de uma pesquisa de log. |
| Logs de atividade por recurso | Mostra o número total de saudação de recursos com logs de atividade e lista superior Olá dez recursos com o registro de conta para cada recurso. Clique em Olá área total toorun uma pesquisa de log para <code>Type=AzureActivity &#124; measure count() by Resource</code>, que mostra todos os recursos do Azure solução toohello disponíveis. Clique em um recurso toorun uma pesquisa de log retornar todos os registros de atividade para esse recurso. |
| Logs de atividade por provedor de recursos | Mostra Olá o número total de provedores de recursos que produzem atividade logs e lista os dez primeiros de saudação. Clique em Olá área total toorun uma pesquisa de log para <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, que mostra todos os provedores de recursos do Azure. Clique em um provedor de recursos toorun uma pesquisa de log retornar todos os registros de atividade para o provedor de saudação. |

![Painel Logs de Atividade do Azure](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Próximas etapas

- Crie um [alerta](log-analytics-alerts-creating.md) quando ocorrer uma atividade específica.
- Use [pesquisa de Log](log-analytics-log-searches.md) tooview obter informações de seus logs de atividade.
