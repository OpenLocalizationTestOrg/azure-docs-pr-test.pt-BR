---
title: Como monitorar o Cache Redis do Azure | Microsoft Docs
description: "Saiba como monitorar a integridade e o desempenho de suas instâncias do Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 8996f5ce03e39557d9cc9c3de1ec214f5cd664b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-monitor-azure-redis-cache"></a>Como monitorar o Cache Redis do Azure
O Cache Redis do Azure usa o [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) para fornecer várias opções para monitorar suas instâncias de cache. Você pode exibir métricas, fixar gráficos de métricas ao quadro inicial, personalizar o intervalo de data e hora de gráficos de monitoramento, adicionar/remover as métricas de gráficos e definir alertas quando determinadas condições forem atendidas. Essas ferramentas permitem monitorar a integridade de suas instâncias de Cache Redis do Azure e ajudá-lo a gerenciar seus aplicativos de cache.

As métricas para instâncias do Cache Redis do Azure são coletadas usando o comando [INFO](http://redis.io/commands/info) de Redis aproximadamente duas vezes por minuto, e são armazenadas automaticamente por 30 dias (consulte [Exportar as métricas de cache](#export-cache-metrics) para configurar uma política de retenção diferente) para que possam ser exibidas nos gráficos de métricas e avaliadas por regras de alerta. Para saber mais sobre os diferentes valores INFO usados para cada métrica de cache, confira [Métricas disponíveis e intervalos de relatórios](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

Para exibir as métricas de cache, [procure](cache-configure.md#configure-redis-cache-settings) sua instância de cache no [portal do Azure](https://portal.azure.com).  O Cache Redis do Azure fornece alguns gráficos internos na folha **Visão geral** e na folha **Métricas de Redis**. Cada gráfico pode ser personalizado com a adição ou remoção de métricas e a alteração do intervalo de relatório.

![Métricas do Redis](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Exibir gráficos de métricas pré-configurados

A folha **Visão geral** tem os seguintes gráficos de monitoramento pré-configurados.

* [Gráficos de monitoramento](#monitoring-charts)
* [Gráficos de uso](#usage-charts)

### <a name="monitoring-charts"></a>Gráficos de monitoramento
A seção **Monitoramento** na folha **Visão geral** tem os gráficos **Acertos e Erros**, **Gets e Sets**, **Conexões** e **Total de Comandos**.

![Gráficos de monitoramento](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Gráficos de uso
A seção **Uso** na folha **Visão geral** tem os gráficos **Carga do Servidor Redis**, **Uso de Memória**, **Largura de Banda de Rede** e **Uso de CPU** e também exibe o **Tipo de preço** para a instância de cache.

![Gráficos de uso](./media/cache-how-to-monitor/redis-cache-usage-part.png)

A **Tipo de preço** exibe a tipo de preço do cache e pode ser usada para [dimensionar](cache-how-to-scale.md) o cache para um tipo de preço diferente.

## <a name="view-metrics-with-azure-monitor"></a>Ver métricas com o Azure Monitor
Para exibir as métricas do Redis e criar gráficos personalizados usando o Azure Monitor, clique em **Métricas** no **menu Recursos** e personalize o gráfico usando as métricas desejadas, intervalo de relatórios, o tipo de gráfico e muito mais.

![Métricas do Redis](./media/cache-how-to-monitor/redis-cache-monitor.png)

Para saber mais sobre como trabalhar com as métricas usando o Azure Monitor, consulte [Visão geral das métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Exportar métricas de cache
Por padrão, as métricas de cache no Azure Monitor são [armazenadas durante 30 dias](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e, em seguida, excluídas. Para persistir suas métricas de cache por mais de 30 dias, [indique uma conta de armazenamento](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) e especifique uma política de **Retenção (dias)** para suas métricas de cache. 

Para configurar uma conta de armazenamento para suas métricas de cache:

1. Clique em **Diagnóstico** no **menu Recursos** na folha **Cache Redis**.
2. Clique em **Ativado**.
3. Marque **Arquivar em uma conta de armazenamento**.
4. Selecione a conta de armazenamento para armazenar as métricas de cache.
5. Marque a caixa de seleção **1 minuto** e especifique uma política de **Retenção (dias)**. Se você não quiser aplicar qualquer política de retenção e manter os dados indefinidamente, defina **Retenção (dias)** como **0**.
6. Clique em **Salvar**.

![Diagnóstico do Redis](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>Além de arquivar suas métricas de cache no armazenamento, você também pode [transmiti-las para um Hub de Eventos ou enviá-las para o Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

Para acessar suas métricas, você pode exibi-las no Portal do Azure conforme descrito anteriormente neste artigo, e também pode acessá-las usando a [API REST das métricas do Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> Se você alterar contas de armazenamento, os dados na conta de armazenamento configurada anteriormente permanecerão disponíveis para download, mas não serão exibidos no portal do Azure.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Métricas disponíveis e intervalos de relatórios
As métricas de cache são relatadas usando vários intervalos de relatórios, incluindo **Última hora**, **Hoje**, **Semana passada** e **Personalizado**. A folha **Métrica** para cada gráfico de métricas exibe os valores médio, mínimo e máximo para cada métrica no gráfico, e algumas métricas exibem um total para o intervalo de relatório. 

Cada métrica inclui duas versões. Uma métrica mede o desempenho de todo o cache, e para os caches que usam [cluster](cache-how-to-premium-clustering.md), uma segunda versão da métrica que inclui `(Shard 0-9)` no nome mede o desempenho de um único fragmento em um cache. Por exemplo, se um cache tiver quatro fragmentos, `Cache Hits` será a quantidade total de ocorrências para todo o cache, e `Cache Hits (Shard 3)` será apenas as ocorrências para esse fragmento do cache.

> [!NOTE]
> Mesmo quando o cache está ocioso sem aplicativos de cliente ativos conectados, você pode ver alguma atividade no cache, como clientes conectados, uso de memória e operações que estão sendo executadas. Essa atividade é normal durante a operação de uma instância do Cache Redis do Azure.
> 
> 

| Métrica | Descrição |
| --- | --- |
| Acertos do Cache |O número de pesquisas de chave com êxito durante o intervalo de relatório especificado. Esse número é mapeado para `keyspace_hits` do comando [INFO](http://redis.io/commands/info) do Redis. |
| Erros de Cache |O número de pesquisas de chave com falha durante o intervalo de relatório especificado. Esse número é mapeado para `keyspace_misses` do comando INFO do Redis. Erros de cache não significam necessariamente que há um problema com o cache. Por exemplo, ao se usar o padrão de programação cache-aside, um aplicativo procura um item no cache primeiro. Se o item não estiver lá (erro de cache), o item será recuperado do banco de dados e adicionado ao cache na próxima vez. Erros de cache são o comportamento normal para o padrão de programação cache-aside. Se o número de erros de cache for maior do que o esperado, examine a lógica do aplicativo que popula e lê do cache. Se os itens estiverem sendo removidos do cache devido à pressão de memória, poderá haver alguns erros de cache, mas uma métrica melhor para monitorar a pressão de memória seria `Used Memory` ou `Evicted Keys`. |
| Clientes conectados |O número de conexões de cliente com o cache durante o intervalo de relatório especificado. Esse número é mapeado para `connected_clients` do comando INFO do Redis. Assim que o [limite de conexão](cache-configure.md#default-redis-server-configuration) for atingido, as tentativas de conexão subsequentes ao cache falharão. Observe que, mesmo que não haja um aplicativo cliente ativo, pode haver ainda algumas instâncias de clientes conectados devido a conexões e processos internos. |
| Chaves removidas |O número de itens removidos do cache durante o intervalo de relatório especificado devido ao limite de `maxmemory` . Esse número é mapeado para `evicted_keys` do comando INFO do Redis. |
| Chaves expiradas |O número de itens expirados do cache durante o intervalo de relatório especificado. Esse valor é mapeado para `expired_keys` do comando INFO do Redis. |
| Total de chaves  | O número máximo de chaves no cache durante o período de relatório anterior. Esse número é mapeado para `keyspace` do comando INFO do Redis. Devido a uma limitação do sistema subjacente de métricas, para os caches com clustering habilitado, o Total de Chaves retorna o número máximo de chaves do fragmento que tinha o número máximo de chaves durante o intervalo do relatório.  |
| Gets |O número de operações get do cache durante o intervalo de relatório especificado. Esse valor é a soma dos seguintes valores de informações do comando INFO all do Redis: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit` e `cmdstat_getrange`. Ele é equivalente à soma de acertos e erros de cache durante o intervalo de relatório. |
| Carga do Servidor Redis |O percentual de ciclos em que o servidor Redis está ocupado processando, em vez de ocioso esperando por mensagens. Se esse contador atingir 100, isso indicará que o servidor Redis atingiu um limite de desempenho, e a CPU não pode processar o trabalho mais depressa. Se houver alta Carga do Servidor Redis, haverá exceções de tempo limite no cliente. Nesse caso, considere escalar verticalmente ou particionar seus dados em vários caches. |
| Sets |O número de operações set para o cache durante o intervalo de relatório especificado. Esse valor é a soma dos seguintes valores de informações do comando INFO all do Redis : `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` e `cmdstat_setnx`. |
| Total de Operações |O número total de comandos processados pelo servidor de cache durante o intervalo de relatório especificado. Esse valor é mapeado para `total_commands_processed` do comando INFO do Redis. Observe que, quando o Cache Redis do Azure for usado somente para publicação/assinatura, não haverá métricas para `Cache Hits`, `Cache Misses`, `Gets` ou `Sets`, mas haverá métricas de `Total Operations` que refletem o uso do cache para operações de publicação/assinatura. |
| Memória Usada |A quantidade de memória de cache usada para os pares de chave/valor no cache, em MB, durante o intervalo de relatório especificado. Esse valor é mapeado para `used_memory` do comando INFO do Redis. Isso não inclui metadados ou fragmentação. |
| Memória RSS Usada |A quantidade de memória de cache usada, em MB, durante o intervalo de relatório especificado, incluindo fragmentação e metadados. Esse valor é mapeado para `used_memory_rss` do comando INFO do Redis. |
| CPU |A utilização da CPU do servidor do Cache Redis do Azure como um percentual durante o intervalo de relatório especificado. Esse valor é mapeado para o contador de desempenho `\Processor(_Total)\% Processor Time` do sistema operacional. |
| Cache Lido |A quantidade de dados lidos do cache, em MB/s, durante o intervalo de relatório especificado. Esse valor é derivado das placas de adaptador de rede que dão suporte à máquina virtual que hospeda o cache e não é específico do Redis. **Esse valor corresponde à largura de banda da rede usada por esse cache. Se você deseja configurar alertas para limites de largura de banda de rede no servidor, crie-os usando o contador `Cache Read`. Confira [esta tabela](cache-faq.md#cache-performance) para ver os limites de largura de banda observados para vários tamanhos e tipos de preço de cache.** |
| Gravação no Cache |A quantidade de dados gravados no cache, em MB/s, durante o intervalo de relatório especificado. Esse valor é derivado das placas de adaptador de rede que dão suporte à máquina virtual que hospeda o cache e não é específico do Redis. Esse valor corresponde à largura de banda de rede de dados enviados para o cache do cliente. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Alertas
É possível configurar para receber alertas com base em métricas e logs de atividades. O Azure Monitor permite configurar um alerta para que ele faça o seguinte quando for acionado:

* Enviar uma notificação por email
* Chamar um webhook
* Invocar um aplicativo lógico do Azure

Para configurar regras de Alerta para seu cache, clique em **Regras de alerta** no **menu Recursos**.

![Monitoramento](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Para saber mais sobre como configurar e usar Alertas, consulte [Visão geral dos alertas](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Logs de atividade
Os logs de atividades fornecem informações sobre as operações realizadas em suas instâncias do Cache Redis do Azure. Anteriormente eles eram conhecidos como "logs de auditoria" ou "logs operacionais". Usando logs de atividades, é possível determinar “o que, quem e quando” para quaisquer operações de gravação (PUT, POST, DELETE) realizadas em suas instâncias do Cache Redis do Azure. 

> [!NOTE]
> Os logs de atividade não incluem operações de leitura (GET).
>
>

Para exibir logs de atividade do seu cache, clique em **Logs de atividade** no **menu Recursos**.

Para saber mais sobre como Logs de atividade, consulte [Visão geral dos logs de atividade do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











