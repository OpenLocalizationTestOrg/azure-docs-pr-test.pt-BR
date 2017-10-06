---
title: "soluções de gerenciamento do Azure Log Analytics aaaAdd | Microsoft Docs"
description: "As soluções de gerenciamento do Log Analytics / OMS (Operations Management Suite) são uma coleção de lógica, visualização e regras de aquisição de dados que fornecem as métricas que giram em torno de uma área de problema específica."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Adicionar espaço de trabalho tooyour soluções de gerenciamento de análise de logs do Azure

As soluções do Log Analytics são uma coleção de **lógica**, **visualização** e **regras de aquisição de dados** que fornecem as métricas que giram em torno de uma área de problema específica. Este artigo lista as soluções de gerenciamento de análise de Log com suporte e mostra como tooadd e remoção de um espaço de trabalho usando Olá portal do Azure. Você também pode adicionar soluções no portal do OMS hello usando a Galeria de soluções de saudação.

As soluções de gerenciamento permitem análises mais profundas em relação ao seguinte:

* Ajudar a investigar e a resolver problemas operacionais com mais rapidez
* Coletar e correlacionar vários tipos de dados de computador
* Ajudá-lo a ser proativo com atividades que expõe solução hello.

> [!NOTE]
> Análise de log inclui a funcionalidade de pesquisa de Log, portanto, você não precisa tooinstall um tooenable de solução de gerenciamento-lo. No entanto, obter ideias, pesquisas sugeridas e visualizações de dados, adicionando o espaço de trabalho do gerenciamento de soluções tooyour.

Usando este artigo, você adiciona gerenciamento soluções tooa espaço de trabalho usando Olá portal do Azure Marketplace. Depois que você tiver adicionado uma solução, os dados são coletados dos servidores de saudação em sua infraestrutura e enviados toohello serviço do OMS. Processamento pelo Olá serviço OMS geralmente leva a hora de tooan alguns minutos. Depois que o serviço de saudação processa dados hello, você pode exibi-lo no OMS.

Você pode facilmente remover uma solução de gerenciamento quando ela não for mais necessária. Quando você remove uma solução de gerenciamento, seus dados não são enviados tooOMS. Se você estiver usando Olá livre de preço, a remoção de uma solução pode reduzir a quantidade de Olá dos dados usados, ajudando você a permanecer em cota diária de dados.

## <a name="view-available-management-solutions"></a>Exiba as soluções de gerenciamento disponíveis

Olá, marketplace do Azure contém Olá lista de [soluções de gerenciamento de análise de Log](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Você pode instalar as soluções de gerenciamento do Azure marketplace clicando Olá **obtê-lo agora** link na parte inferior da saudação de cada solução.

## <a name="add-a-management-solution"></a>Adicionar uma solução de gerenciamento
1. Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com) usando sua assinatura do Azure.
2. Em Olá **novo** folha sob **Marketplace**, selecione **monitoramento + gerenciamento**.
3. Em Olá **monitoramento + gerenciamento** folha, clique em **ver todos os**.  
    ![Folha Monitoramento + gerenciamento](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello à direita do **soluções de gerenciamento de**, clique em **mais**.
5. Em Olá **soluções de gerenciamento** folha, selecione uma solução de gerenciamento que você deseja que o espaço de trabalho do tooadd tooa.  
    ![Folha Monitoramento + gerenciamento](./media/log-analytics-add-solutions/management-solutions.png)  
6. Na folha de solução de gerenciamento Olá, revise as informações sobre solução de gerenciamento de saudação e, em seguida, clique em **criar**.
7. Em Olá *nome de solução de gerenciamento* folha, selecione um espaço de trabalho que você deseja tooassociate com solução de gerenciamento de saudação.
8. Opcionalmente, altere as configurações de espaço de trabalho para Olá assinatura do Azure, o grupo de recursos e o local. Você também pode escolher **Opções de automação**. Clique em **Criar**.  
    ![espaço de trabalho da solução](./media/log-analytics-add-solutions/solution-workspace.png)  
9. toostart usando Olá solução de gerenciamento que você adicionou tooyour o espaço de trabalho, navegue muito**análise de Log** > **assinaturas** > ***nome do espaço de trabalho ***  >  **Visão geral**. Um novo bloco aparece para a solução de gerenciamento. Clique em Olá bloco tooopen-lo e começar a usar a solução de saudação após a coleta de dados para a solução de saudação.

## <a name="remove-a-management-solution"></a>Remover uma solução de gerenciamento

1. Em Olá [portal do Azure](https://portal.azure.com), navegue muito**análise de Log** > **assinaturas** > ***nome do espaço de trabalho*** e, em seguida, em Olá ***nome do espaço de trabalho*** folha, clique em **soluções**.
2. Na lista de saudação de soluções de gerenciamento, selecione solução Olá que você deseja tooremove.
3. Na folha de solução de saudação para seu espaço de trabalho, clique em **excluir**.  
    ![excluir solução](./media/log-analytics-add-solutions/solution-delete.png)  
4. Na caixa de diálogo de confirmação de saudação, clique em **Sim**.

## <a name="offers-and-pricing-tiers"></a>Ofertas e tipos de preços

Olá, a tabela a seguir identifica quais soluções de gerenciamento pertencem a oferta do tooeach Operations Management Suite.
tabela Olá também identifica Olá camadas que estão disponíveis para cada solução de gerenciamento de preços.
Todas as soluções em Olá a tabela a seguir estão disponíveis no hello Azure Galeria de soluções de portal e hello no portal de análise de Log de saudação.

| Solução de gerenciamento                                                                       | Oferta                                                                     | Tipos de preço<sup>1</sup>                                                 | Observações |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Log Analytics de Atividade](log-analytics-activity.md)                                                                   | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | 90 dias de dados estão disponíveis gratuitamente<br>Dados da entidade não toohello cap de camada gratuita |
| [Avaliação do AD](log-analytics-ad-assessment.md)                                           | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Status de replicação do AD](log-analytics-ad-replication-status.md)                           | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | Tooadd não está disponível no portal do Azure/marketplace. |
| [Integridade do Agente](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | Dados da entidade não toohello cap de camada gratuita<br> Tooadd não está disponível no portal do Azure/marketplace. |
| [Gerenciamento de alertas](log-analytics-solution-alert-management.md)                            | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | Tooadd não está disponível no portal do Azure/marketplace. |
| [Conector do Application Insights (versão prévia)](log-analytics-app-insights-connector.md)                                               | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Hybrid Worker de Automação](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automação e Controle</li></ul>                                  | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe vinculado de espaço de trabalho de análise de Log conta de automação |
| [Análise de Gateway de Aplicativo do Azure](log-analytics-azure-networking-analytics.md)    | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Análise de Grupo de Segurança de Rede do Azure](log-analytics-azure-networking-analytics.md)     | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Azure SQL Analytics (Visualização)](log-analytics-azure-sql.md)                                                       | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br>Por&nbsp;Nó&nbsp;(OMS)                                                                          | Requer o tooan de toobe vinculado de espaço de trabalho de análise de Log conta de automação|
| [Análise de Aplicativos Web do Azure](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
|[Backup](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)                                                                       | Requer um cofre de Backup clássico.<br> Tooadd não está disponível no portal do Azure/marketplace. |
| [Capacidade e Desempenho (versão prévia)](log-analytics-capacity.md)                                                   | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Controle de alterações](log-analytics-change-tracking.md)                                       | <ul><li>Automação e Controle</li></ul>                                  | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe vinculado de espaço de trabalho de análise de Log conta de automação |
| [Contêineres](log-analytics-containers.md)                                                 | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Conector de Gerenciamento do Serviço de TI (versão prévia)](log-analytics-itsmc-overview.md)                                              | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)     | |
| Monitoramento do HDInsight HBase <br>(Visualização)                                                  | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Análise do Cofre de Chaves](log-analytics-azure-key-vault.md)                   | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Aplicativos Lógicos B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | Tooadd não está disponível no portal do Azure/marketplace. |
| [Avaliação de malware](log-analytics-malware.md)                                            | <ul><li>Segurança e Conformidade</li></ul>                                 | Grátis<br> Autônomo<br>Por&nbsp;Nó&nbsp;(OMS)                                                                           | Se você adicionar soluções de segurança e conformidade Olá após 19 de junho de 2017 [a cobrança é por nó](https://azure.microsoft.com/pricing/details/security-compliance/), independentemente do espaço de trabalho de saudação de preço. Olá a primeira 60 dias são gratuitos.  |
| [Monitor de Desempenho de Rede](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Insight and Analytics</li></ul>                                   | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)                                                                         | |
| [Análise do Office 365 (versão prévia)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Segurança e Auditoria](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Segurança&nbsp;e&nbsp;Conformidade</li></ul>                       | Grátis<br> Autônomo<br>Por&nbsp;Nó&nbsp;(OMS)                                                                           | Coletar logs de eventos de segurança requer que esta solução<br>Se você adicionar soluções de segurança e conformidade Olá após 19 de junho de 2017 [a cobrança é por nó](https://azure.microsoft.com/pricing/details/security-compliance/), independentemente do espaço de trabalho de saudação de preço. Olá a primeira 60 dias são gratuitos. |
| [Análise do Service Fabric (visualização)](log-analytics-service-fabric.md)                     | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Mapa do Serviço (versão prévia)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Insight and Analytics</li></ul>                      | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)                                                                         | Disponível no Leste dos EUA, na Europa Ocidental e no EUA Central    |
| [Recuperação de Site](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Insight and Analytics</li></ul>                                   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)                                                                       | Requer um cofre clássico do Site Recovery.<br> Tooadd não está disponível no portal do Azure/marketplace. |
| [Avaliação do SQL](log-analytics-sql-assessment.md)                                         | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| Iniciar/Parar VMs durante os horários inativos<br>(Visualização)                                              | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe vinculado de espaço de trabalho de análise de Log conta de automação |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | Tooadd não está disponível no portal do Azure/marketplace. |
| [Avaliação do System Center Operations Manager (versão prévia)](log-analytics-scom-assessment.md)  | <ul><li>Insight and Analytics</li><li>Log Analytics</li></ul>        | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Gerenciamento de atualizações](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automação e Controle</li></ul>                                  | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)                                                                         | Requer o tooan de toobe vinculado de espaço de trabalho de análise de Log conta de automação |
| [Conformidade de Atualizações (versão prévia)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | Sem encargos para dados ou nós<br>Dados da entidade não toohello cap de camada gratuita.<br> Tooadd não está disponível no portal do Azure/marketplace. |
| [Preparação para atualização](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | Sem encargos para dados ou nós<br>Dados da entidade não toohello cap de camada gratuita.<br> Tooadd não está disponível no portal do Azure/marketplace. |
| [Monitoramento do VMware (visualização)](log-analytics-vmware.md)                                | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Standard<br> Premium&nbsp;(OMS)<br> Por&nbsp;GB&nbsp;(Autônomo)<br> Por&nbsp;Nó&nbsp;(OMS)   | |
| [Wire Data 2.0 (versão prévia)](log-analytics-wire-data.md)                                                                 | <ul><li>Insight and Analytics</li></ul>                                   | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)                                                                         | Disponível no Leste dos EUA, na Europa Ocidental e no EUA Central |

<sup>1</sup> Olá *padrão* e *Premium (OMS)* camadas de preços estão disponíveis apenas para os clientes que criou sua análise de Log espaço de trabalho anterior tooSeptember 21, 2016.

### <a name="community-provided-management-solutions"></a>Soluções de gerenciamento fornecidas pela comunidade

Estão disponíveis soluções de comunidade fornecida da saudação [Galeria de modelos do Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) e direto de autores hello.

| Solução de gerenciamento               | Oferta                                                                     | Tipos de preço                         | Observações |
| ---                               | ---                                                                       | ---                                   | ---   |
| Todas as soluções fornecidas pela comunidade  | <ul><li>Insight&nbsp;e&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Grátis<br> Por&nbsp;Nó&nbsp;(OMS)     |   Requer o tooan de toobe vinculado de espaço de trabalho de análise de Log conta de automação |




## <a name="data-collection-details"></a>Detalhes da coleta de dados
Olá tabelas a seguir mostram os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para as fontes de dados e soluções de gerenciamento análise de Log. Olá tabelas são categorizadas por ofertas de solução, que são iguais muito[assinatura camadas de preços](https://go.microsoft.com/fwlink/?linkid=827926). Olá solução de análise de Log de atividade é tooall disponível gratuitamente de camadas de preços.

Olá agente do Windows de análise de Log e o System Center Operations Manager agent são essencialmente Olá mesmo. agente do Windows Hello inclui funcionalidades adicionais tooallow-tooconnect toohello OMS rota através de um proxy e o espaço de trabalho. Se você usar um agente do Operations Manager, ele deve ser direcionado como um toocommunicate de agente do OMS com o OMS. Agentes do Operations Manager nesta tabela são agentes do OMS que são conectados tooOperations Manager. Consulte [tooLog conectar o Operations Manager análise](log-analytics-om-agents.md) para obter informações sobre como conectar seu tooOMS de ambiente existente do Operations Manager.

> [!NOTE]
> tipo de saudação do agente que você usa determina como dados são enviados tooOMS, com hello condições a seguir:
> - Você usar um agente do OMS anexados ao Operations Manager ou o agente do Windows hello.
> - Quando o Operations Manager é necessário, dados de agente do Operations Manager para solução de saudação é sempre enviados tooOMS usando o grupo de gerenciamento do Operations Manager hello. Além disso, quando é necessário o Operations Manager, agente do Operations Manager de saudação somente é usado pela solução de saudação.
> - Quando o Operations Manager não é necessário e tabela Olá mostra que os dados do agente do Operations Manager são enviados tooOMS usando o grupo de gerenciamento hello, dados de agente do Operations Manager é sempre enviada tooOMS usando grupos de gerenciamento. Ignorar o grupo de gerenciamento de saudação de agentes do Windows e enviar seus dados tooOMS diretamente.
> - Quando dados de agente do Operations Manager não são enviados com o uso de um grupo de gerenciamento, Olá os dados são enviados diretamente tooOMS, ignorando o grupo de gerenciamento de saudação.

### <a name="insight--analytics--log-analytics"></a>Insight e Analytics / Log Analytics

| Solução de gerenciamento | Plataforma | Agente de monitoramento da Microsoft | Agente do Operations Manager | Armazenamento do Azure | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | Frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Log Analytics de Atividade | As tabelas |   |   |   |   |   | após a notificação |
| Avaliação do AD |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dias |
| Status de replicação do AD |Windows |&#8226; |&#8226; |  |  |&#8226; |5 dias |
| Integridade do agente | Windows e Linux | &#8226; | &#8226; |   |   | &#8226; | 1 minuto |
| Gerenciamento de Alertas (Nagios) |Linux |&#8226; |  |  |  |  |na chegada |
| Gerenciamento de Alertas (Zabbix) |Linux |&#8226; |  |  |  |  |1 minuto |
| Gerenciamento de alertas (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 minutos |
| Conector do Application Insights (visualização) | As tabelas |   |   |   |   |   | após a notificação |
| Análise de Gateway de Aplicativo do Azure | As tabelas |   |   |   |   |   | após a notificação |
| Análise de Grupo de Segurança de Rede do Azure | As tabelas |   |   |   |   |   | após a notificação |
| Azure SQL Analytics (Visualização) |Windows |  |  |  |  |  | 10 minutos |
| Gerenciamento de Capacidade |Windows |&#8226; |&#8226; |  |  |&#8226; |na chegada |
| Contêineres | Windows e Linux | &#8226; | &#8226; |   |   |   | 3 minutos |
| Análise do Cofre de Chaves |Windows |  |  |  |  |  |após a notificação |
| Monitor de Desempenho de Rede | Windows | &#8226; | &#8226; |   |   |   | Handshakes TCP a cada cinco segundos; dados enviados a cada três minutos |
| Análise do Office 365 (visualização) |Windows |  |  |  |  |  |após a notificação |
| Análise do Service Fabric |Windows |  |  |&#8226; |  |  |5 minutos |
| Mapa do Serviço | Windows e Linux | &#8226; | &#8226; |   |   |   | 15 s |
| Avaliação do SQL |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dias |
| SurfaceHub |Windows |&#8226; |  |  |  |  |na chegada |
| System Center Operations Manager Assessment (Visualização) | Windows | &#8226; | &#8226; |   |   | &#8226; | sete dias |
| Análise de atualização (visualização) | Windows | &#8226; |   |   |   |   | 2 dias |
| Monitoramento de VMware (visualização) | Linux | &#8226; |   |   |   |   | 3 minutos |
| Dados durante a transmissão |Windows (2012 R2/8.1 ou posterior) |&#8226; |&#8226; |  |  |  | 1 minuto |


### <a name="automation--control"></a>Automação e Controle

| Solução de gerenciamento | Plataforma | Agente de monitoramento da Microsoft | Agente do Operations Manager | Armazenamento do Azure | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | Frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Hybrid Worker de AutomaçãoWorker | Windows | &#8226; | &#8226; |   |   |   | n/d |
| Controle de Alterações |Windows |&#8226; |&#8226; |  |  |&#8226; |por hora |
| Controle de Alterações |Linux |&#8226; |  |  |  |  |por hora |
| Gerenciamento de atualizações | Windows |&#8226; |&#8226; |  |  |&#8226; |pelo menos, 2 vezes por dia e 15 minutos após a instalação de uma atualização |

### <a name="security--compliance"></a>Segurança e conformidade

| Solução de gerenciamento | Plataforma | Agente de monitoramento da Microsoft | Agente do Operations Manager | Armazenamento do Azure | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | Frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Avaliação antimalware |Windows |&#8226; |&#8226; |  |  |&#8226; |por hora |
| Segurança e Auditoria<sup>1</sup> | Windows e Linux | parcial | parcial | parcial |   | parcial | vários |

<sup>1</sup> Olá segurança e solução de auditoria pode coletar logs de agentes do Operations Manager, Windows e Linux. Confira [Fontes de dados](#data-sources) para obter informações de coleta de dados sobre:

- syslog
- Logs de eventos de segurança do Windows
- Logs do firewall do Windows
- Logs de eventos do Windows



### <a name="protection--recovery"></a>Proteção e recuperação

| Solução de gerenciamento | Plataforma | Agente de monitoramento da Microsoft | Agente do Operations Manager | Armazenamento do Azure | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | Frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Backup | As tabelas |   |   |   |   |   | n/d |
| Azure Site Recovery | As tabelas |   |   |   |   |   | n/d |


### <a name="data-sources"></a>Fontes de dados


| Fonte de dados | Plataforma | Agente de monitoramento da Microsoft | Agente do Operations Manager | Armazenamento do Azure | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | Frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Logs de atividade do Azure |Windows |  |  |  |  |  |após a notificação |
| Logs de Diagnóstico do Azure |Windows |  |  |  |  |  |após a notificação |
| Métricas de Diagnóstico do Azure |Windows |  |  |  |  |  |após a notificação |
| ETW |Windows |  |  |&#8226; |  |  |5 minutos |
| Logs IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minutos |
| Contadores de desempenho |Windows |&#8226; |&#8226; |  |  |  |conforme agendado, mínimo de 10 segundos |
| Contadores de desempenho |Linux |&#8226; |  |  |  |  |conforme agendado, mínimo de 10 segundos |
| syslog |Linux |&#8226; |  |  |  |  |do armazenamento do Azure: 10 minutos; do agente: na chegada |
| Logs de eventos de segurança do Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |para o armazenamento do Azure: 10 min; para o agente de saudação: na chegada |
| Logs do firewall do Windows |Windows |&#8226; |&#8226; |  |  |  |na chegada |
| Logs de eventos do Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |para o armazenamento do Azure: 10 min; para o agente de saudação: na chegada |



## <a name="preview-management-solutions-and-features"></a>Visualizar soluções e recursos de gerenciamento
Executando um serviço e devops práticas a seguir, somos capaz toopartner com clientes toodevelop recursos e soluções.

Durante a visualização privada, podemos dar um pequeno grupo de clientes acesso tooan antecipado implementação dos comentários de toogain de recurso ou solução hello e melhorias. Essa implementação antecipada tem recursos e funcionalidades operacionais mínimas.

Nosso objetivo é tootry coisas rapidamente para que possa encontrar o que funciona e o que não funciona. Podemos iterar por esse processo até que os comentários de saudação de clientes de visualização privada Olá informam que estamos prontos para visualização pública.

Durante a visualização pública do hello, podemos disponibilizar Olá recursos ou as soluções para tooget de todos os usuários mais comentários e validar nossa dimensionamento e a eficiência. Durante essa fase:

* Recursos de visualização aparecem na guia Configurações de saudação e podem ser habilitados por qualquer usuário.
* Soluções de visualização são adicionadas por meio da Galeria de saudação ou usando um script.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>O que devo saber sobre Recursos e Soluções em visualização?
Estamos felizes sobre novos recursos e soluções de gerenciamento e amamos trabalhar com você toodevelop-los.

Soluções e recursos de visualização não são para todas as pessoas. Antes de solicitar toojoin uma visualização privada ou habilitar uma visualização pública, certifique-se de Okey estiver trabalhando com algo que está em desenvolvimento.

Ao habilitar um recurso de visualização por meio do portal hello, você verá um aviso lembrando que Olá recurso está em visualização.

#### <a name="for-both-private-and-public-preview"></a>Para previews *particulares* e *públicas*
Olá informações a seguir aplica-se tooboth visualizações de públicos e privados:

* As coisas podem não funcionar corretamente sempre.
  * Problemas de intervalo sejam pequenas perturbações por meio de toosomething não funciona em todos os.
* Há uma grande probabilidade de saudação visualização toohave um impacto negativo em seus sistemas / ambiente.
  * Tentamos tooavoid coisas negativo aconteça toohello sistemas que você está usando com o OMS, mas coisas que inesperado, às vezes, ocorrerem.
* Dados podem ser perdidos/corrompidos.
* Podemos pedir que você os logs de diagnóstico toocollect ou outros dados toohelp solucionar problemas.
* recurso de saudação ou solução pode ser removida (temporariamente ou permanentemente).
  * Com base em nossas lições durante a visualização de hello, pode decidir toonot versão Olá recursos ou as soluções.
* Previews podem não funcionar ou não ter sido testadas com todas as configurações, e podemos limitar:
  * Olá sistemas operacionais que podem ser usados (por exemplo, um recurso pode se aplicam somente tooLinux enquanto estiver na visualização).
  * Olá tipo de agente (MMA, Operations Manager) que pode ser usado (por exemplo, um recurso pode não funcionar com o Operations Manager enquanto estiver na visualização).  
* Recursos e soluções de visualização não são cobertos por Olá contrato de nível de serviço.
* O uso de recursos de visualização gera encargos de uso.
* Recursos ou recursos que você precisa para o recurso de saudação / solução toobe útil pode estar ausente ou incompleta.
* Recursos ou soluções podem não estar disponíveis em todas as regiões.
* Recursos ou soluções podem não estar localizados.
* Recursos / soluções podem ter um limite no número de saudação de clientes ou de dispositivos que podem usá-lo.
* Talvez seja necessário toouse scripts tooperform configuração e tooenable Olá/recurso da solução.
* interface de usuário (IU) do Hello está incompleta e pode ser alterado do dia tooday.
* As visualizações públicas podem não ser apropriadas para seus sistemas de produção/críticos.

#### <a name="for-private-preview"></a>Para preview *particular*
Itens de toohello adição acima, Olá informações a seguir é específico tooprivate visualizações:

* Esperamos que você tooprovide nos comentários sobre sua experiência para que possamos realizar Olá recurso/solução melhor.
* Poderemos entrar em contato para solicitar comentários usando pesquisas, chamadas telefônicas ou email.
* As coisas não funcionam corretamente sempre.
* Podemos pode exigir um NDA (acordo de confidencialidade) para a participação ou podemos incluir conteúdo confidencial.
  * Antes de blogs, TWEETS ou qualquer forma de comunicação com terceiros, entre em contato com hello gerente de programa que é responsável por Olá visualização toounderstand quaisquer restrições na divulgação de informações.
* Não execute em sistemas de produção/críticos.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Como obter acesso tooprivate visualização recursos e soluções?
Visualizações de tooprivate de clientes por meio de várias maneiras diferentes, dependendo da visualização Olá convidado.

* Responder a pesquisa de clientes mensais hello e nos conceder permissão toofollow com você melhoram suas chances de visualização privada tooa convidados.
* A equipe de contas da Microsoft pode indicar você.
* Você pode se inscrever com base nos detalhes publicados no twitter [msopsmgmt](https://twitter.com/msopsmgmt).
* Inscreva-se com base em eventos da comunidade que compartilham detalhes, encontre-nos em reuniões, conferências e nas comunidades online.

## <a name="next-steps"></a>Próximas etapas
* [Pesquisar logs](log-analytics-log-searches.md) tooview detalhadas informações coletadas por soluções de gerenciamento.
