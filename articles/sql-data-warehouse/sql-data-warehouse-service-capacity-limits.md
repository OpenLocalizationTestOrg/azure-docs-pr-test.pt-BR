---
title: limites de capacidade do Data Warehouse aaaSQL | Microsoft Docs
description: "Valores máximos para conexões, bancos de dados, tabelas e consultas para o SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>Limites de capacidade do SQL Data Warehouse
Olá tabelas a seguir contêm valores máximos de saudação permitidos para vários componentes do Azure SQL Data Warehouse.

## <a name="workload-management"></a>Gerenciamento de carga de trabalho
| Categoria | Descrição | Máximo |
|:--- |:--- |:--- |
| [DWU (Unidades de Data Warehouse)][Data Warehouse Units (DWU)] |DWU máxima para um único Data Warehouse do SQL |6000 |
| [DWU (Unidades de Data Warehouse)][Data Warehouse Units (DWU)] |DWU máxima para um único servidor SQL |6000 por padrão<br/><br/> Por padrão, cada SQL server (por exemplo, myserver.database.windows.net) tem uma cota de DTU de 45.000 que permite que o DWU too6000. Essa cota é simplesmente um limite de segurança. Você pode aumentar a cota por [criar um tíquete de suporte] [ creating a support ticket] e selecionando *cota* como tipo de solicitação de saudação.  toocalculate precisa, multiplique o DTU Olá 7.5 pelo total de saudação DWU necessário. Você pode exibir seu consumo de DTU atual da folha de saudação SQL server no portal de saudação. Bancos de dados em pausa e retomados contam para a cota de DTU de saudação. |
| Conexão de banco de dados |Sessões abertas simultâneas |1024<br/><br/>Há suporte para um máximo de conexões ativas de 1024, cada um deles pode enviar solicitações tooa SQL Data Warehouse banco de dados Olá simultaneamente. Observe que há limites no número de saudação de consultas que pode executar simultaneamente. Quando Olá simultaneidade limite for excedido, solicitação de Olá passa em uma fila interna em que ele espera toobe processado. |
| Conexão de banco de dados |Memória máxima para instruções preparadas |20 MB |
| [Gerenciamento de carga de trabalho][Workload management] |Máximo de consultas simultâneas |32<br/><br/> Por padrão, o SQL Data Warehouse pode executar um máximo de 32 consultas simultâneas e coloca as consultas restantes na fila.<br/><br/>pode diminuir o nível de simultaneidade Hello quando os usuários são atribuídos a classe de recurso superior tooa ou quando o SQL Data Warehouse é configurado com DWU baixa. Algumas consultas, como consultas DMV, são sempre permitidas toorun. |
| [Tempdb][Tempdb] |Tamanho máximo de Tempdb |399 GB por DW100. Portanto em Tempdb DWU1000 é TB de tamanho too3.99 |

## <a name="database-objects"></a>Objetos de banco de dados
| Categoria | Descrição | Máximo |
|:--- |:--- |:--- |
| Banco de dados |Tamanho máx. |240 TB compactados em disco<br/><br/>Esse espaço é independente de espaço em tempdb ou de log e, portanto, esse espaço é dedicado toopermanent tabelas.  A compactação do columnstore clusterizado é estimada em cinco vezes.  Essa compactação permite Olá banco de dados toogrow tooapproximately 1 PB quando todas as tabelas são columnstore clusterizado (tipo de tabela padrão Olá). |
| Tabela |Tamanho máx. |60 TB compactados em disco |
| Tabela |Tabelas por banco de dados |2 bilhões |
| Tabela |Colunas por tabela |1024 colunas |
| Tabela |Bytes por coluna |Dependente do [tipo de dados][data type] da coluna.  O limite é de 8000 para tipos de dados char, 4000 para nvarchar ou 2 GB para tipos de dados MAX. |
| Tabela |Bytes por linha, tamanho definido |8060 bytes<br/><br/>Olá o número de bytes por linha é calculado no hello exatamente como ele é para o SQL Server com a compactação de página. Como o SQL Server, o SQL Data Warehouse dá suporte ao armazenamento de estouro de linha, que permite **colunas de comprimento variável** toobe empurrados para fora da linha. Quando linhas de comprimento variável são colocadas fora de linha, somente raiz de 24 bytes é armazenada no registro principal hello. Para obter mais informações, consulte Olá [estouro de linha dados exceder 8 KB] [ Row-Overflow Data Exceeding 8 KB] artigo do MSDN. |
| Tabela |Partições por tabela |15.000<br/><br/>De alto desempenho, é recomendável minimizando Olá número de partições necessária enquanto ainda dar suporte a seus requisitos de negócios. Como Olá aumenta o número de partições, sobrecarga de saudação Data Definition Language (DDL) e as operações de linguagem de manipulação de dados (DML) aumenta e faz com que o desempenho mais lento. |
| Tabela |Caracteres por valor de limite de partição. |4000 |
| Índice |Índices não clusterizados por tabela. |999<br/><br/>Aplica-se somente a tabelas toorowstore. |
| Índice |Índices clusterizados por tabela. |1<br><br/>Aplica-se tabelas rowstore e columnstore de tooboth. |
| Índice |Tamanho da chave de índice. |900 bytes.<br/><br/>Aplica-se apenas índices toorowstore.<br/><br/>Índices em colunas varchar com um tamanho máximo de mais de 900 bytes podem ser criados se os dados existentes nas colunas Olá Olá não exceder 900 bytes quando Olá índice é criado. No entanto, depois de inserir ou ações de atualização em colunas de saudação que fazer com que o tamanho total de saudação tooexceed 900 bytes falharão. |
| Índice |Colunas de chave por índice. |16<br/><br/>Aplica-se apenas índices toorowstore. Os índices columnstore clusterizados incluem todas as colunas. |
| Estatísticas |Tamanho de saudação combinados valores de coluna. |900 bytes. |
| Estatísticas |As colunas por objeto de estatísticas. |32 |
| Estatísticas |As estatísticas criadas em colunas por tabela. |30.000 |
| Procedimentos Armazenados |Os níveis máximos de aninhamento. |8 |
| Visualizar |Colunas por exibição |1.024 |

## <a name="loads"></a>Cargas
| Categoria | Descrição | Máximo |
|:--- |:--- |:--- |
| Cargas de Polybase |MB por segundo |1<br/><br/>Polybase cargas são limitados tooloading linhas menor que 1MB e não é possível carregar tooVARCHR(MAX), nvarchar (max) ou varbinary (max).<br/><br/> |

## <a name="queries"></a>Consultas
| Categoria | Descrição | Máximo |
|:--- |:--- |:--- |
| Consultar |Consultas em fila em tabelas de usuário. |1000 |
| Consultar |Consultas simultâneas em exibições do sistema. |100 |
| Consultar |Consultas em fila em exibições do sistema |1000 |
| Consultar |Máximo de parâmetros |2098 |
| Batch |Tamanho máximo |65.536*4096 |
| Resultados de SELECT |Colunas por linha |4096<br/><br/>Você nunca pode ter mais de 4096 colunas por linha hello selecione resultado. Não há garantia de que você sempre terá 4096. Se o plano de consulta Olá requer uma tabela temporária, colunas de 1024 Olá por máximo de tabela podem ser aplicadas. |
| SELECIONAR |Subconsultas aninhadas |32<br/><br/>Nunca será possível ter mais de 32 subconsultas aninhadas em uma instrução SELECT. Não há garantia de que você sempre terá 32. Por exemplo, uma junção pode apresentar uma subconsulta no plano de consulta de saudação. número de saudação de subconsultas também pode ser limitado pela memória disponível. |
| SELECIONAR |Colunas por JOIN |1024 colunas<br/><br/>Você nunca pode ter mais de 1024 colunas em Olá junção. Não há garantia de que você sempre terá 1024. Se o plano de junção Olá requer uma tabela temporária com mais colunas do que o resultado de junção hello, Olá 1024 limite se aplica a tabela temporária toohello. |
| SELECIONAR |Bytes por colunas GROUP BY. |8.060<br/><br/>colunas de saudação na cláusula GROUP BY da saudação podem ter um máximo de 8060 bytes. |
| SELECIONAR |Bytes por colunas ORDER BY |8.060 bytes.<br/><br/>colunas de saudação na cláusula ORDER BY da saudação podem ter um máximo de 8060 bytes. |
| Identificadores e constantes por instrução |O número de identificadores referenciados e constantes. |65.535<br/><br/>SQL Data Warehouse limita o número de saudação de identificadores e constantes que podem ser contidos em uma única expressão de uma consulta. Esse limite é de 65.535. Exceder esse número resulta no erro 8632 do SQL Server. Para obter mais informações, veja [Erro interno: foi atingido o limite de serviços de uma expressão][Internal error: An expression services limit has been reached]. |

## <a name="metadata"></a>Metadados
| Exibição do sistema | Máximo de linhas |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10.000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |Número total de trabalhadores DMS para hello mais recente 1000 solicitações de SQL. |
| sys.dm_pdw_errors |10.000 |
| sys.dm_pdw_exec_requests |10.000 |
| sys.dm_pdw_exec_sessions |10.000 |
| sys.dm_pdw_request_steps |Número total de etapas para solicitações de SQL Olá 1000 mais recentes são armazenadas em sys.dm_pdw_exec_requests. |
| sys.dm_pdw_os_event_logs |10.000 |
| sys.dm_pdw_sql_requests |Olá mais recente 1000 solicitações SQL que são armazenadas em sys.dm_pdw_exec_requests. |

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações de referência, consulte [Visão geral de referência do SQL Data Warehouse][SQL Data Warehouse reference overview].

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
