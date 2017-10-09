---
title: aaaGuide para usar o PolyBase no SQL Data Warehouse | Microsoft Docs
description: "Diretrizes e recomendações para usar o PolyBase em cenários do SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>Guia para usar o PolyBase no SQL Data Warehouse
Este guia fornece informações práticas para usar o PolyBase no SQL Data Warehouse.

tooget iniciado, consulte Olá [carregar dados com o PolyBase] [ Load data with PolyBase] tutorial.

## <a name="rotating-storage-keys"></a>Rotação de chaves de armazenamento
De tootime de tempo, você desejará o armazenamento de blob de chave tooyour do toochange Olá acesso por motivos de segurança.

Olá mais elegante tooperform de forma que essa tarefa é toofollow um processo conhecido como "rotação de chaves de Olá". Você talvez tenha observado que há duas chaves de armazenamento para a conta de armazenamento de blob. Isso é para que você possa fazer a transição

A rotação das suas chaves da conta de Armazenamento do Azure é um processo simples de três etapas

1. Criar segunda credencial no escopo do banco de dados com base na chave de acesso de armazenamento secundário Olá
2. Criar a segunda fonte de dados externa com base nessa nova credencial
3. Descarte e crie Olá tabelas externas apontando toohello nova fonte de dados externa

Depois de migrar todas as tabelas externas toohello nova fonte de dados externa, em seguida, você pode executar o hello Limpar tarefas:

1. Remover a primeira fonte de dados externa
2. Credencial com base na chave de acesso de armazenamento primário Olá com escopo de descarte primeiro o banco de dados
3. Faça logon no Azure e regenerar chave de acesso primária Olá pronto para Olá próxima vez

## <a name="query-azure-blob-storage-data"></a>Consultar dados de armazenamento de blob do Azure
Consultas em tabelas externas simplesmente usam o nome da tabela hello como se fosse uma tabela relacional.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Uma consulta em uma tabela externa pode falhar com o erro Olá *"consulta anulada-limite máximo de rejeição de saudação foi atingido durante a leitura de uma fonte externa"*. Isso indica que os dados externos contêm registros *sujos* . Um registro de dados é considerado 'sujo' se tipos de dados reais Olá/número de colunas não correspondem a definições de coluna de saudação da tabela externa hello ou se dados saudação não está em conformidade toohello formato de arquivo externo especificado. toofix isso, certifique-se de que a tabela externa e as definições de formato de arquivo externo estão corretas e definições de toothese está de acordo com seus dados externos. No caso de um subconjunto de registros de dados externa estiver sujo, você pode escolher tooreject esses registros para as consultas usando as opções de rejeição de saudação em CREATE EXTERNAL TABLE DDL.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Carregar dados do armazenamento de blob do Azure
Este exemplo carrega dados do banco de dados do Data Warehouse tooSQL de armazenamento de BLOBs do Azure.

Armazenando dados diretamente remove Olá tempo de transferência de dados para consultas. Armazenando dados com um índice columnstore melhora o desempenho de consultas de análise pelo backup too10x.

Este exemplo usa dados de tooload de instrução CREATE TABLE AS SELECT saudação. nova tabela de saudação herda colunas de saudação nomeadas na consulta de saudação. Ele herda os tipos de dados Olá dessas colunas de definição de tabela externa hello.

CREATE TABLE AS SELECT é um alto desempenho instrução Transact-SQL que carrega dados Olá em paralelo tooall Olá nós de computação de Data Warehouse do SQL.  Ele foi originalmente desenvolvido para o mecanismo de processamento paralelo em massa (MPP) Olá no sistema de plataforma de análise e está agora no SQL Data Warehouse.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Consulte [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Criar estatísticas sobre os dados recém-carregados
O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.  Em ordem tooget Olá melhor desempenho de suas consultas, é importante que ser criadas estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou alterações substanciais ocorrerem nos dados de saudação.  Para obter uma explicação detalhada de estatísticas, consulte Olá [estatísticas] [ Statistics] tópico no grupo de desenvolver Olá de tópicos.  Abaixo está um exemplo rápido de como toocreate estatísticas na tabela de saudação carregados neste exemplo.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Exportar o armazenamento de blob de tooAzure de dados
Esta seção mostra como o armazenamento de blob dados tooexport tooAzure SQL Data Warehouse. Este exemplo usa CREATE EXTERNAL TABLE AS SELECT que é um altamente funcional Transact-SQL instrução tooexport Olá dados em paralelo de todos os nós de computação de saudação.

Olá, exemplo a seguir cria uma tabela externa Weblogs2014 usando dados de dbo e definições de coluna. Tabela weblogs. definição da tabela externa de saudação é armazenada no SQL Data Warehouse e resultados de Olá da instrução SELECT Olá são exportado toohello directory "/ arquivar/log2014 /" no contêiner de blob Olá especificada pela fonte de dados de saudação. Olá dados são exportados no formato de arquivo de texto especificado hello.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Isolar Usuários em carregamento
Há muitas vezes uma necessidade toohave vários usuários que podem carregar dados em um SQL DW. Porque Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] requer permissões de controle do banco de dados hello, você acabará com vários usuários com controle de acesso sobre todos os esquemas. toolimit isso, você pode usar a instrução de controle negar hello.

Exemplo: considere os esquemas de banco de dados schema_A para o departamento A e schema_B para o departamento B. Os usuários de banco de dados user_A e user_B serão usuários de carregamento de PolyBase nos departamentos A e B, respectivamente. Ambos receberam permissões de banco de dados CONTROL.
criadores de saudação do esquema A e B agora bloquear seus esquemas usando DENY:

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 Com isso, user_A e user_B devem agora ser impedidos de saudação esquema do outro departamento.
 


## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre tooSQL movimentação de dados do Data Warehouse, consulte Olá [visão geral de migração de dados][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
