---
title: aaaMonitoring desempenho de banco de dados SQL do Azure | Microsoft Docs
description: "Saiba mais sobre opções de saudação para o monitoramento de banco de dados com as ferramentas do Azure e exibições de gerenciamento dinâmico."
keywords: monitoramento de banco de dados, desempenho do banco de dados em nuvem
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Monitorar o desempenho do banco de dados no Banco de Dados SQL do Azure
Monitorando o desempenho de saudação do banco de dados SQL no Azure inicia com o monitoramento de nível de toohello relativo de utilização de recursos de saudação de desempenho de banco de dados que você escolher. Monitoramento ajuda a determinar se seu banco de dados tem excesso de capacidade ou está tendo problemas para porque os recursos são maximizados e, em seguida, decidir se ele é o nível de desempenho do tempo tooadjust hello e [camada de serviço](sql-database-service-tiers.md) do banco de dados. Você pode monitorar seu banco de dados usando ferramentas gráficas Olá [portal do Azure](https://portal.azure.com) ou usando o SQL [exibições de gerenciamento dinâmico](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Monitorar bancos de dados usando Olá portal do Azure
Em Olá [portal do Azure](https://portal.azure.com/), você pode monitorar a utilização de um único banco de dados selecionando-o e clicando em Olá **monitoramento** gráfico. Isso abre uma **métrica** janela que pode ser alterado clicando Olá **Editar gráfico** botão. Adicione Olá métricas a seguir:

* Percentual de CPU
* Porcentagem de DTU
* Porcentagem de E/S de dados
* Percentual de tamanho do banco de dados

Depois de adicionar essas métricas, você pode continuar tooview em Olá **monitoramento** gráfico com mais detalhes sobre Olá **métrica** janela. Todas as métricas de quatro mostram Olá utilização média porcentagem relativa toohello **DTU** do banco de dados. Consulte Olá [camadas de serviço](sql-database-service-tiers.md) artigo para obter detalhes sobre DTUs.

![Monitoramento da camada de serviço do desempenho do banco de dados.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

Você também pode configurar alertas em métricas de desempenho de saudação. Clique em Olá **adicionar alerta** botão Olá **métrica** janela. Siga Olá Assistente tooconfigure o alerta. Você tem Olá opção tooalert se métricas Olá excederem um determinado limite ou se Olá ficarem abaixo de determinado limite.

Por exemplo, se você espera que a carga de trabalho de saudação em toogrow seu banco de dados, você pode escolher tooconfigure um alerta por email sempre que seu banco de dados atinge 80% em qualquer uma das métricas de desempenho de saudação. Você pode usar isso como um toofigure aviso antecipado out quando você pode ter tooswitch toohello próximo nível mais alto desempenho.

métricas de desempenho de saudação também podem ajudar a determinar se são capazes de toodowngrade tooa nível de desempenho inferior. Suponha que você estiver usando um banco de dados em Standard S2 e todas as mostram de métricas de desempenho que Olá em média o banco de dados não usa mais de 10% a qualquer momento. É provável que esse banco de dados Olá funcionará bem no Standard S1. No entanto, lembre-se de cargas de trabalho que apresentam picos ou oscilam antes de fazer Olá decisão toomove tooa nível de desempenho inferior.

## <a name="monitor-databases-using-dmvs"></a>Monitorar bancos de dados usando DMVs
Olá mesmas métricas que são expostas no portal de saudação também estão disponíveis por meio de exibições do sistema: [sys. resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) em Olá lógica **mestre** banco de dados do servidor, e [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) no banco de dados de usuário de saudação. Use **sys. resource_stats** se você precisar toomonitor menos dados granulares em um período de tempo maior. Use **sys.DM db_resource_stats** se você precisar toomonitor dados mais granulares em um período de tempo menor. Para obter mais informações, veja [Orientação sobre o desempenho do Banco de Dados SQL do Azure](sql-database-single-database-monitor.md#monitor-resource-use).

> [!NOTE]
> **sys.dm_db_resource_stats** retorna um conjunto de resultados vazio quando usado em bancos de dados Web e Business Edition, que estão desativados.
>
>

### <a name="monitor-resource-use"></a>Monitorar o uso de recursos

Você pode monitorar o uso de recursos usando a [Análise de Desempenho de Consultas de Banco de Dados SQL](sql-database-query-performance.md) e [Repositório de Consultas](https://msdn.microsoft.com/library/dn817826.aspx).

Você também pode monitorar o uso com estes dois modos de exibição:

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
Você pode usar o hello [sys.DM db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) exibição em cada banco de dados SQL. Olá **sys.DM db_resource_stats** exibição mostra a camada de serviço de toohello relativo de dados do recurso uso recente. A porcentagem média de CPU, E/S de dados, gravações de log e memória é registrada a cada 15 segundos e armazenada por 1 hora.

Como essa exibição oferece uma visão mais granular do uso de recursos, use **sys.dm_db_resource_stats** primeiro para qualquer análise de estado atual ou para solução de problemas. Por exemplo, esta consulta mostra recursos máximo e média de saudação usam para banco de dados atual Olá Olá última hora:

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Para outras consultas, consulte os exemplos de saudação em [sys.DM db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>sys.resource_stats
Olá [sys. resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) exibição no hello **mestre** banco de dados tem informações adicionais que podem ajudá-lo a monitorar o desempenho de saudação do banco de dados SQL em seu nível de desempenho e da camada de serviço específico . Olá dados são coletados a cada 5 minutos e são mantidos por aproximadamente 35 dias. Essa exibição é útil para uma análise de histórico de longo prazo de como seu banco de dados SQL usa recursos.

Olá gráfico a seguir mostra uso de recursos de CPU Olá para um banco de dados Premium Olá nível de desempenho P2 para cada hora em uma semana. Esse gráfico começa na segunda-feira, mostra 5 dias de trabalho e, em seguida, exibe um fim de semana, quando muito menos acontece no aplicativo hello.

![Uso de recursos de banco de dados SQL](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Olá pelos dados do, este banco de dados atualmente tem um pico de carga de CPU de pouco mais de 50% CPU usam o nível de desempenho relativo toohello P2 (meio-dia de terça-feira). Se a CPU é o fator dominante no perfil de recursos do aplicativo hello de hello, você pode decidir que P2 é hello direito tooguarantee de nível de desempenho que Olá a carga de trabalho sempre se ajuste. Se você espera que um aplicativo toogrow ao longo do tempo, é uma boa ideia toohave um buffer adicional do recurso para que o aplicativo hello já não atinge o limite de nível de desempenho de saudação. Se você aumentar o nível de desempenho hello, você pode ajudar a evitar erros visíveis para os clientes que podem ocorrer quando um banco de dados não tem suficiente solicitações de tooprocess power efetivamente, especialmente em ambientes sensíveis à latência. Um exemplo é um banco de dados que oferece suporte a um aplicativo que pinta páginas da Web com base nos resultados de saudação de chamadas de banco de dados.

Outros tipos de aplicativos podem interpretar Olá mesmo gráfico de forma diferente. Por exemplo, se um aplicativo tenta tooprocess dados de folha de pagamento por dia e tem Olá mesmo gráfico, nesse tipo de modelo de "trabalho em lotes" pode fazer bem com um nível de desempenho P1. Olá nível de desempenho P1 tem 100 DTUs em relação too200 DTUs no hello nível de desempenho P2. Olá nível de desempenho P1 oferece metade desempenho de saudação de Olá nível de desempenho P2. Portanto, 50% de uso da CPU em P2 equivale a 100% de uso da CPU em P1. Se o aplicativo hello não têm tempo limite, ele pode não importa se um trabalho demorar 2 horas ou 2,5 horas toofinish, a se seja feito hoje. Um aplicativo dessa categoria provavelmente pode usar um nível de desempenho P1. Você pode tirar proveito do fato de saudação que há períodos de tempo durante o dia hello quando o uso de recursos é menor, para que um "pico maior" poderá extrapolar para um dos ciclos de hello mais tarde no dia hello. saudação de nível de desempenho P1 pode ser válida para esse tipo de aplicativo (e economizar dinheiro), como trabalhos Olá podem terminar no tempo por dia.

Expõe de banco de dados SQL do Azure consumido informações de recursos para cada banco de dados ativo no hello **sys. resource_stats** exibição de saudação **mestre** banco de dados em cada servidor. dados de saudação na tabela de saudação são agregados para intervalos de 5 minutos. Com camadas de serviço de Basic, Standard e Premium da saudação, Olá dados podem demorar mais de 5 minutos tooappear na tabela hello, para que esses dados são mais úteis para análise histórica em vez de análise em tempo quase real. Saudação de consulta **sys. resource_stats** exibição toosee Olá histórico recente de um banco de dados e toovalidate se reserva Olá que você escolheu entregues desempenho Olá desejados quando necessário.

> [!NOTE]
> Você deve ser conectado toohello **mestre** banco de dados de sua lógica tooquery de servidor de banco de dados SQL **sys. resource_stats** em Olá exemplos a seguir.
> 
> 

Este exemplo mostra como os dados de saudação nesta exibição são expostos:

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![exibição do catálogo sys. resource_stats Olá](./media/sql-database-performance-guidance/sys_resource_stats.png)

Olá próximo exemplo mostra diferentes maneiras que você pode usar o hello **sys. resource_stats** tooget de exibir informações sobre como o banco de dados SQL usa recursos do catálogo:

1. toolook em Olá após os recursos da semana usado para Olá userdb1 de banco de dados, você pode executar esta consulta:
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. tooevaluate quão bem sua carga de trabalho se ajusta o nível de desempenho hello, você precisa toodrill para baixo em cada aspecto das métricas de recurso Olá: CPU, leituras, gravações, número de trabalhadores e número de sessões. Aqui está um revisado consultar usando **sys. resource_stats** tooreport Olá valores médio e máximo dessas métricas de recurso:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. Com essas informações sobre os valores médio e máximo de saudação de cada métrica de recurso, você pode avaliar como sua carga de trabalho se encaixa no nível de desempenho Olá escolhido. Geralmente, os valores médios de **sys. resource_stats** lhe toouse uma boa linha de base no tamanho do destino hello. Deve ser seu cartão de medida principal. Por exemplo, talvez você esteja usando camada de serviço Standard Olá com nível de desempenho S2. Média Olá usar porcentagens de CPU e e/s de leituras e gravações estão abaixo 40 por cento, número médio de saudação de trabalhadores for inferior a 50 e número médio de saudação de sessões for inferior a 200. A carga de trabalho talvez se enquadre no hello nível de desempenho S1. É fácil toosee se seu banco de dados se encaixa no trabalho hello e limites de sessão. toosee se um banco de dados se adapta a um nível de desempenho inferior com considera tooCPU, leituras e gravações, divida o número DTU de saudação do nível de desempenho inferior Olá por Olá número DTU de nível de desempenho atual e, em seguida, multiplique o resultado de saudação por 100:
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    resultado de Olá é a diferença de desempenho relativo de saudação entre dois níveis de desempenho hello, em porcentagem. Se o uso de recursos não exceder esse valor, a carga de trabalho talvez se enquadre no nível de desempenho inferior hello. No entanto, você precisa toolook todos os intervalos de valores de uso de recursos e determinar, por percentual, quantas vezes sua carga de trabalho do banco de dados se enquadraria no nível de desempenho inferior Olá. Olá consulta a seguir produz Olá ajustar percentual por dimensão de recurso com base no limite de saudação de 40 por cento calculado neste exemplo:
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Com base no seu objetivo de nível de serviço (SLO) do banco de dados, você pode decidir se sua carga de trabalho se encaixa no nível de desempenho inferior hello. Se sua carga de trabalho do banco de dados SLO é de 99,9% e hello consulta acima retorna valores superiores a 99,9% de todas as três dimensões de recurso, sua carga de trabalho provavelmente se enquadra no nível de desempenho inferior hello.
   
    Observando a porcentagem de saudação ajustar também oferece informações sobre se deve-se mover toohello próximo maior toomeet da nível do desempenho seu SLO. Por exemplo, userdb1 mostra Olá uso da CPU para Olá semana passada a seguir:
   
   | Percentual médio da CPU | Percentual máximo da CPU |
   | --- | --- |
   | 24,5 |100,00 |
   
    Olá média de CPU é aproximadamente um quarto do limite de saudação do nível de desempenho hello, que se ajusta bem ao nível de desempenho de saudação do banco de dados de saudação. Mas, o valor máximo Olá mostra que esse banco de dados Olá atinge o limite de saudação de nível de desempenho de saudação. Você precisa toomove toohello próximo nível mais alto desempenho? Analisar quantas vezes sua carga de trabalho atinge 100 por cento e, em seguida, compare-a carga de trabalho do banco de dados do tooyour SLO.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Se esta consulta retorna um valor inferior a 99,9% para qualquer uma das dimensões de recurso Olá três, considere qualquer movimentação toohello próximo nível mais alto desempenho ou usar o ajuste de aplicativo de técnicas tooreduce Olá carga no banco de dados SQL hello.
4. Este exercício também considera o aumento da carga de trabalho projetada no hello futuras.

Para pools Elásticos, você pode monitorar os bancos de dados individuais no pool de saudação com técnicas de saudação descritas nesta seção. Mas você também pode monitorar o pool hello como um todo. Para saber mais, veja [Monitorar e gerenciar um pool elásticos](sql-database-elastic-pool-manage-portal.md).


### <a name="maximum-concurrent-requests"></a>Máximo de solicitações simultâneas
número de saudação toosee de solicitações simultâneas, execute esta consulta Transact-SQL no banco de dados SQL:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

carga de trabalho do tooanalyze Olá de um banco de dados local do SQL Server, modificar essa consulta toofilter no banco de dados específico Olá você deseja tooanalyze. Por exemplo, se você tiver um banco de dados local denominado MyDatabase, essa consulta Transact-SQL retorna contagem de saudação de solicitações simultâneas no banco de dados:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

Isso é apenas um instantâneo em um único ponto no tempo. tooget melhor compreensão de seus requisitos de solicitações simultâneas e a carga de trabalho, você precisará toocollect muitas amostras ao longo do tempo.

### <a name="maximum-concurrent-logins"></a>Máximo de logons simultâneos
Você pode analisar seu tooget de padrões de usuário e aplicativo uma ideia de frequência de saudação de logons. Você também pode executar cargas reais em um toomake do ambiente de teste-se de que você não está atingindo isso ou outros limites que discutimos neste artigo. Não há uma única consulta ou DMV (exibição de gerenciamento dinâmico) que mostre a contagem de logons simultâneos ou o histórico.

Se usam vários clientes Olá a mesma cadeia de caracteres de conexão, hello serviço autentica a cada logon. Se 10 usuários se conectar simultaneamente Olá de tooa banco de dados usando o mesmo nome de usuário e senha, seria 10 logons simultâneos. Esse limite se aplica apenas toohello duração de logon hello e autenticação. Se Olá mesmo 10 usuários se conectam a banco de dados toohello sequencialmente, número de saudação de logons simultâneos nunca ser maior que 1.

> [!NOTE]
> Atualmente, esse limite não se aplica a toodatabases em pools elásticos.
> 
> 

### <a name="maximum-sessions"></a>Máximo de sessões
número de saudação toosee de sessões ativas atuais, execute esta consulta de Transact-SQL no banco de dados SQL:

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

Se você estiver analisando uma carga de trabalho do SQL Server local, modifique Olá toofocus de consulta em um banco de dados específico. Essa consulta ajuda a determinar as necessidades de sessão possíveis para o banco de dados de saudação se você estiver considerando movê-lo tooAzure banco de dados SQL.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Novamente, essas consultas retornam uma contagem pontual. Se você coletar várias amostras ao longo do tempo, você terá melhor compreensão de saudação da sessão de usar.

Para análise de banco de dados SQL, você pode obter estatísticas históricas sobre as sessões consultando Olá [sys. resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) exibir e revisar Olá **active_session_count** coluna. 
