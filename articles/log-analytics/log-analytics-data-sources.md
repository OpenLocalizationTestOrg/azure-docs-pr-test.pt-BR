---
title: "fontes de dados de aaaConfigure na análise de Log do OMS | Microsoft Docs"
description: "Fontes de dados definem dados de saudação que coleta de análise de Log de agentes e outras fontes conectadas.  Este artigo descreve o conceito de saudação como análise de Log usa fontes de dados, explica os detalhes de como Olá tooconfigure-los e fornece um resumo da saudação diferentes fontes de dados disponíveis."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Fontes de dados no Log Analytics
Análise de log coleta dados de fontes conectadas de saudação em seu espaço de trabalho do OMS e armazena-o no repositório do OMS.  dados Olá coletados de cada um são definidos por Olá fontes de dados que você configurar.  Dados no repositório do OMS Olá são armazenados como um conjunto de registros.  Cada fonte de dados cria registros de um determinado tipo com cada tipo de tendo seu próprio conjunto de propriedades.

![Coleta de dados do Log Analytics](./media/log-analytics-data-sources/overview.png)

Fontes de dados são diferentes de soluções do OMS que também coletar dados de fontes conectadas e criar registros no repositório do OMS hello.  Soluções podem ser adicionadas tooyour de espaço de trabalho na Galeria de soluções de saudação e normalmente fornecem ferramentas de análise adicional no portal do OMS Olá.  

## <a name="summary-of-data-sources"></a>Resumo das fontes de dados
fontes de dados de saudação que estão atualmente disponíveis na análise de Log são listados na Olá a tabela a seguir.  Cada um tem um link tooa outro artigo fornece detalhes para essa fonte de dados.

| Fonte de dados | Tipo de evento | Descrição |
|:--- |:--- |:--- |
| [Logs personalizados](log-analytics-data-sources-custom-logs.md) |\<LogName\>_CL |Arquivos de texto em agentes do Windows ou Linux que contenham informações de log. |
| [Logs de eventos do Windows](log-analytics-data-sources-windows-events.md) |Evento |Os eventos coletados do log de eventos de saudação em computadores Windows. |
| [Contadores de desempenho do Windows](log-analytics-data-sources-performance-counters.md) |Perf |Contadores de desempenho coletados de computadores Windows. |
| [Contadores de desempenho do Linux](log-analytics-data-sources-performance-counters.md) |Perf |Contadores de desempenho coletados de computadores Linux. |
| [Logs do IIS](log-analytics-data-sources-iis-logs.md) |W3CIISLog |Serviços de Informações da Internet em formato W3C. |
| [Syslog](log-analytics-data-sources-syslog.md) |syslog |Eventos de syslog em computadores Windows ou Linux. |

## <a name="configuring-data-sources"></a>Configurando fontes de dados
Configurar fontes de dados de saudação **dados** menu na análise de Log **configurações**.  Nenhuma configuração é entregue fontes tooall conectado no seu espaço de trabalho do OMS.  No momento, você não pode excluir nenhum agente dessa configuração.

![Configurar eventos do Windows](./media/log-analytics-data-sources/configure-events.png)

1. No console do OMS Olá clique Olá **configurações** lado a lado ou hello **configurações** botão na parte superior de saudação da tela hello.
2. Selecione **Dados**.
3. Clique em Olá tooconfigure de fonte de dados.
4. Siga a documentação de toohello Olá link para cada fonte de dados de saudação acima da tabela para obter detalhes em sua configuração.

> [!NOTE]
> Atualmente, você não pode configurar fontes de dados de análise de Log no hello portal do Azure.

## <a name="data-collection"></a>Coleta de dados
Configurações de fonte de dados são entregues tooagents que estão diretamente conectado tooLog análise dentro de alguns minutos.  Olá especificado dados são coletados de agente hello e entregue diretamente tooLog análise na fonte de dados específico tooeach intervalos.  Consulte a documentação de saudação para cada fonte de dados para essas especificações.

Para agentes do System Center Operations Manager (SCOM) em um grupo de gerenciamento conectado, configurações de fonte de dados são convertidas em pacotes de gerenciamento e entregue ao grupo de gerenciamento toohello a cada 5 minutos por padrão.  Agente de Olá baixa o pacote de gerenciamento hello como qualquer outro e coleta Olá dados especificados. Dependendo da saudação de fonte de dados Olá dados serão enviadas tooa servidor de gerenciamento que encaminha Olá dados toohello análise de Log ou agente Olá enviará Olá dados tooLog análise sem passar pelo servidor de gerenciamento de saudação. Consulte também[detalhes de coleta de dados para recursos do OMS e soluções](log-analytics-add-solutions.md#data-collection-details) para obter detalhes.  Você pode ler sobre os detalhes da conexão SCOM e o OMS e modificando a frequência de saudação que a configuração é entregue em [configurar a integração com o System Center Operations Manager](log-analytics-om-agents.md).

Se o agente de saudação tooLog tooconnect não é possível análise ou o Operations Manager, ele continuará toocollect dados que fornecerá ao estabelecer uma conexão.  Dados podem ser perdidos se a quantidade de saudação de dados atinge o tamanho máximo do cache de saudação para cliente hello, ou se Olá agente não é capaz de tooestablish uma conexão dentro de 24 horas.

## <a name="log-analytics-records"></a>Registros do Log Analytics
Todos os dados coletados pela análise de Log é armazenado no repositório do OMS hello como registros.  Registros coletados por diferentes fontes de dados terão seu próprio conjunto de propriedades e serão identificados por sua propriedade **Type** .  Ver documentação Olá para cada fonte de dados e a solução para obter detalhes sobre cada tipo de registro.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [soluções](log-analytics-add-solutions.md) que adicionar funcionalidade tooLog análise e também coletar dados no repositório do OMS hello.
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) dados de saudação tooanalyze coletados de fontes de dados e soluções.  
* Configurar [alertas](log-analytics-alerts.md) tooproactively notificá-lo de dados críticos coletados de fontes de dados e soluções.
