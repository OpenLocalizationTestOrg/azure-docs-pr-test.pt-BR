---
title: aaaCreate um painel personalizado no Azure Log Analytics | Microsoft Docs
description: "Este guia ajuda você a entender como os painéis de análise de Log podem visualizar todas as pesquisas de log salvas, dando a você uma única Lente tooview seu ambiente."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Criar um painel personalizado para uso no Log Analytics

>[!NOTE]
> Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), em seguida, você não pode criar novos painéis ou editar painéis existentes. 

Este guia ajuda você a entender como os painéis de análise de Log podem visualizar todas as pesquisas de log salvas, dando a você uma única Lente tooview seu ambiente.

![Painel de Exemplo](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Todos os painéis de saudação personalizada que você cria no portal do OMS Olá também estão disponíveis no hello aplicativo móvel do OMS. Consulte Olá páginas para obter mais informações sobre aplicativos Olá a seguir.

* [Aplicativo móvel do OMS de saudação Microsoft Store](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Aplicativo móvel do OMS no Apple iTunes](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![painel móvel](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>Como crio meu painel?
toobegin, vá toohello página de visão geral do OMS. Você verá Olá **meu painel** bloco Olá esquerda. Clique toodrill para baixo para seu painel.

![Visão geral](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Adicionando um bloco
Nos painéis, os blocos são ativados pelas pesquisas de log salvas. O OMS vem com muitas pesquisas de log salvas previamente, portanto, você pode começar imediatamente. Use Olá as etapas a seguir essa estrutura de tópicos como toobegin.

Em Olá exibição meu painel, basta clicar **personalizar** tooenter no modo de personalização.

![Ilustração](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 Painel de saudação que abre Olá direita da página Olá mostra todas as pesquisas de log salvas do seu espaço de trabalho. toovisualize pesquisar um log salvo como um bloco, passe o mouse sobre uma pesquisa salva e clique em Olá **mais** símbolo.

![Adicionar Blocos 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Quando você clica em Olá **mais** símbolo, um novo bloco aparece na exibição meu painel de saudação.

![Adicionar Blocos 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Editar um bloco
Em Olá exibição meu painel, basta clicar **personalizar** tooenter no modo de personalização. Clique em bloco Olá deseja tooedit. painel direito da saudação altera tooedit e fornece uma seleção de opções:

![Editar Bloco](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Editar Bloco](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Visualizações do bloco
Há três tipos de toochoose de visualizações do bloco do:

| tipo de gráfico | o que ele faz |
| --- | --- |
| ![Gráfico de Barras](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Exibe uma linha do tempo dos resultados salvos da pesquisa de log como um gráfico de barras ou uma lista de resultados por campo, dependendo se sua pesquisa de log agrega os resultados por campo ou não. |
| ![métrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |Exibe as visitas totais dos resultados da pesquisa de log como um número em um bloco. Os blocos da métrica permitem que você tooset um limite que destacará o bloco de saudação quando é atingido o limite de saudação. |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |Exibe uma linha do tempo das ocorrências dos resultados da pesquisa de log salva com valores como um gráfico de linhas. |

### <a name="threshold"></a>Limite
Você pode criar um limite em um bloco usando a visualização métrica hello. Selecione um valor de limite no bloco de saudação em toocreate. Escolha se toohighlight Olá lado a lado ao valor Olá fica acima ou abaixo do limite de saudação escolhida, em seguida, defina o valor abaixo do limite de saudação.

## <a name="organizing-hello-dashboard"></a>Organizando Olá painel
tooorganize seu painel, navegue toohello exibição de meu painel e clique em **personalizar** tooenter no modo de personalização. Clique e arraste o bloco Olá desejado toomove e movê-la toowhere que você deseja que seu toobe lado a lado.

![Organizar seu Painel](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Remover um bloco
tooremove um bloco, navegue toohello exibição de meu painel e clique em **personalizar** tooenter no modo de personalização. Bloco Olá selecione desejado tooremove e no painel à direita da saudação selecione **remover bloco**.

![Remover um bloco](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Próximas etapas
* Criar [alertas](log-analytics-alerts.md) em notificações de toogenerate de análise de Log e tooremediate problemas.
