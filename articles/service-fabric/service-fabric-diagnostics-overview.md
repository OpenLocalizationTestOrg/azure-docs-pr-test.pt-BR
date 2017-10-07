---
title: "aaaAzure visão geral de diagnóstico e monitoramento de malha do serviço | Microsoft Docs"
description: "Saiba mais sobre monitoramento e diagnóstico para clusters, aplicativos e serviços do Service Fabric do Azure."
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Monitoramento e diagnóstico no Azure Service Fabric

Monitoramento e diagnóstico é crítico toodeveloping, teste e implantação de aplicativos e serviços em qualquer ambiente. As soluções do Service Fabric funcionam melhor quando você planeja e implementa o monitoramento e o diagnóstico que ajudam a garantir que aplicativos e serviços funcionem conforme o esperado em um ambiente de desenvolvimento local ou na produção.

Olá principais metas de monitoramento e diagnóstico é para:
* Detectar e diagnosticar problemas de hardware e infraestrutura
* Detectar problemas de software e aplicativos e reduzir o tempo de inatividade do serviço
* Entender o consumo de recursos e ajudar a orientar as decisões de operações
* Otimizar o desempenho de aplicativos, serviços e infraestrutura
* Gerar informações de negócios e identificar áreas de aprimoramento


Olá fluxo geral de monitoramento e diagnóstico consiste em três etapas:

1. **Geração de eventos**: Isso inclui eventos (logs, rastreamentos, eventos personalizados) no nível de aplicativo / serviço, plataforma e infraestrutura de saudação (cluster)
2. **Agregação de eventos**: eventos gerados necessário toobe coletados e agregados antes que possam ser exibidos
3. **Análise**: eventos necessário toobe visualizados e acessíveis em algum formato, tooallow para análise e exibição conforme necessário

Vários produtos estão disponíveis que abrangem essas três áreas e são toochoose livre de tecnologias diferentes para cada um. É importante toomake-se de que Olá várias partes trabalho juntos toodeliver uma solução de monitoramento de ponta a ponta para o cluster.

## <a name="event-generation"></a>Geração de evento

Olá primeira etapa no fluxo de trabalho de monitoramento e diagnóstico Olá é criação hello e a geração de eventos e logs. Esses eventos, os logs e os rastreamentos são gerados em dois níveis: Olá camada de plataforma (incluindo cluster hello, Olá máquinas ou ações de malha do serviço) ou Olá a camada de aplicativo (nenhuma instrumentação adicionado tooapps e serviços implantados toohello cluster). Os eventos em cada um desses níveis são personalizáveis, embora o Service Fabric forneça instrumentação por padrão.

Leia mais sobre [eventos de nível de plataforma](service-fabric-diagnostics-event-generation-infra.md) e [eventos de nível de aplicativo](service-fabric-diagnostics-event-generation-app.md) toounderstand que é fornecido e como tooadd ainda mais a instrumentação.

Depois de tomar uma decisão sobre Olá você gostaria que toouse do provedor de log, você precisa toomake-se de que os logs estão sendo agregados e armazenados corretamente.

## <a name="event-aggregation"></a>Agregação de eventos

Para coletar logs hello e eventos que estão sendo gerados por seus aplicativos e o cluster, geralmente recomendamos o uso [diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md) (coleta de log baseado em tooagent mais semelhante) ou [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(-processo de coleta de log).

Coletar logs de aplicativo usando a extensão de diagnóstico do Azure é uma boa opção para serviços do Service Fabric se Olá conjunto de fontes de log e destinos não são alterados com frequência e há um mapeamento direto entre as origens de saudação e seus destinos. motivo Olá para isso é a configuração de diagnóstico do Azure ocorre na camada do Gerenciador de recursos de hello, para que configuração de toohello fazendo alterações significativas requer atualização/reimplantar o cluster hello. Além disso, é utilizado da melhor forma para garantir que os logs sejam armazenados em algum lugar um pouco mais permanente, do qual possam ser acessados por várias plataformas de análise. Isso significa que ele acaba sendo menos eficiente como pipeline do que uma opção como o EventFlow.

Usando [EventFlow](https://github.com/Azure/diagnostics-eventflow) permite a você serviços toohave enviar os logs diretamente tooan analysis e plataforma de visualização, e/ou toostorage. Outras bibliotecas (ILogger, Serilog, etc.) podem ser usadas para Olá mesmo propósito, mas EventFlow tem benefício de saudação de projetados especificamente para em processo log coleta e toosupport serviços do Service Fabric. Isso tende a toohave várias vantagens potenciais:

* Fácil configuração e implantação
    * configuração de saudação da coleta de dados de diagnóstico é apenas parte da configuração do serviço de saudação. É fácil tooalways manter "sincronizado" com hello-rest do aplicativo hello
    * A configuração por aplicativo ou por serviço é facilmente realizável
    * Configurar destinos de dados por meio de EventFlow é apenas uma questão de adicionar o pacote do NuGet apropriado hello e alterar Olá *eventFlowConfig.json* arquivo
* Flexibilidade
    * aplicativo Hello pode enviar dados Olá sempre que ele precisa toogo, enquanto há uma biblioteca de cliente que oferece suporte ao sistema de armazenamento de dados Olá direcionado. Novos destinos podem ser adicionados conforme desejado
    * Regras de captura complexa, filtragem e agregação de dados podem ser implementadas
* Contexto e acessar dados de aplicativo toointernal
    * subsistema de diagnóstico Olá em execução dentro do processo de serviço do aplicativo hello facilmente pode aumentar rastreamentos Olá com informações contextuais

Um toonote de coisa é que essas duas opções não são mutuamente exclusivas e durante a possíveis tooget um trabalho semelhante com usando um ou Olá outros, ele também faria sentido para você tooset backup. Na maioria das situações, a combinação de um agente com no processo coleta pode levar tooa mais confiável do fluxo de trabalho de monitoramento. Olá extensão de diagnóstico do Azure (agente) poderia ser seu caminho escolhido para logs de nível de plataforma e você pode usar EventFlow (no processo de coleta) para seus logs de nível de aplicativo. Depois que você tenha entendido o que funciona melhor para você, é hora toothink sobre como você deseja que seu toobe dados exibidos e analisados.

## <a name="event-analysis"></a>Análise de eventos

Há várias plataformas grandes que existem no mercado hello quando se trata de toohello análise e à visualização de dados de monitoramento e diagnóstico. Olá dois que recomendamos são [OMS](service-fabric-diagnostics-event-analysis-oms.md) e [Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) devido tootheir melhor integração com o serviço de malha, mas você deve também examinar Olá [pilha Elástico](https://www.elastic.co/products) (especialmente se você estiver considerando a execução de um cluster em um ambiente offline), [Splunk](https://www.splunk.com/), ou qualquer outra plataforma de sua preferência.

Olá pontos-chave para qualquer plataforma que você escolher deve incluir se estiver com interface de usuário hello e consultar opções, Olá dados de toovisualize de capacidade e criar dashboards facilmente legíveis e hello ferramentas adicionais que fornecem tooenhance seu monitoramento, como alertar automatizada.

Além disso plataforma toohello que escolha, quando você configura um cluster do Service Fabric como um recurso do Azure, você também obtém acesso tooAzure fora da caixa monitoramento para computadores, que podem ser útil para desempenho específico e métrica.

### <a name="azure-monitor"></a>Azure Monitor

Você pode usar [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor muitas Olá recursos do Azure no qual um cluster do Service Fabric é criado. Um conjunto de métricas para Olá [conjunto de escalas da máquina virtual](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) individuais e [máquinas virtuais](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) são coletados e exibidos no portal do Azure de saudação automaticamente. Olá tooview coletadas informações em Olá portal do Azure, o grupo de recursos de saudação select que contém o cluster do Service Fabric hello. Em seguida, selecione Olá máquina virtual conjunto de escala que você deseja tooview. Em Olá **monitoramento** seção, selecione **métricas** tooview um gráfico de valores hello.

![Exibição de informações de métrica coletadas no portal do Azure](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

gráficos de saudação toocustomize, siga as instruções de saudação em [métricas no Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md). Você também pode criar alertas com base nessas métricas, conforme descrito em [criar alertas no Azure Monitor para serviços do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Você pode enviar tooa serviço de notificação de alertas usando ganchos web, conforme descrito em [configurar um gancho da web em um alerta de métrica do Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md). O Azure Monitor oferece suporte a apenas uma assinatura. Se você precisar toomonitor várias assinaturas, ou se você precisar de recursos adicionais, [análise de Log](https://azure.microsoft.com/documentation/services/log-analytics/), parte do Microsoft Operations Management Suite, fornece uma abrangente solução de gerenciamento de TI para locais e baseados em nuvem infraestrutura. Você pode encaminhar dados do Monitor do Azure diretamente tooLog análise, para que possa ver as métricas e os logs para todo o ambiente em um único lugar.

## <a name="next-steps"></a>Próximas etapas

### <a name="watchdogs"></a>Watchdogs

Um watchdog é um serviço separado que pode assistir a integridade e a carga em serviços e a integridade de relatório para qualquer coisa na hierarquia de modelo de integridade de saudação. Isso pode ajudar a evitar erros que não seriam detectados com base no modo de exibição de saudação de um único serviço. Watchdogs também são um bom ponto de código de toohost que executa ações corretivas, sem interação do usuário (por exemplo, a limpeza dos arquivos de log no armazenamento em determinados intervalos de tempo). Você pode encontrar uma implementação de serviço de watchdog de exemplo [aqui](https://github.com/Azure-Samples/service-fabric-watchdog-service).

Começar com noções básicas sobre como os eventos e logs de obtenham gerados em Olá [nível plataforma](service-fabric-diagnostics-event-generation-infra.md) e hello [nível de aplicativo](service-fabric-diagnostics-event-generation-app.md).
