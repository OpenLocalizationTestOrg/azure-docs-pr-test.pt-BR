---
title: "Cópia repetida no Azure Data Factory | Microsoft Docs"
description: Saiba como evitar duplicatas mesmo que uma fatia que copia dados seja executada mais de uma vez.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="d972b-103">Cópia repetida no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d972b-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d972b-104">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="d972b-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="d972b-105">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="d972b-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="d972b-106">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="d972b-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d972b-107">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="d972b-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d972b-108">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="d972b-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="d972b-109">Os exemplos a seguir são para o Azure SQL, mas são aplicáveis a qualquer repositório de dados com suporte a conjuntos de dados retangulares.</span><span class="sxs-lookup"><span data-stu-id="d972b-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="d972b-110">Talvez seja necessário ajustar o **tipo** de origem e a propriedade **query** (por exemplo: query em vez de sqlReaderQuery) para o repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="d972b-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="d972b-111">Geralmente, ao ler repositórios relacionais, convém ler apenas os dados correspondentes a essa fatia.</span><span class="sxs-lookup"><span data-stu-id="d972b-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="d972b-112">Uma maneira de fazer isso é usando as variáveis do sistema WindowStart e WindowEnd disponíveis no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d972b-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="d972b-113">Leia sobre as variáveis e funções no Azure Data Factory aqui, no artigo [Azure Data Factory – Funções e Variáveis do Sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="d972b-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="d972b-114">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="d972b-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="d972b-115">Essa consulta lê os dados do intervalo de duração da fatia (WindowStart -> WindowEnd) da tabela MyTable.</span><span class="sxs-lookup"><span data-stu-id="d972b-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="d972b-116">A eventual reexecução dessa fatia também asseguraria sempre que os mesmos dados fossem lidos.</span><span class="sxs-lookup"><span data-stu-id="d972b-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="d972b-117">Em outros casos, talvez seja conveniente ler a tabela inteira e definir sqlReaderQuery da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d972b-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="d972b-118">Gravação repetível para SqlSink</span><span class="sxs-lookup"><span data-stu-id="d972b-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="d972b-119">Ao copiar os dados de outros armazenamentos de dados para o **Azure SQL/SQL Server**, você precisa manter em mente a capacidade de repetição para evitar desfechos não intencionais.</span><span class="sxs-lookup"><span data-stu-id="d972b-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="d972b-120">Ao copiar dados para o Banco de Dados do SQL Server/Azure SQL, a atividade de cópia acrescenta dados à tabela de coletor por padrão.</span><span class="sxs-lookup"><span data-stu-id="d972b-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="d972b-121">Digamos que você estiver copiando dados de um arquivo CSV (valores separados por vírgulas) contendo dois registros na tabela a seguir em um Banco de Dados do SQL Server/Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="d972b-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="d972b-122">Quando uma fatia é executada, os dois registros são copiados para a tabela do SQL.</span><span class="sxs-lookup"><span data-stu-id="d972b-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="d972b-123">Suponha que você encontrou erros no arquivo de origem e atualizou a quantidade de Down Tubes de dois para quatro.</span><span class="sxs-lookup"><span data-stu-id="d972b-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="d972b-124">Se você executar novamente a fatia de dados para esse período manualmente, você encontrará dois novos registros anexados ao banco de dados SQL do Azure/banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d972b-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="d972b-125">Este exemplo pressupõe que nenhuma das colunas na tabela tem a restrição de chave primária.</span><span class="sxs-lookup"><span data-stu-id="d972b-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="d972b-126">Para evitar esse comportamento, você precisa especificar a semântica UPSERT, usando um dos dois mecanismos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d972b-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="d972b-127">Mecanismo 1: usando o sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d972b-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="d972b-128">Você pode usar a propriedade **sqlWriterCleanupScript** para limpar os dados da tabela de coletor antes de inserir os dados quando uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="d972b-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="d972b-129">Quando uma fatia é executada, o script de limpeza é executado pela primeira vez para excluir dados que correspondem à fatia da tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="d972b-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="d972b-130">A atividade de cópia, em seguida, insere dados na tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="d972b-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="d972b-131">Se a fatia é executada novamente, a quantidade é atualizada conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="d972b-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="d972b-132">Suponha que o registro Flat Washer é removido do csv original.</span><span class="sxs-lookup"><span data-stu-id="d972b-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="d972b-133">Nesse caso, executar novamente a fatia geraria o seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="d972b-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="d972b-134">A atividade de cópia executou o script de limpeza para excluir os dados correspondentes àquela fatia.</span><span class="sxs-lookup"><span data-stu-id="d972b-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="d972b-135">Ela então leu a entrada do csv (que continha então apenas um registro) e a inseriu na tabela.</span><span class="sxs-lookup"><span data-stu-id="d972b-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="d972b-136">Mecanismo 2: usando o sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="d972b-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d972b-137">No momento, não há suporte para sliceIdentifierColumnName no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="d972b-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="d972b-138">O segundo mecanismo para atingir a capacidade de repetição é ter uma coluna dedicada (sliceIdentifierColumnName) na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="d972b-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="d972b-139">Essa coluna pode ser usada pelo Azure Data Factory para garantir que a origem e destino permaneçam em sincronia.</span><span class="sxs-lookup"><span data-stu-id="d972b-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="d972b-140">Essa abordagem funciona quando há flexibilidade para alteração ou definição do esquema de tabela SQL de destino.</span><span class="sxs-lookup"><span data-stu-id="d972b-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="d972b-141">Essa coluna é usada pelo Azure Data Factory para fins de capacidade de repetição e, no processo, o Azure Data Factory não faz nenhuma alteração de esquema na tabela.</span><span class="sxs-lookup"><span data-stu-id="d972b-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="d972b-142">Modo de usar essa abordagem:</span><span class="sxs-lookup"><span data-stu-id="d972b-142">Way to use this approach:</span></span>

1. <span data-ttu-id="d972b-143">Defina uma coluna do tipo **binário (32)** na tabela SQL de destino.</span><span class="sxs-lookup"><span data-stu-id="d972b-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="d972b-144">Não deve haver nenhuma restrição nessa coluna.</span><span class="sxs-lookup"><span data-stu-id="d972b-144">There should be no constraints on this column.</span></span> <span data-ttu-id="d972b-145">Vamos nomear esta coluna como AdfSliceIdentifier para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="d972b-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="d972b-146">Tabela de origem:</span><span class="sxs-lookup"><span data-stu-id="d972b-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="d972b-147">Tabela de destino:</span><span class="sxs-lookup"><span data-stu-id="d972b-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="d972b-148">Use-a na atividade de cópia da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d972b-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="d972b-149">A Azure Data Factory popula essa coluna para garantir que a origem e destino permaneçam em sincronia.</span><span class="sxs-lookup"><span data-stu-id="d972b-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="d972b-150">Os valores desta coluna não devem ser usados fora deste contexto.</span><span class="sxs-lookup"><span data-stu-id="d972b-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="d972b-151">Semelhante ao mecanismo 1, os dados da fatia fornecida da tabela SQL de destino são limpos automaticamente pela Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="d972b-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="d972b-152">A Atividade de Cópia então insere dados da origem na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="d972b-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d972b-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d972b-153">Next steps</span></span>
<span data-ttu-id="d972b-154">Examine os artigos sobre conector a seguir para obter exemplos de JSON completos:</span><span class="sxs-lookup"><span data-stu-id="d972b-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="d972b-155">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="d972b-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="d972b-156">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="d972b-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="d972b-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d972b-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)