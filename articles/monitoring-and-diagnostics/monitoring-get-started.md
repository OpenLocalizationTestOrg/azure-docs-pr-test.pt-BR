---
title: "aaaGet de Introdução ao Monitor do Azure | Microsoft Docs"
description: "Começar a usar o Monitor do Azure toogain percepção da operação de saudação de seus recursos e tomar medidas baseadas nos dados."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Introdução ao Azure Monitor
Monitor do Azure é o serviço de plataforma de saudação que fornece uma única fonte para monitorar os recursos do Azure. Monitor do Azure, você pode visualizar, consultar, encaminhar, arquivar e executar ações sobre métricas hello e logs vindos de recursos no Azure. Você pode trabalhar com esses dados usando a folha de portal de Monitor hello, [Cmdlets do PowerShell Monitor](insights-powershell-samples.md), [CLI de plataforma cruzada](insights-cli-samples.md), ou [APIs de REST do Azure Monitor](https://msdn.microsoft.com/library/dn931943.aspx). Neste artigo, mostramos alguns dos principais componentes de saudação do Monitor do Azure, usando o portal de saudação para demonstração.

1. No portal de hello, navegue até muito**mais serviços** e localize Olá **Monitor** opção. Clique em Olá ícone de estrela tooadd lista de favoritos de tooyour essa opção para que sempre é facilmente acessível a partir da barra de navegação do lado esquerdo de saudação.
   
    ![Monitorar na lista de serviços de saudação](./media/monitoring-get-started/monitor-more-services.png)
2. Clique em Olá **Monitor** tooopen opção backup Olá **Monitor** folha. Esta folha reúne todas as suas configurações e dados de monitoramento em uma exibição consolidada. Ele é aberto pela primeira vez toohello **log de atividades** seção.
   
    ![Navegação da folha Monitor](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Monitor do Azure tem três categorias básicas de dados de monitoramento: Olá **log de atividades**, **métricas**, e **logs de diagnóstico**.
3. Clique em **log de atividades** tooensure que Olá seção de log da atividade é exibida.
   
    ![Folha Log de Atividades](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    Olá [ **log de atividades** ](monitoring-overview-activity-logs.md) descreve todas as operações executadas em recursos na sua assinatura. Usando hello atividade de Log, você pode determinar Olá ', quem e quando ' para qualquer criar, atualizar ou excluir operações nos recursos em sua assinatura. Por exemplo, hello atividade de Log informa quando um aplicativo web foi interrompido e que o interrompeu. Eventos de Log de atividade é armazenado na plataforma de saudação e tooquery disponível por 90 dias.
   
    Você pode criar e salvar consultas para filtros comuns e pin hello mais importantes consultas tooa painel do portal para que você sempre saiba se ocorreram eventos que atendem aos seus critérios.
4. Filtrar Olá exibição tooa determinado grupo de recursos sobre Olá última semana, clique em Olá **salvar** botão.
   
    ![Salvar consulta do log de atividades](./media/monitoring-get-started/monitor-act-log-save.png)
5. Agora, clique em Olá **Pin** botão.
   
    ![Clicar para fixar o log de atividades](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    A maioria das exibições de saudação neste passo a passo pode ser fixado tooa painel. Isso ajuda a criar uma única fonte de informações para os dados operacionais em seus serviços. 
6. Painel de retorno tooyour. Agora você pode ver que a consulta hello (e o número de resultados) são exibidos no painel. Isso é útil se você quiser que as ações de Destaque que ocorreram recentemente em sua assinatura, por exemplo, consulte tooquickly. se uma nova função foi atribuída ou uma VM foi excluída.
   
    ![Atividade log fixado toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. Retornar toohello **Monitor** lado a lado e clique em Olá **métricas** seção. É necessário primeiro tooselect um recurso de filtragem e selecionando usando Olá suspenso opções na parte superior de saudação da folha de saudação.
   
    ![Recurso de filtro para métricas](./media/monitoring-get-started/monitor-met-filter.png)
   
    Todos os recursos do Azure emitem [**métricas**](monitoring-overview-metrics.md). Essa exibição reúne todas as métricas em um único painel para que você possa compreender facilmente como os recursos estão sendo executados.
8. Depois que você tiver selecionado um recurso, todas as métricas disponíveis aparecem na Olá lado esquerdo da folha de saudação. Você pode várias métricas de gráfico ao mesmo tempo selecionando métricas e modificar o intervalo de tipo e a hora do gráfico de saudação. Também pode exibir todos os alertas de métrica definidos nesse recurso.
   
    ![Lâmina Métrica](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > Algumas métricas só estão disponíveis habilitando o [Application Insights](../application-insights/app-insights-overview.md) e/ou o Windows ou o Linus Azure Diagnostics em seu recurso.
   > 
   > 
9. Quando estiver satisfeito com seu gráfico, você pode usar o hello **Pin** botão toopin-tooyour painel.
10. Retornar toohello **Monitor** folha e clique em **logs de diagnóstico**.
    
    ![Folha Logs de Diagnóstico](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**Logs de diagnóstico** ](monitoring-overview-of-diagnostic-logs.md) são logs emitidos *por* um recurso que fornecem dados sobre a operação de saudação do recurso específico. Por exemplo, os Contadores de Regras do Grupo de Segurança da Rede e os Logs do Fluxo de Trabalho do Aplicativo Lógico são dois tipos de logs de diagnóstico. Esses logs podem ser armazenados em uma conta de armazenamento, fluxo tooan Hub de eventos, e/ou enviados[análise de Log](../log-analytics/log-analytics-overview.md). O Log Analytics é um produto de inteligência operacional da Microsoft para pesquisa avançada e alertas.
    
    No portal de saudação, você pode exibir e filtrar uma lista de todos os recursos em sua assinatura tooidentify se eles tiverem logs de diagnóstico habilitado.
11. Clique em um recurso na folha de logs de diagnóstico de saudação. Se os logs de diagnóstico estiverem sendo armazenados em uma conta de armazenamento, você verá uma lista dos registros por hora que podem ser baixados diretamente.
    
    ![Logs de diagnóstico para um recurso](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    Você também pode clicar em **configurações de diagnóstico**, que permite que você tooset até ou modificar as configurações para a conta de armazenamento de arquivamento tooa tooEvent Hubs de streaming ou envio de espaço de trabalho de análise de Log tooa.
    
    ![Habilitar logs de diagnóstico](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    Se você configurar logs de diagnóstico tooLog análise, em seguida, você pode pesquisá-los na Olá **pesquisa de Log** seção do portal de saudação.
12. Navegue toohello **alertas** seção da folha de Monitor de saudação.
    
    ![folha de alertas para o público](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    Aqui, você pode gerenciar todos os [**alertas**](monitoring-overview-alerts.md) nos recursos do Azure. Isso inclui alertas sobre as métricas, eventos do log de atividades, testes da Web do Application Insights (Locais) e diagnóstico proativo do Application Insights. Alertas podem acionar um toobe de email enviada ou uma URL de webhook tooa HTTP POST.
13. Clique em **adicionar alerta métrica** toocreate um alerta.
    
    ![Adicionar alerta da métrica](./media/monitoring-get-started/monitor-alerts-add.png)
    
    Você pode fixar um tooeasily do painel alerta tooyour ver seu estado a qualquer momento.
14. Olá seção Monitor também inclui links muito[Application Insights](../application-insights/app-insights-overview.md) aplicativos e [análise de Log](../log-analytics/log-analytics-overview.md) soluções de gerenciamento. Esses outros produtos da Microsoft têm uma profunda integração com o Azure Monitor.
15. Se você não estiver usando o Application Insights nem o Log Analytics, as chances são de que o Azure Monitor tem uma parceria com o monitoramento, log e alerta de produtos atuais. Consulte nossa [página parceiros](monitoring-partners.md) para uma lista completa e instruções sobre como toointegrate.

Seguindo estas etapas e fixar um painel de tooa todos os blocos relevantes, você pode criar exibições detalhadas de seu aplicativo e a infraestrutura como este:

![Painel do Azure Monitor](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Próximas etapas
* Saudação de leitura [visão geral do Monitor do Azure](monitoring-overview.md)

