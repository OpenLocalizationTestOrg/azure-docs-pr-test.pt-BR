---
title: o arquivo de dados aaaLoad de CSV em banco de dados do SQL do Azure (bcp) | Microsoft Docs
description: Para um tamanho de dados pequeno, usa bcp tooimport dados no banco de dados do SQL Azure.
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
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a><span data-ttu-id="39090-103">Carregar dados do CSV para o Banco de Dados SQL do Azure (arquivos simples)</span><span class="sxs-lookup"><span data-stu-id="39090-103">Load data from CSV into Azure SQL Database (flat files)</span></span>
<span data-ttu-id="39090-104">Você pode usar dados de tooimport saudação bcp utilitário de linha de comando de um arquivo CSV para o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="39090-104">You can use hello bcp command-line utility tooimport data from a CSV file into Azure SQL Database.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="39090-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="39090-105">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="39090-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="39090-106">Prerequisites</span></span>
<span data-ttu-id="39090-107">Olá toocomplete as etapas neste artigo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="39090-107">toocomplete hello steps in this article, you need:</span></span>

* <span data-ttu-id="39090-108">Um servidor lógico e um banco de dados do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="39090-108">An Azure SQL Database logical server and database</span></span>
* <span data-ttu-id="39090-109">Utilitário de linha de comando do bcp Olá instalado</span><span class="sxs-lookup"><span data-stu-id="39090-109">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="39090-110">Utilitário de linha de comando do sqlcmd Olá instalado</span><span class="sxs-lookup"><span data-stu-id="39090-110">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="39090-111">Você pode baixar os utilitários de bcp e o sqlcmd Olá do hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="39090-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="39090-112">Dados em formato ASCII ou UTF-16</span><span class="sxs-lookup"><span data-stu-id="39090-112">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="39090-113">Se você estiver tentando neste tutorial com seus próprios dados, os dados precisarem toouse Olá ASCII ou codificação UTF-16 como bcp não oferece suporte a UTF-8.</span><span class="sxs-lookup"><span data-stu-id="39090-113">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="39090-114">1. Criar uma tabela de destino</span><span class="sxs-lookup"><span data-stu-id="39090-114">1. Create a destination table</span></span>
<span data-ttu-id="39090-115">Defina uma tabela no banco de dados SQL como tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="39090-115">Define a table in SQL Database as hello destination table.</span></span> <span data-ttu-id="39090-116">colunas de saudação na tabela Olá devem corresponder dados toohello em cada linha do arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="39090-116">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="39090-117">toocreate uma tabela, abra um prompt de comando e use o sqlcmd.exe toorun Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="39090-117">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="39090-118">2. Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="39090-118">2. Create a source data file</span></span>
<span data-ttu-id="39090-119">Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo de texto e, em seguida, salvar esse arquivo tooyour local diretório temp, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="39090-119">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="39090-120">Esses dados estão no formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="39090-120">This data is in ASCII format.</span></span>

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

<span data-ttu-id="39090-121">(Opcional) tooexport seus próprios dados de um banco de dados do SQL Server, abra um prompt de comando e execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="39090-121">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="39090-122">Substitua TableName, ServerName, DatabaseName, Username e Password por suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="39090-122">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a><span data-ttu-id="39090-123">3. Carregar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="39090-123">3. Load hello data</span></span>
<span data-ttu-id="39090-124">dados de saudação tooload, abra um prompt de comando e execute Olá comando a seguir, substituindo valores de saudação para o nome do servidor, nome do banco de dados, nome de usuário e senha com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="39090-124">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

<span data-ttu-id="39090-125">Use que estes comando tooverify Olá os dados foram carregados corretamente</span><span class="sxs-lookup"><span data-stu-id="39090-125">Use this command tooverify hello data was loaded properly</span></span>

```bcp
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="39090-126">resultados de saudação devem ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="39090-126">hello results should look like this:</span></span>

| <span data-ttu-id="39090-127">DateId</span><span class="sxs-lookup"><span data-stu-id="39090-127">DateId</span></span> | <span data-ttu-id="39090-128">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="39090-128">CalendarQuarter</span></span> | <span data-ttu-id="39090-129">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="39090-129">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39090-130">20150101</span><span class="sxs-lookup"><span data-stu-id="39090-130">20150101</span></span> |<span data-ttu-id="39090-131">1</span><span class="sxs-lookup"><span data-stu-id="39090-131">1</span></span> |<span data-ttu-id="39090-132">3</span><span class="sxs-lookup"><span data-stu-id="39090-132">3</span></span> |
| <span data-ttu-id="39090-133">20150201</span><span class="sxs-lookup"><span data-stu-id="39090-133">20150201</span></span> |<span data-ttu-id="39090-134">1</span><span class="sxs-lookup"><span data-stu-id="39090-134">1</span></span> |<span data-ttu-id="39090-135">3</span><span class="sxs-lookup"><span data-stu-id="39090-135">3</span></span> |
| <span data-ttu-id="39090-136">20150301</span><span class="sxs-lookup"><span data-stu-id="39090-136">20150301</span></span> |<span data-ttu-id="39090-137">1</span><span class="sxs-lookup"><span data-stu-id="39090-137">1</span></span> |<span data-ttu-id="39090-138">3</span><span class="sxs-lookup"><span data-stu-id="39090-138">3</span></span> |
| <span data-ttu-id="39090-139">20150401</span><span class="sxs-lookup"><span data-stu-id="39090-139">20150401</span></span> |<span data-ttu-id="39090-140">2</span><span class="sxs-lookup"><span data-stu-id="39090-140">2</span></span> |<span data-ttu-id="39090-141">4</span><span class="sxs-lookup"><span data-stu-id="39090-141">4</span></span> |
| <span data-ttu-id="39090-142">20150501</span><span class="sxs-lookup"><span data-stu-id="39090-142">20150501</span></span> |<span data-ttu-id="39090-143">2</span><span class="sxs-lookup"><span data-stu-id="39090-143">2</span></span> |<span data-ttu-id="39090-144">4</span><span class="sxs-lookup"><span data-stu-id="39090-144">4</span></span> |
| <span data-ttu-id="39090-145">20150601</span><span class="sxs-lookup"><span data-stu-id="39090-145">20150601</span></span> |<span data-ttu-id="39090-146">2</span><span class="sxs-lookup"><span data-stu-id="39090-146">2</span></span> |<span data-ttu-id="39090-147">4</span><span class="sxs-lookup"><span data-stu-id="39090-147">4</span></span> |
| <span data-ttu-id="39090-148">20150701</span><span class="sxs-lookup"><span data-stu-id="39090-148">20150701</span></span> |<span data-ttu-id="39090-149">3</span><span class="sxs-lookup"><span data-stu-id="39090-149">3</span></span> |<span data-ttu-id="39090-150">1</span><span class="sxs-lookup"><span data-stu-id="39090-150">1</span></span> |
| <span data-ttu-id="39090-151">20150801</span><span class="sxs-lookup"><span data-stu-id="39090-151">20150801</span></span> |<span data-ttu-id="39090-152">3</span><span class="sxs-lookup"><span data-stu-id="39090-152">3</span></span> |<span data-ttu-id="39090-153">1</span><span class="sxs-lookup"><span data-stu-id="39090-153">1</span></span> |
| <span data-ttu-id="39090-154">20150801</span><span class="sxs-lookup"><span data-stu-id="39090-154">20150801</span></span> |<span data-ttu-id="39090-155">3</span><span class="sxs-lookup"><span data-stu-id="39090-155">3</span></span> |<span data-ttu-id="39090-156">1</span><span class="sxs-lookup"><span data-stu-id="39090-156">1</span></span> |
| <span data-ttu-id="39090-157">20151001</span><span class="sxs-lookup"><span data-stu-id="39090-157">20151001</span></span> |<span data-ttu-id="39090-158">4</span><span class="sxs-lookup"><span data-stu-id="39090-158">4</span></span> |<span data-ttu-id="39090-159">2</span><span class="sxs-lookup"><span data-stu-id="39090-159">2</span></span> |
| <span data-ttu-id="39090-160">20151101</span><span class="sxs-lookup"><span data-stu-id="39090-160">20151101</span></span> |<span data-ttu-id="39090-161">4</span><span class="sxs-lookup"><span data-stu-id="39090-161">4</span></span> |<span data-ttu-id="39090-162">2</span><span class="sxs-lookup"><span data-stu-id="39090-162">2</span></span> |
| <span data-ttu-id="39090-163">20151201</span><span class="sxs-lookup"><span data-stu-id="39090-163">20151201</span></span> |<span data-ttu-id="39090-164">4</span><span class="sxs-lookup"><span data-stu-id="39090-164">4</span></span> |<span data-ttu-id="39090-165">2</span><span class="sxs-lookup"><span data-stu-id="39090-165">2</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39090-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39090-166">Next steps</span></span>
<span data-ttu-id="39090-167">toomigrate um banco de dados do SQL Server, consulte [migração de banco de dados do SQL Server](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="39090-167">toomigrate a SQL Server database, see [SQL Server database migration](sql-database-cloud-migrate.md).</span></span>

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
