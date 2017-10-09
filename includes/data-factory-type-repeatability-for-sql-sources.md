## <a name="repeatability-during-copy"></a><span data-ttu-id="26b99-101">Capacidade de repetição durante a cópia</span><span class="sxs-lookup"><span data-stu-id="26b99-101">Repeatability during Copy</span></span>
<span data-ttu-id="26b99-102">Quando a cópia tooAzure de dados SQL do SQL Server de outros dados armazena uma repetição de tookeep necessidades em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="26b99-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="26b99-103">Ao copiar dados tooAzure banco de dados SQL do SQL Server, a atividade de cópia será pela tabela de coletor padrão ACRESCENTAR Olá conjunto de dados toohello por padrão.</span><span class="sxs-lookup"><span data-stu-id="26b99-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="26b99-104">Por exemplo, ao copiar dados de uma fonte de arquivo CSV (dados de valores separados por vírgula) que contém dois registros tooAzure banco de dados SQL do SQL Server, isso é que tabela Olá parece com:</span><span class="sxs-lookup"><span data-stu-id="26b99-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="26b99-105">Suponha que você encontrou erros no arquivo de origem e a quantidade de Olá atualizado de busca tubo de too4 2 no arquivo de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b99-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="26b99-106">Se você executar novamente a fatia de dados Olá para esse período, você encontrará dois novos registros acrescentado tooAzure banco de dados SQL do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="26b99-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="26b99-107">Olá abaixo assume que nenhuma Olá colunas na tabela de saudação tem restrição de chave primária hello.</span><span class="sxs-lookup"><span data-stu-id="26b99-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="26b99-108">tooavoid isso, você precisará de semântica UPSERT toospecify utilizando uma saudação abaixo 2 mecanismos descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="26b99-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="26b99-109">Uma fatia pode ser executada novamente automaticamente na fábrica de dados do Azure de acordo com a política de repetição de saudação especificada.</span><span class="sxs-lookup"><span data-stu-id="26b99-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="26b99-110">Mecanismo 1</span><span class="sxs-lookup"><span data-stu-id="26b99-110">Mechanism 1</span></span>
<span data-ttu-id="26b99-111">Você pode aproveitar **sqlWriterCleanupScript** propriedade toofirst executar a ação de limpeza quando uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="26b99-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="26b99-112">Olá script de limpeza deve ser executado primeiro durante a cópia para uma determinada fatia que excluirá dados saudação da fatia de toothat Olá tabela SQL correspondente.</span><span class="sxs-lookup"><span data-stu-id="26b99-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="26b99-113">atividade de saudação subsequentemente inserirá dados saudação no hello tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="26b99-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="26b99-114">Se a fatia de saudação é agora execute novamente, em seguida, você encontrará a quantidade de saudação é atualizada como desejado.</span><span class="sxs-lookup"><span data-stu-id="26b99-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="26b99-115">Suponha que Olá registro Arruela simples é removido do csv original hello.</span><span class="sxs-lookup"><span data-stu-id="26b99-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="26b99-116">Em seguida, executando novamente fatia de saudação produziria Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b99-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="26b99-117">Nada de novo tinha toobe feito.</span><span class="sxs-lookup"><span data-stu-id="26b99-117">Nothing new had toobe done.</span></span> <span data-ttu-id="26b99-118">atividade de cópia Olá ficou Olá limpeza script toodelete Olá dados correspondentes para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="26b99-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="26b99-119">Em seguida, ele lê a entrada de saudação do csv hello (que, em seguida, continha apenas 1 registro) e inseri-lo no hello tabela.</span><span class="sxs-lookup"><span data-stu-id="26b99-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="26b99-120">Mecanismo 2</span><span class="sxs-lookup"><span data-stu-id="26b99-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="26b99-121">No momento, não há suporte para sliceIdentifierColumnName no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b99-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="26b99-122">Capacidade de repetição do outro mecanismo tooachieve é ter uma coluna dedicada (**sliceIdentifierColumnName**) no hello tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="26b99-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="26b99-123">Essa coluna seria usada pelo Azure Data Factory tooensure Olá origem e destino fique sincronizado.</span><span class="sxs-lookup"><span data-stu-id="26b99-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="26b99-124">Essa abordagem funciona quando há flexibilidade ao alterar ou definir o esquema de tabela SQL de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b99-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="26b99-125">Esta coluna será usada pela fábrica de dados do Azure para fins de repetição e no processo de saudação do Azure Data Factory não fará qualquer esquema toohello tabela é alterado.</span><span class="sxs-lookup"><span data-stu-id="26b99-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="26b99-126">Modo toouse essa abordagem:</span><span class="sxs-lookup"><span data-stu-id="26b99-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="26b99-127">Defina uma coluna do tipo binary (32) no destino Olá tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="26b99-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="26b99-128">Não deve haver nenhuma restrição nessa coluna.</span><span class="sxs-lookup"><span data-stu-id="26b99-128">There should be no constraints on this column.</span></span> <span data-ttu-id="26b99-129">Vamos nomear esta coluna como 'ColumnForADFuseOnly' para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="26b99-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="26b99-130">Usá-lo na atividade de cópia de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="26b99-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="26b99-131">O Azure Data Factory preencherá essa coluna de acordo com sua necessidade tooensure Olá origem e destino permanecem sincronizados.</span><span class="sxs-lookup"><span data-stu-id="26b99-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="26b99-132">valores de saudação desta coluna não devem ser usados fora deste contexto por usuário hello.</span><span class="sxs-lookup"><span data-stu-id="26b99-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="26b99-133">Semelhante toomechanism 1, será de atividade de cópia automaticamente primeiro limpar dados Olá para Olá fornecidas fatia do destino Olá tabela SQL e execute a atividade de cópia Olá normalmente tooinsert dados Olá toodestination de origem para essa fatia.</span><span class="sxs-lookup"><span data-stu-id="26b99-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

