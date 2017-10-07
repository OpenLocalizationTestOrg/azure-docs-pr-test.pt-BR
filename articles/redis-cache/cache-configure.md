---
title: aaaHow tooconfigure Cache Redis do Azure | Microsoft Docs
description: "Entender a configuração de Redis saudação padrão para o Cache Redis do Azure e aprenda como tooconfigure do Azure Redis Cache instâncias"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>Como tooconfigure Cache Redis do Azure
Este tópico descreve como tooreview e atualização Olá configuração para suas instâncias de Cache Redis do Azure e configuração do servidor abrange saudação padrão Redis para instâncias de Cache Redis do Azure.

> [!NOTE]
> Para obter mais informações sobre como configurar e usar os recursos de cache premium, consulte [como persistência tooconfigure](cache-how-to-premium-persistence.md), [como tooconfigure clustering](cache-how-to-premium-clustering.md), e [como o suporte a tooconfigure rede Virtual ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Definir configurações de cache Redis
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Configurações de Cache Redis do Azure são exibidas e configuradas em Olá **Cache Redis** folha usando Olá **Menu recursos**.

![Configurações de Cache Redis](./media/cache-configure/redis-cache-settings.png)

Você pode exibir e configurar Olá seguindo as configurações usando Olá **Menu recursos**.

* [Visão geral](#overview)
* [Log de atividade](#activity-log)
* [Controle de acesso (IAM)](#access-control-iam)
* [Marcas](#tags)
* [Diagnosticar e resolver problemas](#diagnose-and-solve-problems)
* [Configurações](#settings)
    * [Chaves de acesso](#access-keys)
    * [Configurações avançadas](#advanced-settings)
    * [Supervisor do Cache Redis](#redis-cache-advisor)
    * [Escala](#scale)
    * [Tamanho do cluster Redis](#cluster-size)
    * [Persistência de dados do Redis](#redis-data-persistence)
    * [Agendar atualizações](#schedule-updates)
    * [Replicação geográfica](#geo-replication)
    * [Rede Virtual](#virtual-network)
    * [Firewall](#firewall)
    * [Propriedades](#properties)
    * [Bloqueios](#locks)
    * [Script de automação](#automation-script)
* [Administração](#administration)
    * [Importar dados](#importexport)
    * [Exportar Dados](#importexport)
    * [Reboot](#reboot)
* [Monitoramento](#monitoring)
    * [Métricas do Redis](#redis-metrics)
    * [Regras de alerta](#alert-rules)
    * [Diagnostics](#diagnostics)
* [Configurações de suporte e solução de problemas](#support-amp-troubleshooting-settings)
    * [Integridade de recursos](#resource-health)
    * [Nova solicitação de suporte](#new-support-request)


## <a name="overview"></a>Visão geral

**A visão geral** fornece informações básicas sobre o cache como: nome, portas, tipo de preço e métricas de cache selecionadas.

### <a name="activity-log"></a>Log de atividades

Clique em **log de atividades** tooview ações executadas em seu cache. Você também pode usar filtragem tooexpand tooinclude essa exibição outros recursos. Para obter mais informações sobre como trabalhar com logs de auditoria, confira [Operações de auditoria com o Resource Manager](../azure-resource-manager/resource-group-audit.md). Para saber mais sobre como monitorar eventos do Cache Redis do Azure, confira [Operações e alertas](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Controle de acesso (IAM)

Olá **(IAM) do controle de acesso** seção fornece suporte para controle de acesso baseado em função (RBAC) em Olá toohelp portal do Azure organizações atender seus requisitos de gerenciamento de acesso simples e precisa. Para obter mais informações, consulte [controle de acesso baseado em função no portal do Azure de saudação](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Marcas

Olá **marcas** seção ajuda você a organizar os recursos. Para obter mais informações, consulte [usando marcas tooorganize seus recursos do Azure](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Diagnosticar e resolver problemas

Clique em **diagnosticar e resolver problemas** toobe fornecido com problemas comuns e estratégias para resolvê-los.



## <a name="settings"></a>Configurações
Olá **configurações** seção permite que você tooaccess e configurar Olá seguindo as configurações para seu cache.

* [Chaves de acesso](#access-keys)
* [Configurações avançadas](#advanced-settings)
* [Supervisor do Cache Redis](#redis-cache-advisor)
* [Escala](#scale)
* [Tamanho do cluster Redis](#cluster-size)
* [Persistência de dados do Redis](#redis-data-persistence)
* [Agendar atualizações](#schedule-updates)
* [Replicação geográfica](#geo-replication)
* [Rede Virtual](#virtual-network)
* [Firewall](#firewall)
* [Propriedades](#properties)
* [Bloqueios](#locks)
* [Script de automação](#automation-script)



### <a name="access-keys"></a>Chaves de acesso
Clique em **chaves de acesso** chaves de acesso de saudação tooview ou gere novamente para seu cache. Essas chaves são usadas pelos clientes Olá tooyour cache de conexão.

![Chaves de acesso de Cache Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Configurações avançadas
Olá configurações a seguir são configuradas no hello **configurações avançadas** folha.

* [Portas de acesso](#access-ports)
* [Políticas de memória](#memory-policies)
* [Notificações de Keyspace (configurações avançadas)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Portas de acesso
Por padrão, o acesso não SSL está desabilitado para novos caches. tooenable Olá não SSL da porta, clique em **não** para **permitir acesso somente via SSL** em Olá **configurações avançadas** folha e depois clique em **salvar**.

![Portas de acesso de Cache Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Políticas de memória
Olá **política Maxmemory**, **reservado maxmemory**, e **reservado maxfragmentationmemory** configurações Olá **configuraçõesavançadas**folha configurar políticas de saudação de memória para cache de saudação.

![Política Maxmemory de Cache Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Política MaxMemory** configura a política de remoção de saudação de cache hello e permite que você toochoose de saudação políticas de remoção a seguir:

* `volatile-lru`-Este é o padrão de saudação.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Para saber mais sobre políticas `maxmemory`, consulte [Políticas de remoção](http://redis.io/topics/lru-cache#eviction-policies).

Olá **reservado maxmemory** configuração define a quantidade de saudação de memória em MB é reservado para operações de cache não como replicação durante o failover. Definir esse valor permite que você toohave uma experiência mais consistente do servidor Redis quando sua carga varia. Esse valor deve ser definido como maior para cargas de trabalho que executam muitas operações de gravação. Quando a memória é reservada para essas operações, ela não fica disponível para o armazenamento de dados armazenados em cache.

Olá **reservado maxfragmentationmemory** configuração define a quantidade de saudação de memória em MB é reservado tooaccommodate de fragmentação de memória. Definir esse valor permite que você toohave uma experiência mais consistente do servidor Redis quando Olá cache estiver cheio ou fechar taxa de fragmentação toofull e hello também é alta. Quando a memória é reservada para essas operações, ela não fica disponível para o armazenamento de dados armazenados em cache.

Uma coisa tooconsider ao escolher um novo valor de reserva de memória (**reservado maxmemory** ou **reservado maxfragmentationmemory**) é como essa alteração pode afetar um cache que já está em execução com grandes quantidades de dados. Por exemplo, se você tem um cache 53 GB com 49 GB de dados e alterar Olá reserva valor too8 GB, isso removerá Olá max a memória disponível para o sistema Olá too45 GB. Se seu atual `used_memory` ou `used_memory_rss` valores são maiores que o novo limite Olá de 45 GB, em seguida, sistema Olá terá tooevict dados até que as `used_memory` e `used_memory_rss` estão abaixo 45 GB. A remoção pode aumentar a fragmentação de memória e carregamento do servidor. Para obter mais informações sobre métricas do cache, como `used_memory` e `used_memory_rss`, consulte [Métricas disponíveis e intervalos de relatórios](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Olá **reservado maxmemory** e **reservado maxfragmentationmemory** configurações só estão disponíveis para Standard e Premium armazena em cache.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Notificações de Keyspace (configurações avançadas)
Redis keyspace as notificações são configuradas no hello **configurações avançadas** folha. Notificações Keyspace permitem que os clientes tooreceive notificações quando ocorrem determinados eventos.

![Configurações avançadas de Cache Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Keyspace notificações e hello **eventos notificar de keyspace** configuração só estão disponíveis para os caches Standard e Premium.
> 
> 

Para obter mais informações, veja [Notificações de Keyspace do Redis](http://redis.io/topics/notifications). Para exemplo de código, consulte Olá [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) arquivo hello [Olá, mundo](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemplo.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Supervisor do Cache Redis
Olá **Redis Cache Advisor** folha exibe recomendações para seu cache. Durante as operações normais, nenhuma recomendação é exibida. 

![Recomendações](./media/cache-configure/redis-cache-no-recommendations.png)

Se qualquer condição ocorrer durante as operações de saudação do cache como alto uso da memória, largura de banda de rede ou de carga do servidor, um alerta é exibido na Olá **Redis Cache** folha.

![Recomendações](./media/cache-configure/redis-cache-recommendations-alert.png)

Informações adicionais podem ser encontradas em Olá **recomendações** folha.

![Recomendações](./media/cache-configure/redis-cache-recommendations.png)

Você pode monitorar essas métricas em Olá [gráficos de monitoramento](cache-how-to-monitor.md#monitoring-charts) e [gráficos de uso](cache-how-to-monitor.md#usage-charts) seções de saudação **Redis Cache** folha.

Cada tipo de preço tem limites diferentes para conexões de cliente, memória e largura de banda. Se o cache se aproximar da capacidade máxima para essas métricas durante um período prolongado, uma recomendação será criada. Para obter mais informações sobre métricas hello e limites de revisores Olá **recomendações** ferramenta, consulte Olá a tabela a seguir:

| Métrica do Cache Redis | Mais informações |
| --- | --- |
| Uso de largura de banda de rede |[Desempenho do cache - largura de banda disponível](cache-faq.md#cache-performance) |
| Clientes conectados |[Configuração padrão do servidor Redis - maxclients](#maxclients) |
| Carga do servidor |[Gráficos de uso - carga do servidor Redis](cache-how-to-monitor.md#usage-charts) |
| Uso de memória |[Desempenho do cache - tamanho](cache-faq.md#cache-performance) |

tooupgrade seu cache, clique em **atualizar agora** toochange Olá preço e [escala](#scale) seu cache. Para obter mais informações sobre como escolher um tipo de preço, confira [Qual oferta e tamanho de Cache Redis devo usar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Escala
Clique em **escala** Olá tooview ou alteração de preços para seu cache. Para obter mais informações sobre dimensionamento, consulte [como tooScale Cache Redis do Azure](cache-how-to-scale.md).

![Tipo de preço do Cache Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Tamanho do cluster Redis
Clique em **tamanho de Cluster Redis (visualização)** o cache de tamanho do cluster Olá toochange para um premium em execução com cluster habilitado.

> [!NOTE]
> Observe que, enquanto hello Azure Redis Cache Premium camada foi liberado tooGeneral disponibilidade, o recurso de tamanho de Cluster Redis hello está atualmente em visualização.
> 
> 

![Tamanho do cluster Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

tamanho do cluster Olá toochange, use o controle deslizante de saudação ou digite um número entre 1 e 10 Olá **contagem de fragmento** caixa de texto e clique em **Okey** toosave.

> [!IMPORTANT]
> O clustering está disponível apenas para os Caches premium. Para obter mais informações, consulte [como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Persistência de dados do Redis
Clique em **Redis a persistência de dados** tooenable, desabilitar ou configurar persistência de dados para seu cache premium. O Cache Redis do Microsoft Azure oferece persistência Redis usando [persistência RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) ou [persistência AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).

Para obter mais informações, consulte [como tooconfigure persistência para um Premium do Azure Redis Cache](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> A persistência de dados do Redis só está disponível para os caches Premium. 
> 
> 

### <a name="schedule-updates"></a>Agende atualizações
Olá **agendar atualizações** folha permite que você toodesignate uma janela de manutenção para atualizações de servidor Redis para seu cache. 

> [!IMPORTANT]
> janela de manutenção de saudação se aplica apenas atualizações de servidor tooRedis e não tooany Azure atualiza ou atualiza o sistema operacional de toohello de saudação VMs que hospedam o cache de saudação.
> 
> 

![Agende atualizações](./media/cache-configure/redis-schedule-updates.png)

toospecify uma janela de manutenção, verifique dias Olá desejado e especifique a hora de início de janela de manutenção de saudação para cada dia e clique em **Okey**. Observe que o tempo de janela de manutenção de saudação é em UTC. 

> [!IMPORTANT]
> Olá **agendar atualizações** funcionalidade está disponível somente para os caches da camada Premium. Para saber mais e instruções, confira [Como administrar o Cache Redis do Azure – Agendar atualizações](cache-administration.md#schedule-updates).
> 
> 

### <a name="geo-replication"></a>Replicação geográfica

Olá **georeplicação** folha fornece um mecanismo para vincular as duas instâncias de Cache Redis do Azure da camada Premium. Um cache é designado como o cache de vinculado primário hello e hello como cache de vinculado secundário hello. cache de vinculado secundário Olá se torna somente leitura e dados cache primário toohello escrito é replicada toohello cache secundário de vinculado. Essa funcionalidade pode ser usado tooreplicate um cache em regiões do Azure.

> [!IMPORTANT]
> A **replicação geográfica** está disponível somente para caches de camada Premium. Para obter mais informações e instruções, consulte [como tooconfigure replicação geográfica para Cache Redis do Azure](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Rede Virtual
Olá **rede Virtual** seção permite que as configurações de rede virtual de saudação tooconfigure para seu cache. Para obter informações sobre como criar um cache premium com uma rede virtual suporte e atualizar suas configurações, consulte [como tooconfigure dar suporte a rede Virtual para um Premium do Azure Redis Cache](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> As configurações de rede virtual só estão disponíveis para os caches premium configurados com suporte para rede virtual durante a criação do cache. 
> 
> 

### <a name="firewall"></a>Firewall

Clique em **Firewall** tooview e configure as regras de firewall para o Cache Redis do Premium do Azure.

![Firewall](./media/cache-configure/redis-firewall-rules.png)

É possível especificar regras de firewall com um intervalo de endereços IP inicial e final. Quando as regras de firewall estão configuradas, apenas as conexões de cliente de saudação especificado intervalos de endereços IP podem se conectar a toohello cache. Quando uma regra de firewall é salvo há um pequeno atraso antes de regra de saudação é eficaz. Normalmente, esse atraso é inferior a um minuto.

> [!IMPORTANT]
> Conexões dos sistemas de monitoramento do Cache Redis do Azure serão sempre permitidas, mesmo se regras de firewall forem configuradas.
> 
> As regras de firewall estão disponíveis apenas para os caches da camada Premium.
> 
> 

### <a name="properties"></a>Propriedades
Clique em **propriedades** tooview informações sobre seu cache, incluindo o ponto de extremidade de cache hello e portas.

![Propriedades de Cache Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Bloqueios
Olá **bloqueia** seção permite que você toolock uma assinatura, o grupo de recursos ou o recurso tooprevent outros usuários na sua organização do acidentalmente excluir ou modificar recursos críticos. Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Script de automação

Clique em **script de automação** toobuild e exportar um modelo de seus recursos implantados para implantações futuras. Para saber mais sobre como trabalhar com modelos, confira [Implantar recursos com modelos do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Configurações de administração
Olá configurações Olá **administração** seção permitir Olá tooperform tarefas administrativas para o cache a seguir. 

![Administração](./media/cache-configure/redis-cache-administration.png)

* [Importar dados](#importexport)
* [Exportar Dados](#importexport)
* [Reboot](#reboot)


### <a name="importexport"></a>Importar/exportar
Importação/exportação é uma operação de gerenciamento de dados do Cache Redis do Azure, que permite que você tooimport e exportar dados em cache Olá importando e exportando um instantâneo de banco de dados de Cache Redis (RDB) de um blob de páginas de tooa de cache premium em uma conta de armazenamento do Azure. Importação/exportação permite toomigrate entre instâncias diferentes do Cache Redis do Azure ou popular Olá cache com os dados antes do uso.

Importação pode ser usado toobring Redis compatível RDB arquivos de qualquer servidor Redis em execução em qualquer nuvem ou o ambiente, incluindo o Redis em execução no Linux, Windows ou em qualquer provedor de nuvem como Amazon Web Services e outros. Importação de dados é uma maneira fácil de toocreate um cache com dados preenchidos previamente. Durante o processo de importação Olá, Cache Redis do Azure carrega arquivos RDB saudação do armazenamento do Azure na memória e insere chaves Olá cache hello.

Exportação permite que dados de saudação tooexport armazenados em Cache Redis do Azure tooRedis compatível RDB arquivos. Você pode usar esses dados de toomove do recurso de um Cache Redis do Azure instância tooanother ou servidor do Redis tooanother. Durante o processo de exportação hello, um arquivo temporário é criado no hello VM que hospeda Olá instância de servidor de Cache Redis do Azure e arquivo hello é carregado toohello designado a conta de armazenamento. Quando a operação de exportação Olá for concluído com o status de êxito ou falha, o arquivo temporário de saudação é excluído.

> [!IMPORTANT]
> A opção Importar/Exportar está disponível somente para caches do nível Premium. Para saber mais e instruções, confira [Importar e exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Reboot
Olá **reinicializar** folha permite tooreboot nós de saudação do cache. Esse recurso de reinicialização permite que você tootest seu aplicativo para garantir a resiliência se houver uma falha de um nó de cache.

![Reboot](./media/cache-configure/redis-cache-reboot.png)

Se você tiver um cache premium com cluster habilitado, você pode selecionar quais fragmentos de saudação tooreboot de cache.

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot um ou mais nós de seu cache, selecione nós de saudação desejado e clique em **reinicializar**. Se você tiver um cache premium com cluster habilitado, selecione Olá shard(s) tooreboot e, em seguida, clique em **reinicializar**. Depois de alguns minutos, Olá reinicialização do nó (s) selecionado e estiverem online novamente depois de alguns minutos.

> [!IMPORTANT]
> A reinicialização agora está disponível para todos os tipos de preço. Para saber mais e instruções, confira [Como administrar o Cache Redis do Azure – Reinicializar](cache-administration.md#reboot).
> 
> 


## <a name="monitoring"></a>Monitoramento

Olá **monitoramento** seção permite que você tooconfigure diagnóstico e monitoramento para seu Cache Redis. Para obter mais informações sobre diagnóstico e monitoramento do Cache Redis do Azure, consulte [como toomonitor Cache Redis do Azure](cache-how-to-monitor.md).

![Diagnostics](./media/cache-configure/redis-cache-diagnostics.png)

* [Métricas do Redis](#redis-metrics)
* [Regras de alerta](#alert-rules)
* [Diagnostics](#diagnostics)

### <a name="redis-metrics"></a>Métricas do Redis
Clique em **Redis métricas** muito[exibir métricas](cache-how-to-monitor.md#view-cache-metrics) para seu cache.

### <a name="alert-rules"></a>Regras de alerta

Clique em **regras de alerta** tooconfigure alertas com base nas métricas de Cache Redis. Para obter mais informações, consulte [Alertas](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Diagnostics

Por padrão, as métricas de cache no Azure Monitor são [armazenadas durante 30 dias](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e, em seguida, excluídas. toopersist suas métricas de cache por mais de 30 dias, clique **diagnóstico** muito[configurar conta de armazenamento Olá](cache-how-to-monitor.md#export-cache-metrics) usado toostore diagnósticos de cache.

>[!NOTE]
>Em adição tooarchiving seu toostorage de métricas de cache, você também pode [transmiti-los tooan hub de eventos ou enviá-los tooLog análise](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Configurações de suporte e solução de problemas
Olá configurações Olá **suporte + solução de problemas** seção fornecerá opções para resolver problemas com seu cache.

![Suporte + solução de problemas](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Integridade de recursos](#resource-health)
* [Nova solicitação de suporte](#new-support-request)

### <a name="resource-health"></a>Integridade de recursos
**Resource Health** observa seu recurso e informa se ele está sendo executado conforme o esperado. Para obter mais informações sobre Olá serviço de integridade de recursos do Azure, consulte [visão geral da integridade do recurso Azure](../resource-health/resource-health-overview.md).

> [!NOTE]
> Integridade do recurso é atualmente não é possível tooreport na integridade de saudação de instâncias de Cache Redis do Azure hospedado em uma rede virtual. Para saber mais, confira [Todos os recursos de cache funcionam ao hospedar um cache em uma rede virtual?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>Nova solicitação de suporte
Clique em **nova solicitação de suporte** tooopen uma solicitação de suporte para seu cache.





## <a name="default-redis-server-configuration"></a>Configuração padrão do servidor Redis
Novo Cache Redis do Azure são configuradas com hello valores de configuração de Redis a seguir.

> [!NOTE]
> configurações de saudação nesta seção não podem ser alteradas usando Olá `StackExchange.Redis.IServer.ConfigSet` método. Se esse método for chamado com um dos comandos de saudação nesta seção, é gerada uma exceção semelhante toohello a seguir:  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Quaisquer valores que podem ser configuradas como **máxima de memória de política**, podem ser configuradas por meio de saudação portal do Azure ou ferramentas de gerenciamento de linha de comando como CLI do Azure ou o PowerShell.
> 
> 

| Configuração | Valor padrão | Descrição |
| --- | --- | --- |
| `databases` |16 |número de bancos de dados padrão de saudação é 16, mas você pode configurar uma saudação de com base no número diferente de preço. <sup>1</sup> o banco de dados do saudação padrão é o DB 0, você pode selecionar um diferente em uma base por conexão que usa `connection.GetDatabase(dbid)` onde `dbid` é um número entre `0` e `databases - 1`. |
| `maxclients` |Depende de saudação preço<sup>2</sup> |Isso é que o número máximo de saudação de clientes conectados é permitida Olá mesmo tempo. Quando Olá limite é atingido o Redis fecha todas as conexões novas hello, retornando um erro de 'número máximo de clientes atingido'. |
| `maxmemory-policy` |`volatile-lru` |Política MaxMemory é a configuração de saudação para como o Redis seleciona qual tooremove quando `maxmemory` (Olá o tamanho do cache Olá oferta selecionado quando você criou o cache de saudação) é atingido. Padrão de saudação do Cache Redis do Azure com a configuração é `volatile-lru`, que remove as chaves de saudação com um vencimento definido usando um algoritmo LRU. Essa configuração pode ser definida em Olá portal do Azure. Para obter mais informações, consulte [Políticas de memória](#memory-policies). |
| `maxmemory-samples` |3 |memória toosave, LRU e algoritmos TTL mínimo são aproximados algoritmos em vez de algoritmos precisos. Por padrão o Redis verificações três chaves e escolhe Olá um usada menos recentemente. |
| `lua-time-limit` |5.000 |Tempo máximo de execução de um script Lua em milissegundos. Se Olá tempo de execução máximo for atingido, o Redis registra que um script ainda está em execução após Olá máximo permitida de tempo e tooreply tooqueries é iniciado com um erro. |
| `lua-event-limit` |500 |O tamanho máximo da fila de eventos de script. |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |Olá limites de buffer de saída do cliente podem ser usado tooforce desconexão de clientes que não estão lendo dados do servidor de saudação rápido o suficiente, por algum motivo (um motivo comum é que um cliente Pub/Sub não consegue consumir mensagens assim que o publicador Olá pode produzi-las). Para obter mais informações, veja [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>limite Olá para `databases` é diferente para cada Cache Redis do Azure, preço e pode ser definido na criação do cache. Se nenhum `databases` configuração é especificada durante a criação do cache, Olá padrão é 16.

* Caches Básico e Standard
  * C0 cache (250 MB) – backup de bancos de dados too16
  * C1 cache (1 GB) - backup too16 bancos de dados
  * C2 cache (2,5 GB) - backup too16 bancos de dados
  * C3 cache (6 GB) - backup too16 bancos de dados
  * C4 cache (13 GB) - backup too32 bancos de dados
  * C5 cache (26 GB) - backup too48 bancos de dados
  * C6 cache (53 GB) - backup too64 bancos de dados
* Caches Premium
  * P1 (6 GB - 60 GB) - backup too16 bancos de dados
  * P2 (13 GB - 130 GB) - backup too32 bancos de dados
  * P3 (26 GB - 260 GB) - backup too48 bancos de dados
  * P4 (53 GB - 530 GB) - backup too64 bancos de dados
  * Todos os caches premium com cluster Redis habilitado - Redis cluster só dá suporte ao uso do banco de dados 0 então Olá `databases` limite para qualquer cache premium com cluster Redis habilitada efetivamente é 1 e hello [selecione](http://redis.io/commands/select) comando não é permitido. Para obter mais informações, consulte [preciso toomake qualquer toouse de aplicativo alterações toomy cliente clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Para saber mais sobre bancos de dados, veja [O que são bancos de dados Redis?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Olá `databases` configuração pode ser configurado somente durante a criação do cache e somente usando o PowerShell, CLI ou outros clientes de gerenciamento. Para obter um exemplo de configuração `databases` durante a criação de cache usando o PowerShell, confira [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a> 
<sup>2</sup>`maxclients` é diferente para cada tipo de preço do Cache Redis do Azure.

* Caches Básico e Standard
  * C0 cache (250 MB) - too256 conexões
  * C1 cache (1 GB) - backup too1, conexões, 000
  * C2 cache (2,5 GB) - backup too2, conexões, 000
  * C3 cache (6 GB) - backup too5, conexões, 000
  * C4 cache (13 GB) - backup too10, conexões, 000
  * C5 cache (26 GB) - backup too15, conexões, 000
  * C6 cache (53 GB) - backup too20, conexões, 000
* Caches Premium
  * P1 (6 GB - 60 GB) - backup too7, conexões de 500
  * P2 (13 GB - 130 GB) - backup too15, 000 conexões
  * P3 (26 GB - 260 GB) - backup too30, 000 conexões
  * P4 (53 GB - 530 GB) - backup too40, 000 conexões

> [!NOTE]
> Embora cada tamanho de cache permite que *até* um determinado número de conexões, tooRedis cada conexão tem sobrecarga associados a ele. Um exemplo de tal sobrecarga seria o uso da CPU e de memória como resultado de criptografia TLS/SSL. limite de conexão máximo Olá para um tamanho de cache determinado pressupõe um cache pouco carregado. Se carregar de sobrecarga de conexão *mais* carga a partir de operações do cliente excede a capacidade de sistema hello, cache Olá pode enfrentar problemas de capacidade, mesmo se você não tiver excedido o limite de conexão de saudação para o tamanho do cache atual hello.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Comandos Redis não têm suporte no Cache Redis do Azure
> [!IMPORTANT]
> Porque a configuração e gerenciamento de instâncias de Cache Redis do Azure é gerenciada pela Microsoft, hello comandos a seguir são desabilitados. Se você tentar tooinvoke-las, você recebe uma mensagem de erro semelhante muito`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * Salvar
> * SHUTDOWN
> * SLAVEOF
> * CLUSTER - Os comandos de gravação do cluster estão desabilitados, mas comandos do Cluster somente leitura são permitidos.
> 
> 

Para saber mais sobre os comandos do Redis, confira [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Console do Redis
Podem emitir comandos de forma segura tooyour instâncias de Cache Redis do Azure usando Olá **Console Redis**, que está disponível no portal do Azure para todas as camadas de cache de saudação.

> [!IMPORTANT]
> - Olá Console Redis não funciona com [VNET](cache-how-to-premium-vnet.md). Quando o cache faz parte de uma rede virtual, somente a clientes em redes de saudação pode acessar o cache de saudação. Como Redis Console é executado no navegador local, que está fora da saudação VNET, ele não pode se conectar tooyour cache.
> - Nem todos os comandos do Redis têm suporte no Cache Redis do Azure. Para obter uma lista de comandos do Redis que estão desabilitados para o Cache Redis do Azure, consulte Olá anterior [Redis comandos não tem suportados no Cache Redis do Azure](#redis-commands-not-supported-in-azure-redis-cache) seção. Para saber mais sobre os comandos do Redis, confira [http://redis.io/commands](http://redis.io/commands).
> 
> 

Olá tooaccess Console Redis, clique em **Console** de saudação **Redis Cache** folha.

![Console do Redis](./media/cache-configure/redis-console-menu.png)

comandos de tooissue em sua instância de cache, simplesmente saudação do tipo desejado comando no console de saudação.

![Console do Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>Usando Olá Console Redis com um premium cache clusterizados

Quando o cache usando Olá Console Redis com um premium em cluster, você pode emitir comandos tooa único fragmento de cache de saudação. tooissue um fragmento específico do tooa de comando, primeiro conecte-se fragmento desejado toohello clicando no selecionador de fragmento de saudação.

![Console do Redis](./media/cache-configure/redis-console-premium-cluster.png)

Se você tenta tooaccess uma chave armazenada em um fragmento diferente de Olá fragmento conectado, você receberá um toohello semelhantes da mensagem de erro seguinte mensagem.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

No exemplo anterior de saudação, o fragmento 1 é fragmento selecionado do hello, mas `myKey` está localizado no fragmento 0, conforme indicado pelo Olá `(shard 0)` parte da mensagem de saudação do erro. Neste exemplo, tooaccess `myKey`, selecione fragmento 0 usando Olá seletor de fragmento e comando de saudação desejado do problema.


## <a name="move-your-cache-tooa-new-subscription"></a>Mover o cache tooa nova assinatura
Você pode mover o cache tooa nova assinatura clicando **mover**.

![Mover o Cache Redis](./media/cache-configure/redis-cache-move.png)

Para obter informações sobre como mover os recursos de um recurso grupo tooanother e de tooanother de uma assinatura, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre como trabalhar com os comandos do Redis, consulte [Como posso executar comandos do Redis?](cache-faq.md#how-can-i-run-redis-commands)

