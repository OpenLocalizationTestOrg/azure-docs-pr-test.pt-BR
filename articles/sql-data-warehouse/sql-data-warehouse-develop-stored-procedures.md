---
title: procedimentos de aaaStored no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="65c54-103">Procedimentos armazenados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="65c54-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="65c54-104">SQL Data Warehouse dá suporte a muitos dos recursos de Transact-SQL Olá encontrados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="65c54-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="65c54-105">Mais importante é que há recursos específicos que queremos desempenho de saudação do tooleverage toomaximize de sua solução de expansão.</span><span class="sxs-lookup"><span data-stu-id="65c54-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="65c54-106">No entanto, escala de saudação toomaintain e o desempenho do SQL Data Warehouse lá também são alguns recursos e funcionalidades que têm diferenças de comportamento e outras que não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="65c54-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="65c54-107">Este artigo explica como tooimplement armazenados procedimentos no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65c54-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="65c54-108">Apresentação dos procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="65c54-108">Introducing stored procedures</span></span>
<span data-ttu-id="65c54-109">Procedimentos armazenados são uma ótima maneira para encapsular o código SQL; armazenando dados tooyour Fechar no data warehouse de saudação.</span><span class="sxs-lookup"><span data-stu-id="65c54-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="65c54-110">Encapsulando código Olá em unidades gerenciáveis procedimentos armazenados ajudam os desenvolvedores modularizar suas soluções; facilitando maior reutilização de código.</span><span class="sxs-lookup"><span data-stu-id="65c54-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="65c54-111">Cada procedimento armazenado também pode aceitar parâmetros toomake-los ainda mais flexível.</span><span class="sxs-lookup"><span data-stu-id="65c54-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="65c54-112">O SQL Data Warehouse fornece uma implementação simplificada e otimizada de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="65c54-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="65c54-113">Olá maior diferença em comparação comparada tooSQL Server é que Olá procedimento armazenado não é código pré-compilado.</span><span class="sxs-lookup"><span data-stu-id="65c54-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="65c54-114">Em data warehouses estamos geralmente menos preocupados com tempo de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="65c54-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="65c54-115">É mais importante do que o código do procedimento Olá armazenado corretamente é otimizado ao operar em grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="65c54-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="65c54-116">meta de saudação é toosave horas, minutos e segundos não milissegundos.</span><span class="sxs-lookup"><span data-stu-id="65c54-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="65c54-117">Portanto, é mais útil toothink de procedimentos armazenados como contêineres para lógica SQL.</span><span class="sxs-lookup"><span data-stu-id="65c54-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="65c54-118">Quando o SQL Data Warehouse executa suas instruções de SQL de saudação do procedimento armazenado são analisadas, convertidas e otimizadas em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="65c54-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="65c54-119">Durante esse processo, cada instrução é convertida em consultas distribuídas.</span><span class="sxs-lookup"><span data-stu-id="65c54-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="65c54-120">Olá código SQL que realmente é executado em relação aos dados de saudação é toohello diferentes consulta enviada.</span><span class="sxs-lookup"><span data-stu-id="65c54-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="65c54-121">Aninhamento de procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="65c54-121">Nesting stored procedures</span></span>
<span data-ttu-id="65c54-122">Quando os procedimentos armazenados chamam outros procedimentos armazenados ou executar sql dinâmico, procedimento armazenado de interna hello ou invocação de código é considerada toobe aninhados.</span><span class="sxs-lookup"><span data-stu-id="65c54-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="65c54-123">O SQL Data Warehouse oferece suporte a um máximo de 8 níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="65c54-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="65c54-124">Este é um pouco diferente tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="65c54-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="65c54-125">nível de aninhamento de saudação no SQL Server é 32.</span><span class="sxs-lookup"><span data-stu-id="65c54-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="65c54-126">chamada de procedimento armazenado de nível superior de saudação é igual a toonest nível 1</span><span class="sxs-lookup"><span data-stu-id="65c54-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="65c54-127">Se Olá armazenado procedimento também faz EXEC outra chamada e isso aumentará too2 de nível de aninhamento de saudação</span><span class="sxs-lookup"><span data-stu-id="65c54-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="65c54-128">Se o segundo procedimento de hello, em seguida, executa algum sql dinâmico, em seguida, isso aumentará too3 de nível de aninhamento de saudação</span><span class="sxs-lookup"><span data-stu-id="65c54-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="65c54-129">Observe que atualmente o SQL Data Warehouse não dá suporte ao @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="65c54-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="65c54-130">Você será necessário tookeep uma faixa de seu nível de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="65c54-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="65c54-131">É improvável que você atingirá o limite de nível de aninhamento de saudação 8, mas nesse caso você será necessário trabalho toore seu código e "mesclar"-la para que ela caiba dentro desse limite.</span><span class="sxs-lookup"><span data-stu-id="65c54-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="65c54-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="65c54-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="65c54-133">SQL Data Warehouse não permite que você tooconsume conjunto de resultados de saudação de um procedimento armazenado com uma instrução INSERT.</span><span class="sxs-lookup"><span data-stu-id="65c54-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="65c54-134">No entanto, há uma abordagem alternativa.</span><span class="sxs-lookup"><span data-stu-id="65c54-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="65c54-135">Consulte toohello artigo a seguir [tabelas temporárias] para obter um exemplo sobre como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="65c54-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="65c54-136">Limitações</span><span class="sxs-lookup"><span data-stu-id="65c54-136">Limitations</span></span>
<span data-ttu-id="65c54-137">Há alguns aspectos de procedimentos armazenados Transact-SQL que não são implementados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="65c54-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="65c54-138">Eles são:</span><span class="sxs-lookup"><span data-stu-id="65c54-138">They are:</span></span>

* <span data-ttu-id="65c54-139">procedimentos armazenados temporariamente</span><span class="sxs-lookup"><span data-stu-id="65c54-139">temporary stored procedures</span></span>
* <span data-ttu-id="65c54-140">procedimentos armazenados numerados</span><span class="sxs-lookup"><span data-stu-id="65c54-140">numbered stored procedures</span></span>
* <span data-ttu-id="65c54-141">procedimentos armazenados estendidos</span><span class="sxs-lookup"><span data-stu-id="65c54-141">extended stored procedures</span></span>
* <span data-ttu-id="65c54-142">procedimentos armazenados de CLR</span><span class="sxs-lookup"><span data-stu-id="65c54-142">CLR stored procedures</span></span>
* <span data-ttu-id="65c54-143">opção de criptografia</span><span class="sxs-lookup"><span data-stu-id="65c54-143">encryption option</span></span>
* <span data-ttu-id="65c54-144">opção de replicação</span><span class="sxs-lookup"><span data-stu-id="65c54-144">replication option</span></span>
* <span data-ttu-id="65c54-145">parâmetros com valor de tabela</span><span class="sxs-lookup"><span data-stu-id="65c54-145">table-valued parameters</span></span>
* <span data-ttu-id="65c54-146">parâmetros somente leitura</span><span class="sxs-lookup"><span data-stu-id="65c54-146">read-only parameters</span></span>
* <span data-ttu-id="65c54-147">parâmetros padrão</span><span class="sxs-lookup"><span data-stu-id="65c54-147">default parameters</span></span>
* <span data-ttu-id="65c54-148">contextos de execução</span><span class="sxs-lookup"><span data-stu-id="65c54-148">execution contexts</span></span>
* <span data-ttu-id="65c54-149">instrução return</span><span class="sxs-lookup"><span data-stu-id="65c54-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="65c54-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65c54-150">Next steps</span></span>
<span data-ttu-id="65c54-151">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="65c54-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[tabelas temporárias]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
