---
title: "aaaAzure nível de monitoramento do serviço do Fabric plataforma | Microsoft Docs"
description: "Saiba mais sobre os eventos de nível de plataforma e logs usados toomonitor e diagnosticar os clusters de malha do serviço do Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>Geração de eventos e logs no nível de plataforma

## <a name="monitoring-hello-cluster"></a>Monitoramento de cluster Olá

É importante toomonitor em toodetermine de nível de plataforma do hello o hardware e o cluster ou não estão funcionando conforme o esperado. Embora o Service Fabric pode manter os aplicativos em execução durante uma falha de hardware, mas você ainda precisa toodiagnose se o erro está ocorrendo em um aplicativo ou em infraestrutura subjacente hello. Você também deve monitorar seu plano de toobetter clusters para capacidade, ajudando a decisões sobre a adição ou remoção de hardware.

Serviço de malha fornece cinco log diferentes canais-de-prontos que geram Olá eventos a seguir:

* Canal operacional: operações de alto nível executadas pelo serviço de malha e cluster hello, incluindo eventos de um nó chegando, um novo aplicativo que está sendo implantado, ou um SF atualizar reversão, etc.
* Canal operacional – detalhado: relatórios de integridade e decisões de balanceamento de carga
* Canal de dados & Messaging: críticos logs e eventos gerados em nosso sistema de mensagens (atualmente apenas Olá ReverseProxy) e o caminho de dados (modelos de serviços confiáveis)
* Canal de dados e mensagens - detalhada: canal detalhado que contém todos os logs de saudação não críticos dos dados e de mensagens no cluster hello (esse canal tem um volume muito alto de eventos)   
* [Eventos do Reliable Services](service-fabric-reliable-services-diagnostics.md): eventos específicos do modelo de programação
* [Eventos do Reliable Actors](service-fabric-reliable-actors-diagnostics.md): contadores de desempenho e eventos específicos do modelo de programação
* Suporte a logs: logs de sistema gerados pelo Service Fabric toobe somente usado por nós ao fornecer suporte

Esses canais abrangem a maior parte do log de nível de plataforma Olá recomendado. nível de plataforma tooimprove log, pense em investir em melhor compreensão Olá modelo de integridade e adicionando relatórios de integridade personalizado e adicionando personalizado **contadores de desempenho** toobuild afetar uma compreensão em tempo real de saudação do seus serviços e aplicativos em cluster hello.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Relatórios de carga e integridade do Azure Service Fabric

O Service Fabric tem seu próprio modelo de integridade que é descrito em detalhes nestes artigos:
- [Monitoramento da integridade de malha do tooService de Introdução](service-fabric-health-introduction.md)
- [Relatar e verificar a integridade de serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Adicionar relatórios de integridade personalizados do Service Fabric](service-fabric-report-health.md)
- [Como exibir relatórios de integridade do Service Fabric](service-fabric-view-entities-aggregated-health.md)

Monitoramento de integridade é crítico toomultiple aspectos de operação de um serviço. Monitoramento de integridade é especialmente importante quando o Service Fabric executa uma atualização do aplicativo nomeado. Depois de cada domínio de atualização do serviço de saudação é atualizado e disponível tooyour clientes, o domínio de atualização de saudação deve passar verificações de integridade antes da implantação Olá move toohello próximo domínio de atualização. Se o status bom estado de integridade não pode ser feito, implantação de saudação será revertida, para que o aplicativo hello está em um estado bom conhecido. Embora alguns clientes podem ser afetados antes de serviços hello serão revertidos, a maioria dos clientes não apresentar um problema. Além disso, uma resolução ocorre relativamente rapidamente e sem a necessidade de toowait para a ação de um operador humano. Olá mais verificações de integridade que são incorporadas no seu código, hello mais resiliente do que seu serviço é toodeployment problemas.

Outro aspecto da integridade do serviço está relatando métricas do serviço de saudação. Métricas são importantes na malha do serviço, porque eles são usados toobalance o uso de recursos. As métricas também podem ser um indicador de integridade do sistema. Por exemplo, você pode ter um aplicativo que tenha muitos serviços, e cada instância informa uma métrica RPS (solicitações por segundo). Se um serviço estiver usando mais recursos do que outro serviço, o Service Fabric move instâncias de serviço em torno de cluster hello, utilização de recursos uniforme toomaintain tootry. Para obter uma explicação mais detalhada de como funciona a utilização de recursos, consulte [gerenciar o consumo de recursos e carga na Service Fabric com métricas](service-fabric-cluster-resource-manager-metrics.md).

Métricas também podem ajudar a fornecer informações sobre o desempenho do seu serviço. Ao longo do tempo, você pode usar toocheck de métricas que Olá serviço está operando dentro dos parâmetros esperados. Por exemplo, se as tendências mostram que às 9: 00 em Olá segunda-feira de manhã médio RPS é 1.000, você pode configurar um relatório de integridade que o alerta se hello RPS estiver abaixo de 500 ou acima 1.500. Tudo o que pode ser perfeitamente normal, mas vale um toobe aparência-se de que seus clientes tenham uma ótima experiência. O serviço pode definir um conjunto de métricas que podem ser relatadas para fins de verificação de integridade, mas que não afetam a saudação balanceamento de recursos de cluster de saudação. toodo, toozero de peso da métrica de saudação de conjunto. É recomendável que você comece todas as métricas com um peso de zero e não aumente peso Olá até ter certeza de que entendeu como peso métricas Olá afeta os recursos para o cluster de balanceamento.

> [!TIP]
> Não use um número excessivo de métricas ponderadas. Pode ser difícil toounderstand por que instâncias de serviço estão sendo movidas em torno de balanceamento. Algumas métricas podem ir muito longe!

Todas as informações que podem indicar Olá integridade e o desempenho de seu aplicativo são um candidato para relatórios de integridade e métricas. Um contador de desempenho de CPU pode dizer como seu nó é utilizado, mas não diz se um serviço em particular está íntegro ou não, porque vários serviços podem estar em execução em um único nó. Mas, métricas como RPS, itens processados, e todos os de latência de solicitações pode indicar integridade Olá de um serviço específico.

tooreport integridade, use código semelhante toothis:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport uma métrica, use toothis semelhante de código:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Logs de suporte do Service Fabric

Se você precisar toocontact o suporte da Microsoft para obter ajuda com o cluster do Azure Service Fabric, logs de suporte são quase sempre necessárias. Se o cluster está hospedado no Azure, os logs de suporte são automaticamente configurados e coletados como parte da criação de um cluster. Olá logs são armazenados em uma conta de armazenamento dedicado no grupo de recursos do cluster. conta de armazenamento Olá não tem um nome fixo, mas na conta hello, você vê os contêineres de blob e tabelas com nomes que começam com *malha*. Para obter informações sobre como configurar coleções de log para um cluster autônomo, consulte [criar e gerenciar um cluster de Service Fabric Azure autônomo](service-fabric-cluster-creation-for-windows-server.md) e [definições de configuração para um cluster do Windows autônoma](service-fabric-cluster-manifest.md). Para instâncias do Service Fabric autônomo, hello logs devem ser enviados tooa compartilhamento de arquivo local. Você está **necessária** toohave esses logs para suporte, mas eles não são toobe pretendido utilizável por qualquer pessoa fora da equipe de suporte de cliente do Microsoft hello.

## <a name="enabling-diagnostics-for-a-cluster"></a>Habilitar o diagnóstico para um cluster

Em ordem tootake aproveitar esses logs, é altamente recomendável que, durante a criação do cluster, "diagnóstico" está habilitado. Ativando o diagnóstico, quando Olá cluster for implantado, diagnóstico do Windows Azure é capaz de tooacknowledge Olá operacional, serviços confiáveis e atores confiável canais e armazenar dados de saudação como explicado mais [agregar eventos com Diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md).

Como mostrado acima, há também um campo opcional de tooadd uma chave de instrumentação do Application Insights (AI). Se você escolher toouse AI para qualquer análise de eventos (Leia mais sobre isso em [análise de eventos com o Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)), incluem hello AppInsights recurso instrumentationKey (GUID) aqui.


Se você for toodeploy cluster de tooyour de contêineres, habilite WAD toopick backup estatísticas de docker adicionando este tooyour "WadCfg > DiagnosticMonitorConfiguration":

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Medir o desempenho

Medir o desempenho do cluster ajuda você a entender como ele é toohandle capaz de carga e unidade decisões relacionadas ao dimensionamento do cluster (ver mais informações sobre dimensionamento de um cluster [no Azure](service-fabric-cluster-scale-up-down.md), ou [local](service-fabric-cluster-windows-server-add-remove-nodes.md)). Dados de desempenho também são útil quando comparados tooactions você ou seus aplicativos e serviços podem ter obtido ao analisando os logs em hello futuras. 

Para obter uma lista de toocollect de contadores de desempenho ao usar o serviço de malha, consulte [contadores de desempenho do Service Fabric](service-fabric-diagnostics-event-generation-perf.md)

Aqui estão duas maneiras com as quais você pode configurar a coleta de dados de desempenho para o cluster:

* Usando um agente: essa é a forma preferencial de saudação de coleta de desempenho de um computador, como agentes geralmente têm uma lista de métricas de desempenho possíveis que podem ser coletadas e é uma métrica do processo relativamente fácil toochoose Olá desejado toocollect ou alterá-los . Leia sobre [como tooconfigure Olá OMS para Service Fabric](service-fabric-diagnostics-event-analysis-oms.md) e [Configurando Olá agente do OMS Windows](../log-analytics/log-analytics-windows-agents.md) artigos toolearn mais sobre o agente do OMS hello, que é um esse agente de monitoramento que é capaz de toopick backup dados de desempenho para VMs do cluster e contêineres implantados.

* Configurando o diagnóstico toowrite desempenho contadores tabela tooa: clusters no Azure, isso significa alterar Olá toopick de configuração de diagnóstico do Azure backup contadores de desempenho apropriadas de saudação do hello VMs no cluster e habilitá-la toopick backup Se você estiver implantando recipientes de estatísticas do docker. Leia sobre como configurar [contadores de desempenho em WAD](service-fabric-diagnostics-event-aggregation-wad.md) no Service Fabric tooset a coleta de contador de desempenho.

## <a name="next-steps"></a>Próximas etapas

Seus logs e eventos necessário toobe agregado para que eles possam ser enviados tooany plataforma de análise. Leia sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter entender alguns dos Olá opções recomendada.
