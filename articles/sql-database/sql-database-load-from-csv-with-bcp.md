---
title: Carregar dados do arquivo CSV para o Banco de Dados SQL do Azure (bcp) | Microsoft Docs
description: Para um tamanho de dados pequeno, use bcp para importar dados para o Banco de Dados SQL.
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 84bebab7763bb21f73880a6c8b367a62b0c137d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="e8ab7-103">Carregar dados do CSV para o Banco de Dados SQL do Azure (arquivos simples)</span><span class="sxs-lookup"><span data-stu-id="e8ab7-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="e8ab7-104">Você pode usar o utilitário de linha de comando bcp para importar dados de um arquivo CSV para o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-104">You can use the bcp command-line utility to import data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e8ab7-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="e8ab7-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="e8ab7-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e8ab7-106">Prerequisites</span></span>
<span data-ttu-id="e8ab7-107">Para completar as etapas neste artigo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e8ab7-107">To complete the steps in this article, you need:</span></span>

* <span data-ttu-id="e8ab7-108">Um servidor lógico e um banco de dados do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="e8ab7-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="e8ab7-109">O utilitário de linha de comando bcp instalado</span><span class="sxs-lookup"><span data-stu-id="e8ab7-109">The bcp command-line utility installed</span></span>
* <span data-ttu-id="e8ab7-110">O utilitário de linha de comando sqlcmd instalado</span><span class="sxs-lookup"><span data-stu-id="e8ab7-110">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="e8ab7-111">Você pode baixar os utilitários bcp e sqlcmd do [Centro de Download da Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="e8ab7-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="e8ab7-112">Dados em formato ASCII ou UTF-16</span><span class="sxs-lookup"><span data-stu-id="e8ab7-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="e8ab7-113">Se você estiver experimentando este tutorial com seus próprios dados, eles precisarão usar a codificação ASCII ou UTF-16, já que bcp não oferece suporte a UTF-8.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-113">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="e8ab7-114">1. Criar uma tabela de destino</span><span class="sxs-lookup"><span data-stu-id="e8ab7-114">1. Create a destination table</span></span>
<span data-ttu-id="e8ab7-115">Defina uma tabela no Banco de Dados SQL como a tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-115">Define a table in SQL Database as the destination table.</span></span> <span data-ttu-id="e8ab7-116">As colunas na tabela devem corresponder aos dados em cada linha do arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-116">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="e8ab7-117">Para criar uma tabela, abra um prompt de comando e use sqlcmd.exe para executar o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8ab7-117">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="e8ab7-118">2. Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="e8ab7-118">2. Create a source data file</span></span>
<span data-ttu-id="e8ab7-119">Abra o Bloco de Notas e copie as seguintes linhas de dados em um novo arquivo de texto. Em seguida, salve esse arquivo em seu diretório temporário local, c:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-119">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="e8ab7-120">Esses dados estão no formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-120">This data is in ASCII format.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

<span data-ttu-id="e8ab7-121">(Opcional) Para exportar seus próprios dados de um banco de dados do SQL Server, abra um prompt de comando e execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-121">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="e8ab7-122">Substitua TableName, ServerName, DatabaseName, Username e Password por suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-the-data"></a><span data-ttu-id="e8ab7-123">3. Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="e8ab7-123">3. Load the data</span></span>
<span data-ttu-id="e8ab7-124">Para carregar os dados, abra um prompt de comando e execute o comando a seguir, substituindo os valores de Nome do Servidor, Nome do Banco de Dados, Nome de Usuário e Senha por suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="e8ab7-124">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="e8ab7-125">Use este comando para verificar se os dados foram carregados corretamente</span><span class="sxs-lookup"><span data-stu-id="e8ab7-125">Use this command to verify the data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="e8ab7-126">O resultado deve parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e8ab7-126">The results should look like this:</span></span>

| <span data-ttu-id="e8ab7-127">DateId</span><span class="sxs-lookup"><span data-stu-id="e8ab7-127">DateId</span></span> | <span data-ttu-id="e8ab7-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="e8ab7-128">CalendarQuarter</span></span> | <span data-ttu-id="e8ab7-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="e8ab7-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8ab7-130">20150101</span><span class="sxs-lookup"><span data-stu-id="e8ab7-130">20150101</span></span> |<span data-ttu-id="e8ab7-131">1</span><span class="sxs-lookup"><span data-stu-id="e8ab7-131">1</span></span> |<span data-ttu-id="e8ab7-132">3</span><span class="sxs-lookup"><span data-stu-id="e8ab7-132">3</span></span> |
| <span data-ttu-id="e8ab7-133">20150201</span><span class="sxs-lookup"><span data-stu-id="e8ab7-133">20150201</span></span> |<span data-ttu-id="e8ab7-134">1</span><span class="sxs-lookup"><span data-stu-id="e8ab7-134">1</span></span> |<span data-ttu-id="e8ab7-135">3</span><span class="sxs-lookup"><span data-stu-id="e8ab7-135">3</span></span> |
| <span data-ttu-id="e8ab7-136">20150301</span><span class="sxs-lookup"><span data-stu-id="e8ab7-136">20150301</span></span> |<span data-ttu-id="e8ab7-137">1</span><span class="sxs-lookup"><span data-stu-id="e8ab7-137">1</span></span> |<span data-ttu-id="e8ab7-138">3</span><span class="sxs-lookup"><span data-stu-id="e8ab7-138">3</span></span> |
| <span data-ttu-id="e8ab7-139">20150401</span><span class="sxs-lookup"><span data-stu-id="e8ab7-139">20150401</span></span> |<span data-ttu-id="e8ab7-140">2</span><span class="sxs-lookup"><span data-stu-id="e8ab7-140">2</span></span> |<span data-ttu-id="e8ab7-141">4</span><span class="sxs-lookup"><span data-stu-id="e8ab7-141">4</span></span> |
| <span data-ttu-id="e8ab7-142">20150501</span><span class="sxs-lookup"><span data-stu-id="e8ab7-142">20150501</span></span> |<span data-ttu-id="e8ab7-143">2</span><span class="sxs-lookup"><span data-stu-id="e8ab7-143">2</span></span> |<span data-ttu-id="e8ab7-144">4</span><span class="sxs-lookup"><span data-stu-id="e8ab7-144">4</span></span> |
| <span data-ttu-id="e8ab7-145">20150601</span><span class="sxs-lookup"><span data-stu-id="e8ab7-145">20150601</span></span> |<span data-ttu-id="e8ab7-146">2</span><span class="sxs-lookup"><span data-stu-id="e8ab7-146">2</span></span> |<span data-ttu-id="e8ab7-147">4</span><span class="sxs-lookup"><span data-stu-id="e8ab7-147">4</span></span> |
| <span data-ttu-id="e8ab7-148">20150701</span><span class="sxs-lookup"><span data-stu-id="e8ab7-148">20150701</span></span> |<span data-ttu-id="e8ab7-149">3</span><span class="sxs-lookup"><span data-stu-id="e8ab7-149">3</span></span> |<span data-ttu-id="e8ab7-150">1</span><span class="sxs-lookup"><span data-stu-id="e8ab7-150">1</span></span> |
| <span data-ttu-id="e8ab7-151">20150801</span><span class="sxs-lookup"><span data-stu-id="e8ab7-151">20150801</span></span> |<span data-ttu-id="e8ab7-152">3</span><span class="sxs-lookup"><span data-stu-id="e8ab7-152">3</span></span> |<span data-ttu-id="e8ab7-153">1</span><span class="sxs-lookup"><span data-stu-id="e8ab7-153">1</span></span> |
| <span data-ttu-id="e8ab7-154">20150801</span><span class="sxs-lookup"><span data-stu-id="e8ab7-154">20150801</span></span> |<span data-ttu-id="e8ab7-155">3</span><span class="sxs-lookup"><span data-stu-id="e8ab7-155">3</span></span> |<span data-ttu-id="e8ab7-156">1</span><span class="sxs-lookup"><span data-stu-id="e8ab7-156">1</span></span> |
| <span data-ttu-id="e8ab7-157">20151001</span><span class="sxs-lookup"><span data-stu-id="e8ab7-157">20151001</span></span> |<span data-ttu-id="e8ab7-158">4</span><span class="sxs-lookup"><span data-stu-id="e8ab7-158">4</span></span> |<span data-ttu-id="e8ab7-159">2</span><span class="sxs-lookup"><span data-stu-id="e8ab7-159">2</span></span> |
| <span data-ttu-id="e8ab7-160">20151101</span><span class="sxs-lookup"><span data-stu-id="e8ab7-160">20151101</span></span> |<span data-ttu-id="e8ab7-161">4</span><span class="sxs-lookup"><span data-stu-id="e8ab7-161">4</span></span> |<span data-ttu-id="e8ab7-162">2</span><span class="sxs-lookup"><span data-stu-id="e8ab7-162">2</span></span> |
| <span data-ttu-id="e8ab7-163">20151201</span><span class="sxs-lookup"><span data-stu-id="e8ab7-163">20151201</span></span> |<span data-ttu-id="e8ab7-164">4</span><span class="sxs-lookup"><span data-stu-id="e8ab7-164">4</span></span> |<span data-ttu-id="e8ab7-165">2</span><span class="sxs-lookup"><span data-stu-id="e8ab7-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8ab7-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8ab7-166">Next steps</span></span>
<span data-ttu-id="e8ab7-167">Para migrar um banco de dados do SQL Server, confira [Migração de banco de dados do SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="e8ab7-167">To migrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
