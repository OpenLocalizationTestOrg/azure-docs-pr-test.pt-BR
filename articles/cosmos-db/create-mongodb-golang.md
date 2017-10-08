---
<span data-ttu-id="d2d6e-101">título: aaa "banco de dados do Azure Cosmos: criar um aplicativo de console do MongoDB API com Golang e Olá portal do Azure | Descrição de Microsoft Docs": apresenta um exemplo de código Golang você pode usar tooconnect tooand consultar os serviços do Azure Cosmos DB: cosmos db autor: manager Durgaprasad Budhwani: jhubbard editor: mimig1</span><span class="sxs-lookup"><span data-stu-id="d2d6e-101">title: aaa"Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal | Microsoft Docs" description: Presents a Golang code sample you can use tooconnect tooand query Azure Cosmos DB services: cosmos-db author: Durgaprasad-Budhwani manager: jhubbard editor: mimig1</span></span>

<span data-ttu-id="d2d6e-102">MS. Service: cosmos db MS. Topic: hero-article MS. Date: 21/07/2017 Author: mimig</span><span class="sxs-lookup"><span data-stu-id="d2d6e-102">ms.service: cosmos-db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span></span>
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a><span data-ttu-id="d2d6e-103">Banco de dados do Azure do Cosmos: Criar um aplicativo de console do MongoDB API com Golang e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2d6e-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal</span></span>

<span data-ttu-id="d2d6e-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d2d6e-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="d2d6e-106">Esse início rápido demonstra como toouse existente [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) aplicativo escrito em [Golang](https://golang.org/) e conectá-lo tooyour Azure Cosmos banco de dados, que oferece suporte a conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-106">This quick-start demonstrates how toouse an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="d2d6e-107">Em outras palavras, o aplicativo Golang só sabe que ele está se conectando tooa banco de dados usando APIs do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-107">In other words, your Golang application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="d2d6e-108">Isso é transparente toohello aplicativo hello dados é armazenado no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2d6e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d2d6e-109">Prerequisites</span></span>

- <span data-ttu-id="d2d6e-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-110">An Azure subscription.</span></span> <span data-ttu-id="d2d6e-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="d2d6e-112">[Vá](https://golang.org/dl/) e um conhecimento básico de saudação [vá](https://golang.org/) idioma.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-112">[Go](https://golang.org/dl/) and a basic knowledge of hello [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="d2d6e-113">Um IDE — [Gogland](https://www.jetbrains.com/go/) da Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) ou [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="d2d6e-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="d2d6e-114">Neste tutorial, estou usando Goglang.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="d2d6e-115">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="d2d6e-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="d2d6e-116">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="d2d6e-116">Clone hello sample application</span></span>

<span data-ttu-id="d2d6e-117">Clonar o aplicativo de exemplo hello e instalar pacotes de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-117">Clone hello sample application and install hello required packages.</span></span>

1. <span data-ttu-id="d2d6e-118">Crie uma pasta chamada CosmosDBSample Olá GOROOT\src pasta, que é C:\Go\ por padrão.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-118">Create a folder named CosmosDBSample inside hello GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="d2d6e-119">Execute hello usando uma janela do terminal de git, como o repositório do git bash tooclone Olá exemplo na pasta de CosmosDBSample de saudação do comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-119">Run hello following command using a git terminal window such as git bash tooclone hello sample repository into hello CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="d2d6e-120">Olá executar pacote do comando tooget Olá mgo a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-120">Run hello following command tooget hello mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="d2d6e-121">Olá [mgo](http://labix.org/mgo) driver (pronunciado como *mango*) é um [MongoDB](http://www.mongodb.org/) driver para Olá [ir idioma](http://golang.org/) que implementa um conjunto avançado e bem testado seleção de recursos em uma API muito simple de linguagens de Go padrão a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-121">hello [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for hello [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="d2d6e-122">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="d2d6e-122">Update your connection string</span></span>

<span data-ttu-id="d2d6e-123">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-123">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="d2d6e-124">Clique em **início rápido** Olá menu de navegação à esquerda e, em seguida, clique em **outros** informações da cadeia de conexão Olá tooview exigidas pelo Olá aplicativo Go.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-124">Click **Quick start** in hello left navigation menu, and then click **Other** tooview hello connection string information required by hello Go application.</span></span>

2. <span data-ttu-id="d2d6e-125">Em Goglang, abra o arquivo de main.go de saudação no diretório de GOROOT\CosmosDBSample hello e atualize Olá linhas seguintes do código usando informações da cadeia de conexão Olá da saudação portal do Azure, conforme mostrado no hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-125">In Goglang, open hello main.go file in hello GOROOT\CosmosDBSample directory and update hello following lines of code using hello connection string information from hello Azure portal as shown in hello following screenshot.</span></span> 

    <span data-ttu-id="d2d6e-126">nome do banco de dados de saudação é o prefixo de saudação do hello **Host** valor no painel de cadeia de caracteres de conexão de portal do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-126">hello Database name is hello prefix of hello **Host** value in hello Azure portal connection string pane.</span></span> <span data-ttu-id="d2d6e-127">Para a conta de Olá mostrada na imagem de saudação abaixo, o nome do banco de dados de saudação é treinador golang.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-127">For hello account shown in hello image below, hello Database name is golang-coach.</span></span>

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Início rápido de painel, outra guia de informações da cadeia de conexão Olá Olá mostrando portal do Azure](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="d2d6e-129">Salve o arquivo de main.go hello.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-129">Save hello main.go file.</span></span>

## <a name="review-hello-code"></a><span data-ttu-id="d2d6e-130">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="d2d6e-130">Review hello code</span></span>

<span data-ttu-id="d2d6e-131">Vamos fazer uma rápida revisão do que está acontecendo no arquivo de main.go hello.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-131">Let's make a quick review of what's happening in hello main.go file.</span></span> 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a><span data-ttu-id="d2d6e-132">Conectando Olá Go aplicativo tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d2d6e-132">Connecting hello Go app tooAzure Cosmos DB</span></span>

<span data-ttu-id="d2d6e-133">Banco de dados do Azure Cosmos dá suporte a saudação MongoDB SSL habilitado.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-133">Azure Cosmos DB supports hello SSL-enabled MongoDB.</span></span> <span data-ttu-id="d2d6e-134">tooconnect tooan MongoDB habilitado para SSL, você precisa Olá toodefine **DialServer** funcionar em [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)e fazer uso de saudação [tls. *Discagem* ](http://golang.org/pkg/crypto/tls#Dial) tooperform conexão de saudação de função.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-134">tooconnect tooan SSL-enabled MongoDB, you need toodefine hello **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of hello [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function tooperform hello connection.</span></span>

<span data-ttu-id="d2d6e-135">Olá Golang trecho de código a seguir se conecta a saudação Go aplicativo com a API do Azure Cosmos DB MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-135">hello following Golang code snippet connects hello Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="d2d6e-136">Olá *DialInfo* classe contém opções para estabelecer uma sessão com um cluster do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-136">hello *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="d2d6e-137">Olá **mgo. Dial()** método é usado quando não houver nenhuma conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-137">hello **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="d2d6e-138">Para uma conexão SSL, Olá **mgo. DialWithInfo()** método é necessário.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-138">For an SSL connection, hello **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="d2d6e-139">Uma instância do hello **{DialWIthInfo}** é objeto de sessão Olá toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-139">An instance of hello **DialWIthInfo{}** object is used toocreate hello session object.</span></span> <span data-ttu-id="d2d6e-140">Quando a sessão de saudação é estabelecida, você pode acessar a coleção de hello usando Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2d6e-140">Once hello session is established, you can access hello collection by using hello following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="d2d6e-141">Criar um documento</span><span class="sxs-lookup"><span data-stu-id="d2d6e-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="d2d6e-142">Consultar ou ler um documento</span><span class="sxs-lookup"><span data-stu-id="d2d6e-142">Query or read a document</span></span>

<span data-ttu-id="d2d6e-143">O Azure Cosmos DB dá suporte a consultas avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="d2d6e-144">Olá código exemplo a seguir mostra uma consulta que você pode executar em documentos de saudação em sua coleção.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-144">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="d2d6e-145">Atualizar um documento</span><span class="sxs-lookup"><span data-stu-id="d2d6e-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="d2d6e-146">Excluir um documento</span><span class="sxs-lookup"><span data-stu-id="d2d6e-146">Delete a document</span></span>

<span data-ttu-id="d2d6e-147">O Azure Cosmos DB dá suporte à exclusão de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a><span data-ttu-id="d2d6e-148">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d2d6e-148">Run hello app</span></span>

1. <span data-ttu-id="d2d6e-149">Em Goglang, certifique-se de que seu GOPATH (disponível em **arquivo**, **configurações**, **vá**, **GOPATH**) incluem local Olá no qual Olá gopkg foi instalado, que é USERPROFILE\go por padrão.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include hello location in which hello gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="d2d6e-150">Comentar as linhas de saudação excluir documento hello, linhas 91-96, para que você pode ver o documento hello após o aplicativo hello em execução.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-150">Comment out hello lines that delete hello document, lines 91-96, so that you can see hello document after running hello app.</span></span>
3. <span data-ttu-id="d2d6e-151">No Goglang, clique em **Executar**e em **Run 'Build main.go and run'**.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="d2d6e-152">aplicativo Hello termina e exibe a descrição Olá Olá documento criado no [criar um documento](#create-document).</span><span class="sxs-lookup"><span data-stu-id="d2d6e-152">hello app finishes and displays hello description of hello document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang mostrando a saída de saudação do aplicativo hello](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="d2d6e-154">Revisar o documento no Data Explorer</span><span class="sxs-lookup"><span data-stu-id="d2d6e-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="d2d6e-155">Volte toohello toosee portal do Azure seu documento no Explorador de dados.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-155">Go back toohello Azure portal toosee your document in Data Explorer.</span></span>

1. <span data-ttu-id="d2d6e-156">Clique em **Gerenciador de dados (visualização)** no menu de navegação à esquerda do hello, expanda **golang treinador**, **pacote**e, em seguida, clique em **documentos**.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-156">Click **Data Explorer (Preview)** in hello left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="d2d6e-157">Em Olá **documentos** , clique em Olá \_documento de saudação toodisplay id no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-157">In hello **Documents** tab, click hello \_id toodisplay hello document in hello right pane.</span></span> 

    ![Documento de saudação recém-criado do Gerenciador de dados mostrando](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="d2d6e-159">Você pode trabalhar com hello documento embutido e clique em **atualização** toosave-lo.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-159">You can then work with hello document inline and click **Update** toosave it.</span></span> <span data-ttu-id="d2d6e-160">Você também pode excluir o documento de saudação ou criar novos documentos ou consultas.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-160">You can also delete hello document, or create new documents or queries.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="d2d6e-161">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2d6e-161">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="d2d6e-162">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="d2d6e-162">Clean up resources</span></span>

<span data-ttu-id="d2d6e-163">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2d6e-163">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="d2d6e-164">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-164">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="d2d6e-165">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-165">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2d6e-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2d6e-166">Next steps</span></span>

<span data-ttu-id="d2d6e-167">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos e executar um aplicativo Golang usando Olá API para o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-167">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a Golang app using hello API for MongoDB.</span></span> <span data-ttu-id="d2d6e-168">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="d2d6e-168">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2d6e-169">Importe dados para o banco de dados do Azure Cosmos para Olá MongoDB API</span><span class="sxs-lookup"><span data-stu-id="d2d6e-169">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)
