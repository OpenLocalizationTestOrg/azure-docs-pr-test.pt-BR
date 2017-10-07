---
title: aaaInvestigate e compartilhamento de dados de uso com pastas de trabalho interativas no Azure Application Insights | Documentos da Microsoft
description: "Análise demográfica dos usuários de seu aplicativo Web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Investigar e compartilhar dados de uso com pastas de trabalho interativas no Application Insights

As pastas de trabalho combinam as visualizações de dados do [Azure Application Insights](app-insights-overview.md), as [consultas do Analytics](app-insights-analytics.md) e textos em documentos interativos. Pastas de trabalho são editáveis por outros membros da equipe com acesso toohello mesmo recurso do Azure. Isso significa Olá controles e consultas usado toocreate uma pasta de trabalho são tooother disponível pessoas lendo a pasta de trabalho hello, tornando-os tooexplore fácil, estender e verificar se há erros.

As pastas de trabalho são úteis para cenários como:

* Explorando o uso de saudação do seu aplicativo quando não souber com antecedência métricas de saudação de interesse: números de usuários, as taxas de retenção, taxas de conversão, etc. Ao contrário de outras ferramentas de análise de uso do Application Insights, as pastas de trabalho permitem combinar vários tipos de visualizações e análises, tornando-as excelentes para esse tipo de exploração de forma livre.
* Explicar team tooyour como um recurso recém-lançado está funcionando, por usuário mostra contagens de interações de chave e outras métricas.
* Compartilhar os resultados de saudação de um A / B experiências em seu aplicativo com outros membros da equipe. Você pode explicar metas Olá para Olá fazer experiências com texto e mostram cada métrica de uso e consulta de análise usado experiência de saudação tooevaluate, junto com as transferências de chamada claras para se cada métrica foi acima ou abaixo do destino.
* Relatório impacto de saudação de uma interrupção no uso de saudação do seu aplicativo, combinando dados explicação de texto e uma discussão das interrupções de tooprevent etapas Avançar no hello futuras.

> [!NOTE]
> O recurso do Application Insights deve conter modos de exibição de página ou pastas de trabalho de toouse eventos personalizados. [Saiba como tooset sua página de toocollect aplicativo exibe automaticamente com hello SDK de JavaScript do Application Insights](app-insights-javascript.md).
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>Editando, reorganizando, clonando e excluindo seções da pasta de trabalho

Uma pasta de trabalho é composta por seções: visualizações de uso editáveis de forma independente, gráficos, tabelas, textos ou resultados de consultas do Analytics.

conteúdo de saudação tooedit de uma seção de pasta de trabalho, clique em Olá **editar** botão abaixo e toohello à direita da seção de pasta de trabalho de saudação.

![Controles de edição da seção Pastas de Trabalho do Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. Quando você terminar uma seção de edição, clique em **feito editando** na Olá inferior esquerda da seção de saudação.

2. toocreate uma duplicata de uma seção, clique em Olá **clonar nesta seção** ícone. Criando seções duplicadas é um tooiterate tooway grande em uma consulta sem perder iterações anteriores.

3. toomove uma seção em uma pasta de trabalho, clique em Olá **mover para cima** ou **mover para baixo** ícone.

4. tooremove uma seção permanentemente, clique em Olá **remover** ícone.

## <a name="adding-usage-data-visualization-sections"></a>Adicionando seções de visualização de dados de uso

As pastas de trabalho oferecem quatro tipos de visualizações internas de análise de uso. Cada responde a uma pergunta comum sobre o uso de saudação do seu aplicativo. tooadd tabelas e gráficos diferentes quatro seções, adicione seções de consulta de análise (veja abaixo).

tooadd aos usuários, sessões, eventos ou retenção seção tooyour de pasta de trabalho, use Olá **adicionar usuários** ou outro botão correspondente na parte inferior da saudação da pasta de trabalho hello, ou na parte inferior da saudação de qualquer seção.

![Seção Usuários no Workbooks](./media/app-insights-usage-workbooks/users-section.png)

As seções **Usuários** respondem à pergunta “Quantos usuários exibiram alguma página ou usaram algum recurso de meu site?”

As seções **Sessões** respondem à pergunta “Quantas sessões os usuários gastaram exibindo alguma página ou usando algum recurso de meu site?”

As seções **Eventos** respondem à pergunta “Quantas vezes os usuários exibiram alguma página ou usaram algum recurso de meu site?”

Cada um desses tipos de três seção oferece Olá mesmos conjuntos de controles e visualizações:

* [Saiba mais sobre como editar as seções Usuários, Sessões e Eventos](app-insights-usage-segmentation.md)
* Alternar de gráfico principal hello, grades de histograma, insights automática e visualizações de usuários de exemplo usando Olá **Mostrar gráfico**, **Mostrar grade de**, **Insights Mostrar**e **De esses usuários de exemplo** caixas de seleção na parte superior de saudação de cada seção.

![Seção Retenção no Workbooks](./media/app-insights-usage-workbooks/retention-section.png)

As seções **Retenção** respondem à pergunta: “Das pessoas que exibiram alguma página ou usaram algum recurso em um dia ou uma semana, quantas voltaram no dia ou na semana seguinte?”

* [Saiba mais sobre como editar as seções Retenção](app-insights-usage-retention.md)
* Ativar/desativar Olá opcional retenção geral gráfico usando Olá **Mostrar gráfico de retenção geral** caixa de seleção na parte superior de saudação da seção de saudação.

## <a name="adding-application-insights-analytics-sections"></a>Adicionando as seções do Analytics do Application Insights

![Seção do Analytics no Workbooks](./media/app-insights-usage-workbooks/analytics-section.png)

tooadd uma análise do aplicativo Insights consulta seção tooyour pasta de trabalho, use Olá **consulta analítica adicionar** botão na parte inferior da saudação da pasta de trabalho hello, ou na parte inferior da saudação de qualquer seção.

As seções de consulta do Analytics permitem que você adicione consultas arbitrárias dos dados do Application Insights a pastas de trabalho. Essa flexibilidade mostra seções de consulta de análise devem ser o go-toofor responder perguntas sobre seu site além daquele Olá quatro listados acima para usuários, sessões, eventos e retenção, como:

* Como muitas exceções foram throw seu site durante a saudação mesmo tempo como uma recusa de uso?
* Qual foi a distribuição de saudação de tempos de carregamento de página para que os usuários exibindo alguma página?
* Quantos usuários exibiram algum conjunto de páginas no site, mas não algum outro conjunto de páginas? Isso pode ser útil toounderstand se você tiver clusters de usuários que usam diferentes subconjuntos de funcionalidade do site (use Olá `join` operador com hello `kind=leftanti` modificador Olá linguagem de consulta de análise de Log).

Saudação de uso [referência de linguagem de consulta de análise de Log](https://docs.loganalytics.io/) toolearn mais sobre a escrita de consultas.

## <a name="adding-text-and-markdown-sections"></a>Adicionando texto e seções de Markdown

Adicionar títulos, explicações e pastas de trabalho comentários tooyour ajuda a transformar um conjunto de tabelas e gráficos em uma narrativa. Suportam a seções de texto em pastas de trabalho Olá [sintaxe de Markdown](https://daringfireball.net/projects/markdown/) para formatação de texto, como títulos, negrito, itálico e listas com marcadores.

tooadd uma pasta de trabalho de tooyour seção texto, use Olá **adicionar texto** botão na parte inferior da saudação da pasta de trabalho hello, ou na parte inferior da saudação de qualquer seção.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>Salvando e compartilhando pastas de trabalho com sua equipe

Pastas de trabalho são salvos em um recurso do Application Insights, em Olá **meus relatórios** seção tooyou privada ou em Olá **relatórios compartilhados** seção que é acessível tooeveryone com acesso toohello recurso do Application Insights. tooview todas as pastas de trabalho de saudação no recurso Olá, clique em Olá **abrir** botão na barra de ação de saudação.

tooshare uma pasta de trabalho está atualmente em **meus relatórios**:

1. Clique em **abrir** na barra de ação Olá
2. Clique no botão "…" hello ao lado da pasta de trabalho Olá deseja tooshare
3. Clique em **mover relatórios tooShared**.

tooshare uma pasta de trabalho com um link ou por meio de email, clique em **compartilhamento** na barra de ação de saudação. Tenha em mente que os destinatários do link de saudação precisam acessar o recurso de toothis na pasta de trabalho de saudação do hello tooview portal do Azure. edições toomake, os destinatários precisarão pelo menos permissões de Colaborador para o recurso de saudação.

toopin um tooan de pasta de trabalho do link tooa painel do Azure:

1. Clique em **abrir** na barra de ação Olá
2. Clique no botão "…" hello ao lado da pasta de trabalho Olá deseja toopin
3. Clique em **toodashboard Pin**.

## <a name="next-steps"></a>Próximas etapas

## <a name="next-steps"></a>Próximas etapas
- uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.
    - [Usuários, Sessões, Eventos](app-insights-usage-segmentation.md)
    - [Funis](usage-funnels.md)
    - [Retenção](app-insights-usage-retention.md)
    - [Fluxos de Usuário](app-insights-usage-flows.md)
    - [Adicionar contexto de usuário](app-insights-usage-send-user-context.md)
    
