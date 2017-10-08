---
title: aaaAzure modelo de dados de telemetria do aplicativo Insights | Microsoft Docs
description: "Visão geral do modelo de dados do Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Modelo de dados do Application Insights Telemetry

[Informações de aplicativo do Azure](app-insights-overview.md) envia telemetria do seu aplicativo de web toohello portal do Azure, para que você possa analisar desempenho hello e uso do seu aplicativo. modelo de telemetria Olá é padronizado para que seja possível toocreate plataforma e monitoramento independente de linguagem. 

Os dados coletados pelo Application Insights modelam esse padrão de execução típico do aplicativo:

![Modelo de aplicativo do Application Insights](./media/application-insights-data-model/application-insights-data-model.png)

Olá seguintes tipos de telemetria são usadas toomonitor Olá execução do seu aplicativo. Hello três tipos seguintes são normalmente automaticamente coletados por Olá SDK do Application Insights da estrutura de aplicativo web hello:

* [**Solicitação** ](application-insights-data-model-request-telemetry.md) -gerado toolog uma solicitação recebida pelo seu aplicativo. Por exemplo, Olá web Application Insights que SDK gera automaticamente um item de telemetria de solicitação para cada solicitação HTTP que recebe do seu aplicativo web. 

    Um **operação** é Olá threads de execução que processa uma solicitação. Você também pode [escrever código](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor outros tipos de operação, como um "Ativar" em uma web de trabalho ou função que periodicamente processa dados.  Cada operação tem uma ID. Essa ID que pode ser usado too[group]((application-insights-correlation.md) toda a telemetria gerado enquanto o aplicativo está processando a solicitação de saudação. Cada operação é bem-sucedida ou falha, além de ter uma duração.
* [**Exceção** ](application-insights-data-model-exception-telemetry.md) -normalmente representa uma exceção que faz com que uma operação toofail.
* [**Dependência** ](application-insights-data-model-dependency-telemetry.md) -representa uma chamada do seu serviço externo do aplicativo tooan ou armazenamento, como uma API REST ou SQL. No ASP.NET, tooSQL de chamadas de dependência são definidos por `System.Data`. Pontos de extremidade de tooHTTP chamadas são definidos por `System.Net`. 

O Application Insights fornece três tipos de dados adicionais para telemetria personalizada:

* [Rastreamento](application-insights-data-model-trace-telemetry.md) - usado diretamente ou por meio de um log de diagnóstico do adaptador tooimplement usando uma estrutura de instrumentação é tooyou familiar, como `Log4Net` ou `System.Diagnostics`.
* [Evento](application-insights-data-model-event-telemetry.md) -geralmente usado toocapture interação do usuário com o serviço, tooanalyze padrões de uso.
* [Métrica](application-insights-data-model-metric-telemetry.md) -usado tooreport medidas periódica de escalar.

Todos os itens de telemetria podem definir Olá [informações de contexto](application-insights-data-model-context.md) como id de sessão de usuário ou a versão de aplicativo. O contexto é um conjunto de campos fortemente tipados que desbloqueia determinados cenários. Quando a versão do aplicativo é inicializada corretamente, o Application Insights pode detectar novos padrões no comportamento do aplicativo correlacionado com a reimplantação. Id da sessão pode ser usado toocalculate Olá interrupção ou um problema impacto sobre os usuários. Calcular a contagem distinta de valores de id de sessão para determinadas dependência com falha, rastreamento de erro ou exceção crítica dá uma boa compreensão de um impacto.

Application Insights modelo telemetria define uma maneira muito[correlacionar](application-insights-correlation.md) operação toohello de telemetria do qual faz parte. Por exemplo, uma solicitação pode tomar informações de diagnóstico registradas e de chamadas de um Banco de Dados SQL. Você pode definir o contexto de correlação Olá para os itens de telemetria que unem toohello back telemetria de solicitação.

## <a name="schema-improvements"></a>Aprimoramentos de esquema

Modelo de dados do Application Insights é um toomodel de maneira simples e básica e poderosas a telemetria de aplicativos. É buscar cenários essenciais do tookeep Olá modelo toosupport simples e fino e permitir que o esquema de saudação tooextend para uso avançado.

problemas de esquema ou o modelo de dados tooreport e sugestões usam GitHub [ApplicationInsights inicial](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) repositório.

## <a name="next-steps"></a>Próximas etapas

- [Escrever telemetria personalizada](app-insights-api-custom-events-metrics.md)
- Saiba como muito[estender e filtrar telemetria](app-insights-api-filtering-sampling.md).
- Use [amostragem](app-insights-sampling.md) toominimize quantidade de telemetria com base no modelo de dados.
- Confira as [plataformas](app-insights-platforms.md) com suporte do Application Insights.
