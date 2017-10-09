---
title: esquemas definidos aaaUser no SQL Data Warehouse | Microsoft Docs
description: "Dicas para usar esquemas de Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Esquemas definidos pelo usuário no SQL Data Warehouse
Data warehouses tradicionais geralmente usar bancos de dados separados toocreate limites para o aplicativo com base na carga de trabalho, domínio ou segurança. Por exemplo, um data warehouse tradicional do SQL Server pode incluir um banco de dados de preparo, um banco de dados do data warehouse e alguns bancos de dados do data mart. Nessa topologia cada banco de dados funciona como uma carga de trabalho e o limite de segurança na arquitetura de saudação.

Por outro lado, o SQL Data Warehouse é executado a carga de trabalho do hello todo o data warehouse em um banco de dados. Uniões cruzadas de banco de dados não são permitidas. Portanto, SQL Data Warehouse espera que todas as tabelas usadas pelo Olá warehouse toobe armazenado em um banco de dados de saudação.

> [!NOTE]
> O SQL Data Warehouse não oferece suporte a consultas cruzadas de banco de dados de qualquer tipo. Consequentemente, as implementações de data warehouse que aproveitam esse padrão precisará toobe revisado.
> 
> 

## <a name="recommendations"></a>Recomendações
Estas são recomendações para consolidar limites funcionais, de carga de trabalho, segurança e domínio usando esquemas definidos pelo usuário

1. Usar um toorun de banco de dados do SQL Data Warehouse sua carga de trabalho de depósito de dados inteiro
2. Consolidar dados warehouse ambiente toouse um SQL Data Warehouse banco de dados existente
3. Aproveite **esquemas definidos pelo usuário** tooprovide limites de saudação implementado anteriormente usando bancos de dados.

Se esquemas definidos pelo usuário não tiverem sido usados anteriormente, então você tem uma área limpa. Simplesmente use nome de banco de dados antigo hello como base Olá para os esquemas definidos pelo usuário no banco de dados do SQL Data Warehouse hello.

Se já tiverem sido usados esquemas, então você tem algumas opções:

1. Remover os nomes de esquema herdados hello e começar do zero
2. Reter nomes de esquema herdados Olá pelo nome de tabela Olá previamente pendente esquema herdados nome toohello
3. Manter nomes de esquema herdados Olá implementando exibições em tabela Olá em um esquema extra toore-criar estrutura do esquema antigo hello.

> [!NOTE]
> Na primeira inspeção opção 3 pode parecer a opção mais atraente hello. No entanto, Diabo Olá é detalhadamente hello. Os modos de exibição são somente leitura no SQL Data Warehouse. Qualquer modificação de dados ou tabela teria toobe executada na tabela base hello. A opção 3 também apresenta uma camada de modos de exibição em seu sistema. Talvez você queira toogive esta consideração adicional se você estiver usando modos de exibição em sua arquitetura já.
> 
> 

### <a name="examples"></a>Exemplos:
Implementar esquemas definidos pelo usuário com base em nomes de banco de dados

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Manter esquema herdada nomeia acrescentando toohello nome da tabela. Use esquemas para limite de carga de trabalho de saudação.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Manter nomes de esquema herdados usando modos de exibição

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Qualquer alteração na estratégia de esquema precisa de uma revisão de saudação do modelo de segurança para o banco de dados de saudação. Em muitos casos é toosimplify capaz de modelo de segurança de hello, atribuindo permissões no nível de esquema hello. Se forem necessárias permissões mais granulares, então você poderá usar funções de banco de dados.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
