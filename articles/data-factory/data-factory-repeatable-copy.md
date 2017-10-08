---
title: "cópia de aaaRepeatable na fábrica de dados do Azure | Microsoft Docs"
description: "Saiba como tooavoid duplicatas, embora uma fatia que copia dados é executada mais de uma vez."
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
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="1814e-103">Cópia repetida no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1814e-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1814e-104">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="1814e-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="1814e-105">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="1814e-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="1814e-106">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="1814e-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1814e-107">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="1814e-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1814e-108">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="1814e-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="1814e-109">Hello exemplos a seguir são para o SQL Azure, mas são aplicáveis tooany repositório de dados que oferece suporte a conjuntos de dados retangulares.</span><span class="sxs-lookup"><span data-stu-id="1814e-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="1814e-110">Talvez você tenha tooadjust Olá **tipo** de origem e hello **consulta** propriedade (por exemplo: consulta em vez de sqlReaderQuery) para dados Olá armazenar.</span><span class="sxs-lookup"><span data-stu-id="1814e-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="1814e-111">Normalmente, ao ler de armazenamentos relacionais, você deseja tooread somente dados de saudação correspondente toothat fatia.</span><span class="sxs-lookup"><span data-stu-id="1814e-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="1814e-112">Uma maneira toodo assim seria usando Olá WindowStart e WindowEnd variáveis de sistema disponíveis no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1814e-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="1814e-113">Leia sobre as variáveis de saudação e funções do Azure Data Factory aqui em Olá [do Azure Data Factory - funções e variáveis de sistema](data-factory-functions-variables.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="1814e-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="1814e-114">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="1814e-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="1814e-115">Essa consulta lê os dados que se encaixa no intervalo de duração de fatias de saudação (WindowStart -> WindowEnd) da tabela Olá MyTable.</span><span class="sxs-lookup"><span data-stu-id="1814e-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="1814e-116">Execute novamente dessa fatia sempre garantiria que Olá tais dados são lidos.</span><span class="sxs-lookup"><span data-stu-id="1814e-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="1814e-117">Em outros casos, você poderá tooread Olá toda a tabela e pode definir Olá sqlReaderQuery da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1814e-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="1814e-118">Gravação REPEATABLE tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="1814e-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="1814e-119">Ao copiar dados muito**Azure SQL do SQL Server** outros armazenamentos de dados, você precisa tookeep repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="1814e-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="1814e-120">Ao copiar dados tooAzure banco de dados SQL do SQL Server, atividade de cópia Olá acrescenta a tabela de dados do coletor toohello por padrão.</span><span class="sxs-lookup"><span data-stu-id="1814e-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="1814e-121">Significa que você está copiando dados de um CSV (valores separados por vírgula) arquivos contendo dois registros toohello em um banco de dados do Azure SQL do SQL Server a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="1814e-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="1814e-122">Quando uma fatia é executado, Olá dois registros são copiados toohello tabela do SQL.</span><span class="sxs-lookup"><span data-stu-id="1814e-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="1814e-123">Suponha que você encontrou erros no arquivo de origem e quantidade de saudação do tubo de busca de 2 too4 atualizada.</span><span class="sxs-lookup"><span data-stu-id="1814e-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="1814e-124">Se você executar novamente a fatia de dados Olá para aquele período manualmente, você encontrará dois novos registros acrescentado tooAzure banco de dados SQL do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1814e-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="1814e-125">Este exemplo presume que nenhuma Olá colunas na tabela de saudação tem restrição de chave primária hello.</span><span class="sxs-lookup"><span data-stu-id="1814e-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="1814e-126">tooavoid esse comportamento, você precisa semântica UPSERT toospecify usando uma saudação dois mecanismos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1814e-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="1814e-127">Mecanismo 1: usando o sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="1814e-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="1814e-128">Você pode usar o hello **sqlWriterCleanupScript** tooclean propriedade backup de dados de tabela de coletor de saudação antes de inserir dados hello quando uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="1814e-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="1814e-129">Quando uma fatia é executado, script de limpeza de saudação é executado primeiro dados toodelete que corresponde a fatia toohello da tabela de saudação do SQL.</span><span class="sxs-lookup"><span data-stu-id="1814e-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="1814e-130">atividade de cópia Hello, em seguida, insere dados em Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="1814e-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="1814e-131">Se a fatia de saudação for executado novamente, a quantidade de saudação é atualizada conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="1814e-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="1814e-132">Suponha que Olá registro Arruela simples é removido do csv original hello.</span><span class="sxs-lookup"><span data-stu-id="1814e-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="1814e-133">Em seguida, executar novamente a fatia de saudação produziria Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="1814e-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="1814e-134">atividade de cópia Olá ficou Olá limpeza script toodelete Olá dados correspondentes para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="1814e-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="1814e-135">Em seguida, ele lê a entrada de saudação do csv hello (que, em seguida, continha apenas um registro) e inseri-lo no hello tabela.</span><span class="sxs-lookup"><span data-stu-id="1814e-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="1814e-136">Mecanismo 2: usando o sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="1814e-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1814e-137">No momento, não há suporte para sliceIdentifierColumnName no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="1814e-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="1814e-138">repetição do Hello segundo mecanismo tooachieve é ter uma coluna dedicada (sliceIdentifierColumnName) na tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="1814e-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="1814e-139">Essa coluna seria usada pelo Azure Data Factory tooensure Olá origem e destino fique sincronizado.</span><span class="sxs-lookup"><span data-stu-id="1814e-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="1814e-140">Essa abordagem funciona quando há flexibilidade ao alterar ou definir o esquema de tabela SQL de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="1814e-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="1814e-141">Esta coluna é usada pela fábrica de dados do Azure para fins de repetição e no processo de saudação do Azure Data Factory não faz qualquer esquema toohello tabela é alterado.</span><span class="sxs-lookup"><span data-stu-id="1814e-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="1814e-142">Modo toouse essa abordagem:</span><span class="sxs-lookup"><span data-stu-id="1814e-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="1814e-143">Definir uma coluna do tipo **binary (32)** no destino Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="1814e-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="1814e-144">Não deve haver nenhuma restrição nessa coluna.</span><span class="sxs-lookup"><span data-stu-id="1814e-144">There should be no constraints on this column.</span></span> <span data-ttu-id="1814e-145">Vamos nomear esta coluna como AdfSliceIdentifier para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="1814e-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="1814e-146">Tabela de origem:</span><span class="sxs-lookup"><span data-stu-id="1814e-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="1814e-147">Tabela de destino:</span><span class="sxs-lookup"><span data-stu-id="1814e-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="1814e-148">Usá-lo na atividade de cópia de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1814e-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="1814e-149">A fábrica de dados do Azure preenche essa coluna de acordo com sua necessidade tooensure Olá origem e destino permanecem sincronizados.</span><span class="sxs-lookup"><span data-stu-id="1814e-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="1814e-150">os valores dessa coluna Olá não devem ser usados fora neste contexto.</span><span class="sxs-lookup"><span data-stu-id="1814e-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="1814e-151">Semelhante toomechanism 1, atividade de cópia limpa automaticamente os dados de saudação para Olá fornecida fatia do destino Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="1814e-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="1814e-152">Em seguida, insere dados de origem na tabela de destino toohello.</span><span class="sxs-lookup"><span data-stu-id="1814e-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1814e-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1814e-153">Next steps</span></span>
<span data-ttu-id="1814e-154">Examine Olá conector artigos para concluir os exemplos JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="1814e-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="1814e-155">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1814e-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="1814e-156">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="1814e-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="1814e-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1814e-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)