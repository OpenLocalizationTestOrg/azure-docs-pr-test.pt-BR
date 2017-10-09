---
title: "aaaOverview de métricas no Microsoft Azure | Microsoft Docs"
description: "Visão geral das métricas e seus usos no Microsoft Azure"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Visão geral das métricas no Microsoft Azure
Este artigo descreve quais são as métricas no Microsoft Azure, seus benefícios e como usá-los de toostart.  

## <a name="what-are-metrics"></a>O que são métricas?
Monitor do Azure permite que você tooconsume telemetria toogain visibilidade do desempenho de saudação e a integridade de suas cargas de trabalho no Azure. tipo mais importante de saudação de dados de telemetria do Azure é métricas hello (também chamadas de contadores de desempenho) emitidas por recursos mais do Azure. Monitor do Azure fornece tooconfigure de diversas maneiras e consumir essas métricas para monitorar e solucionar problemas.

## <a name="what-can-you-do-with-metrics"></a>O que você pode fazer com as métricas?
Métricas são uma fonte valiosa de telemetria e permitem que você toodo Olá tarefas a seguir:

* **Rastrear o desempenho de saudação** do recurso (como uma VM, site ou lógica de aplicativo) por plotagem suas métricas em um gráfico de portal e fixando tooa esse gráfico do painel.
* **Ser notificado de um problema** que impactos Olá desempenho do recurso quando uma métrica ultrapassar um certo limite.
* **Configurar ações automatizadas**, como dimensionar automaticamente um recurso ou disparar um runbook quando uma métrica cruza certo limite.
* **Executar análises avançadas** ou gerar relatórios sobre as tendências de desempenho ou uso do recurso.
* **Arquivamento** Olá histórico de desempenho ou a integridade do recurso **para conformidade e auditoria** fins.

## <a name="what-are-hello-characteristics-of-metrics"></a>Quais são as características de saudação de métricas?
Métricas têm Olá características a seguir:

* Todas as métricas têm uma **frequência de um minuto**. Você recebe um valor de métrica cada minuto de seus recursos, fornecendo próximo visibilidade em tempo real de estado de saudação e a integridade de seus recursos.
* As métricas são **disponibilizadas imediatamente**. Você não precisa tooopt em ou configurar diagnósticos adicionais.
* Você pode acessar **30 dias do histórico** para cada métrica. Você pode ver rapidamente tendências de Olá recentes e um mensal no desempenho de saudação ou integridade do recurso.

Você também pode:

* Configurar uma métrica **regra que envia uma notificação ou leva automatizada de ação de alerta** quando o métrica Olá exceder o limite de saudação que você definiu. O dimensionamento automático é uma ação automatizada especial que permite que você tooscale suas solicitações de entrada toomeet recursos ou carrega em seu site ou recursos de computação. Você pode configurar um configuração regra tooscale ou com base em uma métrica cruzar um limite de dimensionamento automático.

* **Rota** todas as métricas do Application Insights ou análise de Log (OMS) tooenable instantâneas analytics, pesquisa e alertas personalizados de dados de métricas de seus recursos. Você também pode transmitir métricas tooan Hub de eventos, permitindo que você toothen encaminhá-los tooAzure Stream Analytics ou aplicativos de toocustom para análise em tempo quase real. Você configura o Hub de Eventos usando as configurações de diagnóstico de streaming.

* **Arquivar métricas toostorage** para maior retenção ou usá-las para relatórios offline. Quando você configura as definições de diagnóstico para o recurso, você pode rotear o tooAzure métricas armazenamento de Blob.

* Descobrir facilmente, acesso e **exibir todas as métricas** por meio do portal do Azure, quando você seleciona um recurso e plotar Olá métricas em um gráfico de saudação.

* **Consumir** métricas Olá via Olá novas APIs de REST do Monitor do Azure.

* **Consulta** métricas usando Olá cmdlets do PowerShell ou Olá API de REST de plataforma cruzada.

  ![Roteamento das Métricas no Azure Monitor](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Métricas de acesso por meio do portal de saudação
A seguir está uma rápida explicação passo a passo de como toocreate um gráfico de métrica usando Olá portal do Azure.

### <a name="tooview-metrics-after-creating-a-resource"></a>métricas de tooview depois de criar um recurso
1. Olá Abrir portal do Azure.
2. Crie um site do Serviço de Aplicativo do Azure.
3. Depois de criar um site, vá toohello **visão geral** folha do site de saudação.
4. É possível exibir novas métricas como um bloco **Monitoramento**. Você pode editar bloco de saudação e selecionar as métricas mais.

   ![Métricas em um recurso no Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess todas as métricas em um único lugar
1. Olá Abrir portal do Azure.
2. Navegue toohello novo **Monitor** guia e selecione e, em seguida, Olá **métricas** opção abaixo dele.
3. Selecione sua assinatura, o grupo de recursos e o nome de saudação do recurso de saudação na lista suspensa de saudação.
4. Exiba a lista de métricas disponíveis hello. Em seguida, selecione métrica hello está interessado e plotá-lo.
5. Você pode fixar-toohello painel clicando Olá pino no canto superior direito de saudação.

   ![Acessar todas as métricas em um único lugar no Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> Você pode acessar as métricas no nível do host nas VMs (baseadas no Azure Resource Manager) e nos conjuntos de dimensionamento de máquinas virtuais sem nenhuma configuração de diagnóstico adicional. Essas novas métricas no nível do host estão disponíveis para as instâncias do Windows e do Linux. Essas métricas não estão toobe confundido com hello métricas de nível de sistema operacional convidado que você tem acesso toowhen que ativar o diagnóstico do Azure em suas VMs ou conjuntos de escala de máquina virtual. toolearn mais informações sobre como configurar o diagnóstico, consulte [o que é o Microsoft Azure Diagnostics](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Métricas de acesso por meio de saudação API REST
As métricas do Azure podem ser acessadas via Olá APIs do Monitor do Azure. Há duas APIs que ajudam você a descobrir e acessar as métricas:

* Saudação de uso [definições de métrica do Monitor do Azure API REST](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess Olá lista de métricas que estão disponíveis para um serviço.
* Saudação de uso [API de REST de métricas de Monitor do Azure](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess Olá dados de métrica real.

> [!NOTE]
> Este artigo aborda as métricas de saudação via Olá [nova API de métricas](https://msdn.microsoft.com/library/dn931930.aspx) para recursos do Azure. versão da API Olá para definições de métrica nova API de saudação é 2016-03-01 e versão Olá para métricas de API é 2016-09-01. métricas e definições de métrica herdados Olá podem ser acessadas com hello API versão 2014-04-01.
>
>

Para obter uma explicação mais detalhada usando Olá APIs de REST do Monitor do Azure, consulte [passo a passo de API REST do Azure Monitor](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Exportar métricas
Você pode ir toohello **as configurações de diagnóstico** folha sob Olá **Monitor** guia e exibir opções de exportação de saudação de métricas. Você pode selecionar as métricas (e logs de diagnóstico) toobe roteadas tooBlob armazenamento, os Hubs de eventos tooAzure ou tooOMS para casos de uso que foram mencionados anteriormente neste artigo.

 ![Opções de exportação das métricas no Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview3.png)

Você pode configurar isso usando os modelos do Resource Manager, o [PowerShell](insights-powershell-samples.md), a [CLI do Azure](insights-cli-samples.md) ou as [APIs REST](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Executar uma ação com base nas métricas
notificações de tooreceive ou ações de take automatizada em dados de métrica, você pode configurar regras de alerta ou configurações de dimensionamento automático.

### <a name="configure-alert-rules"></a>Configurar regras de alerta
Você pode configurar regras de alerta sobre as métricas. Essas regras de alerta podem verificar se uma métrica ultrapassou um determinado limite. Em seguida, podem notificá-lo por email ou disparar um webhook que pode ser usado toorun qualquer script personalizado. Você também pode usar as integrações do hello webhook tooconfigure produtos de terceiros.

 ![Métricas e regras de alerta no Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Dimensionar automaticamente os recursos do Azure
Alguns recursos do Azure oferecem suporte a saudação scaling out ou em de toohandle de várias instâncias suas cargas de trabalho. Dimensionamento automático aplica tooApp serviço (aplicativos da Web), conjuntos de escala de máquinas virtuais e serviços de nuvem clássico do Azure. Você pode configurar a AutoEscala regras tooscale out ou em quando certa métrica que afeta sua carga de trabalho exceder um limite que você especificar. Para obter mais informações, consulte [Visão geral do dimensionamento automático](monitoring-overview-autoscale.md).

 ![Métricas e dimensionamento automático no Azure Monitor](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Conheça os serviços e as métricas compatíveis
O Azure Monitor é uma nova infraestrutura das métricas. Ele dá suporte a saudação serviços do Azure em hello Azure portal e hello nova versão de hello Azure Monitor API a seguir:

* VMs (baseadas no Azure Resource Manager)
* conjuntos de escala de máquina virtual
* Batch
* Namespace do Hubs de Eventos
* Namespace do Barramento de Serviço (SKU premium somente)
* Banco de Dados SQL (versão 12)
* Pool SQL Elástico
* Sites
* Farms do servidor Web
* Aplicativos Lógicos
* Hubs IoT
* Cache Redis
* Rede: gateways de aplicativo
* Pesquisar

Você pode exibir uma lista detalhada de todos os serviços de saudação com suporte e suas métricas [métricas do Monitor do Azure — métricas suportadas por tipo de recurso](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Próximas etapas
Consulte os links toohello neste artigo. Além disso, saiba mais sobre:  

* [Métricas comuns para dimensionamento automático](insights-autoscale-common-metrics.md)
* [Como as regras de alerta toocreate](insights-alerts-portal.md)
* [Analisar logs do Armazenamento do Azure com o Log Analytics](../log-analytics/log-analytics-azure-storage.md)
