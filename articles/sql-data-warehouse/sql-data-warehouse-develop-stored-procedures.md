---
title: Procedimentos armazenados no SQL Data Warehouse | Microsoft Docs
description: "Dicas para implementar procedimentos armazenados no SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="67098-103">Procedimentos armazenados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="67098-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="67098-104">O SQL Data Warehouse oferece suporte a muitos recursos Transact-SQL encontrados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="67098-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="67098-105">Mais importante, há recursos específicos de expansão que vamos aproveitar para maximizar o desempenho da sua solução.</span><span class="sxs-lookup"><span data-stu-id="67098-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span></span>

<span data-ttu-id="67098-106">No entanto, para manter a escala e o desempenho do SQL Data Warehouse também há alguns recursos e funcionalidades que apresentam diferenças de comportamento e outros que não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="67098-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="67098-107">Este artigo explica como implementar procedimentos armazenados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="67098-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="67098-108">Apresentação dos procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="67098-108">Introducing stored procedures</span></span>
<span data-ttu-id="67098-109">Os procedimentos armazenados são uma ótima maneira de encapsular o código SQL, armazenando-o perto de seus dados no data warehouse.</span><span class="sxs-lookup"><span data-stu-id="67098-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="67098-110">O encapsulamento do código em unidades gerenciáveis de procedimentos armazenados ajuda os desenvolvedores a modularizar suas soluções; facilitando a maior reutilização do código.</span><span class="sxs-lookup"><span data-stu-id="67098-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="67098-111">Cada procedimento armazenado também pode aceitar parâmetros para torná-lo ainda mais flexível.</span><span class="sxs-lookup"><span data-stu-id="67098-111">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="67098-112">O SQL Data Warehouse fornece uma implementação simplificada e otimizada de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="67098-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="67098-113">A maior diferença em comparação ao SQL Server é que o procedimento armazenado não é um código pré-compilado.</span><span class="sxs-lookup"><span data-stu-id="67098-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="67098-114">Normalmente, quando se trata de data warehouses, nos preocupamos menos com o tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="67098-114">In data warehouses we are generally less concerned with the compilation time.</span></span> <span data-ttu-id="67098-115">É mais importante que o código do procedimento armazenado seja otimizado corretamente ao operar com grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="67098-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="67098-116">O objetivo é economizar horas, minutos e segundos, não milissegundos.</span><span class="sxs-lookup"><span data-stu-id="67098-116">The goal is to save hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="67098-117">Portanto, é mais útil pensar em procedimentos armazenados como contêineres para a lógica SQL.</span><span class="sxs-lookup"><span data-stu-id="67098-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="67098-118">Quando o SQL Data Warehouse executa o procedimento armazenado, as instruções SQL são analisadas, traduzidas e otimizadas no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="67098-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="67098-119">Durante esse processo, cada instrução é convertida em consultas distribuídas.</span><span class="sxs-lookup"><span data-stu-id="67098-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="67098-120">O código SQL realmente executado nos dados é diferente da consulta enviada.</span><span class="sxs-lookup"><span data-stu-id="67098-120">The SQL code that is actually executed against the data is different to the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="67098-121">Aninhamento de procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="67098-121">Nesting stored procedures</span></span>
<span data-ttu-id="67098-122">Quando os procedimentos armazenados chamam outros procedimentos armazenados ou executam sql dinâmico, a invocação interna de código ou procedimento armazenado é considerada aninhada.</span><span class="sxs-lookup"><span data-stu-id="67098-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="67098-123">O SQL Data Warehouse oferece suporte a um máximo de 8 níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="67098-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="67098-124">Isso é um pouco diferente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="67098-124">This is slightly different to SQL Server.</span></span> <span data-ttu-id="67098-125">O nível de aninhamento no SQL Server é de 32.</span><span class="sxs-lookup"><span data-stu-id="67098-125">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="67098-126">A chamada de procedimento armazenado de nível superior é igual ao nível 1 de aninhamento</span><span class="sxs-lookup"><span data-stu-id="67098-126">The top level stored procedure call equates to nest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="67098-127">Se o procedimento armazenado também fizer outra chamada EXEC, isso aumentará o nível de aninhamento para 2</span><span class="sxs-lookup"><span data-stu-id="67098-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="67098-128">Se o segundo procedimento então executar algum sql dinâmico, isso aumentará o nível de aninhamento para 3</span><span class="sxs-lookup"><span data-stu-id="67098-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="67098-129">Observe que atualmente o SQL Data Warehouse não dá suporte ao @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="67098-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="67098-130">Você precisará manter o controle de seu nível de aninhamento por conta própria.</span><span class="sxs-lookup"><span data-stu-id="67098-130">You will need to keep a track of your nest level yourself.</span></span> <span data-ttu-id="67098-131">É improvável que você atinja o limite 8 de nível de aninhamento, mas, se atingir, será necessário trabalhar novamente seu código e "nivelá-lo" para que fique dentro do limite.</span><span class="sxs-lookup"><span data-stu-id="67098-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="67098-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="67098-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="67098-133">O SQL Data Warehouse não permite que você consuma o conjunto de resultados de um procedimento armazenado com uma instrução INSERT.</span><span class="sxs-lookup"><span data-stu-id="67098-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="67098-134">No entanto, há uma abordagem alternativa.</span><span class="sxs-lookup"><span data-stu-id="67098-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="67098-135">Confira o seguinte artigo sobre [tabelas temporárias] para obter um exemplo de como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="67098-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span></span>

## <a name="limitations"></a><span data-ttu-id="67098-136">Limitações</span><span class="sxs-lookup"><span data-stu-id="67098-136">Limitations</span></span>
<span data-ttu-id="67098-137">Há alguns aspectos de procedimentos armazenados Transact-SQL que não são implementados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="67098-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="67098-138">Eles são:</span><span class="sxs-lookup"><span data-stu-id="67098-138">They are:</span></span>

* <span data-ttu-id="67098-139">procedimentos armazenados temporariamente</span><span class="sxs-lookup"><span data-stu-id="67098-139">temporary stored procedures</span></span>
* <span data-ttu-id="67098-140">procedimentos armazenados numerados</span><span class="sxs-lookup"><span data-stu-id="67098-140">numbered stored procedures</span></span>
* <span data-ttu-id="67098-141">procedimentos armazenados estendidos</span><span class="sxs-lookup"><span data-stu-id="67098-141">extended stored procedures</span></span>
* <span data-ttu-id="67098-142">procedimentos armazenados de CLR</span><span class="sxs-lookup"><span data-stu-id="67098-142">CLR stored procedures</span></span>
* <span data-ttu-id="67098-143">opção de criptografia</span><span class="sxs-lookup"><span data-stu-id="67098-143">encryption option</span></span>
* <span data-ttu-id="67098-144">opção de replicação</span><span class="sxs-lookup"><span data-stu-id="67098-144">replication option</span></span>
* <span data-ttu-id="67098-145">parâmetros com valor de tabela</span><span class="sxs-lookup"><span data-stu-id="67098-145">table-valued parameters</span></span>
* <span data-ttu-id="67098-146">parâmetros somente leitura</span><span class="sxs-lookup"><span data-stu-id="67098-146">read-only parameters</span></span>
* <span data-ttu-id="67098-147">parâmetros padrão</span><span class="sxs-lookup"><span data-stu-id="67098-147">default parameters</span></span>
* <span data-ttu-id="67098-148">contextos de execução</span><span class="sxs-lookup"><span data-stu-id="67098-148">execution contexts</span></span>
* <span data-ttu-id="67098-149">instrução return</span><span class="sxs-lookup"><span data-stu-id="67098-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="67098-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67098-150">Next steps</span></span>
<span data-ttu-id="67098-151">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="67098-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
<span data-ttu-id="67098-152">[tabelas temporárias]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span><span class="sxs-lookup"><span data-stu-id="67098-152">[temporary tables]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span></span>
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
