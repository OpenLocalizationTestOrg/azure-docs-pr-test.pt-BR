---
title: "códigos de erro aaaSQL - erro de conexão de banco de dados | Microsoft Docs"
description: "Saiba mais sobre os códigos de erro de SQL para aplicativos cliente do Banco de Dados SQL, como erros comuns de conexão de banco de dados, problemas de cópia de banco de dados e erros gerais. "
keywords: "código de erro de sql, acessar sql, erro de conexão de banco de dados, códigos de erro de sql"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>Códigos de erro de SQL para aplicativos cliente do Banco de Dados SQL: erro de conexão de banco de dados e outros problemas
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


Este artigo lista os códigos de erro de SQL para aplicativos cliente do Banco de Dados SQL, incluindo erros de conexão de banco de dados, erros transitórios (também chamados de falhas transitórias), erros de governança de recursos, problemas de cópia de banco de dados, pool elástico e outros erros. A maioria das categorias são tooAzure determinado banco de dados SQL e não se aplicam a tooMicrosoft do SQL Server.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>Erros de conexão de banco de dados, erros transitórios e outros erros temporários
Olá tabela a seguir aborda os códigos de erro SQL Olá para erros de perda de conexão e outros erros transitórios, que você pode encontrar ao seu aplicativo tenta tooaccess banco de dados SQL. Para obter tutoriais de introdução sobre como tooconnect tooAzure banco de dados SQL, consulte [conexão tooAzure banco de dados SQL](sql-database-libraries.md).

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>Erros de conexão de banco de dados mais comuns e erros de falhas transitórias mais comuns
Olá infraestrutura do Azure tem Olá capacidade toodynamically reconfigurar os servidores quando surgem cargas de trabalho pesadas em Olá serviço de banco de dados SQL.  Esse comportamento dinâmico pode causar a seu cliente toolose programa tooSQL sua conexão banco de dados. Essa variante de condição de erro é chamada de uma *falha transitória*.

É altamente recomendável que seu programa cliente tem a lógica de repetição para que ele pôde restabelecer uma conexão após conceder Olá falhas transitórias tempo toocorrect em si.  É recomendável que você aguarde 5 segundos antes de sua primeira tentativa. Repetir após um intervalo menor do que 5 segundos corre o risco de serviço de nuvem Olá imenso. Para cada repetição subsequente atraso Olá deve crescer exponencialmente, tooa máximo de 60 segundos.

Erros de falha transitória normalmente manifesto como uma das seguintes mensagens de erro de seus programas de cliente de saudação:

* O banco de dados &lt;nome_do_bd&gt; no servidor &lt;instância_do_Azure&gt; não está disponível no momento. Tente novamente mais tarde a conexão hello. Se Olá problema persistir, entre em contato com o atendimento ao cliente e fornecê-los a ID de rastreamento da sessão Olá &lt;session_id&gt;
* O banco de dados &lt;nome_do_bd&gt; no servidor &lt;instância_do_Azure&gt; não está disponível no momento. Tente novamente mais tarde a conexão hello. Se Olá problema persistir, entre em contato com o atendimento ao cliente e fornecê-los a ID de rastreamento da sessão Olá &lt;session_id&gt;. (Microsoft SQL Server, erro: 40613)
* Uma conexão existente foi fechada forçadamente pelo host remoto hello.
* System.Data.Entity.Core.EntityCommandExecutionException: Ocorreu um erro ao executar a definição de comando hello. Consulte a exceção interna para obter detalhes hello. ---> System.Data.SqlClient.SqlException: Ocorreu um erro de nível de transporte ao receber os resultados do servidor de saudação. (provedor: Provedor de Sessão, erro: 19 - a conexão física não é utilizável)
* Um conexão tentativa tooa banco de dados secundário falhou porque a saudação de banco de dados no processo de saudação do reconfguration e está ocupado aplicar novas páginas ao mesmo tempo no meio de saudação de uma transação ativa no banco de dados primário hello. 

Para obter exemplos de código de lógica de repetição, consulte:

* [Bibliotecas de conexões para Banco de Dados SQL e SQL Server](sql-database-libraries.md) 
* [Erros de conexão toofix ações e erros transitórios no banco de dados SQL](sql-database-connectivity-issues.md)

Uma discussão de saudação *período de bloqueio* para clientes que usam o ADO.NET está disponível em [Pooling de Conexão do SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

### <a name="transient-fault-error-codes"></a>Códigos de erros de falha transitória
Olá erros a seguir são transitórios e devem ser repetidos na lógica do aplicativo 

| Código do erro | Severidade | Descrição |
| ---:| ---:|:--- |
| 4060 |16 |Não é possível abrir o banco de dados "%. & #x2a; ls" solicitado pelo logon hello. Falha no logon de saudação. |
| 40197 |17 |serviço de saudação encontrou um erro ao processar sua solicitação. Tente novamente. Código de erro %d.<br/><br/>Você receberá esse erro quando hello está inoperante devido toosoftware ou atualizações de hardware, falhas de hardware ou outros problemas de failover. código de erro de saudação (%d) inserido na mensagem de saudação de erro 40197 fornece informações adicionais sobre o tipo de saudação de falha ou failover ocorrido. Alguns exemplos de erro Olá códigos são inseridos na mensagem de saudação de erro 40197 são 40020, 40143, 40166 e 40540.<br/><br/>Servidor de banco de dados SQL tooyour reconectar automaticamente conectará tooa a cópia íntegra do seu banco de dados. Seu aplicativo deve capturar o erro 40197, log Olá inserido código de erro (%d) na mensagem de saudação para solução de problemas e tente se reconectar tooSQL banco de dados até que Olá recursos estão disponíveis e sua conexão é restabelecida. |
| 40501 |20 |serviço de saudação está ocupado no momento. Repita a solicitação de saudação após 10 segundos. ID do incidente: %ls. Código: %d.<br/><br/>*Observação:* para obter mais informações, consulte:<br/>• [Limites de recursos do Banco de Dados SQL do Azure](sql-database-resource-limits.md). |
| 40613 |17 |O banco de dados “%.&#x2a;ls” no servidor “%.&#x2a;ls” não está disponível momento. Tente novamente mais tarde a conexão hello. Se Olá problema persistir, entre em contato com o atendimento ao cliente e forneça Olá ID de rastreamento de sessão de '%. & #x2a; ls'. |
| 49918 |16 |Não é possível processar a solicitação. Não há tooprocess de recursos de solicitação.<br/><br/>serviço de saudação está ocupado no momento. Tente novamente a solicitação hello mais tarde. |
| 49919 |16 |Não é possível criar o processo ou atualizar a solicitação. Muitas operações de criação ou atualização em andamento para a assinatura "%ld".<br/><br/>saudação de serviço está ocupada processando várias criar ou atualizar solicitações para sua assinatura ou o servidor. As solicitações estão bloqueadas no momento para a otimização de recursos. Consulte [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) para obter as operações pendentes. Espere até que as solicitações pendentes de criação ou atualização sejam concluídas ou exclua uma das suas solicitações pendentes e tente a solicitação novamente mais tarde. |
| 49920 |16 |Não é possível processar a solicitação. Muitas operações em andamento para assinatura "% ld".<br/><br/>serviço de saudação estiver ocupado processando várias solicitações para essa assinatura. As solicitações estão bloqueadas no momento para a otimização de recursos. Consulte [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) para obter o status da operação. Espere até que as solicitações pendentes estejam concluídas ou exclua uma das suas solicitações pendentes e tente a solicitação novamente mais tarde. |
| 4221 |16 |Falha de logon tooread-secundário devido toolong aguardar 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING'. réplica Olá não está disponível para logon porque as versões de linha estão ausentes para transações que estão em curso quando a réplica de saudação foi reciclada. Olá pode ser resolvido, reverter ou confirmar transações ativas de saudação na réplica primária Olá. Ocorrências dessa condição podem ser minimizadas, evitando transações de gravação longo em Olá primário. |

## <a name="database-copy-errors"></a>Erros de cópia de banco de dados
Olá, os erros a seguir pode ser encontrado ao copiar um banco de dados no banco de dados do SQL Azure. Para saber mais, confira [Copiar um Banco de Dados SQL do Azure](sql-database-copy.md).

| Código do erro | Severidade | Descrição |
| ---:| ---:|:--- |
| 40635 |16 |O cliente com endereço IP “%.&#x2a;ls” está desabilitado temporariamente. |
| 40637 |16 |A criação da cópia do banco de dados está desabilitada no momento. |
| 40561 |16 |Falha na cópia do banco de dados. O banco de dados de origem ou destino de saudação não existe. |
| 40562 |16 |Falha na cópia do banco de dados. banco de dados de origem de saudação foi descartado. |
| 40563 |16 |Falha na cópia do banco de dados. banco de dados de destino Olá foi descartado. |
| 40564 |16 |Falha na cópia de banco de dados devido a erro interno tooan. Remova o banco de dados de destino e tente novamente. |
| 40565 |16 |Falha na cópia do banco de dados. Cópia de banco de dados simultâneas não mais de 1 de saudação de mesma origem é permitida. Remova o banco de dados de destino e tente novamente mais tarde. |
| 40566 |16 |Falha na cópia de banco de dados devido a erro interno tooan. Remova o banco de dados de destino e tente novamente. |
| 40567 |16 |Falha na cópia de banco de dados devido a erro interno tooan. Remova o banco de dados de destino e tente novamente. |
| 40568 |16 |Falha na cópia do banco de dados. O banco de dados de origem tornou-se indisponível. Remova o banco de dados de destino e tente novamente. |
| 40569 |16 |Falha na cópia do banco de dados. O banco de dados de destino tornou-se indisponível. Remova o banco de dados de destino e tente novamente. |
| 40570 |16 |Falha na cópia de banco de dados devido a erro interno tooan. Remova o banco de dados de destino e tente novamente mais tarde. |
| 40571 |16 |Falha na cópia de banco de dados devido a erro interno tooan. Remova o banco de dados de destino e tente novamente mais tarde. |

## <a name="resource-governance-errors"></a>Erros de governança de recursos
Olá os erros a seguir é causado pelo uso excessivo de recursos enquanto estiver trabalhando com o banco de dados do SQL Azure. Por exemplo:

* Uma transação está aberta há muito tempo.
* Uma transação está mantendo bloqueios demais.
* Um aplicativo está consumindo muita memória.
* Um aplicativo está consumindo muito espaço de `TempDb` .

Tópicos relacionados:

* Informações mais detalhadas estão disponíveis aqui: [Limites de recursos do Banco de Dados SQL do Azure](sql-database-resource-limits.md)

| Código do erro | Severidade | Descrição |
| ---:| ---:|:--- |
| 10928 |20 |ID do recurso: %d. limite de %s de saudação do banco de dados de saudação é %d e foi atingido. Para saber mais, confira [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637).<br/><br/>Olá ID do recurso indica o recurso de saudação que já atingiu o limite de saudação. Para threads de trabalho, Olá ID de recursos = 1. Para sessões, Olá ID de recursos = 2.<br/><br/>*Observação:* para obter mais informações sobre o erro e como tooresolve, consulte:<br/>• [Limites de recursos do Banco de Dados SQL do Azure](sql-database-resource-limits.md). |
| 10929 |20 |ID do recurso: %d. garantia mínima de %s Olá é %d, o limite máximo é %d e uso atual de saudação do banco de dados de saudação é %d. No entanto, servidor de saudação está muito ocupado toosupport solicitações maior %d deste banco de dados. Para saber mais, confira [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637). Caso contrário, tente novamente mais tarde.<br/><br/>Olá ID do recurso indica o recurso de saudação que já atingiu o limite de saudação. Para threads de trabalho, Olá ID de recursos = 1. Para sessões, Olá ID de recursos = 2.<br/><br/>*Observação:* para obter mais informações sobre o erro e como tooresolve, consulte:<br/>• [Limites de recursos do Banco de Dados SQL do Azure](sql-database-resource-limits.md). |
| 40544 |20 |banco de dados de saudação atingiu sua cota de tamanho. Particione ou exclua dados, remova índices ou consulte a documentação de saudação para obter possíveis resoluções. |
| 40549 |16 |A sessão foi encerrada porque você tem uma transação de longa duração. Tente encurtar a transação. |
| 40550 |16 |Olá sessão foi encerrada porque adquiriu muitos bloqueios. Tente ler ou modificar menos linhas em uma única transação. |
| 40551 |16 |Olá sessão foi encerrada devido a excesso `TEMPDB` uso. Tente modificar o uso de espaço de tabela temporária do consulta tooreduce hello.<br/><br/>*Dica:* se você estiver usando objetos temporários, conserve espaço no hello `TEMPDB` removendo objetos temporários depois que não são mais necessários por sessão de saudação do banco de dados. |
| 40552 |16 |Olá sessão foi encerrada devido ao uso de espaço de log de transações excessiva. Tente modificar menos linhas em uma única transação.<br/><br/>*Dica:* se você executar inserções em massa usando Olá `bcp.exe` utilitário ou hello `System.Data.SqlClient.SqlBulkCopy` classe, tente usar Olá `-b batchsize` ou `BatchSize` número de saudação toolimit opções de linhas copiadas toohello server em cada transação. Se você estiver reconstruindo um índice com hello `ALTER INDEX` instrução, tente usar Olá `REBUILD WITH ONLINE = ON` opção. |
| 40553 |16 |Olá sessão foi encerrada devido ao uso excessivo de memória. Tente modificar sua consulta tooprocess menos linhas.<br/><br/>*Dica:* reduzindo o número de saudação do `ORDER BY` e `GROUP BY` operações no seu código Transact-SQL reduz os requisitos de memória de saudação de sua consulta. |

## <a name="elastic-pool-errors"></a>Erros de pool elástico
Olá os erros a seguir é toocreating relacionada e usar Pools de Elastics.

| ErrorNumber | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |pool Elástico Olá atingiu seu limite de armazenamento. uso do armazenamento Olá para pool Elástico Olá não pode exceder (%d) MBs. |O limite de espaço do pool elástico é medido em MB. |Tentando toowrite dados tooa banco de dados quando o limite de armazenamento de saudação do pool Elástico Olá foi atingido. |. Considere crescentes DTUs de saudação do hello pool Elástico se possível na ordem tooincrease seu limite de armazenamento, reduzir o armazenamento de saudação usado por bancos de dados individuais dentro de pool Elástico hello ou remover bancos de dados do pool Elástico hello. |
| 10929 |EX_USER |garantia mínima de %s Olá é %d, o limite máximo é %d e uso atual de saudação do banco de dados de saudação é %d. No entanto, servidor de saudação está muito ocupado toosupport solicitações maior %d deste banco de dados. Consulte [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) para obter assistência. Caso contrário, tente novamente mais tarde. |Mínimo de DTUs por banco de dados; máximo de DTUs por banco de dados |Olá número total de trabalhos simultâneos (solicitações) em todos os bancos de dados no limite do pool de saudação do hello pool Elástico tooexceed tentativa. |. Considere aumentar Olá DTUs do hello pool Elástico se possível na ordem tooincrease seu limite de trabalho, ou remover bancos de dados do pool Elástico hello. |
| 40844 |EX_USER |O banco de dados '%ls' no servidor '%ls' é um banco de dados edição '%ls' em um pool elástico e não pode ter um relacionamento de cópia contínuo. |nome do banco de dados, edição do banco de dados, nome do servidor |Um comando StartDatabaseCopy é emitido para um banco de dados não premium em um pool elástico. |Em breve |
| 40857 |EX_USER |Pool elástico não encontrado para o servidor: '%ls', nome do pool elástico: '%ls'. |nome do servidor; nome do pool elástico |Pool Elástico especificado não existe no servidor de saudação especificado. |Forneça um nome de pool elástico válido. |
| 40858 |EX_USER |O pool elástico '%ls' já existe no servidor: '%ls' |nome do pool elástico, nome do servidor |Pool Elástico especificado já existe no servidor lógico especificado de saudação. |Forneça um novo nome de pool elástico. |
| 40859 |EX_USER |O pool elástico não dá suporte à camada de serviço '%ls'. |camada de serviço do pool elástico |A camada de serviço especificada não dá suporte ao provisionamento de pool elástico. |Fornecer a edição correta Olá ou deixar a camada de serviço do serviço da camada toouse em branco saudação padrão. |
| 40860 |EX_USER |A combinação de pool elástico '%ls' e objetivo de serviço '%ls' é inválida. |nome do pool elástico; nome de objetivo de nível de serviço |O pool elástico e o objetivo de serviço podem ser especificados juntos somente se o objetivo de serviço for especificado como “ElasticPool”. |Especifique a combinação correta de pool elástico e objetivo de serviço. |
| 40861 |EX_USER |edição de banco de dados de saudação ' %. *ls' não podem ser diferentes da camada de serviço do pool Elástico Olá que é ' %.* ls'. |edição do banco de dados, camada de serviço do pool elástico |edição de banco de dados de saudação é diferente da camada de serviço de pool Elástico hello. |Não especifique uma edição do banco de dados que é diferente da camada de serviço de pool Elástico hello.  Observe que essa edição do banco de dados de saudação não precisa toobe especificado. |
| 40862 |EX_USER |Nome do pool Elástico deve ser especificado se o objetivo de serviço de pool Elástico Olá for especificado. |Nenhum |O objetivo de serviço do pool elástico não identifica exclusivamente um pool elástico. |Especifique o nome do pool Elástico Olá se usando o objetivo de serviço de pool Elástico Olá. |
| 40864 |EX_USER |Olá DTUs para pool Elástico Olá deve ter pelo menos (%d) DTUs para a camada de serviço ' %. * ls'. |DTUs para o pool elástico; camada de serviço do pool elástico. |Tentando tooset Olá DTUs para pool Elástico de saudação abaixo do limite mínimo de saudação. |Tente novamente a configuração Olá DTUs para Olá pool Elástico tooat menos limite mínimo de saudação. |
| 40865 |EX_USER |Olá DTUs para pool Elástico Olá não pode exceder (%d) DTUs para a camada de serviço ' %. * ls'. |DTUs para o pool elástico; camada de serviço do pool elástico. |Tentando tooset Olá DTUs para pool Elástico de saudação acima do limite máximo de saudação. |Tente definir Olá DTUs para Olá pool Elástico toono maior que o limite máximo de saudação. |
| 40867 |EX_USER |Olá máximo de DTU por banco de dados deve ser de pelo menos (%d) para a camada de serviço ' %. * ls'. |máximo de DTUs por banco de dados, camada de serviço do pool elástico |Tentar tooset Olá máximo de DTU por banco de dados abaixo Olá o limite suportado. |Considere usar a camada de serviço do pool Elástico Olá que dá suporte à configuração de saudação desejada. |
| 40868 |EX_USER |Olá máximo de DTU por banco de dados não pode exceder (%d) para a camada de serviço ' %. * ls'. |máximo de DTUs por banco de dados, camada de serviço do pool elástico. |Tentar tooset Olá máximo de DTU por banco de dados além Olá o limite suportado. |Considere usar a camada de serviço do pool Elástico Olá que dá suporte à configuração de saudação desejada. |
| 40870 |EX_USER |Olá mínimo de DTU por banco de dados não pode exceder (%d) para a camada de serviço ' %. * ls'. |mínimo de DTUs por banco de dados, camada de serviço do pool elástico. |Tentar tooset Olá DTU min por banco de dados além da saudação o limite suportado. |Considere usar a camada de serviço do pool Elástico Olá que dá suporte à configuração de saudação desejada. |
| 40873 |EX_USER |número de saudação de bancos de dados (%d) e o mínimo de DTU por banco de dados (%d) não pode exceder Olá DTUs do pool Elástico de saudação (%d). |Número de bancos de dados no pool elástico; mínimo de DTUs por banco de dados; DTUs do pool elástico. |Tentando toospecify DTU mínimo para bancos de dados no pool Elástico Olá excede Olá DTUs do pool Elástico hello. |Considere aumentar Olá DTUs do pool Elástico do hello, ou diminuir Olá mínimo de DTU por banco de dados ou diminuir Olá número de bancos de dados no pool Elástico hello. |
| 40877 |EX_USER |Não é possível excluir um pool elástico, a menos que ele não contenha bancos de dados. |Nenhum |pool Elástico Olá contém um ou mais bancos de dados e, portanto, não pode ser excluído. |Por favor, remover bancos de dados do pool Elástico de saudação em ordem toodelete-lo. |
| 40881 |EX_USER |Olá pool Elástico ' %. * ls' atingiu seu limite de contagem de banco de dados.  limite de contagem de banco de dados de saudação para pool Elástico Olá não pode exceder (%d) para um pool Elástico com DTUs (%d). |Nome do pool elástico; limite de contagem de bancos de dados do pool elástico; e DTUs para pool de recursos. |Tentativa de toocreate ou adicionar pool de tooelastic do banco de dados quando o limite de contagem de banco de dados de saudação do pool Elástico Olá foi atingido. |. Considere aumentar Olá DTUs do hello pool Elástico se possível na ordem tooincrease seu limite de banco de dados, ou remover bancos de dados do pool Elástico hello. |
| 40889 |EX_USER |Olá DTUs ou limite de armazenamento do pool Elástico Olá ' %. * ls' não podem ser diminuídos desde que não ofereceria espaço de armazenamento suficiente para seus bancos de dados. |Nome do pool elástico. |Tentativa de limite de armazenamento toodecrease saudação do pool Elástico de saudação abaixo o uso do armazenamento. |Considere reduzir o uso de armazenamento de saudação de bancos de dados individuais no pool Elástico hello ou remover bancos de dados do pool de saudação em ordem tooreduce seu DTUs ou armazenamento limite. |
| 40891 |EX_USER |Olá mínimo de DTU por banco de dados (%d) não pode exceder Olá DTU máx por banco de dados (%d). |Mínimo de DTUs por banco de dados; máximo de DTUs por banco de dados. |Tentando tooset Olá DTU min por banco de dados maior do que Olá máximo de DTU por banco de dados. |Certifique-se de saudação DTU min por bancos de dados não exceda Olá máximo de DTU por banco de dados. |
| TBD |EX_USER |tamanho do armazenamento de saudação para um banco de dados individual em um pool Elástico não pode exceder o tamanho máximo de saudação permitido por ' %. * ls' pool Elástico da camada de serviço. |camada de serviço do pool elástico |tamanho máximo de saudação do banco de dados de saudação excede o tamanho máximo de saudação permitido pela camada de serviço do pool Elástico hello. |Defina o tamanho máximo de saudação do banco de dados hello dentro dos limites de tamanho máximo de saudação permitido pela camada de serviço do pool Elástico Olá Olá. |

Tópicos relacionados:

* [Criar um pool elástico (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [Gerenciar um pool elástico (C#)](sql-database-elastic-pool-manage-csharp.md). 
* [Criar um pool elástico (PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [Monitorar e gerenciar um pool elástico (PowerShell)](sql-database-elastic-pool-manage-powershell.md).

## <a name="general-errors"></a>Erros gerais
Olá, os erros a seguir não se encaixam em quaisquer categorias anteriores.

| Código do erro | Severidade | Descrição |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin> não é um nome válido porque contém caracteres inválidos. |
| 18452 |14 |Falha no logon. Olá logon é de um domínio não confiável e não pode ser usado com o Windows authentication.%. & #x2a; ls (logons do Windows não têm suporte nesta versão do SQL Server.) |
| 18456 |14 |Falha de logon do usuário ' %. #x2a;ls'.%. & #x2a % ls. & #x2a; ls (Falha de logon de saudação do usuário "%. & #x2a; ls". Falha na alteração de senha de saudação. A alteração de senha durante o logon não tem suporte nesta versão do SQL Server.) |
| 18470 |14 |Falha no logon do usuário '%.&#x2a;ls'. Motivo: a conta de saudação é disabled.%. & #x2a; ls |
| 40014 |16 |Vários bancos de dados não podem ser usados em Olá mesma transação. |
| 40054 |16 |Tabelas sem um índice clusterizado não têm suporte nesta versão do SQL Server. Criar um índice clusterizado e tente novamente. |
| 40133 |15 |Esta operação não tem suporte nesta versão do SQL Server. |
| 40506 |16 |O SID especificado é inválido para esta versão do SQL Server. |
| 40507 |16 |'%.&#x2a;ls' não pode ser invocado com parâmetros nesta versão do SQL Server. |
| 40508 |16 |Instrução USE não é tooswitch com suporte entre bancos de dados. Use um nova conexão tooconnect tooa banco de dados diferente. |
| 40510 |16 |A instrução '%.&#x2a;ls' não tem suporte nesta versão do SQL Server |
| 40511 |16 |A função incorporada '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. |
| 40512 |16 |O recurso substituído '%ls' não tem suporte nesta versão do SQL Server. |
| 40513 |16 |A variável do servidor '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. |
| 40514 |16 |'ls' não tem suporte nesta versão do SQL Server. |
| 40515 |16 |Nome de referência toodatabase e/ou servidor em '%. & #x2a; ls' não tem suporte nesta versão do SQL Server. |
| 40516 |16 |Objetos temporários globais não têm suporte nesta versão do SQL Server. |
| 40517 |16 |A opção de instrução ou palavra-chave '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. |
| 40518 |16 |O comando DBCC '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. |
| 40520 |16 |A classe protegível '%S_MSG' não tem suporte nesta versão do SQL Server. |
| 40521 |16 |A classe protegível '% S_MSG' não tem suporte no escopo do servidor de saudação nesta versão do SQL Server. |
| 40522 |16 |O banco de dados com tipo de entidade de segurança '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. |
| 40523 |16 |A criação de usuário implícito '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. Crie usuário Olá explicitamente antes de usá-lo. |
| 40524 |16 |O tipo de dados '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. |
| 40525 |16 |WITH 'ls' não tem suporte nesta versão do SQL Server. |
| 40526 |16 |O provedor de conjunto de linhas '%.&#x2a;ls' não tem suporte nesta versão do SQL Server. |
| 40527 |16 |Os servidores vinculados não têm suporte nesta versão do SQL Server. |
| 40528 |16 |Os usuários não podem ser mapeado toocertificates, chaves assimétricas ou logons do Windows nesta versão do SQL Server. |
| 40529 |16 |A função incorporada '%.&#x2a;ls' no contexto de representação não tem suporte nesta versão do SQL Server. |
| 40532 |11 |Não é possível abrir o servidor "%. & #x2a; ls" solicitado pelo logon hello. Falha no logon de saudação. |
| 40553 |16 |Olá sessão foi encerrada devido ao uso excessivo de memória. Tente modificar sua consulta tooprocess menos linhas.<br/><br/>*Observação:* reduzindo o número de saudação do `ORDER BY` e `GROUP BY` operações no seu código Transact-SQL ajuda a reduzir os requisitos de memória de saudação de sua consulta. |
| 40604 |16 |Pode não CREATE/ALTER DATABASE, pois isso excederia a cota de saudação do servidor de saudação. |
| 40606 |16 |Anexar bancos de dados não tem suporte nesta versão do SQL Server. |
| 40607 |16 |Logons do Windows não têm suporte nesta versão do SQL Server. |
| 40611 |16 |Os servidores podem ter no máximo 128 regras de firewall definidas. |
| 40614 |16 |O endereço IP inicial da regra de firewall não pode ultrapassar o endereço IP final. |
| 40615 |16 |Não é possível abrir o servidor '{0}' solicitado pelo logon hello. Cliente com endereço IP '\\{1 \\}' não é permitido para servidor de saudação tooaccess.  tooenable acesso, use Olá Portal do banco de dados SQL ou execute sp_set_firewall_rule no banco de dados mestre de saudação toocreate uma regra de firewall para esse endereço IP ou intervalo de endereços.  Pode levar até toofive minutos para esse efeito tootake de alteração. |
| 40617 |16 |nome de regra de firewall de saudação que começa com <rule name> é muito longo. O comprimento máximo é 128. |
| 40618 |16 |nome da regra de firewall Olá não pode ficar vazio. |
| 40620 |16 |Falha no logon de saudação do usuário "%. & #x2a; ls". Falha na alteração de senha de saudação. A alteração de senha durante o logon não tem suporte nesta versão do SQL Server. |
| 40627 |20 |A operação no servidor '{0}' e banco de dados '{1}' está em andamento. Aguarde alguns minutos antes de tentar novamente. |
| 40630 |16 |Falha na validação da senha. senha de Olá não atende aos requisitos da política porque é muito curta. |
| 40631 |16 |senha de saudação especificado é muito longa. senha Olá deve ter não mais de 128 caracteres. |
| 40632 |16 |Falha na validação da senha. senha de saudação não atende aos requisitos da política porque ele não é complexo o bastante. |
| 40636 |16 |Não é possível usar um nome de banco de dados reservado '%.&#x2a;ls' nesta operação. |
| 40638 |16 |ID de assinatura inválida <subscription-id>. A assinatura não existe. |
| 40639 |16 |Solicitação não está de acordo com tooschema: <schema error>. |
| 40640 |20 |servidor de saudação encontrou uma exceção inesperada. |
| 40641 |16 |Olá especificado local é inválido. |
| 40642 |17 |servidor Hello está muito ocupado no momento. Tente novamente mais tarde. |
| 40643 |16 |Olá especificado o valor do cabeçalho x-ms-version é inválido. |
| 40644 |14 |Falha tooauthorize acesso toohello especificado assinatura. |
| 40645 |16 |Servername <servername> não pode ser nulo ou vazio. Ele pode ser composto somente por letras minúsculas 'a'-'z', números de saudação 0-9 e hífen hello. hífen Olá não pode levar ou terminar Olá nome. |
| 40646 |16 |A ID da assinatura não pode ficar vazia. |
| 40647 |16 |A assinatura <id da assinatura> não tem um nome de servidor. |
| 40648 |17 |Muitas solicitações foram executadas. Tente novamente mais tarde. |
| 40649 |16 |Tipo de conteúdo inválido especificado. Somente aplicativo/xml tem suporte. |
| 40650 |16 |Assinatura < id da assinatura > não existe ou não está pronta para operação de saudação. |
| 40651 |16 |Falha na toocreate servidor porque a assinatura hello < id da assinatura > está desabilitada. |
| 40652 |16 |Não é possível mover ou criar o servidor. A assinatura <subscription-id> ultrapassará a cota do servidor. |
| 40671 |17 |Falha de comunicação entre o gateway Olá Olá serviço e gerenciamento. Tente novamente mais tarde. |
| 40852 |16 |Não é possível abrir o banco de dados ' %. *ls' no servidor ' %.* ls' solicitado pelo logon de saudação. O banco de dados do Access toohello é permitido apenas usando uma cadeia de caracteres de conexão habilitadas para segurança. tooaccess este banco de dados, modificar sua toocontain de cadeias de caracteres de conexão segura no servidor de saudação FQDN -.database.windows 'nome do servidor'.net deve ser modificado too'server nome '. Database. `secure`. windows.net. |
| 45168 |16 |Olá sistema SQL Azure está sob carga e está estabelecendo um limite superior em operações CRUD de BD simultâneas para um único servidor (por exemplo, criar banco de dados). servidor de saudação especificado na mensagem de erro de saudação excedeu o número máximo de saudação de conexões simultâneas. Tente novamente mais tarde. |
| 45169 |16 |saudação de sistema do SQL azure está sob carga e está estabelecendo um limite superior no número de saudação de operações CRUD de servidor simultâneas para uma única assinatura (por exemplo, criar servidor). assinatura de saudação especificado em erro Olá mensagem excedeu o número máximo de saudação de conexões simultâneas e Olá solicitação foi negada. Tente novamente mais tarde. |

## <a name="related-links"></a>Links relacionados
* [Recursos do Banco de Dados SQL do Azure](sql-database-features.md)
* [Limites de recursos do Banco de Dados SQL do Azure](sql-database-resource-limits.md)

