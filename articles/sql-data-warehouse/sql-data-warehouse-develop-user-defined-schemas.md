---
title: "Esquemas definidos pelo usuário no SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="48012-103">Esquemas definidos pelo usuário no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="48012-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="48012-104">Os data warehouses tradicionais normalmente usam bancos de dados separados para criar limites de aplicativo com base na carga de trabalho, domínio ou segurança.</span><span class="sxs-lookup"><span data-stu-id="48012-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="48012-105">Por exemplo, um data warehouse tradicional do SQL Server pode incluir um banco de dados de preparo, um banco de dados do data warehouse e alguns bancos de dados do data mart.</span><span class="sxs-lookup"><span data-stu-id="48012-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="48012-106">Nesta topologia, cada banco de dados funciona como uma carga de trabalho e limite de segurança na arquitetura.</span><span class="sxs-lookup"><span data-stu-id="48012-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="48012-107">Por outro lado, o SQL Data Warehouse executa toda a carga de trabalho do data warehouse em um só banco de dados.</span><span class="sxs-lookup"><span data-stu-id="48012-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="48012-108">Uniões cruzadas de banco de dados não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="48012-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="48012-109">Portanto, o SQL Data Warehouse espera que todas as tabelas usadas pelo warehouse sejam armazenadas em um só banco de dados.</span><span class="sxs-lookup"><span data-stu-id="48012-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="48012-110">O SQL Data Warehouse não oferece suporte a consultas cruzadas de banco de dados de qualquer tipo.</span><span class="sxs-lookup"><span data-stu-id="48012-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="48012-111">Consequentemente, implementações de data warehouse que utilizam esse padrão precisarão ser revisadas.</span><span class="sxs-lookup"><span data-stu-id="48012-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="48012-112">Recomendações</span><span class="sxs-lookup"><span data-stu-id="48012-112">Recommendations</span></span>
<span data-ttu-id="48012-113">Estas são recomendações para consolidar limites funcionais, de carga de trabalho, segurança e domínio usando esquemas definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="48012-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="48012-114">Use um banco de dados do SQL Data Warehouse para executar toda a carga de trabalho do data warehouse</span><span class="sxs-lookup"><span data-stu-id="48012-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="48012-115">Consolide seu ambiente de data warehouse existente para usar um banco de dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="48012-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="48012-116">Utilize **esquemas definidos pelo usuário** para fornecer o limite implementado anteriormente usando bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="48012-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="48012-117">Se esquemas definidos pelo usuário não tiverem sido usados anteriormente, então você tem uma área limpa.</span><span class="sxs-lookup"><span data-stu-id="48012-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="48012-118">Basta usar o nome antigo do banco de dados como base para os esquemas definidos pelo usuário no banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="48012-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="48012-119">Se já tiverem sido usados esquemas, então você tem algumas opções:</span><span class="sxs-lookup"><span data-stu-id="48012-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="48012-120">Remover os nomes de esquema herdados e começar do zero</span><span class="sxs-lookup"><span data-stu-id="48012-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="48012-121">Manter os nomes de esquema herdados acrescentando o nome do esquema herdado ao nome da tabela</span><span class="sxs-lookup"><span data-stu-id="48012-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="48012-122">Manter os nomes de esquema herdados implementando exibições sobre a tabela em um esquema extra para recriar a estrutura do esquema antigo.</span><span class="sxs-lookup"><span data-stu-id="48012-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="48012-123">Na primeira inspeção, a opção 3 pode parecer a opção mais atraente.</span><span class="sxs-lookup"><span data-stu-id="48012-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="48012-124">No entanto, o detalhe é traiçoeiro.</span><span class="sxs-lookup"><span data-stu-id="48012-124">However, the devil is in the detail.</span></span> <span data-ttu-id="48012-125">Os modos de exibição são somente leitura no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="48012-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="48012-126">Qualquer modificação nos dados ou na tabela precisariam ser executados em relação à tabela base.</span><span class="sxs-lookup"><span data-stu-id="48012-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="48012-127">A opção 3 também apresenta uma camada de modos de exibição em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="48012-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="48012-128">Talvez você queira pensar um pouco sobre isso se já estiver usando modos de exibição em sua arquitetura.</span><span class="sxs-lookup"><span data-stu-id="48012-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="48012-129">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="48012-129">Examples:</span></span>
<span data-ttu-id="48012-130">Implementar esquemas definidos pelo usuário com base em nomes de banco de dados</span><span class="sxs-lookup"><span data-stu-id="48012-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="48012-131">Manter nomes de esquema herdados acrescentando-os ao nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="48012-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="48012-132">Usar esquemas para o limite de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="48012-132">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="48012-133">Manter nomes de esquema herdados usando modos de exibição</span><span class="sxs-lookup"><span data-stu-id="48012-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="48012-134">Qualquer alteração na estratégia de esquema precisa de uma revisão do modelo de segurança para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="48012-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="48012-135">Em muitos casos, você poderá simplificar o modelo de segurança ao atribuir permissões no nível do esquema.</span><span class="sxs-lookup"><span data-stu-id="48012-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="48012-136">Se forem necessárias permissões mais granulares, então você poderá usar funções de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="48012-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="48012-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48012-137">Next steps</span></span>
<span data-ttu-id="48012-138">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="48012-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
