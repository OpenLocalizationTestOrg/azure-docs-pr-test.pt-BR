---
title: "aaaView dados analíticos de aplicativos Web do Azure | Microsoft Docs"
description: "Você pode usar informações de toogain de solução de análise de aplicativos da Web do Azure Olá sobre seus aplicativos da Web do Azure pela coleta de métricas diferentes entre todos os recursos do aplicativo Web do Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>Exibir dados analíticos de métricas entre todos os recursos do aplicativo Web do Azure

![Símbolo dos aplicativos Web](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Olá solução de análise de aplicativos da Web do Azure (visualização) fornece ideias sobre seus [aplicativos Web do Azure](../app-service-web/app-service-web-overview.md) coletando diferentes métricas em todos os recursos do aplicativo Web do Azure. Com a solução hello, analisar e pesquisar dados métrica de recursos de aplicativo web.

Usando Olá solução, você pode exibir o:

- Aplicativos Web superior com tempo de resposta mais alto Olá
- O número de solicitações em seus aplicativos Web, incluindo solicitações bem-sucedidas e com falha
- Os principais aplicativos Web com o tráfego de entrada e de saída mais alto
- Os principais planos de serviço com alta utilização de CPU e Memória
- Operações de log de atividades de aplicativos Web do Azure

## <a name="connected-sources"></a>Fontes conectadas

Ao contrário da maioria das outras soluções do Log Analytics, os dados não são coletados para os aplicativos Web do Azure por agentes. Todos os dados usados pela solução de saudação vem diretamente do Azure.

| Fonte Conectada | Suportado | Descrição |
| --- | --- | --- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Não | solução de saudação não coletará informações de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não | solução de saudação não coletará informações de agentes do Linux. |
| [Grupo de gerenciamento do SCOM](log-analytics-om-agents.md) | Não | solução de saudação não coletará informações de agentes em um grupo de gerenciamento do SCOM conectado. |
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | é a solução de saudação não coleção de informações do armazenamento do Azure. |

## <a name="prerequisites"></a>Pré-requisitos

- tooaccess informações de medição de recursos do aplicativo Web do Azure, você deve ter uma assinatura do Azure.

## <a name="configuration"></a>Configuração

Execute Olá solução de análise de aplicativos da Web do Azure de saudação etapas tooconfigure para seus espaços de trabalho a seguir.

1. Habilitar a solução de análise de aplicativos da Web do Azure de saudação do [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. [Habilitar tooOMS de log de métricas de recurso do Azure usando o PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

Olá solução de análise de aplicativos da Web do Azure coleta dois conjuntos de métricas do Azure:

- Métricas de aplicativos Web do Azure
  - Conjunto de Trabalho de Memória Média
  - Tempo Médio de Resposta
  - Bytes recebido s/enviados
  - Tempo de CPU
  - Solicitações
  - Conjunto de Trabalho de Memória
  - Httpxxx
- Métricas do Plano do Serviço de Aplicativo
  - Bytes recebido s/enviados
  - Percentual de CPU
  - Tamanho da fila do disco
  - Tamanho da Fila de Http
  - Porcentagem de Memória

As métricas do Plano do Serviço de Aplicativo serão coletadas apenas se você estiver usando um plano de serviço dedicado. Isso não se aplica a toofree ou compartilhado planos de serviço de aplicativo.

Se você adicionar a solução hello usando o portal do OMS Olá, você verá a seguir Olá lado a lado. É necessário muito[habilitar tooOMS de log de métricas de recurso do Azure usando o PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

![Notificação Executando a Avaliação](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

Depois de configurar a solução hello, dados devem iniciar fluxo de trabalho tooyour dentro de 15 minutos.

## <a name="using-hello-solution"></a>Usando a solução de saudação

Quando você adiciona o espaço de trabalho tooyour solução de análise de aplicativos da Web do Azure de hello, Olá **análise de aplicativos da Web do Azure** bloco é adicionado o painel de visão geral de tooyour. Este bloco exibe uma contagem do número de saudação de aplicativos Web do Azure que solução Olá tem acesso tooin sua assinatura do Azure.

![Bloco Análise de Aplicativos Web do Azure](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Exibir informações do Análise de Aplicativos Web do Azure

Clique em Olá **análise de aplicativos da Web do Azure** bloco tooopen Olá **análise de aplicativos da Web do Azure** painel. painel Olá inclui folhas Olá Olá a tabela a seguir. Cada folha lista os itens tooten correspondência critérios da folha de saudação especificado escopo e tempo de intervalo. Você pode executar uma pesquisa de log que retorna todos os registros clicando **ver todos os** na parte inferior da folha de saudação ou clicando o cabeçalho de folha de saudação do hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| Coluna | Descrição |
| --- | --- |
| Aplicativos Web do Azure |   |
| Tendências de Solicitações de Aplicativos Web | Mostra um gráfico de linha de saudação tendência de solicitação de aplicativos Web hello intervalo de datas selecionado e mostra uma lista de solicitações de web dez principais da saudação. Clique em toorun de gráfico de linha hello uma pesquisa de log para<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>Clique em um toorun de item de solicitação da web para Olá web solicitação métrica tendência que solicitam uma pesquisa de log. |
| Tempo de Resposta de Aplicativos Web | Mostra um gráfico de linha de tempo de resposta de aplicativos Web Olá Olá intervalo de datas que você selecionou. Também mostra uma lista de uma lista de saudação resposta de aplicativos Web de superior dez vezes. Clique em Olá gráfico toorun uma pesquisa de log para<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> Clique em um aplicativo Web toorun uma pesquisa de log retornando tempos de resposta Olá aplicativo Web. |
| Tráfego de aplicativos Web | Mostra um gráfico de linhas para o tráfego de aplicativos Web, em MB e lista superior Olá tráfego de aplicativos Web. Clique em Olá gráfico toorun uma pesquisa de log para<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> Ele mostra todos os aplicativos Web com tráfego Olá último minuto. Clique em toorun um aplicativo Web, uma pesquisa de log mostrando bytes recebidos e enviados para Olá aplicativo Web. |
| Planos do Serviço de Aplicativo do Azure |   |
| Planos de Serviço de Aplicativo com utilização de CPU &gt; 80% | Mostra o número total de saudação do aplicativo planos de serviço com a utilização de CPU maior do que 80% e listas Olá 10 principais planos de serviço de aplicativo por utilização da CPU. Clique em Olá área total toorun uma pesquisa de log para<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> Ela mostra uma lista de seus Planos do Serviço de Aplicativo e sua utilização da CPU média. Clique em um plano de serviço de aplicativo toorun uma pesquisa de log, mostrando a utilização média da CPU. |
| Planos de Serviço de Aplicativo com utilização de memória &gt; 80% | Mostra o número total de saudação do aplicativo planos de serviço com a utilização de memória maior do que 80% e listas Olá 10 principais planos de serviço de aplicativo por utilização de memória. Clique em Olá área total toorun uma pesquisa de log para<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> Ela mostra uma lista de seus Planos do Serviço de Aplicativo e sua utilização da memória média. Clique em um plano de serviço de aplicativo toorun uma pesquisa de log, mostrando o uso médio de memória. |
| Logs de Atividades de Aplicativos Web do Azure |   |
| Auditoria de Atividades de Aplicativos Web do Azure | Mostra Olá número total de aplicativos Web com [logs de atividade](log-analytics-activity.md) e listas Olá operações de log de atividade de 10 principais. Clique em Olá área total toorun uma pesquisa de log para<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> Ele mostra uma lista de saudação operações de log de atividade. Clique em um toorun de operação de log de atividade uma pesquisa de log que lista os registros de saudação para operação de saudação. |



### <a name="azure-web-apps"></a>Aplicativos Web do Azure 

No painel de saudação, você pode fazer drill down tooget mais aprofundado sobre suas métricas de aplicativos Web. Esse primeiro conjunto de folhas mostrar a tendência Olá Olá solicitações de aplicativos Web, número de erros (por exemplo, HTTP404), o tráfego e o tempo médio de resposta ao longo do tempo. Ele também mostra uma análise dessas métricas para diferentes aplicativos Web.

![Folhas de aplicativos Web do Azure](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

O principal motivo para a exibição de dados é para que você pode identificar um aplicativo Web com tempo de resposta e investigar a causa de saudação toofind. Um limite também é aplicado toohelp é que mais fácil de identificar Olá aqueles com problemas.

- Aplicativos Web mostrados em vermelho têm tempo de resposta maior do que 1 segundo.
- Aplicativos Web mostrados em laranja têm um tempo de resposta superior a 0,7 segundo e menor de 1 segundo.
- Aplicativos Web mostrados em verde têm um tempo de resposta menor que 0,7 segundo.

Olá imagem de exemplo de pesquisa de log a seguir, você pode ver que Olá *anugup3* aplicativo web tinha um tempo de resposta muito maior de Olá outros aplicativos da web.

![exemplo de pesquisa de logs](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>Planos de serviço de aplicativo

Se estiver usando Planos de Serviço dedicados, você também poderá coletar métricas para seus Planos do Serviço de Aplicativo. Nessa exibição, você vê os Planos do Serviço de Aplicativo com alta utilização de CPU ou memória (&gt; 80%). Ele também mostra Olá principais serviços de aplicativos com alta utilização de CPU ou memória. Da mesma forma, um limite é aplicado toohelp é que mais fácil de identificar Olá aqueles com problemas.

- Planos do Serviço de Aplicativo mostrados em vermelho têm uma utilização de CPU/memória maior do que 80%.
- Planos do Serviço de Aplicativo mostrados em laranja têm uma utilização de CPU/memória maior do que 60% e menor do que 80%.
- Planos do Serviço de Aplicativo mostrados em verde têm uma utilização de CPU/memória menor do que 60%.

![Folhas de Planos do Serviço de Aplicativo do Azure](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Pesquisas de logs de aplicativos Web do Azure

Olá **lista de populares do Azure Web Apps consultas de pesquisa** mostra todos os Olá relacionados a logs de atividade para aplicativos Web, que fornece informações sobre operações de saudação que foram executadas em seus recursos de aplicativos Web. Ela também lista todas as operações e número de saudação de vezes em que ocorreram relacionadas a saudação.

Usando qualquer uma das consultas de pesquisa de log hello como ponto de partida, você pode criar facilmente um alerta. Por exemplo, convém toocreate um alerta quando o tempo de resposta médio da métrica é maior que a cada segundo.

## <a name="next-steps"></a>Próximas etapas

- Criar um [alerta](log-analytics-alerts-creating.md) para uma métrica específica.
- Use [pesquisa de Log](log-analytics-log-searches.md) tooview obter informações de seus logs de atividade.
