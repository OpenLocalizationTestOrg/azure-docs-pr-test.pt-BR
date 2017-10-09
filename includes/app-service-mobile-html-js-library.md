## <a name="create-client"></a>Criar uma conexão de cliente
Crie uma conexão de cliente por meio da criação de um objeto `WindowsAzure.MobileServiceClient` .  Substituir `appUrl` com o aplicativo móvel do tooyour de URL.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Trabalhar com tabelas
tooaccess ou atualização de dados, crie uma tabela de back-end do toohello de referência. Substituir `tableName` com nome de saudação da tabela

```
var table = client.getTable(tableName);
```

Depois que tiver uma referência de tabela, será possível trabalhar ainda mais com sua tabela:

* [Consultar uma tabela](#querying)
  * [Filtrando dados](#table-filter)
  * [Paginando pelos dados](#table-paging)
  * [Classificando dados](#sorting-data)
* [Inserindo dados](#inserting)
* [Modificando dados](#modifying)
* [Excluindo dados](#deleting)

### <a name="querying"></a>Como consultar uma referência de tabela
Quando você tem uma referência de tabela, você pode usá-lo tooquery para os dados no servidor de saudação.  As consultas são feitas em uma linguagem "parecida com LINQ".
tooreturn código de todos os dados da tabela hello, Olá uso a seguir:

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

função de sucesso de saudação é chamada com resultados de saudação.  Não use `for (var i in results)` sucesso Olá funcionar conforme o que irá iterar sobre as informações que são incluídas nos resultados de saudação quando outras funções de consulta (como `.includeTotalCount()`) são usados.

Para obter mais informações sobre sintaxe de consulta de hello, consulte Olá [consultar a documentação do objeto].

#### <a name="table-filter"></a>Filtrando dados no servidor de saudação
Você pode usar um `where` cláusula na referência de tabela hello:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Você também pode usar uma função que filtra o objeto hello.  Nesse caso, Olá `this` variável é atribuída toothe objeto atual que está sendo filtrado.  saudação de código a seguir é exemplo anterior toohello funcionalmente equivalentes:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Paginando pelos dados
Utilizar saudação `take()` e `skip()` métodos.  Por exemplo, se você quiser toosplit tabela de saudação em linha de 100 registros:

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

Olá `.includeTotalCount()` método é usado tooadd um objeto de resultados toohello totalCount campo.  O campo totalCount é preenchido com o número total de saudação de registros que seria retornado se nenhuma a paginação é usada.

Você pode usar variável de páginas hello e alguns botões de interface do usuário tooprovide uma lista de página; Use `loadPage()` para carregar novos registros Olá para cada página.  Implementar cache toospeed toorecords de acesso que já foram carregados.

#### <a name="sorting-data"></a>Como: retornar dados classificados
Saudação de uso `.orderBy()` ou `.orderByDescending()` métodos de consulta:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Para obter mais informações sobre o objeto de consulta hello, consulte Olá [consultar a documentação do objeto].

### <a name="inserting"></a>Como inserir dados
Criar um objeto de JavaScript com data apropriada hello e chame `table.insert()` assíncrona:

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

Na inserção bem-sucedida, item Olá inserido é retornado com os campos Olá adicionais são necessários para operações de sincronização.  Atualize seu próprio cache com essas informações para atualizações posteriores.

Olá SDK do Azure Mobile aplicativos Node. js Server dá suporte a esquema dinâmico para fins de desenvolvimento.  Esquema dinâmico permite que você tooadd tabela de toohello de colunas, especificando-os em uma operação de inserção ou atualização.  É recomendável que você desative esquema dinâmico antes de mover tooproduction seu aplicativo.

### <a name="modifying"></a>Como modificar dados
Semelhante toohello `.insert()` método, você deve criar um objeto de atualização e, em seguida, chamar `.update()`.  Olá Atualizar objeto deve conter ID de saudação do hello toobe registro atualizado - Olá ID é obtido durante a leitura de registro de saudação ou ao chamar `.insert()`.

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

### <a name="deleting"></a>Como excluir dados
toodelete um registro, chamada hello `.del()` método.  ID de saudação de passagem em uma referência de objeto:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
