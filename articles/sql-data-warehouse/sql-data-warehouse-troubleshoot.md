---
title: aaaTroubleshooting Azure SQL Data Warehouse | Microsoft Docs
description: "Solução de problemas do Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Solução de problemas do Azure SQL Data Warehouse
Este tópico lista alguns dos Olá perguntas mais comuns de solução de problemas ouvimos de nossos clientes.

## <a name="connecting"></a>Conexão
| Problema | Resolução |
|:--- |:--- |
| Falha de logon do usuário 'NT AUTHORITY\ANONYMOUS LOGON'. (Microsoft SQL Server, erro: 18456) |Esse erro ocorre quando um usuário do AAD tenta toohello tooconnect banco de dados mestre, mas não tem um usuário em mestre.  toocorrect esse problema, especifique Olá você deseja o tempo de conexão tooat tooconnect ou adicionar Olá usuário toohello banco de dados mestre do SQL Data Warehouse.  Confira o artigo [Visão geral de segurança][Security overview] para obter mais detalhes. |
| servidor de saudação principal "MyUserName" não é capaz de tooaccess hello "mestre" do banco de dados no contexto de segurança atual hello. Não é possível abrir o banco de dados padrão do usuário. Falha no logon. Falha de logon do usuário 'MyUserName'. (Microsoft SQL Server, erro: 916) |Esse erro ocorre quando um usuário do AAD tenta toohello tooconnect banco de dados mestre, mas não tem um usuário em mestre.  toocorrect esse problema, especifique Olá você deseja o tempo de conexão tooat tooconnect ou adicionar Olá usuário toohello banco de dados mestre do SQL Data Warehouse.  Confira o artigo [Visão geral de segurança][Security overview] para obter mais detalhes. |
| Erro CTAIP |Esse erro pode ocorrer quando um logon tiver sido criado no hello SQL server banco de dados mestre, mas não no banco de dados do SQL Data Warehouse Olá.  Se você encontrar esse erro, dê uma olhada Olá [visão geral de segurança] [ Security overview] artigo.  Este artigo explica como toocreate criar um logon e um usuário no mestre e, em seguida, como Olá a toocreate um usuário no banco de dados do SQL Data Warehouse. |
| Bloqueado pelo firewall |Bancos de dados SQL do Azure são protegidos pelo tooensure firewalls de nível de servidor e banco de dados conhecida apenas endereços IP têm o banco de dados do access tooa. firewalls Olá são seguros por padrão, o que significa que você deve habilitar explicitamente e endereço IP ou intervalo de endereços antes de você se conectar.  tooconfigure seu firewall para acesso, execute as etapas de saudação em [configurar o acesso ao servidor de firewall para o IP do cliente] [ Configure server firewall access for your client IP] em Olá [provisionamento instruções] [Provisioning instructions]. |
| Não é possível conectar-se com a ferramenta ou driver |SQL Data Warehouse recomenda o uso de [SSMS][SSMS], [SSDT para Visual Studio][SSDT for Visual Studio], ou [sqlcmd] [ sqlcmd] tooquery seus dados. Para obter mais detalhes sobre drivers e tooSQL conexão do Data Warehouse, consulte [Drivers para o Azure SQL Data Warehouse] [ Drivers for Azure SQL Data Warehouse] e [conectar tooAzure SQL Data Warehouse] [ Connect tooAzure SQL Data Warehouse] artigos. |

## <a name="tools"></a>Ferramentas
| Problema | Resolução |
|:--- |:--- |
| O Pesquisador de objetos do Visual Studio não tem usuários de AAD |Esse é um problema conhecido.  Como alternativa, exibir os usuários Olá [database_principals][sys.database_principals].  Consulte [tooAzure autenticação SQL Data Warehouse] [ Authentication tooAzure SQL Data Warehouse] toolearn mais sobre como usar o Active Directory do Azure SQL Data warehouse. |
|Manual de script, usando o Assistente de script hello ou conectando-se via SSMS é lento, suspenso ou produção erros| Certifique-se de que os usuários foram criados no banco de dados mestre hello. Nas opções de script, também Certifique-se de que a edição do mecanismo de saudação é definida como "Microsoft Azure SQL Data Warehouse Edition" e o tipo de mecanismo é "Microsoft Azure SQL Database".|

## <a name="performance"></a>Desempenho
| Problema | Resolução |
|:--- |:--- |
| Solucionar problemas de desempenho da consulta |Se você estiver tentando tootroubleshoot uma consulta específica, comece com [aprender como toomonitor suas consultas][Learning how toomonitor your queries]. |
| Planos e consultas com um desempenho ruim normalmente são o resultado da falta de estatísticas |causa mais comum de saudação do baixo desempenho é a falta de estatísticas em tabelas.  Consulte [manter estatísticas de tabela] [ Statistics] para obter detalhes sobre como toocreate estatísticas e porque eles tooyour crítico de desempenho. |
| Baixa simultaneidade/consultas em fila |Noções básicas sobre [gerenciamento de carga de trabalho] [ Workload management] é importante em ordem toounderstand como toobalance alocação de memória com simultaneidade. |
| Como tooimplement práticas recomendadas |Olá melhor lugar toostart toolearn maneiras tooimprove desempenho de consulta é [práticas recomendadas do SQL Data Warehouse] [ SQL Data Warehouse best practices] artigo. |
| Como tooimprove desempenho com o dimensionamento |Às vezes, o desempenho da solução de saudação tooimproving é toosimply adicionar mais consultas tooyour potência de computação [dimensionando o Data Warehouse do SQL][Scaling your SQL Data Warehouse]. |
| Desempenho ruim da consulta como resultado da baixa qualidade do índice |Às vezes, as consultas podem apresentar lentidão devido à [Baixa qualidade do índice columnstore][Poor columnstore index quality].  Consulte este artigo para obter mais informações e como muito[recompilar índices qualidade de segmento tooimprove][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Gerenciamento do sistema
| Problema | Resolução |
|:--- |:--- |
| Msg 40847: Não foi possível executar a operação de saudação porque o servidor excederia Olá permitido da cota de unidade de transação do banco de dados de 45000. |Reduza Olá [DWU] [ DWU] de banco de dados de saudação tentar toocreate ou [solicitar um aumento de cota][request a quota increase]. |
| Investigação da utilização de espaço |Consulte [tamanhos de tabela] [ Table sizes] toounderstand utilização do espaço de saudação do seu sistema. |
| Ajuda com o gerenciamento de tabelas |Consulte Olá [visão geral da tabela] [ Overview] artigo para obter ajuda com o gerenciamento de suas tabelas.  Este artigo também inclui links para tópicos mais detalhados, como [Tipos de dados de tabela][Data types], [Distribuindo uma tabela][Distribute], [Indexando uma tabela][Index], [Particionando uma tabela][Partition], [Mantendo as estatísticas da tabela][Statistics] e [Tabelas temporárias][Temporary]. |
|Barra de progresso (TDE) criptografia transparente de dados não está atualizando no hello Portal do Azure|Você pode exibir o estado de saudação de TDE por meio de [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>Polybase
| Problema | Resolução |
|:--- |:--- |
| Falha no carregamento devido a linhas grandes |Atualmente, o suporte para linhas grandes não está disponível para o Polybase.  Isso significa que se sua tabela contiver varchar (max), nvarchar (max) ou varbinary (max), tabelas externas não podem ser usado tooload seus dados.  Carrega linhas grande é atualmente só tem suporte por meio do Azure Data Factory (com BCP), Azure Stream Analytics, SSIS, BCP ou Olá classe .NET SQLBulkCopy. O suporte do PolyBase para linhas grandes será adicionado em uma versão futura. |
| Falha de carregamento bcp de tabela com o tipo de dados MAX |Há um problema conhecido que requer que varchar (max), nvarchar (max) ou varbinary (max) seja colocado no final de saudação da tabela de saudação em alguns cenários.  Tente mover o final de toohello MAX colunas da tabela de saudação. |

## <a name="differences-from-sql-database"></a>Diferenças do Banco de Dados SQL
| Problema | Resolução |
|:--- |:--- |
| Recursos do Banco de Dados SQL sem suporte |Confira [Recursos de tabela sem suporte][Unsupported table features]. |
| Tipos de dados do Banco de Dados SQL sem suporte |Confira [Tipos de dados sem suporte][Unsupported data types]. |
| Limitações de DELETE e UPDATE |Consulte [soluções alternativas de atualização][UPDATE workarounds], [soluções alternativas de exclusão] [ DELETE workarounds] e [toowork usando CTAS em torno de atualização sem suporte e Sintaxe DELETE][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| Não há suporte para a instrução MERGE |Confira [Soluções alternativas para MERGE][MERGE workarounds]. |
| Limitações de procedimento armazenado |Consulte [limitações do procedimento de armazenado] [ Stored procedure limitations] toounderstand algumas das limitações de saudação de procedimentos armazenados. |
| UDFs não oferecem suporte a instruções SELECT |Esta é uma limitação atual de nossos UDFs.  Consulte [CREATE FUNCTION] [ CREATE FUNCTION] para obter a sintaxe de saudação oferecemos suporte. |

## <a name="next-steps"></a>Próximas etapas
Se você estiver foram toofind não é possível um problema de tooyour solução acima, aqui estão alguns outros recursos que você pode tentar.

* [Blogs]
* [Solicitações de recursos]
* [Vídeos]
* [Blogs da equipe CAT]
* [Criar um tíquete de suporte]
* [Fórum do MSDN]
* [Fórum Stack Overflow]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Criar um tíquete de suporte]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogs da equipe CAT]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Solicitações de recursos]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Fórum do MSDN]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Fórum Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vídeos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
