---
title: "tópicos de aaaAll para o serviço do SQL Data Warehouse | Microsoft Docs"
description: "Tabela de todos os tópicos de saudação do serviço do Azure denominada SQL Data Warehouse que existem em http://azure.microsoft.com/documentation/articles/, título e descrição."
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Todos os tópicos sobre o serviço do SQL Data Warehouse do Azure
Este tópico lista todos os tópicos que se aplica diretamente toohello **SQL Data Warehouse** serviço do Azure. Você pode pesquisar esta página da Web para palavras-chave usando **Ctrl + F**, tópicos de saudação toofind de interesse atual.

## <a name="new"></a>Novo
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 1 |[Backups do SQL Data Warehouse](sql-data-warehouse-backups.md) |Saiba mais sobre backups de banco de dados interno do SQL Data Warehouse que permitem que você toorestore um ponto de restauração do Azure SQL Data Warehouse tooa ou uma região geográfica diferente. |

## <a name="updated-articles-sql-data-warehouse"></a>Artigos atualizados, SQL Data Warehouse
Esta seção lista os artigos que foram atualizados recentemente, onde Olá atualizar era grande ou significativa. Para cada artigo atualizado, um trecho aproximado de saudação adicionado markdown texto é exibido. artigos de saudação foram atualizados no intervalo de datas de saudação da **2016-08-22** muito**2016-10-05**.

| &nbsp; | Artigo | Texto atualizado, trecho | Data da atualização |
| ---:|:--- |:--- |:--- |
| 2 |[Carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |bytes/tootrack e arquivos selecione r.command, s.request_id, r.status, count (distinct input_name) como nbr_files, sum (s.bytes_processed) / 1024/1024 como gb_processed de sys.dm_pdw_exec_requests r junção interna sys.dm_pdw_dms_external_work s em r.request_id = s.request_id WHERE r. label  = 'CTAS : Load  cso . DimProduct  '  OU r. label  = 'CTAS : Load  cso . AGRUPAR POR r.command dos FactOnlineSales, s.request_id, r.status CLASSIFICAR POR nbr_files desc, desc gb_processed; |2016-09-07 |
| 3 |[Restauração do SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |* * Pode restaurar um depósito de dados pausada? * * toorestore um data warehouse está em pausa, você precisa toofirst volte a ficar online. Depois que o data warehouse de saudação está novamente online, você tem sete dias de toochoose de pontos de restauração do. * * Restaurar tooa com redundância geográfica região * * se você estiver usando armazenamento com redundância geográfica hello, você pode restaurar Olá data warehouse tooyour emparelhados data center em uma região geográfica diferente. data warehouse de saudação é restaurado a partir do último backup diário de saudação. * * Restaure você pode restaurar um ponto de restauração do banco de dados tooany em Olá últimos sete dias cronograma * *. Instantâneos de iniciar a cada quatro horas tooeight e estão disponíveis por sete dias. Quando um instantâneo possui mais de sete dias, ele expira e seu ponto de restauração fica indisponível. * * Restauração custos * * hello custos de armazenamento para o data warehouse de saudação restaurado é cobrado na taxa de armazenamento do Azure Premium Olá. Se você pausar um depósito de dados restaurado, você é cobrado para armazenamento a taxa de armazenamento do Azure Premium Olá. vantagem de saudação pausar não é que são custos |2016-09-29 |

## <a name="get-started"></a>Introdução
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 4 |[Autenticação tooAzure SQL Data Warehouse](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) e SQL Server authentication tooAzure SQL Data Warehouse. |
| 5 |[Práticas recomendadas para o Azure SQL Data Warehouse](sql-data-warehouse-best-practices.md) |Recomendações e práticas recomendadas que você deve saber quando for desenvolver soluções para o SQL Data Warehouse do Azure. Isto irá ajudá-lo a alcançar o sucesso. |
| 6 |[Drivers do Azure SQL Data Warehouse](sql-data-warehouse-connection-strings.md) |Cadeias de conexão e drivers para SQL Data Warehouse |
| 7 |[Conecte-se tooAzure SQL Data Warehouse](sql-data-warehouse-connect-overview.md) |Como cadeia de conexão e o nome do servidor de saudação toofind do seu SQL Data Warehouse tooAzure |
| 8 |
            [Analisar dados com o Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Use um modelo com base nos dados armazenados no Azure SQL Data Warehouse de aprendizado de máquina previsão de toobuild de aprendizado de máquina do Azure. |
| 9 |[Consultar o SQL Data Warehouse do Azure (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Consultando o Azure SQL Data Warehouse com o utilitário de linha de comando de sqlcmd hello. |
| 10 |[Criar um banco de dados do SQL Data Warehouse usando TSQL (Transact-SQL)](sql-data-warehouse-get-started-create-database-tsql.md) |Saiba como toocreate um Azure SQL Data Warehouse com TSQL |
| 11 |[Como toocreate suporte um tíquete para SQL Data Warehouse](sql-data-warehouse-get-started-create-support-ticket.md) |Como toocreate suporte um tíquete no Azure SQL Data Warehouse. |
| 12 |[Carregar dados com o Azure Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |Saiba mais dados tooload com o Azure Data Factory |
| 13 |[Carregar dados com o PolyBase no SQL Data Warehouse](sql-data-warehouse-get-started-load-with-polybase.md) |Saiba o que é o PolyBase e como toouse para cenários de data warehouse. |
| 14 |[Criar um Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md) |Saiba como toocreate um Azure SQL Data Warehouse em Olá portal do Azure |
| 15 |[Criar um SQL Data Warehouse usando o PowerShell](sql-data-warehouse-get-started-provision-powershell.md) |Criar SQL Data Warehouse usando o PowerShell |
| 16 |[Visualizar os dados com o Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md) |Visualizar os dados do SQL Data Warehouse com o Power BI |
| 17 |[Consultar o SQL Data Warehouse do Azure (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Consultar o SQL Data Warehouse com o Visual Studio. |

## <a name="develop"></a>Desenvolver
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 18 |[Otimização de transações para o SQL Data Warehouse](sql-data-warehouse-develop-best-practices-transactions.md) |Diretrizes de práticas recomendadas sobre como gravar atualizações de transação eficientes no SQL Data Warehouse do Azure |
| 19 |[Gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md) |Compreender o gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse do Azure para desenvolvimento de soluções. |
| 20 |[Instrução Create Table As Select (CTAS) no SQL Data Warehouse](sql-data-warehouse-develop-ctas.md) |Dicas para codificação com hello criar tabela como selecionar instrução (CTAS) no Azure SQL Data Warehouse para o desenvolvimento de soluções. |
| 21 |[SQL dinâmico no SQL Data Warehouse](sql-data-warehouse-develop-dynamic-sql.md) |Dicas para usar SQL dinâmico no SQL Data Warehouse do Azure para desenvolvimento de soluções. |
| 22 |[Agrupar por opções de SQL Data Warehouse](sql-data-warehouse-develop-group-by-options.md) |Dicas para implementar o agrupamento por opções no SQL Data Warehouse do Azure para desenvolver soluções. |
| 23 |[Usar consultas de tooinstrument de rótulos no SQL Data Warehouse](sql-data-warehouse-develop-label.md) |Dicas para usar rótulos tooinstrument consultas no Data Warehouse do Azure SQL para desenvolver soluções. |
| 24 |[Executar loops no SQL Data Warehouse](sql-data-warehouse-develop-loops.md) |Dicas para execução de loops do Transact_SQL e substituição de cursores no SQL Data Warehouse Azure para desenvolver soluções. |
| 25 |[Procedimentos armazenados no SQL Data Warehouse](sql-data-warehouse-develop-stored-procedures.md) |Dicas para implementar procedimentos armazenados no SQL Data Warehouse do Azure para desenvolvimento de soluções. |
| 26 |[Transações no SQL Data Warehouse](sql-data-warehouse-develop-transactions.md) |Dicas para implementar transações no Azure SQL Data Warehouse para o desenvolvimento de soluções. |
| 27 |[Esquemas definidos pelo usuário no SQL Data Warehouse](sql-data-warehouse-develop-user-defined-schemas.md) |Dicas para usar esquemas de Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções. |
| 28 |[Atribuir variáveis no SQL Data Warehouse](sql-data-warehouse-develop-variable-assignment.md) |Dicas para atribuir variáveis de Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções. |
| 29 |[Modos de exibição no SQL Data Warehouse](sql-data-warehouse-develop-views.md) |Dicas para usar exibições Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções. |
| 30 |[Decisões de design e técnicas de codificação para o SQL Data Warehouse](sql-data-warehouse-overview-develop.md) |Conceitos de desenvolvimento, decisões de design, recomendações e técnicas de codificação para o SQL Data Warehouse. |

## <a name="manage"></a>Gerenciar
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 31 |[Gerenciar poder de computação no SQL Data Warehouse do Azure (Visão Geral)](sql-data-warehouse-manage-compute-overview.md) |Funcionalidades de escala horizontal de desempenho no SQL Data Warehouse do Azure. Expansão ajustando DWUs ou pausar e retomar os custos de toosave de recursos de computação. |
| 32 |[Gerenciar poder de computação no SQL Data Warehouse do Azure (portal do Azure)](sql-data-warehouse-manage-compute-portal.md) |Capacidade de computação toomanage tarefas do portal do Azure. Dimensionar recursos de computação ajustando as DWUs. Ou, pausar e retomar os custos de toosave de recursos de computação. |
| 33 |[Gerenciar poder de computação no SQL Data Warehouse do Azure (PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |Capacidade de computação toomanage de tarefas do PowerShell. Dimensionar recursos de computação ajustando as DWUs. Ou, pausar e retomar os custos de toosave de recursos de computação. |
| 34 |[Gerenciar poder de computação no SQL Data Warehouse do Azure (REST)](sql-data-warehouse-manage-compute-rest-api.md) |Capacidade de computação toomanage de tarefas do PowerShell. Dimensionar recursos de computação ajustando as DWUs. Ou, pausar e retomar os custos de toosave de recursos de computação. |
| 35 |[Gerenciar poder de computação no SQL Data Warehouse do Azure (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Transact-SQL (T-SQL) tarefas tooscale desempenho ajustando DWUs. Reduzir custos por meio da redução durante horários que não sejam de pico. |
| 36 |[Monitore sua carga de trabalho usando DMVs](sql-data-warehouse-manage-monitor.md) |Saiba como toomonitor sua carga de trabalho usando DMVs. |
| 37 |[Gerenciar bancos de dados no SQL Data Warehouse do Azure](sql-data-warehouse-overview-manage.md) |Visão geral do gerenciamento de bancos de dados do SQL Data Warehouse. Inclui ferramentas de gerenciamento, DWUs e escalar o desempenho horizontalmente, solucionar problemas de desempenho de consulta, estabelecer políticas de segurança e restaurar um banco de dados contra dados corrompidos ou de uma interrupção regional. |
| 38 |[Monitorar consultas de usuário no SQL Data Warehouse do Azure](sql-data-warehouse-overview-manage-user-queries.md) |Visão geral de considerações de hello, práticas recomendadas e tarefas de monitoramento de consultas de usuário no Azure SQL Data Warehouse |
| 11,8 |[Restauração do SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |Visão geral das opções de restauração de banco de dados de saudação para recuperar um banco de dados no Azure SQL Data Warehouse. |
| 40 |[Restaurar um Azure SQL Data Warehouse (Portal)](sql-data-warehouse-restore-database-portal.md) |Tarefas do portal do Azure para restaurar um Azure SQL Data Warehouse. |
| 41 |[Restaurar um Azure SQL Data Warehouse (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |Tarefas do PowerShell para restaurar um Azure SQL Data Warehouse. |
| 42 |[Recuperar um SQL Data Warehouse do Azure (API REST)](sql-data-warehouse-restore-database-rest-api.md) |Tarefas da API REST para restaurar um Azure SQL Data Warehouse. |

## <a name="tables-and-indexes"></a>Tabelas e índices
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 43 |[Tipos de dados para as tabelas no SQL Data Warehouse](sql-data-warehouse-tables-data-types.md) |Introdução aos tipos de dados para as tabelas do Azure SQL Data Warehouse. |
| 44 |[Distribuindo tabelas no SQL Data Warehouse](sql-data-warehouse-tables-distribute.md) |Introdução à distribuição de tabelas no Azure SQL Data Warehouse. |
| 45 |[Indexando tabelas no SQL Data Warehouse](sql-data-warehouse-tables-index.md) |Introdução à indexação de tabela no Azure SQL Data Warehouse. |
| 46 |[Visão geral das tabelas no SQL Data Warehouse](sql-data-warehouse-tables-overview.md) |Introdução às Tabelas do Azure SQL Data Warehouse. |
| 47 |[Particionando tabelas no SQL Data Warehouse](sql-data-warehouse-tables-partition.md) |Introdução ao particionamento de tabela no Azure SQL Data Warehouse. |
| 48 |[Gerenciamento de estatísticas em tabelas no SQL Data Warehouse](sql-data-warehouse-tables-statistics.md) |Introdução às estatísticas em tabelas no Azure SQL Data Warehouse. |
| 49 |[Tabelas temporárias no SQL Data Warehouse](sql-data-warehouse-tables-temporary.md) |Introdução às tabelas temporárias no Azure SQL Data Warehouse. |

## <a name="integrate"></a>Integração
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 50 |[Use o Azure Data Factory com o SQL Data Warehouse](sql-data-warehouse-integrate-azure-data-factory.md) |Dicas de utilização do  Azure Data Factory (ADF) com o Azure SQL Data Warehouse para o desenvolvimento de soluções. |
| 51 |
            [Use o Azure Machine Learning com o SQL Data Warehouse](sql-data-warehouse-integrate-azure-machine-learning.md) |Tutorial para usar o Azure Machine Learning com o Data Warehouse do SQL Azure para desenvolver soluções. |
| 52 |[Usar o Stream Analytics do Azure com o SQL Data Warehouse](sql-data-warehouse-integrate-azure-stream-analytics.md) |Dicas para usar o Stream Analytics do Azure com o Azure SQL Data Warehouse para desenvolver as soluções. |
| 53 |[Usar o Power BI com o SQL Data Warehouse](sql-data-warehouse-integrate-power-bi.md) |Dicas para usar o Power BI com o SQL Data Warehouse do Azure para desenvolvimento de soluções. |
| 54 |[Aproveitar outros serviços com o SQL Data Warehouse](sql-data-warehouse-overview-integrate.md) |Ferramentas e parceiros com soluções que podem ser integradas ao SQL Data Warehouse |

## <a name="load"></a>Carregar
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 55 |[Carregar dados do Armazenamento de Blobs do Azure no Azure SQL Data Warehouse (Azure Data Factory).](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |Saiba mais dados tooload com o Azure Data Factory |
| 56 |[Carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Saiba como toouse tooload dados do Azure blob storage no SQL Data Warehouse. Carregar algumas tabelas de dados públicos no esquema de Data Warehouse da Contoso varejo hello. |
| 57 |[Carregar dados do SQL Server no Azure SQL Data Warehouse (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Usa bcp tooexport dados de arquivos de tooflat do SQL Server, o armazenamento de blob do AZCopy tooimport dados tooAzure e dados Olá tooingest no Azure SQL Data Warehouse. |
| 58 |[Carregar dados do SQL Server no Azure SQL Data Warehouse (arquivos simples)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |Para um tamanho de dados pequeno, usa bcp tooexport dados de arquivos do SQL Server tooflat e importar dados de saudação diretamente no Azure SQL Data Warehouse. |
| 59 |[Carregar dados do SQL Server no Azure SQL Data Warehouse (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |Mostra como toocreate um SQL Server Integration Services (SSIS) pacote toomove os dados de uma ampla variedade de dados de fontes tooSQL Data Warehouse. |
| 60 |[Carregar dados com o PolyBase no SQL Data Warehouse](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Usa bcp tooexport dados de arquivos de tooflat do SQL Server, o armazenamento de blob do AZCopy tooimport dados tooAzure e dados Olá tooingest no Azure SQL Data Warehouse. |
| 61 |[Guia para usar o PolyBase no SQL Data Warehouse](sql-data-warehouse-load-polybase-guide.md) |Diretrizes e recomendações para usar o PolyBase em cenários do SQL Data Warehouse. |
| 62 |[Carregar dados de amostra no SQL Data Warehouse](sql-data-warehouse-load-sample-databases.md) |Carregar dados de amostra no SQL Data Warehouse |
| 63 |[Carregar dados com o bcp](sql-data-warehouse-load-with-bcp.md) |Saiba quais bcp é e como toouse para cenários de data warehouse. |
| 64 |[Carregar dados no SQL Data Warehouse do Azure](sql-data-warehouse-overview-load.md) |Saiba mais cenários comuns de saudação para carregamento no SQL Data Warehouse de dados. Essas opções incluem usar PolyBase, armazenamento de blobs do Azure, arquivos simples e envio de disco. Você também pode usar ferramentas de terceiros. |

## <a name="migrate"></a>Migrar
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 65 |[Migrar seu tooSQL de código do SQL Data Warehouse](sql-data-warehouse-migrate-code.md) |Dicas para migrar seu código SQL tooAzure SQL Data Warehouse para o desenvolvimento de soluções. |
| 66 |[Migrar seus dados](sql-data-warehouse-migrate-data.md) |Dicas para migrar sua tooAzure de dados SQL Data Warehouse para o desenvolvimento de soluções. |
| 67 |[Utilitário de Migração do Data Warehouse (visualização)](sql-data-warehouse-migrate-migration-utility.md) |Migre tooSQL Data Warehouse. |
| 68 |[Migrar seu tooSQL de esquema do Data Warehouse](sql-data-warehouse-migrate-schema.md) |Dicas para migrar seu tooAzure esquema SQL Data Warehouse para o desenvolvimento de soluções. |
| 69 |[Migrar tooSQL sua solução do Data Warehouse](sql-data-warehouse-overview-migrate.md) |Orientação de migração para colocar sua plataforma de SQL Data Warehouse tooAzure solução. |

## <a name="partners"></a>Parceiros
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 70 |[Parceiros de business intelligence do SQL Data Warehouse](sql-data-warehouse-partner-business-intelligence.md) |Listas de parceiros terceirizados de business intelligence com soluções que dão suporte ao SQL Data Warehouse. |
| 71 |[Parceiros de integração de dados do SQL Data Warehouse](sql-data-warehouse-partner-data-integration.md) |Listas de parceiros terceirizados com soluções de integração de dados que oferecem suporte ao Azure SQL Data Warehouse. |
| 72 |[Parceiros de gerenciamento de dados do SQL Data Warehouse](sql-data-warehouse-partner-data-management.md) |Lista de parceiros terceirizados de gerenciamento de dados com soluções que oferecem suporte ao SQL Data Warehouse. |

## <a name="reference"></a>Referência
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 73 |[Tópicos de referência para o SQL Data Warehouse](sql-data-warehouse-overview-reference.md) |Links de conteúdo de referência para o SQL Data Warehouse. |
| 74 |[Cmdlets do PowerShell e as APIs REST para SQL Data Warehouse](sql-data-warehouse-reference-powershell-cmdlets.md) |Localizar Olá principais cmdlets do PowerShell para Azure SQL Data Warehouse incluindo como toopause e retomar um banco de dados. |
| 75 |[Elementos de linguagem](sql-data-warehouse-reference-tsql-language-elements.md) |Lista de conteúdo de tooreference links para elementos de linguagem Transact-SQL de saudação usado para o SQL Data Warehouse. |
| 76 |[Tópicos do Transact-SQL](sql-data-warehouse-reference-tsql-statements.md) |Conteúdo de tooreference links para tópicos de Transact-SQL Olá usado pelo SQL Data Warehouse. |
| 77 |[Exibições do sistema](sql-data-warehouse-reference-tsql-system-views.md) |Links toosystem exibe o conteúdo para o SQL Data Warehouse. |

## <a name="security"></a>Segurança
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 78 |[SQL Data Warehouse - Suporte de versão anterior a clientes para auditoria e Máscara de Dados Dinâmicos](sql-data-warehouse-auditing-downlevel-clients.md) |Saiba mais sobre o suporte a clientes de versão anterior do SQL Data Warehouse para auditoria de dados |
| 79 |[Auditoria no Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) |Introdução à auditoria no SQL Data Warehouse |
| 80 |[Introdução aos dados TDE (Transparent Data Encryption) no SQL Data Warehouse](sql-data-warehouse-encryption-tde.md) |TDE (Transparent Data Encryption) no SQL Data Warehouse |
| 81 |[Introdução ao Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md) |TDE (Transparent Data Encryption) no SQL Data Warehouse (T-SQL) |
| 82 |[Proteger um banco de dados no SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md) |Dicas para proteger um banco de dados no SQL Data Warehouse do Azure para desenvolvimento de soluções. |

## <a name="miscellaneous"></a>Diversos
| &nbsp; | Title | Descrição |
| ---:|:--- |:--- |
| 83 |[Instalar o Visual Studio e o SSDT para o SQL Data Warehouse](sql-data-warehouse-install-visual-studio.md) |Instalar o Visual Studio e o SSDT (Ferramentas de Desenvolvimento do SQL Server) para o SQL Data Warehouse do Azure |
| 84 |[Migração tooPremium detalhes de armazenamento](sql-data-warehouse-migrate-to-premium-storage.md) |Instruções para migrar um armazenamento de toopremium SQL Data Warehouse existente |
| 85 |[Introdução à detecção de ameaças](sql-data-warehouse-security-threat-detection.md) |Como tooget iniciada com detecção de ameaças |
| 86 |[Limites de capacidade do SQL Data Warehouse](sql-data-warehouse-service-capacity-limits.md) |Valores máximos para conexões, bancos de dados, tabelas e consultas para o SQL Data Warehouse. |
| 87 |[Solução de problemas do Azure SQL Data Warehouse](sql-data-warehouse-troubleshoot.md) |Solução de problemas do Azure SQL Data Warehouse. |

