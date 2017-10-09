## <span data-ttu-id="8d1cd-101"><a name="create-client"></a>Criar uma conexão de cliente</span><span class="sxs-lookup"><span data-stu-id="8d1cd-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="8d1cd-102">Crie uma conexão de cliente por meio da criação de um objeto `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="8d1cd-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="8d1cd-103">Substituir `appUrl` com o aplicativo móvel do tooyour de URL.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="8d1cd-104"><a name="table-reference"></a>Trabalhar com tabelas</span><span class="sxs-lookup"><span data-stu-id="8d1cd-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="8d1cd-105">tooaccess ou atualização de dados, crie uma tabela de back-end do toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="8d1cd-106">Substituir `tableName` com nome de saudação da tabela</span><span class="sxs-lookup"><span data-stu-id="8d1cd-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="8d1cd-107">Depois que tiver uma referência de tabela, será possível trabalhar ainda mais com sua tabela:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="8d1cd-108">Consultar uma tabela</span><span class="sxs-lookup"><span data-stu-id="8d1cd-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="8d1cd-109">Filtrando dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="8d1cd-110">Paginando pelos dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="8d1cd-111">Classificando dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="8d1cd-112">Inserindo dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="8d1cd-113">Modificando dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="8d1cd-114">Excluindo dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="8d1cd-115"><a name="querying"></a>Como consultar uma referência de tabela</span><span class="sxs-lookup"><span data-stu-id="8d1cd-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="8d1cd-116">Quando você tem uma referência de tabela, você pode usá-lo tooquery para os dados no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="8d1cd-117">As consultas são feitas em uma linguagem "parecida com LINQ".</span><span class="sxs-lookup"><span data-stu-id="8d1cd-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="8d1cd-118">tooreturn código de todos os dados da tabela hello, Olá uso a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-118">tooreturn all data from hello table, use hello following code:</span></span>

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="8d1cd-119">função de sucesso de saudação é chamada com resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="8d1cd-120">Não use `for (var i in results)` sucesso Olá funcionar conforme o que irá iterar sobre as informações que são incluídas nos resultados de saudação quando outras funções de consulta (como `.includeTotalCount()`) são usados.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="8d1cd-121">Para obter mais informações sobre sintaxe de consulta de hello, consulte Olá [consultar a documentação do objeto].</span><span class="sxs-lookup"><span data-stu-id="8d1cd-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="8d1cd-122"><a name="table-filter"></a>Filtrando dados no servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="8d1cd-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="8d1cd-123">Você pode usar um `where` cláusula na referência de tabela hello:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="8d1cd-124">Você também pode usar uma função que filtra o objeto hello.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="8d1cd-125">Nesse caso, Olá `this` variável é atribuída toothe objeto atual que está sendo filtrado.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="8d1cd-126">saudação de código a seguir é exemplo anterior toohello funcionalmente equivalentes:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="8d1cd-127"><a name="table-paging"></a>Paginando pelos dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="8d1cd-128">Utilizar saudação `take()` e `skip()` métodos.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="8d1cd-129">Por exemplo, se você quiser toosplit tabela de saudação em linha de 100 registros:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
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

<span data-ttu-id="8d1cd-130">Olá `.includeTotalCount()` método é usado tooadd um objeto de resultados toohello totalCount campo.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="8d1cd-131">O campo totalCount é preenchido com o número total de saudação de registros que seria retornado se nenhuma a paginação é usada.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="8d1cd-132">Você pode usar variável de páginas hello e alguns botões de interface do usuário tooprovide uma lista de página; Use `loadPage()` para carregar novos registros Olá para cada página.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="8d1cd-133">Implementar cache toospeed toorecords de acesso que já foram carregados.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="8d1cd-134"><a name="sorting-data"></a>Como: retornar dados classificados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="8d1cd-135">Saudação de uso `.orderBy()` ou `.orderByDescending()` métodos de consulta:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="8d1cd-136">Para obter mais informações sobre o objeto de consulta hello, consulte Olá [consultar a documentação do objeto].</span><span class="sxs-lookup"><span data-stu-id="8d1cd-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="8d1cd-137"><a name="inserting"></a>Como inserir dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="8d1cd-138">Criar um objeto de JavaScript com data apropriada hello e chame `table.insert()` assíncrona:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="8d1cd-139">Na inserção bem-sucedida, item Olá inserido é retornado com os campos Olá adicionais são necessários para operações de sincronização.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="8d1cd-140">Atualize seu próprio cache com essas informações para atualizações posteriores.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="8d1cd-141">Olá SDK do Azure Mobile aplicativos Node. js Server dá suporte a esquema dinâmico para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="8d1cd-142">Esquema dinâmico permite que você tooadd tabela de toohello de colunas, especificando-os em uma operação de inserção ou atualização.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="8d1cd-143">É recomendável que você desative esquema dinâmico antes de mover tooproduction seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="8d1cd-144"><a name="modifying"></a>Como modificar dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="8d1cd-145">Semelhante toohello `.insert()` método, você deve criar um objeto de atualização e, em seguida, chamar `.update()`.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="8d1cd-146">Olá Atualizar objeto deve conter ID de saudação do hello toobe registro atualizado - Olá ID é obtido durante a leitura de registro de saudação ou ao chamar `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="8d1cd-147"><a name="deleting"></a>Como excluir dados</span><span class="sxs-lookup"><span data-stu-id="8d1cd-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="8d1cd-148">toodelete um registro, chamada hello `.del()` método.</span><span class="sxs-lookup"><span data-stu-id="8d1cd-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="8d1cd-149">ID de saudação de passagem em uma referência de objeto:</span><span class="sxs-lookup"><span data-stu-id="8d1cd-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
