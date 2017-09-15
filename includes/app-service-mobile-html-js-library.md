## <span data-ttu-id="a7335-101"><a name="create-client"></a>Criar uma conexão de cliente</span><span class="sxs-lookup"><span data-stu-id="a7335-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="a7335-102">Crie uma conexão de cliente por meio da criação de um objeto `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="a7335-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="a7335-103">Substitua `appUrl` pela URL de seu Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="a7335-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="a7335-104"><a name="table-reference"></a>Trabalhar com tabelas</span><span class="sxs-lookup"><span data-stu-id="a7335-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="a7335-105">Para acessar ou atualizar dados, crie uma referência à tabela de back-end.</span><span class="sxs-lookup"><span data-stu-id="a7335-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="a7335-106">Substitua `tableName` pelo nome de sua tabela</span><span class="sxs-lookup"><span data-stu-id="a7335-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="a7335-107">Depois que tiver uma referência de tabela, será possível trabalhar ainda mais com sua tabela:</span><span class="sxs-lookup"><span data-stu-id="a7335-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="a7335-108">Consultar uma tabela</span><span class="sxs-lookup"><span data-stu-id="a7335-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="a7335-109">Filtrando dados</span><span class="sxs-lookup"><span data-stu-id="a7335-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="a7335-110">Paginando pelos dados</span><span class="sxs-lookup"><span data-stu-id="a7335-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="a7335-111">Classificando dados</span><span class="sxs-lookup"><span data-stu-id="a7335-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="a7335-112">Inserindo dados</span><span class="sxs-lookup"><span data-stu-id="a7335-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="a7335-113">Modificando dados</span><span class="sxs-lookup"><span data-stu-id="a7335-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="a7335-114">Excluindo dados</span><span class="sxs-lookup"><span data-stu-id="a7335-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="a7335-115"><a name="querying"></a>Como consultar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="a7335-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="a7335-116">Depois que você tiver uma referência de tabela, será possível usá-la para consultar dados no servidor.</span><span class="sxs-lookup"><span data-stu-id="a7335-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="a7335-117">As consultas são feitas em uma linguagem "parecida com LINQ".</span><span class="sxs-lookup"><span data-stu-id="a7335-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="a7335-118">Para retornar todos os dados da tabela, use o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a7335-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="a7335-119">A função de sucesso é chamada com os resultados.</span><span class="sxs-lookup"><span data-stu-id="a7335-119">The success function is called with the results.</span></span>  <span data-ttu-id="a7335-120">Não use `for (var i in results)` na função de sucesso, pois isso causará a iteração de informações incluídas nos resultados quando outras funções de consulta (como `.includeTotalCount()`) forem usadas.</span><span class="sxs-lookup"><span data-stu-id="a7335-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="a7335-121">Para obter mais informações sobre a sintaxe Query, confira a [documentação do objeto Query].</span><span class="sxs-lookup"><span data-stu-id="a7335-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="a7335-122"><a name="table-filter"></a>Filtragem de dados no servidor</span><span class="sxs-lookup"><span data-stu-id="a7335-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="a7335-123">É possível usar uma cláusula `where` na referência de tabela:</span><span class="sxs-lookup"><span data-stu-id="a7335-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="a7335-124">Você também pode usar uma função que filtra o objeto.</span><span class="sxs-lookup"><span data-stu-id="a7335-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="a7335-125">Nesse caso, a variável `this` é atribuída ao objeto atual que está sendo filtrado.</span><span class="sxs-lookup"><span data-stu-id="a7335-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="a7335-126">O código a seguir é uma funcionalidade equivalente ao exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="a7335-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="a7335-127"><a name="table-paging"></a>Paginando pelos dados</span><span class="sxs-lookup"><span data-stu-id="a7335-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="a7335-128">Utilize os métodos `take()` e `skip()`.</span><span class="sxs-lookup"><span data-stu-id="a7335-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="a7335-129">Por exemplo, se você quiser dividir a tabela em registros de 100 linhas:</span><span class="sxs-lookup"><span data-stu-id="a7335-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

<span data-ttu-id="a7335-130">O método `.includeTotalCount()` é usado para adicionar um campo totalCount ao objeto de resultados.</span><span class="sxs-lookup"><span data-stu-id="a7335-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="a7335-131">O campo totalCount é preenchido com o número total de registros que retornariam se nenhuma paginação fosse usada.</span><span class="sxs-lookup"><span data-stu-id="a7335-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="a7335-132">Depois, você pode usar a variável de páginas e alguns botões da interface de usuário para fornecer uma lista de páginas; use `loadPage()` para carregar os novos registros de cada página.</span><span class="sxs-lookup"><span data-stu-id="a7335-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="a7335-133">Implemente cache para agilizar o acesso a registros que já foram carregados.</span><span class="sxs-lookup"><span data-stu-id="a7335-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="a7335-134"><a name="sorting-data"></a>Como: retornar dados classificados</span><span class="sxs-lookup"><span data-stu-id="a7335-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="a7335-135">Use os métodos de consulta `.orderBy()` ou `.orderByDescending()`:</span><span class="sxs-lookup"><span data-stu-id="a7335-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="a7335-136">Para obter mais informações sobre o objeto Query, confira a [documentação do objeto Query].</span><span class="sxs-lookup"><span data-stu-id="a7335-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="a7335-137"><a name="inserting"></a>Como inserir dados</span><span class="sxs-lookup"><span data-stu-id="a7335-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="a7335-138">Crie um objeto JavaScript com a data adequada e chame `table.insert()` de maneira assíncrona:</span><span class="sxs-lookup"><span data-stu-id="a7335-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

<span data-ttu-id="a7335-139">Após a inserção bem-sucedida, o item inserido retorna com os campos adicionais necessários para as operações de sincronização.</span><span class="sxs-lookup"><span data-stu-id="a7335-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="a7335-140">Atualize seu próprio cache com essas informações para atualizações posteriores.</span><span class="sxs-lookup"><span data-stu-id="a7335-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="a7335-141">O SDK de Node.js Server dos Aplicativos Móveis do Azure dá suporte ao esquema dinâmico para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="a7335-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="a7335-142">O esquema Dinâmico permite que você adicione colunas à tabela, especificando-as em uma operação de inserção ou atualização.</span><span class="sxs-lookup"><span data-stu-id="a7335-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="a7335-143">Recomendamos que você desative o esquema antes de mover seu aplicativo para produção.</span><span class="sxs-lookup"><span data-stu-id="a7335-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="a7335-144"><a name="modifying"></a>Como modificar dados</span><span class="sxs-lookup"><span data-stu-id="a7335-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="a7335-145">Assim como o método `.insert()`, você deve criar um objeto de atualização e, em seguida, chamar `.update()`.</span><span class="sxs-lookup"><span data-stu-id="a7335-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="a7335-146">O objeto de atualização deve conter a ID do registro a ser atualizada. Essa ID é obtida ao ler o registro ou ao chamar `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="a7335-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <span data-ttu-id="a7335-147"><a name="deleting"></a>Como excluir dados</span><span class="sxs-lookup"><span data-stu-id="a7335-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="a7335-148">Chame o método `.del()` para excluir um registro.</span><span class="sxs-lookup"><span data-stu-id="a7335-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="a7335-149">Passe a ID em uma referência de objeto:</span><span class="sxs-lookup"><span data-stu-id="a7335-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
