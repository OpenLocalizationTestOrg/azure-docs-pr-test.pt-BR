---
title: "Análise de eventos de malha do serviço com o Application Insights de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre visualização e análise de eventos utilizando o Application Insights para o monitoramento e diagnóstico de clusters do Azure Service Fabric."
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Visualização e análise de eventos com o Application Insights

O Azure Application Insights é uma plataforma extensível para monitoramento e diagnóstico de aplicativos. Inclui uma poderosa ferramenta de análise e consulta, visualizações e dashboard personalizável e outras opções, incluindo alertas automatizados. Ele é hello recomendado plataforma para monitoramento e diagnóstico para serviços e aplicativos do Service Fabric.

## <a name="setting-up-application-insights"></a>Configurando o Application Insights

### <a name="creating-an-ai-resource"></a>Criar um Recurso do AI

recurso de toocreate um AI, principal toohello Azure Marketplace e procure "Application Insights". Ele deve aparecer como primeira solução de saudação (está sob a categoria "Web + móvel"). Clique em **criar** quando você estiver procurando no recurso direito da saudação (confirme se o caminho corresponde a imagem de saudação abaixo).

![Novo recurso do Application Insights](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Você precisará toofill-out de alguns recursos de saudação tooprovision informações corretamente. Em Olá *tipo de aplicativo* campo, use "Aplicativo web do ASP.NET" Se você estiver usando qualquer serviço de malha de modelos de programação ou publicar um cluster de toohello do aplicativo .NET. Utilize "Geral" se você estiver implantando contêineres e executáveis do convidado. Em geral, padrão toousing "Aplicativo web do ASP.NET" tookeep suas opções abra no hello futuras. nome de saudação é a preferência de tooyour e o grupo de recursos hello e assinatura são mutável pós-implantação do recurso de saudação. Recomendamos que o recurso AI em Olá mesmo grupo de recursos que o seu cluster. Caso precise de mais informações, consulte [Criar um recurso do Application Insights](../application-insights/app-insights-create-new-resource.md)

Você precisa Olá chave de instrumentação AI tooconfigure AI com sua ferramenta de agregação de eventos. Depois que o recurso AI estiver configurado (leva alguns minutos após a implantação de saudação é validada), navegue tooit e localize Olá **propriedades** seção na barra de navegação à esquerda de saudação. Uma nova folha será aberta e exibirá uma *CHAVE DE INSTRUMENTAÇÃO*. Se você precisar de assinatura de saudação toochange ou grupo de recursos do recurso hello, ele pode ser feito aqui também.

### <a name="configuring-ai-with-wad"></a>Configurar o AI com WAD

Há duas maneiras principais dados toosend do WAD tooAzure AI, que são obtidos pela adição de uma configuração do AI coletor toohello WAD, conforme detalhado no [neste artigo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Adicione uma Chave de Instrumentação do AI ao criar um cluster no Portal do Azure

![Adicionar uma AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

Ao criar um cluster, se o diagnóstico está ativado "", um campo opcional tooenter uma chave de instrumentação do Application Insights mostrará. Se você colar o IKey AI aqui, o coletor Olá AI será automaticamente configurado por você no modelo do Gerenciador de recursos de saudação que é usado toodeploy seu cluster.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Adicionar Olá modelo do coletor AI toohello Gerenciador de recursos

Adicione "Sink" hello "WadCfg" do modelo do Gerenciador de recursos de Olá, incluindo Olá duas alterações a seguir:

1. Adicione configuração do coletor de saudação:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Inclua Olá coletor Olá DiagnosticMonitorConfiguration por adicionar Olá a seguinte linha no "DiagnosticMonitorConfiguration" hello "WadCfg":

    ```json
    "sinks": "applicationInsights"
    ```

Em ambos os trechos de código Olá acima, Olá nome "applicationInsights" era coletor de saudação toodescribe usado. Isso não é um requisito e como nome de saudação do coletor de saudação é incluído no "coletores", você pode definir a cadeia de caracteres hello name tooany.

Atualmente, os logs de cluster Olá aparecerão como rastreamentos no Visualizador de log do AI. Desde que a maioria dos rastreamentos Olá provenientes de plataforma de saudação for de nível de "Informação", você também pode considerar a alteração de logs de envio de tooonly Olá coletor configuração do tipo "Crítico" ou "Error". Isso pode ser feito adicionando o coletor de tooyour de "Canais", conforme demonstrado no [neste artigo](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Se você usar um IKey AI incorreto no portal ou em seu modelo do Gerenciador de recursos, você terá toomanually alterar chave hello e atualizar cluster Olá / reimplantá-lo. 

### <a name="configuring-ai-with-eventflow"></a>Configurar AI com EventFlow

Se você estiver usando EventFlow tooaggregate eventos, verifique se Olá de tooimport `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`pacote NuGet. seguir Hello tem toobe incluído no hello *gera* seção Olá *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Alterar toomake se Olá necessário seus filtros, bem como incluir quaisquer outras entradas (junto com seus respectivos pacotes NuGet).

## <a name="aisdk"></a>AI.SDK

Geralmente, é recomendável toouse EventFlow e WAD como soluções de agregação, porque que permitem um toodiagnostics abordagem mais modular e não monitoramento, ou seja, se você quiser que suas saídas de EventFlow toochange, requer a nenhum tooyour alteração real Instrumentação, apenas um arquivo de configuração de tooyour simples modificação. Se, no entanto, você decide tooinvest usando o Application Insights e não é provavelmente toochange tooa diferentes plataformas, você deve examinar usando novo SDK do AI para agregar eventos e enviá-los tooAI. Isso significa que você não terá mais tooconfigure EventFlow toosend tooAI seus dados, mas em vez disso, instalará o pacote de NuGet de malha do serviço do hello ApplicationInsight. Detalhes sobre o pacote de saudação podem ser encontrados [aqui](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Suporte do Application Insights para Microservices e contêineres](https://azure.microsoft.com/app-insights-microservices/) mostra alguns dos Olá novos recursos que estão sendo trabalhados (ainda atualmente em beta), que permitem que você toohave mais avançada da caixa Opções de monitoramento com AI. Esses incluem controle de dependência (usado na criação de um AppMap de todos os seus serviços e aplicativos em um cluster e hello a comunicação entre eles) e a correlação melhor de rastreamentos provenientes de seus serviços (ajuda a melhor identificar um problema no Olá fluxo de trabalho de um aplicativo ou serviço).

Se você estiver desenvolvendo no .NET e provavelmente ser usando alguns dos modelos de programação do Service Fabric e são disposto toouse AI como plataforma para visualizar e analisar dados de eventos e log, em seguida, é recomendável que você passe por meio de saudação rota AI SDK como o monitoramento e fluxo de trabalho de diagnóstico. Leitura [isso](../application-insights/app-insights-asp-net-more.md) e [isso](../application-insights/app-insights-asp-net-trace-logs.md) tooget foi iniciado com usando toocollect AI e exibir os logs.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Navegando pelo recurso de AI Olá no portal do Azure

Depois que você configurou AI como uma saída para seus eventos e logs, informações devem iniciar tooshow em seu recurso AI em alguns minutos. Navegue toohello o recurso AI, que levará você toohello AI painel recursos. Clique em **pesquisa** Olá AI na barra de tarefas toosee hello mais recentes rastreamentos que recebeu e toofilter capaz de toobe por eles.

*Metrics Explorer* é uma ferramenta útil para criar painéis personalizados com base em métricas que seus aplicativos, serviços e clusters podem estar reportando. Consulte [explorando métricas no Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset backup alguns gráficos para si mesmo com base nos dados de saudação coletar.

Clicando em **análise** levará você toohello portal do Application Insights Analytics, onde você pode consultar eventos e rastreamentos com o maior escopo e opções. Leia mais sobre isso em [Análise no Application Insights](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Próximas etapas

* [Configurar alertas em AI](../application-insights/app-insights-alerts.md) toobe notificado sobre as alterações no desempenho ou de uso
* [Inteligente de detecção no Application Insights](../application-insights/app-insights-proactive-diagnostics.md) realiza uma análise proativa de telemetria Olá enviada tooAI toowarn sobre possíveis problemas de desempenho
