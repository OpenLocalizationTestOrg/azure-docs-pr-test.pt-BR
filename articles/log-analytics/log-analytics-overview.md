---
title: "aaaWhat é a análise de Log no OMS Operations Management Suite ()? | Microsoft Docs"
description: "O Log Analytics é um serviço no OMS (Operations Management Suite) que ajuda a coletar e analisar operacionais dados gerados pelos recursos nos seus ambientes local e de nuvem.  Este artigo fornece uma visão geral dos diferentes componentes de saudação de análise de Log e o conteúdo de toodetailed links."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>O que é o Log Analytics?
Análise de log é um serviço em [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) que monitora o toomaintain de ambientes de nuvem e local sua disponibilidade e desempenho.  Ele coleta dados gerados pelos recursos em seus ambientes de nuvem e locais e de outras análises de tooprovide ferramentas monitoramento em várias origens.  Este artigo fornece uma breve discussão de valor de saudação que a análise de Log fornece uma visão geral de como ele funciona, e links toomore detalhadas de conteúdo para que você pode se aprofundar ainda mais.

## <a name="is-log-analytics-for-you"></a>O Log Analytics serve para você?
Se no momento você não tiver nenhum monitoramento de seu ambiente do Azure em vigor, comece com o [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md), que coleta e analisa dados de monitoramento de seus recursos do Azure.  Análise de log pode [coletar dados do Monitor do Azure](log-analytics-azure-storage.md) toocorrelate-lo com outros dados e fornecer análise adicional.

Se você quiser toomonitor seu ambiente local ou ter o monitoramento existente usando serviços como o Monitor do Azure ou o System Center Operations Manager, análise de Log pode adicionar valor significativo.  Ele pode coletar dados diretamente de seus agentes e também dessas outras ferramentas em um único repositório.  Ferramentas de análise no Log Analytics como pesquisas, exibições e soluções de log funcionam em todos os dados coletados, oferecendo análise centralizada de todo o ambiente.


## <a name="using-log-analytics"></a>Como usar o Log Analytics
Você pode acessar a análise de Log por meio do portal do OMS hello ou hello portal do Azure que são executados em qualquer navegador e fornecer as configurações do acesso tooconfiguration e tooanalyze de várias ferramentas e agir sobre dados coletados.  No portal de saudação, você pode aproveitar [pesquisas de log](log-analytics-log-searches.md) onde você pode criar consultas tooanalyze coletado dados, [painéis](log-analytics-dashboards.md) que você pode personalizar com exibições gráficas das pesquisas mais valiosas, e [soluções](log-analytics-add-solutions.md) que fornece ferramentas adicionais de análise e funcionalidade.

imagem de saudação abaixo é do portal do OMS Olá qual painel Olá mostra que exibe informações de resumo para Olá [soluções](#add-functionality-with-management-solutions) que estão instalados no espaço de trabalho de saudação.  Você pode clicar em qualquer toodrill lado a lado mais dados Olá para a solução.

![Portal do OMS](media/log-analytics-overview/portal.png)

Análise de log inclui um recuperar de tooquickly de linguagem de consulta e consolidar dados no repositório de saudação.  Você pode criar e salvar [pesquisas de Log](log-analytics-log-searches.md) toodirectly analisar dados no portal de saudação ou pesquisas de log executou automaticamente toocreate um alerta se Olá de consulta Olá indicar um critério importante.

![Pesquisa de log](media/log-analytics-overview/log-search.png)

tooget uma exibição gráfica rápida da integridade de saudação de todo o seu ambiente, você pode adicionar visualizações para log salvo pesquisas tooyour [painel](log-analytics-dashboards.md).   

![Painel](media/log-analytics-overview/dashboard.png)

Dados de pedidos tooanalyze fora de análise de Log, você pode exportar dados de saudação do repositório do OMS Olá em ferramentas como [Power BI](log-analytics-powerbi.md) ou Excel.  Você também pode aproveitar Olá [API de pesquisa de Log](log-analytics-log-search-api.md) toobuild soluções personalizadas que aproveitam os dados de análise de Log ou toointegrate com outros sistemas.

## <a name="add-functionality-with-management-solutions"></a>Adicionar funcionalidade com soluções de gerenciamento
[Soluções de gerenciamento](log-analytics-add-solutions.md) adicionar funcionalidade tooOMS, fornecendo dados adicionais e ferramentas de análise tooLog análise.  Eles também podem definir novos toobe de tipos de registro coletado que pode ser analisado com pesquisas de Log ou pela interface de usuário adicionais fornecidos pela solução de saudação no painel de saudação.  imagem de exemplo Hello abaixo mostra Olá [solução controle de alterações](log-analytics-change-tracking.md)

![Solução de Controle de Alterações](media/log-analytics-overview/change-tracking.png)

As soluções estão disponíveis para várias funções, e outras soluções são adicionadas constantemente.  Você pode navegar facilmente soluções disponíveis e [adicioná-los tooyour espaço de trabalho do OMS](log-analytics-add-solutions.md) da Galeria de soluções de saudação ou Azure Marketplace.  Muitas delas serão implantados automaticamente e começarão a funcionar imediatamente, enquanto outras podem exigir uma configuração moderada.

![Galeria de Soluções](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Componentes do Log Analytics
Em hello center de análise de Log é repositório do OMS Olá que está hospedado na nuvem do Azure de saudação.  Dados são coletados no repositório de saudação de fontes conectadas por configurar fontes de dados e Adicionar assinatura tooyour de soluções.  Soluções e fontes de dados irá criar diferentes tipos de registro que têm seu próprio conjunto de propriedades, mas ainda podem ser analisados no repositório de toohello de consultas.  Isso permite que você toouse Olá mesmo toowork de ferramentas e os métodos com diferentes tipos de dados coletado por fontes diferentes.

![Repositório do OMS](media/log-analytics-overview/overview.png)

Fontes conectadas são computadores hello e outros recursos que geram dados coletados pela análise de Log.  Isso pode incluir os agentes instalados em computadores [Windows](log-analytics-windows-agents.md) e [Linux](log-analytics-linux-agents.md) que se conectam diretamente ou agentes em um [grupo de gerenciamento do System Center Operations Manager conectado](log-analytics-om-agents.md).  Para os recursos do Azure, o Log Analytics coleta dados do [Azure Monitor e dos Diagnóstico do Azure](log-analytics-azure-storage.md).

[Fontes de dados](log-analytics-data-sources.md) são Olá diferentes tipos de dados coletados de cada origem conectada.  Isso inclui [eventos](log-analytics-data-sources-windows-events.md) e [dados de desempenho](log-analytics-data-sources-performance-counters.md) de [Windows](log-analytics-data-sources-windows-events.md) e agentes do Linux na adição toosources como [logs do IIS](log-analytics-data-sources-iis-logs.md)e [logs de texto personalizado](log-analytics-data-sources-custom-logs.md).  Configurar cada fonte de dados que você deseja toocollect, e a configuração de saudação é origem conectada tooeach entregue automaticamente.

Se você tem requisitos personalizados, você pode usar o hello [API do coletor de dados de HTTP](log-analytics-data-collector-api.md) toowrite repositório de toohello de dados de um cliente de API REST.

## <a name="log-analytics-architecture"></a>Arquitetura do Log Analytics
requisitos de implantação de saudação da análise de Log são mínimos, desde que os componentes de saudação central são hospedados em Olá nuvem do Azure.  Isso inclui o repositório de saudação nos serviços de toohello adição que permitem a você toocorrelate e analisar os dados coletados.  portal de saudação pode ser acessado em qualquer navegador, portanto não há nenhum requisito para o software cliente.

Você deve instalar agentes em computadores [Windows](log-analytics-windows-agents.md) e [Linux](log-analytics-linux-agents.md), mas nenhum agente adicional é necessário para computadores que já são membros de um [grupo de gerenciamento do SCOM conectado](log-analytics-om-agents.md).  Agentes SCOM continuará toocommunicate com servidores de gerenciamento que será encaminhada tooLog seus dados análise.  Embora algumas soluções exigirá toocommunicate agentes diretamente com a análise de Log.  documentação de saudação para cada solução especificará a seus requisitos de comunicação.

Ao [inscrever-se para o Log Analytics](log-analytics-get-started.md), você criará um espaço de trabalho do OMS.  Você pode pensar no espaço de trabalho hello como um ambiente de análise de Log exclusivo com seu próprio repositório de dados, fontes de dados e soluções. Você pode criar vários espaços de trabalho em sua assinatura toosupport vários ambientes, como produção e teste.

![Arquitetura do Log Analytics](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Próximas etapas
* [Inscreva-se para uma conta gratuita de análise de Log](log-analytics-get-started.md) tootest em seu próprio ambiente.
* Saudação de exibição diferente [fontes de dados](log-analytics-data-sources.md) dados toocollect disponíveis no repositório do OMS hello.
* [Procurar soluções disponíveis Olá Olá Galeria de soluções](log-analytics-add-solutions.md) tooadd funcionalidade tooLog análise.

