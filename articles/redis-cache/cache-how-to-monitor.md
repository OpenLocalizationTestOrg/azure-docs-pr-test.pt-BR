---
title: aaaHow toomonitor Cache Redis do Azure | Microsoft Docs
description: "Saiba como toomonitor Olá integridade e desempenho suas instâncias de Cache Redis do Azure"
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
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>Como toomonitor Cache Redis do Azure
Cache Redis do Azure usa [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide várias opções para monitorar suas instâncias de cache. Você pode exibir métricas, fixar gráficos de métricas toohello quadro inicial, personalizar o intervalo de data e hora de saudação de gráficos de monitoramento, adicionar e remover as métricas de gráficos de saudação e definir alertas quando determinadas condições forem atendidas. Essas ferramentas permitem a você toomonitor Olá integridade das instâncias de Cache Redis do Azure e ajudarão-lo a gerenciar seus aplicativos de cache.

Métricas para instâncias de Cache Redis do Azure são coletadas usando Olá Redis [informações](http://redis.io/commands/info) comando aproximadamente duas vezes por minuto e armazenados automaticamente por 30 dias (consulte [exportar métricas de cache](#export-cache-metrics) tooconfigure um política de retenção diferente) para que possam ser exibidos em gráficos de métricas de saudação e avaliadas por regras de alerta. Para obter mais informações sobre valores de informações diferentes Olá usados para cada métrica de cache, consulte [métricas disponíveis e intervalos de emissão de relatórios](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

métricas de cache de tooview [procurar](cache-configure.md#configure-redis-cache-settings) tooyour instância de cache em Olá [portal do Azure](https://portal.azure.com).  Cache Redis do Azure fornece alguns gráficos internos em Olá **visão geral** folha e hello **Redis métricas** folha. Cada gráfico pode ser personalizado adicionando ou removendo métricas e alterando Olá intervalo de relatório.

![Métricas do Redis](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Exibir gráficos de métricas pré-configurados

Olá **visão geral** folha tem Olá pré-configurado gráficos de monitoramento a seguir.

* [Gráficos de monitoramento](#monitoring-charts)
* [Gráficos de uso](#usage-charts)

### <a name="monitoring-charts"></a>Gráficos de monitoramento
Olá **monitoramento** seção Olá **visão geral** folha tem **acertos e erros**, **obtém e define**, **conexões**, e **comandos Total** gráficos.

![Gráficos de monitoramento](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Gráficos de uso
Olá **uso** seção Olá **visão geral** folha tem **de carga do servidor Redis**, **uso de memória**, **largura de banda de rede** , e **uso da CPU** gráficos e também exibe o saudação **preço** da instância de cache de saudação.

![Gráficos de uso](./media/cache-how-to-monitor/redis-cache-usage-part.png)

Olá **preço** exibe Olá cache preços camada e pode ser usada muito[escala](cache-how-to-scale.md) Olá tooa de cache diferente tipos de preço.

## <a name="view-metrics-with-azure-monitor"></a>Ver métricas com o Azure Monitor
tooview Redis métricas e criar gráficos personalizados usando o Monitor do Azure, clique em **métricas** de saudação **menu recursos**e personalizar o gráfico de uso de métricas de saudação desejada, intervalo, o tipo de gráfico de relatório e mais.

![Métricas do Redis](./media/cache-how-to-monitor/redis-cache-monitor.png)

Para saber mais sobre como trabalhar com as métricas usando o Azure Monitor, consulte [Visão geral das métricas no Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Exportar métricas de cache
Por padrão, as métricas de cache no Azure Monitor são [armazenadas durante 30 dias](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e, em seguida, excluídas. toopersist suas métricas de cache por mais de 30 dias, você pode [designar uma conta de armazenamento](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) e especifique um **retenção (dias)** política para suas métricas de cache. 

tooconfigure uma conta de armazenamento para suas métricas de cache:

1. Clique em **diagnóstico** de saudação **menu recursos** em Olá **Redis Cache** folha.
2. Clique em **Ativado**.
3. Verificar **tooa conta de armazenamento de arquivos**.
4. Selecione a conta de armazenamento de saudação em métricas de cache que toostore hello.
5. Verificar Olá **1 minuto** caixa de seleção e especifique um **retenção (dias)** política. Se você não deseja tooapply qualquer política de retenção e reter dados indefinidamente, defina **retenção (dias)** muito**0**.
6. Clique em **Salvar**.

![Diagnóstico do Redis](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>Em adição tooarchiving seu toostorage de métricas de cache, você também pode [transmiti-los tooan hub de eventos ou enviá-los tooLog análise](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

tooaccess suas métricas, você pode exibi-los no hello portal do Azure conforme descrito anteriormente neste artigo e você também pode acessá-los usando Olá [API de REST de métricas de Monitor do Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> Se você alterar contas de armazenamento, dados de saudação na conta de armazenamento de saudação configurada anteriormente permanecem disponíveis para download, mas ele não será exibido no portal do Azure de saudação.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Métricas disponíveis e intervalos de relatórios
As métricas de cache são relatadas usando vários intervalos de relatórios, incluindo **Última hora**, **Hoje**, **Semana passada** e **Personalizado**. Olá **métrica** folha para cada gráfico de métricas exibe valores de média, mínimo e máximo de saudação para cada métrica no gráfico de saudação e algumas métricas exibem um total de saudação intervalo de relatório. 

Cada métrica inclui duas versões. Uma métrica mede o desempenho de todo o cache de saudação e para caches que usam [clustering](cache-how-to-premium-clustering.md), uma segunda versão da métrica de saudação inclui `(Shard 0-9)` em desempenho de medidas de nome Olá para um único fragmento em um cache. Por exemplo, se um cache tem 4 fragmentos, `Cache Hits` Olá a quantidade total de acertos do cache de todo Olá, e `Cache Hits (Shard 3)` é apenas as ocorrências de saudação para esse fragmento do cache de saudação.

> [!NOTE]
> Mesmo quando o cache de saudação está ocioso sem aplicativos de cliente ativo conectado, você poderá ver alguma atividade de cache, como os clientes conectados, uso de memória e operações que está sendo executadas. Esta atividade é normal durante a operação de saudação de uma instância de Cache Redis do Azure.
> 
> 

| Métrica | Descrição |
| --- | --- |
| Acertos do Cache |número de saudação de pesquisas de chave com êxito durante o intervalo de relatório especificado hello. Isso mapeia muito`keyspace_hits` de saudação Redis [informações](http://redis.io/commands/info) comando. |
| Erros de Cache |número de saudação de pesquisas de chave com falha durante o intervalo de relatório especificado hello. Isso mapeia muito`keyspace_misses` de saudação comando Redis INFO. Erros de cache não significa necessariamente que há um problema com o cache de saudação. Por exemplo, ao usar o saudação padrão de programação cache-aside, um aplicativo procura primeiro no cache de saudação para um item. Se hello item não estiver lá (erro de cache), o item Olá é recuperado do banco de dados de saudação e adicionado toohello cache na próxima vez. Erros de cache são o comportamento normal para saudação padrão de programação cache-aside. Se o número de saudação de erros de cache for maior do que o esperado, examine a lógica do aplicativo hello que preenche e leituras do cache de saudação. Se os itens estão sendo removidos do cache de saudação devido a pressão toomemory, em seguida, pode haver alguns erros de cache, mas seria uma toomonitor métrica melhor para pressão de memória `Used Memory` ou `Evicted Keys`. |
| Clientes conectados |número de saudação do cache de toohello de conexões de cliente durante o intervalo de relatório especificado hello. Isso mapeia muito`connected_clients` de saudação comando Redis INFO. Uma vez Olá [limite de conexão](cache-configure.md#default-redis-server-configuration) é atingido tentativas de conexão subsequentes toohello cache falhará. Observe que mesmo se não houver nenhum aplicativo cliente ativo, pode ainda haver algumas instâncias de clientes conectados devido toointernal processos e conexões. |
| Chaves removidas |número de itens removidos do cache de saudação durante a saudação Hello especificado intervalo de relatório devido toohello `maxmemory` limite. Isso mapeia muito`evicted_keys` de saudação comando Redis INFO. |
| Chaves expiradas |número de saudação de itens expirados do cache Olá durante o intervalo de relatório especificado hello. Esse valor é mapeado muito`expired_keys` de saudação comando Redis INFO. |
| Total de chaves  | número máximo de saudação de chaves no cache de saudação durante a saudação após o período de tempo de relatório. Isso mapeia muito`keyspace` de saudação comando Redis INFO. Devido a limitação de tooa de saudação subjacente do sistema de métricas, para caches com clustering habilitada, Total de chaves retorna o número de máximo de saudação das chaves de fragmento de saudação que tinha o número máximo de saudação de chaves durante a saudação intervalo de relatório.  |
| Gets |número de saudação de operações get do cache de saudação durante o intervalo de relatório especificado hello. Esse valor é a soma de saudação do seguinte Olá valores da saudação informações Redis comando todos os: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, e `cmdstat_getrange`, e é equivalente toohello soma de acertos do cache e erros durante a saudação intervalo de relatório. |
| Carga do Servidor Redis |Olá o percentual de ciclos de em qual Olá servidor Redis está ocupado processando e não espera ocioso para mensagens. Se este contador atingir 100 significa servidor do Redis Olá atingiu o limite de desempenho e saudação da CPU não é possível processar funcionam qualquer mais rapidamente. Se você estiver vendo alta carga de servidor Redis, em seguida, você verá exceções de tempo limite no cliente de saudação. Nesse caso, considere escalar verticalmente ou particionar seus dados em vários caches. |
| Sets |número de saudação do cache de toohello de operações de conjunto durante a saudação especificado intervalo de relatório. Esse valor é a soma de saudação do seguinte Olá valores da saudação informações Redis comando todos os: `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` , e `cmdstat_setnx`. |
| Total de Operações |Olá o número total de comandos processados pelo servidor de cache Olá durante a saudação especificado intervalo de relatório. Esse valor é mapeado muito`total_commands_processed` de saudação comando Redis INFO. Observe que quando o Cache Redis do Azure é usada somente para publicação/assinatura não haverá nenhuma métrica para `Cache Hits`, `Cache Misses`, `Gets`, ou `Sets`, mas haverá `Total Operations` métricas que refletem o uso de cache Olá para operações de publicação/assinatura. |
| Memória Usada |quantidade de saudação de memória de cache usada para pares de chave/valor no cache de saudação em MB durante a saudação especificado intervalo de relatório. Esse valor é mapeado muito`used_memory` de saudação comando Redis INFO. Isso não inclui metadados ou fragmentação. |
| Memória RSS Usada |quantidade de saudação de memória de cache usada em MB durante a saudação intervalo de relatório especificado, incluindo a fragmentação e metadados. Esse valor é mapeado muito`used_memory_rss` de saudação comando Redis INFO. |
| CPU |saudação de utilização de CPU do servidor de Cache Redis do Azure hello como uma porcentagem durante a saudação especificado intervalo de relatório. Esse valor é mapeado sistema de operacional toohello `\Processor(_Total)\% Processor Time` contador de desempenho. |
| Cache Lido |Olá dados lidos do cache de saudação em Megabytes por segundo (MB/s) durante a saudação especificado intervalo de relatório. Esse valor é derivado de placas de interface de rede de saudação que dão suporte a saudação VM que hospeda o cache de saudação e é não Redis específico. **Esse valor corresponde a largura de banda de rede de toohello usada por esse cache. Se você quiser tooset alertas para limites de largura de banda de rede de lado do servidor, crie-a usando esta `Cache Read` contador. Consulte [essa tabela](cache-faq.md#cache-performance) para Olá observado limites de largura de banda para o cache de vários tamanhos e as camadas de preços.** |
| Gravação no Cache |Olá a quantidade de dados gravados toohello cache em Megabytes por segundo (MB/s) durante o intervalo de relatório especificado hello. Esse valor é derivado de placas de interface de rede de saudação que dão suporte a saudação VM que hospeda o cache de saudação e é não Redis específico. Esse valor corresponde toohello largura de banda de rede de dados enviados toohello cache do cliente de saudação. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Alertas
Você pode configurar alertas de tooreceive com base nas métricas e registros de atividades. Monitor do Azure permite que você tooconfigure uma saudação de alerta toodo após quando ele dispara:

* Enviar uma notificação por email
* Chamar um webhook
* Invocar um aplicativo lógico do Azure

regras de alerta tooconfigure para seu cache, clique em **regras de alerta** de saudação **menu recursos**.

![Monitoramento](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Para saber mais sobre como configurar e usar Alertas, consulte [Visão geral dos alertas](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Logs de atividade
Logs de atividade fornecem informações sobre operações de saudação que foram executadas em suas instâncias de Cache Redis do Azure. Anteriormente eles eram conhecidos como "logs de auditoria" ou "logs operacionais". Usando logs de atividade, você pode determinar hello ", que e quando" para qualquer gravação as operações executadas em suas instâncias de Cache Redis do Azure (PUT, POST, DELETE). 

> [!NOTE]
> Os logs de atividade não incluem operações de leitura (GET).
>
>

logs de atividade tooview para seu cache, clique em **logs de atividade** de saudação **menu recursos**.

Para obter mais informações sobre logs de atividade, consulte [visão geral da saudação Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











