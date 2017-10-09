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
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="7e77c-103">Esquemas definidos pelo usuário no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7e77c-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="7e77c-104">Data warehouses tradicionais geralmente usar bancos de dados separados toocreate limites para o aplicativo com base na carga de trabalho, domínio ou segurança.</span><span class="sxs-lookup"><span data-stu-id="7e77c-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="7e77c-105">Por exemplo, um data warehouse tradicional do SQL Server pode incluir um banco de dados de preparo, um banco de dados do data warehouse e alguns bancos de dados do data mart.</span><span class="sxs-lookup"><span data-stu-id="7e77c-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="7e77c-106">Nessa topologia cada banco de dados funciona como uma carga de trabalho e o limite de segurança na arquitetura de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e77c-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="7e77c-107">Por outro lado, o SQL Data Warehouse é executado a carga de trabalho do hello todo o data warehouse em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7e77c-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="7e77c-108">Uniões cruzadas de banco de dados não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="7e77c-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="7e77c-109">Portanto, SQL Data Warehouse espera que todas as tabelas usadas pelo Olá warehouse toobe armazenado em um banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e77c-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="7e77c-110">O SQL Data Warehouse não oferece suporte a consultas cruzadas de banco de dados de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="7e77c-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="7e77c-111">Consequentemente, as implementações de data warehouse que aproveitam esse padrão precisará toobe revisado.</span><span class="sxs-lookup"><span data-stu-id="7e77c-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="7e77c-112">Recomendações</span><span class="sxs-lookup"><span data-stu-id="7e77c-112">Recommendations</span></span>
<span data-ttu-id="7e77c-113">Estas são recomendações para consolidar limites funcionais, de carga de trabalho, segurança e domínio usando esquemas definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="7e77c-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="7e77c-114">Usar um toorun de banco de dados do SQL Data Warehouse sua carga de trabalho de depósito de dados inteiro</span><span class="sxs-lookup"><span data-stu-id="7e77c-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="7e77c-115">Consolidar dados warehouse ambiente toouse um SQL Data Warehouse banco de dados existente</span><span class="sxs-lookup"><span data-stu-id="7e77c-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="7e77c-116">Aproveite **esquemas definidos pelo usuário** tooprovide limites de saudação implementado anteriormente usando bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="7e77c-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="7e77c-117">Se esquemas definidos pelo usuário não tiverem sido usados anteriormente, então você tem uma área limpa.</span><span class="sxs-lookup"><span data-stu-id="7e77c-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="7e77c-118">Simplesmente use nome de banco de dados antigo hello como base Olá para os esquemas definidos pelo usuário no banco de dados do SQL Data Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="7e77c-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="7e77c-119">Se já tiverem sido usados esquemas, então você tem algumas opções:</span><span class="sxs-lookup"><span data-stu-id="7e77c-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="7e77c-120">Remover os nomes de esquema herdados hello e começar do zero</span><span class="sxs-lookup"><span data-stu-id="7e77c-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="7e77c-121">Reter nomes de esquema herdados Olá pelo nome de tabela Olá previamente pendente esquema herdados nome toohello</span><span class="sxs-lookup"><span data-stu-id="7e77c-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="7e77c-122">Manter nomes de esquema herdados Olá implementando exibições em tabela Olá em um esquema extra toore-criar estrutura do esquema antigo hello.</span><span class="sxs-lookup"><span data-stu-id="7e77c-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="7e77c-123">Na primeira inspeção opção 3 pode parecer a opção mais atraente hello.</span><span class="sxs-lookup"><span data-stu-id="7e77c-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="7e77c-124">No entanto, Diabo Olá é detalhadamente hello.</span><span class="sxs-lookup"><span data-stu-id="7e77c-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="7e77c-125">Os modos de exibição são somente leitura no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e77c-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="7e77c-126">Qualquer modificação de dados ou tabela teria toobe executada na tabela base hello.</span><span class="sxs-lookup"><span data-stu-id="7e77c-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="7e77c-127">A opção 3 também apresenta uma camada de modos de exibição em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="7e77c-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="7e77c-128">Talvez você queira toogive esta consideração adicional se você estiver usando modos de exibição em sua arquitetura já.</span><span class="sxs-lookup"><span data-stu-id="7e77c-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="7e77c-129">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="7e77c-129">Examples:</span></span>
<span data-ttu-id="7e77c-130">Implementar esquemas definidos pelo usuário com base em nomes de banco de dados</span><span class="sxs-lookup"><span data-stu-id="7e77c-130">Implement user-defined schemas based on database names</span></span>

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

<span data-ttu-id="7e77c-131">Manter esquema herdada nomeia acrescentando toohello nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="7e77c-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="7e77c-132">Use esquemas para limite de carga de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e77c-132">Use schemas for hello workload boundary.</span></span>

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

<span data-ttu-id="7e77c-133">Manter nomes de esquema herdados usando modos de exibição</span><span class="sxs-lookup"><span data-stu-id="7e77c-133">Retain legacy schema names using views</span></span>

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
> <span data-ttu-id="7e77c-134">Qualquer alteração na estratégia de esquema precisa de uma revisão de saudação do modelo de segurança para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e77c-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="7e77c-135">Em muitos casos é toosimplify capaz de modelo de segurança de hello, atribuindo permissões no nível de esquema hello.</span><span class="sxs-lookup"><span data-stu-id="7e77c-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="7e77c-136">Se forem necessárias permissões mais granulares, então você poderá usar funções de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7e77c-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7e77c-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e77c-137">Next steps</span></span>
<span data-ttu-id="7e77c-138">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="7e77c-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
