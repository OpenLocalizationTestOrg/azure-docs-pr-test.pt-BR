---
title: alertas de banco de dados SQL do Azure toocreate portal aaaUse | Microsoft Docs
description: "Use os alertas de banco de dados SQL toocreate portal do Azure hello, que podem disparar notificações ou automação quando Olá que especificar condições."
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Usar alertas toocreate portal do Azure para o banco de dados do SQL Azure e o Data Warehouse

## <a name="overview"></a>Visão geral
Este artigo mostra como tooset os alertas de banco de dados do SQL Azure e o Data Warehouse usando Olá portal do Azure. Este artigo também fornece as práticas recomendadas para definir os períodos de alerta.    

Você pode receber um alerta com base em métricas de monitoramento ou em eventos nos serviços do Azure.

* **Valores da métrica** - Olá gatilhos de alerta quando o valor de saudação de uma métrica especificada cruza um limite que você atribui em qualquer direção. Ou seja, ela aciona ambos quando Olá primeiro condição e, em seguida, posteriormente quando que condição é não está sendo atendida.    
* **Eventos do log de atividades** - um alerta pode disparar em *cada* evento ou somente quando ocorre determinado número de eventos.

Você pode configurar um alerta toodo Olá após acionará:

* enviar o administrador do serviço de toohello de notificações de email e coadministradores
* Envie email tooadditional emails que você especificar.
* chamar um webhook

Você pode configurar e obter informações sobre o uso de regras de alerta

* [Portal do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [CLI (Interface de linha de comando)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [API REST do Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Criar uma regra de alerta em uma métrica com hello portal do Azure
1. Em Olá [portal](https://portal.azure.com/), localize o recurso Olá você está interessado no monitoramento e selecioná-lo.
2. Esta etapa é diferente para o BD SQL e pools elásticos do que para o SQL DW: 

   - **Banco de dados SQL e Pools de Elástico somente**: selecione **alertas** ou **regras de alerta** em Olá seção monitoramento. ícone e o texto de saudação podem variar um pouco para recursos diferentes.  
   
     ![Monitoramento](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **SQL DW somente**: selecione **monitoramento** em Olá seção de tarefas comuns. Clique em Olá **DWU uso** gráfico.

     ![TAREFAS COMUNS](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Selecione Olá **adicionar alerta** de comando e preencha os campos de saudação.
   
    ![Adicionar alerta](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. Dê um **Nome** para o alerta de regra e escolha uma **Descrição**, que também mostre os emails de notificação.
5. Selecione Olá **métrica** você deseja toomonitor, em seguida, escolha um **condição** e **limite** valor de métrica de saudação. Também tiver escolhido Olá **período** de tempo que Olá métrica regra deve ser atendida antes de gatilhos de alerta de saudação. Por exemplo, se você usar o período de hello "PT5M" e a alerta de procura da CPU acima de 80%, alerta Olá dispara quando Olá CPU foi consistentemente acima de 80% por 5 minutos. Depois que o primeiro gatilho de saudação ocorre, ele novamente dispara quando Olá da CPU permanece abaixo de 80% de 5 minutos. Olá medida de CPU ocorre a cada 1 minuto.   
6. Verificar **proprietários de Email...**  se você quiser que os administradores e coadministradores toobe enviado por email quando Olá alerta acionado.
7. Se você quiser emails adicionais tooreceive notificação hello quando o alerta é acionado, adicioná-los em Olá **email(s) administrador adicional** campo. Vários emails separados com ponto e vírgula – *email@contoso.com;email2@contoso.com*
8. Colocar em um URI válido no hello **Webhook** campo se você quiser chamada hello alerta acionado quando.
9. Selecione **Okey** quando concluído toocreate Olá alerta.   

Em poucos minutos, o alerta de hello está ativa e dispara conforme descrito anteriormente.

## <a name="managing-your-alerts"></a>Gerenciar seus alertas
Depois de criar um alerta, você poderá selecioná-lo e:

* Exiba um gráfico que mostra o limite de métrica hello e os valores reais de Olá Olá dia anterior.
* Editar ou exclui-lo.
* **Desabilitar** ou **habilitar** se deseja tootemporarily parar ou continuar recebendo notificações para o alerta.


## <a name="sql-database-alert-values"></a>Valores de alerta do Banco de Dados SQL

| Tipo de recurso | Nome da métrica | Nome amigável | Tipo de agregação | Janela de tempo mínimo de alerta|
| --- | --- | --- | --- | --- |
| Banco de dados SQL | cpu_percent | Percentual de CPU | Média | 5 minutos |
| Banco de dados SQL | physical_data_read_percent | Porcentagem de E/S de dados | Média | 5 minutos |
| Banco de dados SQL | log_write_percent | Porcentagem de E/S de log | Média | 5 minutos |
| Banco de dados SQL | dtu_consumption_percent | Porcentagem de DTU | Média | 5 minutos |
| Banco de dados SQL | storage | Tamanho total do banco de dados | Máximo | 30 minutos |
| Banco de dados SQL | connection_successful | Conexões bem sucedidas | Total | 10 minutos |
| Banco de dados SQL | connection_failed | Conexões com falha | Total | 10 minutos |
| Banco de dados SQL | blocked_by_firewall | Bloqueado pelo firewall | Total | 10 minutos |
| Banco de dados SQL | deadlock | Deadlocks | Total | 10 minutos |
| Banco de dados SQL | storage_percent | Percentual de tamanho do banco de dados | Máximo | 30 minutos |
| Banco de dados SQL | xtp_storage_percent | Percentual (Visualização) de armazenamento do OLTP na memória | Média | 5 minutos |
| Banco de dados SQL | workers_percent | Porcentagem de funcionários | Média | 5 minutos |
| Banco de dados SQL | sessions_percent | Porcentagem de sessões | Média | 5 minutos |
| Banco de dados SQL | dtu_limit | Limite de DTU | Média | 5 minutos |
| Banco de dados SQL | dtu_used | DTU usado | Média | 5 minutos |
||||||
| Pool elástico | cpu_percent | Percentual de CPU | Média | 10 minutos |
| Pool elástico | physical_data_read_percent | Porcentagem de E/S de dados | Média | 10 minutos |
| Pool elástico | log_write_percent | Porcentagem de E/S de log | Média | 10 minutos |
| Pool elástico | dtu_consumption_percent | Porcentagem de DTU | Média | 10 minutos |
| Pool elástico | storage_percent | Porcentagem de armazenamento | Média | 10 minutos |
| Pool elástico | workers_percent | Porcentagem de funcionários | Média | 10 minutos |
| Pool elástico | eDTU_limit | Limite de eDTU | Média | 10 minutos |
| Pool elástico | storage_limit | Limite de armazenamento | Média | 10 minutos |
| Pool elástico | eDTU_used | eDTU usado | Média | 10 minutos |
| Pool elástico | storage_used | Armazenamento usado | Média | 10 minutos |
||||||               
| SQL Data Warehouse | cpu_percent | Percentual de CPU | Média | 10 minutos |
| SQL Data Warehouse | physical_data_read_percent | Porcentagem de E/S de dados | Média | 10 minutos |
| SQL Data Warehouse | storage | Tamanho total do banco de dados | Máximo | 10 minutos |
| SQL Data Warehouse | connection_successful | Conexões bem sucedidas | Total | 10 minutos |
| SQL Data Warehouse | connection_failed | Conexões com falha | Total | 10 minutos |
| SQL Data Warehouse | blocked_by_firewall | Bloqueado pelo firewall | Total | 10 minutos |
| SQL Data Warehouse | service_level_objective | Objetivo de nível de serviço de banco de dados de saudação | Total | 10 minutos |
| SQL Data Warehouse | dwu_limit | limite de dwu | Máximo | 10 minutos |
| SQL Data Warehouse | dwu_consumption_percent | Porcentagem de DWU | Média | 10 minutos |
| SQL Data Warehouse | dwu_used | DWU usado | Média | 10 minutos |
||||||


## <a name="next-steps"></a>Próximas etapas
* [Obter uma visão geral do monitoramento do Azure](../monitoring-and-diagnostics/monitoring-overview.md) incluindo Olá tipos de informações você pode coletar e monitorar.
* Saiba mais sobre como [configurar webhooks em alertas](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Tenha uma [visão geral dos logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) e colete métricas detalhadas de alta frequência em seu serviço.
* Obter um [visão geral da coleção de métricas](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.
