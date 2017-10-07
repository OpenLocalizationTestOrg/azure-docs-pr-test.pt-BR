---
title: "aaaAzure solução de análise do SQL na análise de Log | Microsoft Docs"
description: "Olá solução de análise do SQL Azure ajuda a gerenciar seus bancos de dados do SQL Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Monitorar o Banco de Dados SQL do Azure usando a Análise do Azure SQL (Visualização) no Log Analytics

![Símbolo da Análise de SQL do Azure](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Olá solução de análise do SQL Azure no Azure Log Analytics coleta e visualiza as métricas importantes de desempenho do SQL Azure. Usando métricas Olá coletados com solução hello, você pode criar regras personalizadas de monitoramentos e alertas. E você pode monitorar o Banco de Dados SQL e métricas de pool elástico em várias assinaturas do Azure e pools elásticos e visualizá-los. Olá solução também ajuda a tooidentify problemas em cada camada da pilha de seu aplicativo.  Ele usa [métricas de diagnóstico do Azure](log-analytics-azure-storage.md) junto com a análise de Log exibições toopresent dados sobre todos os bancos de dados SQL do Azure e pools Elásticos em um único espaço de trabalho de análise de Log.

No momento, esta solução visualização dá suporte para até too150, 000 bancos de dados do SQL do Azure e 5.000 Pools Elásticos de SQL por espaço de trabalho.

Olá solução de análise do SQL Azure, como outros disponíveis para análise de Log ajuda a monitorar e receber notificações sobre integridade de saudação de seus recursos do Azure – nesse caso, o banco de dados do SQL Azure. Banco de dados SQL do Microsoft Azure é um serviço de banco de dados relacional escalonável que fornece familiar tooapplications de recursos de tipo de SQL Server em execução no hello nuvem do Azure. Análise de log ajuda a toocollect, correlacionar e visualizar dados estruturados e não estruturados.

## <a name="connected-sources"></a>Fontes conectadas

Olá solução de análise do SQL Azure não usa agentes tooconnect toohello serviço de análise de Log.

Olá, a tabela a seguir descreve Olá conectado fontes que são suportadas por essa solução.

| Fonte Conectada | Suporte | Descrição |
| --- | --- | --- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Não | Direcione os agentes não são usados pela solução de saudação do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não | Direcione os agentes não são usados pela solução de saudação do Linux. |
| [Grupo de gerenciamento do SCOM](log-analytics-om-agents.md) | Não | Uma conexão direta de saudação SCOM agente tooLog Analytics não é usada pela solução de saudação. |
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | Análise de log não lê dados saudação de uma conta de armazenamento. |
| [Diagnóstico do Azure](log-analytics-azure-storage.md) | Sim | Dados de métrica do Azure são enviados tooLog análise diretamente pelo Azure. |

## <a name="prerequisites"></a>Pré-requisitos

- Uma assinatura do Azure. Se não tiver uma, você poderá criá-la [grátis](https://azure.microsoft.com/free/).
- Um espaço de trabalho do Log Analytics. Você pode usar um existente ou pode [criar um novo](log-analytics-get-started.md) para começar a usar essa solução.
- Habilitar o diagnóstico do Azure para seus bancos de dados SQL do Azure e pools Elásticos e [configurá-las toosend tooLog seus dados análise](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Configuração

Execute Olá etapas tooadd Olá análise do SQL Azure solução tooyour espaço de trabalho a seguir.

1. Adicionar espaço de trabalho do hello análise do SQL Azure solução tooyour em [do Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. No portal do Azure de Olá, clique em **novo** (Olá símbolo de +), na lista de saudação de recursos, selecione **monitoramento + gerenciamento**.  
    ![Monitoramento + Gerenciamento](./media/log-analytics-azure-sql/monitoring-management.png)
3. Em Olá **monitoramento + gerenciamento** lista, clique em **ver todos os**.
4. Em Olá **recomendado** lista, clique em **mais** e, em seguida, na lista de novos hello, localize **análise do SQL Azure (visualização)** e, em seguida, selecione-o.  
    ![Solução de Análise do Azure SQL](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. Em Olá **análise do SQL Azure (visualização)** folha, clique em **criar**.  
    ![Criar](./media/log-analytics-azure-sql/portal-create.png)
6. Em Olá **criar nova solução** folha, no espaço de trabalho Olá selecione que você deseja tooadd Olá solução tooand e clique em **criar**.  
    ![Adicionar tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure várias assinaturas do Azure

toosupport várias assinaturas, use o script do PowerShell de saudação do [log de métricas de recursos de habilitar o Azure usando o PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Fornece Olá ID de recurso de espaço de trabalho como um parâmetro ao executar dados de diagnóstico Olá script toosend de recursos no espaço de trabalho de tooa de uma assinatura do Azure em outra assinatura do Azure.

**Exemplo**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>Usando a solução de saudação

Quando você adiciona o espaço de trabalho do hello solução tooyour, Olá bloco de análise do SQL Azure é adicionado tooyour espaço de trabalho, e ele aparece na visão geral. bloco Olá mostra o número de saudação de bancos de dados SQL do Azure e pools Elásticos do SQL Azure conectado à solução de saudação.

![Bloco de Análise do SQL Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Exibindo dados da Análise de SQL do Azure

Clique em Olá **análise do SQL Azure** o painel de controle do bloco tooopen Olá análise do SQL Azure. Painel de saudação inclui folhas Olá definidas abaixo. Cada folha lista os recursos de too15 (assinatura, server, pool Elástico e banco de dados). Clique em qualquer painel da saudação tooopen Olá recursos para o recurso específico. Banco de dados ou Pool Elástico contém gráficos-Olá com métricas para um recurso selecionado. Clique em uma caixa de diálogo de pesquisa de Log de saudação do tooopen de gráfico.

| Folha | Descrição |
|---|---|
| Assinaturas | Lista de assinaturas com o número de servidores, pools e bancos de dados conectados. |
| Servidores | Lista de servidores com o número de pools e bancos de dados conectados. |
| Pools elásticos | Lista de pools Elásticos conectados com máximo GB e eDTU em Olá observado período. |
|Bancos de dados | Lista de bancos de dados conectados com GB e DTU máximo em Olá observado período.|


### <a name="analyze-data-and-create-alerts"></a>Analisar dados e criar alertas

Facilmente, você pode criar alertas com dados Olá provenientes de recursos do Azure SQL Database. Aqui estão algumas das consultas de [pesquisa de logs](log-analytics-log-searches.md) úteis que você pode usar para alertas:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*DTU alta no Banco de Dados SQL do Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Alta DTU no pool elástico do Banco de Dados SQL do Azure*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

Você pode usar essas consultas com base no alerta tooalert em limites específicos para o banco de dados do SQL Azure e pools elásticos. tooconfigure um alerta para seu espaço de trabalho do OMS:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure um alerta para seu espaço de trabalho

1. Vá toohello [portal do OMS](http://mms.microsoft.com/) e entrar.
2. Abra o espaço de trabalho de saudação que você configurou para solução de saudação.
3. Na página de visão geral de saudação, clique em Olá **análise do SQL Azure (visualização)** lado a lado.
4. Execute uma das consultas de exemplo hello.
5. Na Pesquisa de Log, clique em **Alerta**.  
![criar alerta na pesquisa](./media/log-analytics-azure-sql/create-alert01.png)
6. Em Olá **Adicionar regra de alerta** página, defina propriedades adequadas hello e Olá limites específicos que você deseja e, em seguida, clique em **salvar**.  
![adicionar regra de alerta](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Tomar decisões com base em dados da Análise de SQL do Azure

Por exemplo, uma das consultas de hello mais úteis que você pode executar é toocompare utilização de DTU Olá para todos os Pools de Elástico do SQL Azure em todas as suas assinaturas do Azure. Unidade de taxa de transferência de banco de dados (DTU) fornece uma maneira toodescribe Olá a capacidade relativa de um nível de desempenho de pools e os bancos de dados Basic, Standard e Premium. DTUs são baseadas em uma medida combinada de CPU, memória, leituras e gravações. Quando as DTUs aumentam, Olá capacidade oferecida pelo aumento de nível de desempenho de saudação. Por exemplo, um nível de desempenho com cinco DTUs tem cinco vezes mais energia do que um nível de desempenho com uma DTU. Uma cota DTU máxima aplica-se o pool de servidor e elástica tooeach.

Executando Olá consulta de pesquisa de Log a seguir, você pode dizer facilmente se você subutilização ou mais utilizar os pools Elásticos do SQL Azure.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), então Olá acima consulta alteraria toohello a seguir.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

Saudação de exemplo a seguir, você pode ver um pool Elástico tem um alto uso quase 100% enquanto outros têm muito pouca utilização DTU. Você pode investigar mais tootroubleshoot recentes alterações em potencial em seu ambiente usando logs de atividades do Azure.

![Resultados de pesquisa de log - alta utilização](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Consulte também

- Use [pesquisas de Log](log-analytics-log-searches.md) no tooview de análise de Log detalhado de dados do SQL Azure.
- [Criar seus próprios painéis](log-analytics-dashboards.md) mostrando os dados do Azure SQL.
- [Criar alertas](log-analytics-alerts.md) quando ocorrerem eventos específicos do Azure SQL.
