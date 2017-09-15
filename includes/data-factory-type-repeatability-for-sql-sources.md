## <a name="repeatability-during-copy"></a><span data-ttu-id="99cd2-101">Capacidade de repetição durante a cópia</span><span class="sxs-lookup"><span data-stu-id="99cd2-101">Repeatability during Copy</span></span>
<span data-ttu-id="99cd2-102">Ao copiar os dados de outros repositórios de dados para o Azure SQL/SQL Server, a pessoa precisa manter em mente a capacidade de repetição para evitar desfechos não intencionais.</span><span class="sxs-lookup"><span data-stu-id="99cd2-102">When copying data to Azure SQL/SQL Server from other data stores one needs to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="99cd2-103">Ao copiar dados ao Azure SQL/Banco de dados do servidor do SQL, a atividade de cópia vai, por padrão, ACRESCENTAR o conjunto de dados à tabela de coletor por padrão.</span><span class="sxs-lookup"><span data-stu-id="99cd2-103">When copying data to Azure SQL/SQL Server Database, copy activity will by default APPEND the data set to the sink table by default.</span></span> <span data-ttu-id="99cd2-104">Por exemplo, ao copiar dados de uma fonte de arquivo CSV (dados com valores separados por vírgulas) contendo dois registros de banco de dados do SQL do Azure/SQL Server, a aparência da tabela é semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="99cd2-104">For example, when copying data from a CSV (comma separated values data) file source containing two records to Azure SQL/SQL Server Database, this is what the table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="99cd2-105">Suponha que você encontrou erros no arquivo de origem e atualizou a quantidade de Down Tubes de 2 para 4 no arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="99cd2-105">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4 in the source file.</span></span> <span data-ttu-id="99cd2-106">Se você executar novamente a fatia de dados para esse período, você encontrará dois novos registros anexados ao banco de dados SQL do Azure/banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="99cd2-106">If you re-run the data slice for that period, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="99cd2-107">O exemplo abaixo pressupõe que nenhuma das colunas na tabela tenha a restrição de chave primária.</span><span class="sxs-lookup"><span data-stu-id="99cd2-107">The below assumes none of the columns in the table have the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="99cd2-108">Para evitar isso, você precisará especificar a semântica UPSERT, aproveitando um dos 2 mecanismos descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="99cd2-108">To avoid this, you will need to specify UPSERT semantics by leveraging one of the below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="99cd2-109">Uma fatia pode ser reexecutada automaticamente no Azure Data Factory, de acordo com a política de repetição especificada.</span><span class="sxs-lookup"><span data-stu-id="99cd2-109">A slice can be re-run automatically in Azure Data Factory as per the retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="99cd2-110">Mecanismo 1</span><span class="sxs-lookup"><span data-stu-id="99cd2-110">Mechanism 1</span></span>
<span data-ttu-id="99cd2-111">Você pode aproveitar a propriedade **sqlWriterCleanupScript** para executar primeiro a ação de limpeza quando uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="99cd2-111">You can leverage **sqlWriterCleanupScript** property to first perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="99cd2-112">O script de limpeza deve ser executado primeiro durante a cópia para uma determinada fatia que excluiria os dados da tabela SQL correspondente a essa fatia.</span><span class="sxs-lookup"><span data-stu-id="99cd2-112">The cleanup script would be executed first during copy for a given slice which would delete the data from the SQL Table corresponding to that slice.</span></span> <span data-ttu-id="99cd2-113">A atividade vai inserir, subsequentemente, os dados na tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="99cd2-113">The activity will subsequently insert the data into the SQL Table.</span></span> 

<span data-ttu-id="99cd2-114">Se a fatia for executada novamente, você verá que a quantidade é atualizada conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="99cd2-114">If the slice is now re-run, then you will find the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="99cd2-115">Suponha que o registro Flat Washer é removido do csv original.</span><span class="sxs-lookup"><span data-stu-id="99cd2-115">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="99cd2-116">Nesse caso, reexecutar novamente a fatia geraria o seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="99cd2-116">Then re-running the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="99cd2-117">Não era necessário fazer nada de novo.</span><span class="sxs-lookup"><span data-stu-id="99cd2-117">Nothing new had to be done.</span></span> <span data-ttu-id="99cd2-118">A atividade de cópia executou o script de limpeza para excluir os dados correspondentes àquela fatia.</span><span class="sxs-lookup"><span data-stu-id="99cd2-118">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="99cd2-119">Em seguida, lê a entrada do csv (que continha apenas 1 registro) e insere-a na tabela.</span><span class="sxs-lookup"><span data-stu-id="99cd2-119">Then it read the input from the csv (which then contained only 1 record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="99cd2-120">Mecanismo 2</span><span class="sxs-lookup"><span data-stu-id="99cd2-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="99cd2-121">No momento, não há suporte para sliceIdentifierColumnName no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="99cd2-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="99cd2-122">Outro mecanismo para atingir a capacidade de repetição é ter uma coluna dedicada (**sliceIdentifierColumnName**) na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="99cd2-122">Another mechanism to achieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in the target Table.</span></span> <span data-ttu-id="99cd2-123">Essa coluna pode ser usada pelo Azure Data Factory para garantir que a origem e destino permaneçam em sincronia.</span><span class="sxs-lookup"><span data-stu-id="99cd2-123">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="99cd2-124">Essa abordagem funciona quando há flexibilidade para alteração ou definição do esquema de tabela SQL de destino.</span><span class="sxs-lookup"><span data-stu-id="99cd2-124">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="99cd2-125">Essa coluna seria usada pelo Azure Data Factory para fins de capacidade de repetição e, no processo, o Azure Data Factory não fará alterações de esquema à tabela.</span><span class="sxs-lookup"><span data-stu-id="99cd2-125">This column would be used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory will not make any schema changes to the Table.</span></span> <span data-ttu-id="99cd2-126">Modo de usar essa abordagem:</span><span class="sxs-lookup"><span data-stu-id="99cd2-126">Way to use this approach:</span></span>

1. <span data-ttu-id="99cd2-127">Defina uma coluna do tipo binário (32) na tabela SQL de destino.</span><span class="sxs-lookup"><span data-stu-id="99cd2-127">Define a column of type binary (32) in the destination SQL Table.</span></span> <span data-ttu-id="99cd2-128">Não deve haver nenhuma restrição nessa coluna.</span><span class="sxs-lookup"><span data-stu-id="99cd2-128">There should be no constraints on this column.</span></span> <span data-ttu-id="99cd2-129">Vamos nomear esta coluna como 'ColumnForADFuseOnly' para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="99cd2-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="99cd2-130">Use-a na atividade de cópia da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="99cd2-130">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="99cd2-131">A Azure Data Factory vai popular essa coluna para garantir que a origem e destino permaneçam em sincronia.</span><span class="sxs-lookup"><span data-stu-id="99cd2-131">Azure Data Factory will populate this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="99cd2-132">Os valores desta coluna não devem ser usados fora deste contexto pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="99cd2-132">The values of this column should not be used outside of this context by the user.</span></span> 

<span data-ttu-id="99cd2-133">Semelhante ao mecanismo 1, a atividade de cópia limpará primeiro automaticamente os dados para a fatia determinada da tabela SQL de destino e, em seguida, executará a atividade de cópia normalmente para inserir os dados da origem para o destino, nessa fatia.</span><span class="sxs-lookup"><span data-stu-id="99cd2-133">Similar to mechanism 1, Copy Activity will automatically first clean up the data for the given slice from the destination SQL Table and then run the copy activity normally to insert the data from source to destination for that slice.</span></span> 

