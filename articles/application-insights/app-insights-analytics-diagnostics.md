---
title: "diagnóstico aaaSmart das alterações de desempenho de aplicativo web no Azure Application Insights | Microsoft Docs"
description: "Diagnóstico automático de picos ou etapas em telemetria de desempenho do seu aplicativo Web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a>Diagnosticar alterações repentinas na telemetria do aplicativo

*Esse recurso está em visualização.*

Faça o diagnóstico de alterações repentinas no uso ou no desempenho do seu aplicativo Web com um único clique! recurso de diagnóstico inteligente de saudação está disponível sempre que você cria um gráfico de tempo em [análise](app-insights-analytics.md) na [Application Insights](app-insights-overview.md). Sempre que houver uma alteração incomum de tendência de saudação de resultados, como um aumento ou um dip, diagnóstico inteligente identifica um padrão de dimensões e valores relacionados que possam explicar a alteração de saudação. Isso ajuda você a diagnosticar o problema de saudação rapidamente. 

Neste exemplo, diagnóstico inteligente identificou um padrão de valores de propriedade associados a alteração hello e realça Olá diferença entre os resultados com e sem esse padrão:

![resultado de diagnóstico analítico de exemplo](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a>Diagnosticar alterações de dados

1.  Execute uma consulta no Analytics e renderize-o como um gráfico de tempo. 
2.  Clique em qualquer ponto de pico destacado, se houver.
 
    ![ponto de pico](./media/app-insights-analytics-diagnostics/peak.png)

    Diagnóstico leva alguns segundos toodiscover um padrão.

3. Guia de resultados do diagnóstico de saudação mostra um padrão que pode explicar descontinuidade seus dados.

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    texto de saudação mostra os valores de dimensão Olá exibidos toocorrelate com shift hello. Nesse exemplo, isso está associado a uma solicitação específica e uma versão específica do navegador.

    Observe também componentes Olá dois de gráfico hello, com hello filtro true e false. componente de saudação false mostra uma tendência inalterada. Em outras palavras, não há nenhuma alteração nos resultados de telemetria hello, se excluímos combinação problemático Olá dimensões diagnóstico identificou. Por outro lado, os resultados de saudação em combinação mostram uma alteração radical na área de saudação realçada da investigação. Isso mostra que o diagnóstico encontrou uma combinação das propriedades que explica a alteração de saudação.

4.  Se o padrão de saudação é complexo, você precisa toohover pela **Mostrar tudo** toosee dimensões de saudação.

    ![mostrar tudo](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  No caso de diagnóstico não localiza toonotify nenhum padrão significativo sobre Olá que será exibida a página 'Nenhum resultado'. Nesse momento, você pode alterar sua consulta. Por exemplo, você pode restringir o intervalo de tempo de saudação e agrupamento na consulta de análise, para uma análise adicional e potencialmente melhores resultados.

Armado com conhecimento de saudação que uma página específica do site tem um problema em um navegador específico, você pode agora vá reta toohello problema página e investigar alterações recentes.

## <a name="try-hello-demo"></a>Experimente Olá demonstração

[Clique aqui toosee uma demonstração](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) em dados de exemplo.

## <a name="how-it-works"></a>Como ele funciona

O diagnóstico inteligente usa um algoritmo de aprendizado de máquina sem supervisão avançado baseado em Olá [DiffPatterns](app-insights-analytics-reference.md) operação. Ele procura por padrões de candidato que podem explicar Olá alteração de dados. Ele analisa o impacto de saudação de cada candidato na métrica hello e mostra o padrão de saudação que melhor se correlaciona com alteração de saudação.

## <a name="no-diagnostic-points"></a>Não há pontos de diagnóstico?

Diagnóstico inteligente só funciona quando Olá critérios a seguir forem atendida:

 * A configuração do Diagnóstico Inteligente está ativada. Procure o ícone de configurações de saudação na análise.
 * Olá opção diagnóstico inteligente nas configurações de análise é selecionado. 
 * Eixo de tempo: Olá eixo x do gráfico de saudação deve ser do tipo `datetime`.
 * Gráfico de linha ou área: o diagnóstico funciona somente com esses tipos de gráfico. Use `| render timechart` ou `| render areachart` no final de saudação de sua consulta; ou selecione a linha ou um gráfico de área de seletor de lista suspensa de saudação.
 * Descontinuidade: Deve haver uma interrupção significativa nos dados de saudação.
 * Tooanalyze de pontos suficientes.
 * Não mais de um resumir cláusula na consulta de saudação.
 * Nenhuma cláusula de projeto que contém uma definição de nome antes de saudação resumir cláusula.

 
 ## <a name="related-articles"></a>Artigos relacionados

 * [Tutorial do Analytics](app-insights-analytics-tour.md)
 * [Detecção de Smart](app-insights-proactive-diagnostics.md) alerta automaticamente tooperformance problemas.
