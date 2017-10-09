---
title: "práticas recomendadas de aaaBest para o Azure SQL Data Warehouse | Microsoft Docs"
description: "Recomendações e práticas recomendadas que você deve saber quando for desenvolver soluções para o SQL Data Warehouse do Azure. Isto irá ajudá-lo a alcançar o sucesso."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Práticas recomendadas para o Azure SQL Data Warehouse
Este artigo é um conjunto de práticas recomendadas que ajudarão você tooachieve o desempenho ideal do Data Warehouse do SQL do Azure.  Alguns dos conceitos de saudação neste artigo são tooexplain básica e fácil, outros conceitos mais avançados e estamos apenas rascunho superfície Olá neste artigo.  Olá finalidade deste artigo é toogive alguns reconhecimento de orientação e tooraise básico de toofocus áreas importantes que você criar o data warehouse.  Cada seção apresenta o conceito de tooa e aponte toomore detalhada artigos conceito de saudação que abrangem mais detalhadamente.

Se você está apenas começando a usar o SQL Data Warehouse, não deixe que este artigo assuste você.  sequência de saudação dos tópicos de saudação é principalmente em ordem de saudação de importância.  Se você iniciar focalizando Olá primeiro alguns conceitos, você estará em bom estado.  Conforme você se familiariza e se sente mais à vontade usando o SQL Data Warehouse, volte e examine mais alguns conceitos.  Ele não terão sentido toomake de comprimento para tudo.

## <a name="reduce-cost-with-pause-and-scale"></a>Reduzir custos com pausa e dimensionamento
Um recurso principal do SQL Data Warehouse é toopause de capacidade de hello quando você não estiver usando, que interrompe a cobrança de saudação de recursos de computação.  Outro recurso importante é que os recursos de tooscale de capacidade de saudação.  Pausando e escala podem ser feito por meio de saudação portal do Azure ou comandos do PowerShell.  Familiarize-se com esses recursos como eles podem reduzir o custo de saudação do data warehouse significativamente quando ele não está em uso.  Se você desejar que o data warehouse acessível, convém tooconsider dimensioná-lo para baixo toohello menor tamanho, um DW100 em vez de pausar.

Confira também [Pausar os recursos de computação][Pause compute resources], [Retomar os recursos de computação][Resume compute resources], [Dimensionar os recursos de computação].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Esvaziar as transações antes de pausar ou dimensionar
Quando você pausa ou dimensionar seu SQL Data Warehouse, em segundo plano do hello que suas consultas são canceladas quando você iniciar Olá pausar ou dimensionar a solicitação.  Cancelar uma simple consulta SELECT é uma operação rápida e não tem quase nenhum impacto toohello tempo toopause ou dimensionar sua instância.  No entanto, consultas transacionais, que modificar a estrutura de dados ou hello dos dados Olá, podem não ser capaz de toostop rapidamente.  **As consultas transacionais, por definição, devem ser concluídas na íntegra ou reverter suas alterações.**  Revertendo o trabalho Olá concluído por uma consulta transacional pode tomar conforme longa, ou ainda mais, de alteração original Olá Olá consulta foi aplicada.  Por exemplo, se você cancelar uma consulta que foi excluindo linhas e já está em execução para uma hora, pode levar sistema Olá uma hora tooinsert Olá voltar as linhas que foram excluídos.  Se você executar pausa ou dimensionamento enquanto as transações em trânsito, seu pausar ou dimensionamento pode parecer tootake muito tempo como pausar e dimensionamento tem toowait para Olá reversão toocomplete para que ele possa continuar.

Confira também [Compreendendo as transações][Understanding transactions], [Otimizando as transações][Optimizing transactions]

## <a name="maintain-statistics"></a>Manter as estatísticas
Ao contrário do SQL Server, que detecta e cria automaticamente ou atualiza as estatísticas em colunas, o SQL Data Warehouse requer uma manutenção manual das estatísticas.  Enquanto estamos planejando toochange isso em Olá futuro, para agora você desejará toomaintain seu tooensure estatísticas que Olá planos SQL Data Warehouse são otimizadas.  planos de saudação criados pelo otimizador Olá somente são tão boas quanto estatísticas disponíveis hello.  **Criando estatísticas por amostra em cada coluna é uma maneira fácil tooget iniciado com estatísticas.**  É igualmente importante tooupdate estatísticas que alterações significativas acontecem tooyour dados.  Uma abordagem conservadora pode ser tooupdate estatísticas diariamente ou após cada carga.  Sempre há compensações entre desempenho e Olá custo toocreate e atualizar as estatísticas. Se você achar que está levando muito toomaintain todas as estatísticas, convém tootry toobe mais seletivo sobre as colunas que têm estatísticas ou as colunas que precisa frequentes de atualização.  Por exemplo, convém tooupdate colunas de data, onde novos valores podem ser adicionado, diária. **Você obterá Olá maior benefício fazendo com que as estatísticas em colunas envolvidas em relações, colunas usadas em Olá onde cláusula e colunas encontrado no GROUP BY.**

Confira também [Gerenciar as estatísticas da tabela][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS], [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>Agrupar instruções INSERT em lotes
Uma única carga tooa pequena tabela com uma instrução INSERT ou até mesmo um recarregamento periódico de uma pesquisa pode executar bem para suas necessidades com uma instrução como `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  No entanto, se você precisar tooload milhares ou milhões de linhas em todo dia hello, você pode achar que singleton inserções apenas não podem acompanhar.  Em vez disso, desenvolva seus processos para que eles gravar arquivo tooa e outro processo periodicamente acompanha e carrega o arquivo.

Confira também [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>Use tooload e exportar dados rapidamente
O SQL Data Warehouse oferece suporte ao carregamento e exportação dos dados por meio de várias ferramentas, incluindo o Azure Data Factory, PolyBase e BCP.  Para pequenas quantidades de dados em que o desempenho não é essencial, qualquer ferramenta poderá ser suficiente para satisfazer suas necessidades.  No entanto, quando você estiver carregando ou exportação de grandes volumes de dados ou desempenho rápido é necessária, o PolyBase é Olá melhor opção.  PolyBase é projetado tooleverage Olá MPP (altamente processamento paralelo) arquitetura do SQL Data Warehouse e, portanto, carregará e exportar magnitudes de dados mais rápido do que qualquer outra ferramenta.  As cargas do PolyBase podem ser executadas usando CTAS ou INSERT INTO.  **Usar CTAS minimize o log de transações e tooload de maneira mais rápida de saudação seus dados.**  O Azure Data Factory também oferece suporte para as cargas do PolyBase.  O PolyBase oferece suporte a vários formatos de arquivo, incluindo os arquivos Gzip.  **produção de toomaximize quando usando gzip arquivos de texto quebra em 60 ou mais arquivos toomaximize paralelismo sua carga.**  Para ter uma taxa de transferência total mais rápida, considere carregar os dados simultaneamente.

Confira também [Carregar dados][Load data], [Guia para usar o PolyBase][Guide for using PolyBase], [Padrões e estratégias de carregamento do SQL Data Warehouse do Azure][Azure SQL Data Warehouse loading patterns and strategies], [Carregar os Dados com o Azure Data Factory][Load Data with Azure Data Factory], [Mover dados com o Azure Data Factory][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT], [CREATE EXTERNAL FILE FORMAT][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Carregar e consultar tabelas externas
Enquanto o Polybase, também conhecido como tabelas externas, pode ser dados de tooload de maneira mais rápidos de saudação, não é ideal para consultas. As tabelas Polybase do SQL Data Warehouse atualmente são compatíveis apenas com arquivos de blob do Azure. Esses arquivos não tem quaisquer recursos de computação que os assegure.  Como resultado, o SQL Data Warehouse não pode deixar esse trabalho e deve ler todo o arquivo hello Carregando-tootempdb dados de pedidos tooread hello.  Portanto, se você tiver várias consultas que serão consultados esses dados, é melhor tooload esses dados uma vez e tem consultas usam a tabela local hello.

Confira também [Guia para usar o PolyBase][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Tabelas grandes com distribuição Hash
Por padrão, as tabelas são distribuídas pelo método Round Robin.  Isso facilita para os usuários tooget começou a criar tabelas sem ter que toodecide como as tabelas devem ser distribuídas.  Tabelas Round Robin podem apresentar desempenho suficiente para algumas cargas de trabalho, mas, na maioria das vezes, o desempenho será muito melhor se uma coluna de distribuição for escolhida.  Olá exemplo mais comum quando uma tabela distribuída por uma coluna será muito superar o desempenho de uma tabela de rodízio é quando dois grandes tabelas de fatos são unidas.  Por exemplo, se você tiver uma tabela de pedidos, que é distribuída por order_id, e uma tabela de transações, que é distribuída por order_id, quando você unir a tabela de transações de tooyour de tabela de pedidos em order_id, essa consulta se torna uma consulta de passagem, o que significa eliminar a operações de movimentação de dados.  Menos etapas significam uma consulta mais rápida.  Menos movimento de dados também resulta em consultas mais rápidas.  Esta explicação apenas aborda superficialmente de saudação. Ao carregar uma tabela distribuída, certifique-se de que os dados de entrada não são classificados na chave de distribuição hello como isso retardará a carrega.  Consulte os links de saudação abaixo para muito mais detalhes sobre como selecionar uma coluna de distribuição pode melhorar o desempenho, bem como toodefine uma tabela distribuída em uma cláusula WITH Olá de sua instrução criar tabelas.

Confira também [Visão geral das tabelas][Table overview], [Distribuição de tabelas][Table distribution], [Selecionando a distribuição de tabelas][Selecting table distribution], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Não estender a partição
Embora o particionamento dos dados possa ser muito eficiente para manter seus dados na troca de partições ou otimizar as varreduras com a eliminação de partições, ter muitas partições pode reduzir a velocidade de suas consultas.  Geralmente, uma estratégia de particionamento com alta granularidade que pode funcionar bem no SQL Server pode não funcionar bem no SQL Data Warehouse.  Ter muitas partições também pode reduzir a eficácia dos índices columnstore clusterizados Olá se cada partição tem menos de 1 milhão de linhas.  Tenha em mente que em segundo plano hello, SQL Data Warehouse particiona os dados para você em 60 bancos de dados, portanto, se você criar uma tabela com 100 partições, isso resulta em 6000 partições realmente.  Cada carga de trabalho é diferente para que Olá melhor conselho é tooexperiment com o particionamento toosee o que funciona melhor para sua carga de trabalho.  Considere uma granularidade menor do que pode ter funcionado para você no SQL Server.  Por exemplo, considere usar partições semanais ou mensais, em vez de partições diárias.

Confira também [Particionamento de tabelas][Table partitioning]

## <a name="minimize-transaction-sizes"></a>Minimizar os tamanhos das transações
As instruções INSERT, UPDATE e DELETE são executadas em uma transação e quando falham, devem ser revertidas.  toominimize Olá possível para uma reversão longo, minimizar os tamanhos de transação sempre que possível.  Isso pode ser feito dividindo as instruções INSERT, UPDATE e DELETE em partes.  Por exemplo, se você tiver uma inserção que você espera tootake 1 hora, se possível, divida Olá INSERT em 4 partes, o que cada uma serão executada em 15 minutos.  Aproveite os casos especiais de registro em log mínimo, como CTAS, TRUNCATE, DROP TABLE ou INSERT tooempty tabelas, tooreduce risco de reversão.  Reversões de tooeliminate outra maneira é toouse metadados somente operações, como gerenciamento de dados de comutação de partição.  Por exemplo, em vez de executar um toodelete de instrução de excluir todas as linhas em uma tabela onde Olá order_date estava em outubro de 2001, você pode particionar seus dados mensal e, em seguida, alternar a partição Olá com os dados de uma partição vazia de outra tabela (consulte ALTER Exemplos de tabela).  Para tabelas não particionadas, considere usando um CTAS toowrite Olá dados que você deseja tookeep em uma tabela em vez de usar DELETE.  Se um CTAS usa Olá mesmo período de tempo, é um toorun muito mais seguro de operação como ele tem log de transação mínima e pode ser cancelado rapidamente, se necessário.

Confira também [Compreendendo as transações][Understanding transactions], [Otimizando as transações][Optimizing transactions], [Particionamento de tabelas][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE], [Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>Use o menor tamanho de coluna possíveis Olá
Ao definir o DDL, usar Olá menor tipo de dados que oferecem suporte a seus dados melhorará o desempenho da consulta.  Isso é especialmente importante para as colunas CHAR e VARCHAR.  Se o valor de hello mais longa em uma coluna é 25 caracteres, em seguida, defina a coluna como varchar (25).  Evite definir todas as colunas tooa padrão grande de caracteres.  Além disso, defina as colunas como VARCHAR quando isso for realmente necessário em vez de usar NVARCHAR.

Confira também [Visão geral das tabelas][Table overview], [Tipos de dados da tabela][Table data types], [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Usar tabelas de heap temporárias para dados transitórios
Quando você temporariamente é inicial dados no SQL Data Warehouse, você pode achar que usar uma tabela heap fará Olá processo geral mais rapidamente.  Se você estiver carregando dados toostage somente antes de executar mais transformações, carregando tooheap da tabela de saudação será muito mais rápido que carregar Olá dados tooa clusterizado tabela columnstore.  Além disso, ao carregar dados tooa tabela temporária também carregará muito mais rápido do que carregar uma toopermanent de armazenamento de tabela.  Tabelas temporárias começam com "#" e são acessíveis apenas por sessão Olá que foi criado, para que eles só podem funcionar em cenários limitados.   Heap tabelas são definidas em uma cláusula WITH Olá de CREATE TABLE.  Se você usar uma tabela temporária, lembre-se toocreate estatísticas nessa tabela temporária muito.

Confira também [Tabelas temporárias][Temporary tables], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Otimizar tabelas columnstore clusterizadas
Índices columnstore clusterizados são uma das maneiras mais eficientes hello, que você pode armazenar seus dados no Azure SQL Data Warehouse.  Por padrão, as tabelas no SQL Data Warehouse são criadas como ColumnStore Clusterizado.  tooget Olá melhor desempenho para consultas em tabelas columnstore, tenham de segmento de boa qualidade é importante.  Quando linhas são gravadas toocolumnstore tabelas sob pressão de memória, columnstore qualidade de segmento poderá ser afetado.  A qualidade de segmento pode ser medida pelo número de linhas em um grupo de linhas compactado.  Consulte Olá [causas de columnstore baixa qualidade do índice] [ Causes of poor columnstore index quality] em Olá [índices de tabela] [ Table indexes] do artigo para obter instruções passo a passo em detectando e melhorar a qualidade do segmento para tabelas columnstore clusterizado.  Como segmentos de columnstore de alta qualidade é importante, é uma boa ideia toouse usuários ids na classe de recurso de médias ou grandes de saudação de carregamento de dados.  Olá menos DWUs usar, Olá Olá recursos classe maior você desejará tooyour tooassign carregar o usuário.

Como tabelas columnstore geralmente não enviar dados por push em um segmento compactado columnstore até que há mais de 1 milhão de linhas por tabela e cada tabela do SQL Data Warehouse é particionada em 60 tabelas, como regra geral, tabelas columnstore não se beneficiar de uma consulta a menos que a tabela de saudação tem mais de 60 milhões de linhas.  Para a tabela com menos de 60 milhões de linhas, ele pode não ter qualquer toohave sentido um índice columnstore.  Também pode não prejudicar.  Além disso, se você particionar seus dados, você desejará tooconsider que cada partição precisará de 1 milhão de toohave toobenefit de linhas de um índice columnstore clusterizado.  Se uma tabela tem 100 partições, será necessário pelo menos 6 bilhões de toohave toobenefit de linhas de um repositório de colunas clusterizadas (60 distribuições * 100 partições * 1 milhão de linhas).  Se a tabela não tiver 6 bilhões de linhas neste exemplo, reduzir o número de saudação de partições ou considere o uso de uma tabela de heap em vez disso.  Ele também pode ser vale a pena testar toosee se pode conseguir um melhor desempenho com uma tabela de heap com índices secundários em vez de uma tabela columnstore.  As tabelas columnStore ainda não dão suporte aos índices secundários.

Ao consultar uma tabela columnstore, consultas serão executadas mais rapidamente se você selecionar somente colunas Olá que necessárias.  

Confira também [Índices de tabela][Table indexes], [Guia dos índices columnstore][Columnstore indexes guide], [Recriando índices columnstore][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Use o maior desempenho de consulta tooimprove de recursos de classe
SQL Data Warehouse usa grupos de recursos como um tooqueries de memória do modo tooallocate.  Fora da caixa hello, todos os usuários são atribuídos a classe do recurso pequeno toohello que concede a 100 MB de memória por distribuição.  Como há sempre 60 distribuições e cada distribuição recebe um mínimo de 100 MB, memória total do hello grande sistema alocação é 6.000 MB ou pouco menos de 6 GB.  Determinadas consultas, como junções grandes ou carrega tooclustered columnstore tabelas, se beneficiarão das alocações de memória maior.  Algumas consultas, como as varreduras puras, não terão qualquer benefício.  Olá inverter lado, utilizar classes de recursos maiores afeta simultaneidade, portanto, será conveniente tootake isso em consideração antes de mover todos da sua classe de recurso grande tooa usuários.

Confira também [Gerenciamento de simultaneidade e carga de trabalho][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Use a classe de recurso menor tooIncrease simultaneidade
Se você é perceba que as consultas de usuário parecerem toohave um longo atraso, é possível que os usuários são executados em classes de recursos maiores e estão consumindo muito slots de simultaneidade, fazendo com que outras consultas tooqueue backup.  toosee se as consultas que os usuários são enfileiradas, execute `SELECT * FROM sys.dm_pdw_waits` toosee se todas as linhas são retornadas.

Confira também [Gerenciamento de simultaneidade e carga de trabalho][Concurrency and workload management], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Use DMVs toomonitor e otimizar suas consultas
SQL Data Warehouse tem várias DMVs que podem ser usado toomonitor a execução da consulta.  Olá monitoramento artigo a seguir percorre instruções passo a passo sobre como toolook detalhes da saudação da execução de uma consulta.  tooquickly localizar consultas esses DMVs, usando a opção de rótulo Olá com suas consultas pode ajudar.

Confira também [Monitore sua carga de trabalho usando DMVs][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Outros recursos
Confira também nosso artigo de [Solução de problemas][Troubleshooting] para conhecer os problemas e as soluções comuns.

Se você não encontrar o que você está procurando neste artigo, tente usar hello "Pesquisa para documentos" no lado esquerdo da saudação desse toosearch página todos os de documentos do Azure SQL Data Warehouse Olá.  Olá [Fórum do MSDN do Azure SQL Data Warehouse] [ Azure SQL Data Warehouse MSDN Forum] foi criar como um local para você tooask perguntas tooother usuários e toohello grupo de produto do SQL Data Warehouse.  Podemos monitorar ativamente este tooensure Fórum que suas perguntas foram respondidas por outro usuário ou um de nós.  Se você preferir tooask suas perguntas sobre estouro de pilha, também temos um [Azure Data Warehouse pilha estouro Fórum do SQL][Azure SQL Data Warehouse Stack Overflow Forum].

Por fim, use Olá [Azure SQL Data Warehouse comentários] [ Azure SQL Data Warehouse Feedback] toomake recurso solicitações de página.  Adicionar suas solicitações ou recomendar outras solicitações realmente nos ajudará a priorizar os recursos.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Dimensionar os recursos de computação]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
