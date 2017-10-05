---
title: 'BD Cosmos do Azure: compilar um aplicativo de console da API do MongoDB com Golang e o portal do Azure | Microsoft Docs'
description: "Apresenta um exemplo de código Golang que pode ser usado para conectar e consultar o BD Cosmos do Azure"
services: cosmos-db
author: Durgaprasad-Budhwani
manager: jhubbard
editor: mimig1
ms.service: cosmos-db
ms.topic: hero-article
ms.date: 07/21/2017
ms.author: mimig
ms.openlocfilehash: 9461a5d86b321fd02167379ba8751d44a861ebc2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-the-azure-portal"></a><span data-ttu-id="295b1-103">BD Cosmos do Azure: compilar um aplicativo de console da API do MongoDB com Golang e o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="295b1-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal</span></span>

<span data-ttu-id="295b1-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="295b1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="295b1-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="295b1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="295b1-106">Este início rápido demonstra como usar um aplicativo [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) existente escrito em [Golang](https://golang.org/) e como conectá-lo ao banco de dados do BD Cosmos do Azure, que dá suporte a conexões de cliente do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="295b1-106">This quick-start demonstrates how to use an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it to your Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="295b1-107">Em outras palavras, o aplicativo Golang só sabe que está se conectando a um banco de dados usando as APIs do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="295b1-107">In other words, your Golang application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="295b1-108">Está claro para o aplicativo que os dados estão armazenados no BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="295b1-108">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="295b1-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="295b1-109">Prerequisites</span></span>

- <span data-ttu-id="295b1-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="295b1-110">An Azure subscription.</span></span> <span data-ttu-id="295b1-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="295b1-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="295b1-112">[Go](https://golang.org/dl/) e um conhecimento básico sobre a linguagem [Go](https://golang.org/).</span><span class="sxs-lookup"><span data-stu-id="295b1-112">[Go](https://golang.org/dl/) and a basic knowledge of the [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="295b1-113">Um IDE — [Gogland](https://www.jetbrains.com/go/) da Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) ou [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="295b1-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="295b1-114">Neste tutorial, estou usando Goglang.</span><span class="sxs-lookup"><span data-stu-id="295b1-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="295b1-115">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="295b1-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="295b1-116">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="295b1-116">Clone the sample application</span></span>

<span data-ttu-id="295b1-117">Clone o aplicativo de exemplo e instale os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="295b1-117">Clone the sample application and install the required packages.</span></span>

1. <span data-ttu-id="295b1-118">Crie uma pasta chamada CosmosDBSample dentro da pasta GOROOT\src, que é C:\Go\ por padrão.</span><span class="sxs-lookup"><span data-stu-id="295b1-118">Create a folder named CosmosDBSample inside the GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="295b1-119">Execute o comando a seguir usando uma janela do terminal git como git bash para clonar o repositório de exemplo na pasta CosmosDBSample.</span><span class="sxs-lookup"><span data-stu-id="295b1-119">Run the following command using a git terminal window such as git bash to clone the sample repository into the CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="295b1-120">Execute o comando a seguir para obter o pacote mgo.</span><span class="sxs-lookup"><span data-stu-id="295b1-120">Run the following command to get the mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="295b1-121">O driver [mgo](http://labix.org/mgo) (pronuncia-se *mango*) é um driver [MongoDB](http://www.mongodb.org/) para a [linguagem Go](http://golang.org/) que implementa uma seleção bem testada e avançada de recursos em uma API muito simples seguindo expressões Go padrão.</span><span class="sxs-lookup"><span data-stu-id="295b1-121">The [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for the [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="295b1-122">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="295b1-122">Update your connection string</span></span>

<span data-ttu-id="295b1-123">Agora, volte ao portal do Azure para obter informações sobre a cadeia de conexão e copiá-las para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="295b1-123">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="295b1-124">Clique em **Início rápido** no menu de navegação à esquerda e clique em **Outros** para exibir as informações de cadeia de conexão exigidas pelo aplicativo Go.</span><span class="sxs-lookup"><span data-stu-id="295b1-124">Click **Quick start** in the left navigation menu, and then click **Other** to view the connection string information required by the Go application.</span></span>

2. <span data-ttu-id="295b1-125">No Goglang, abra o arquivo main.go no diretório GOROOT\CosmosDBSample e atualize as linhas de código a seguir usando as informações de cadeia de conexão do portal do Azure, conforme mostrado na captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="295b1-125">In Goglang, open the main.go file in the GOROOT\CosmosDBSample directory and update the following lines of code using the connection string information from the Azure portal as shown in the following screenshot.</span></span> 

    <span data-ttu-id="295b1-126">O Nome do banco de dados é o prefixo do valor **Host** no painel de cadeia de conexão de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="295b1-126">The Database name is the prefix of the **Host** value in the Azure portal connection string pane.</span></span> <span data-ttu-id="295b1-127">Para a conta mostrada na imagem abaixo, o nome do banco de dados é golang-coach.</span><span class="sxs-lookup"><span data-stu-id="295b1-127">For the account shown in the image below, the Database name is golang-coach.</span></span>

    ```go
    Database: "The prefix of the Host value in the Azure portal",
    Username: "The Username in the Azure portal",
    Password: "The Password in the Azure portal",
    ```

    ![Painel Início rápido, guia Outros no portal do Azure mostrando as informações de cadeia de conexão](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="295b1-129">Salve o arquivo main.go.</span><span class="sxs-lookup"><span data-stu-id="295b1-129">Save the main.go file.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="295b1-130">Examine o código</span><span class="sxs-lookup"><span data-stu-id="295b1-130">Review the code</span></span>

<span data-ttu-id="295b1-131">Façamos uma rápida revisão do que está acontecendo no arquivo main.go.</span><span class="sxs-lookup"><span data-stu-id="295b1-131">Let's make a quick review of what's happening in the main.go file.</span></span> 

### <a name="connecting-the-go-app-to-azure-cosmos-db"></a><span data-ttu-id="295b1-132">Conectando o aplicativo Go para o BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="295b1-132">Connecting the Go app to Azure Cosmos DB</span></span>

<span data-ttu-id="295b1-133">O BD Cosmos do Azure dá suporte ao MongoDB habilitado para SSL.</span><span class="sxs-lookup"><span data-stu-id="295b1-133">Azure Cosmos DB supports the SSL-enabled MongoDB.</span></span> <span data-ttu-id="295b1-134">Para se conectar a um MongoDB habilitado para SSL, você precisa definir a função **DialServer** em [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo)e usar a função [tls.*Dial* ](http://golang.org/pkg/crypto/tls#Dial) para realizar a conexão.</span><span class="sxs-lookup"><span data-stu-id="295b1-134">To connect to an SSL-enabled MongoDB, you need to define the **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of the [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function to perform the connection.</span></span>

<span data-ttu-id="295b1-135">O trecho de código Golang a seguir se conecta ao aplicativo Go com a API MongoDB do Cosmos DB do Azure.</span><span class="sxs-lookup"><span data-stu-id="295b1-135">The following Golang code snippet connects the Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="295b1-136">A classe *DialInfo* contém opções para estabelecer uma sessão com um cluster do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="295b1-136">The *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

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
// to our Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect to mongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes the session safety mode.
// If the safe parameter is nil, the session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. The unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="295b1-137">O método **mgo.Dial()** é usado quando não há nenhuma conexão SSL.</span><span class="sxs-lookup"><span data-stu-id="295b1-137">The **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="295b1-138">Para uma conexão SSL, o método **mgo.DialWithInfo()** é necessário.</span><span class="sxs-lookup"><span data-stu-id="295b1-138">For an SSL connection, the **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="295b1-139">Uma instância do objeto **DialWIthInfo{}** é usada para criar o objeto de sessão.</span><span class="sxs-lookup"><span data-stu-id="295b1-139">An instance of the **DialWIthInfo{}** object is used to create the session object.</span></span> <span data-ttu-id="295b1-140">Quando a sessão é estabelecida, você pode acessar a coleção usando o trecho de código abaixo:</span><span class="sxs-lookup"><span data-stu-id="295b1-140">Once the session is established, you can access the collection by using the following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="295b1-141">Criar um documento</span><span class="sxs-lookup"><span data-stu-id="295b1-141">Create a document</span></span>

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

### <a name="query-or-read-a-document"></a><span data-ttu-id="295b1-142">Consultar ou ler um documento</span><span class="sxs-lookup"><span data-stu-id="295b1-142">Query or read a document</span></span>

<span data-ttu-id="295b1-143">O Azure Cosmos DB dá suporte a consultas avançadas de documentos JSON armazenados em cada coleção.</span><span class="sxs-lookup"><span data-stu-id="295b1-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="295b1-144">O código de exemplo a seguir mostra uma consulta que pode ser executada em documentos em sua coleção.</span><span class="sxs-lookup"><span data-stu-id="295b1-144">The following sample code shows a query that you can run against the documents in your collection.</span></span>

```go
// Get a Document from the collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="295b1-145">Atualizar um documento</span><span class="sxs-lookup"><span data-stu-id="295b1-145">Update a document</span></span>

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

### <a name="delete-a-document"></a><span data-ttu-id="295b1-146">Excluir um documento</span><span class="sxs-lookup"><span data-stu-id="295b1-146">Delete a document</span></span>

<span data-ttu-id="295b1-147">O Azure Cosmos DB dá suporte à exclusão de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="295b1-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-the-app"></a><span data-ttu-id="295b1-148">Execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="295b1-148">Run the app</span></span>

1. <span data-ttu-id="295b1-149">Em Goglang, verifique se seu GOPATH (disponível em **Arquivo**, **Configurações**, **Go**, **GOPATH**) inclui o local no qual o gopkg foi instalado, que é PERFILDOUSUÁRIO/go por padrão.</span><span class="sxs-lookup"><span data-stu-id="295b1-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include the location in which the gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="295b1-150">Comente as linhas que excluem o documento, linhas 91 a 96, para que você possa ver o documento depois de executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="295b1-150">Comment out the lines that delete the document, lines 91-96, so that you can see the document after running the app.</span></span>
3. <span data-ttu-id="295b1-151">No Goglang, clique em **Executar**e em **Run 'Build main.go and run'**.</span><span class="sxs-lookup"><span data-stu-id="295b1-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="295b1-152">O aplicativo termina e exibe a descrição do documento criado em [Criar um documento](#create-document).</span><span class="sxs-lookup"><span data-stu-id="295b1-152">The app finishes and displays the description of the document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang mostrando a saída do aplicativo](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="295b1-154">Revisar o documento no Data Explorer</span><span class="sxs-lookup"><span data-stu-id="295b1-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="295b1-155">Volte para o portal do Azure a fim de ver o documento no Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="295b1-155">Go back to the Azure portal to see your document in Data Explorer.</span></span>

1. <span data-ttu-id="295b1-156">Clique em **Data Explorer (Versão prévia)** no menu de navegação à esquerda, expanda **golang-coach**, **pacote**e clique em **Documentos**.</span><span class="sxs-lookup"><span data-stu-id="295b1-156">Click **Data Explorer (Preview)** in the left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="295b1-157">Na guia **Documentos** , clique na \_id para exibir o documento no painel direito.</span><span class="sxs-lookup"><span data-stu-id="295b1-157">In the **Documents** tab, click the \_id to display the document in the right pane.</span></span> 

    ![Data Explorer mostrando o documento recém-criado](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="295b1-159">Você pode trabalhar com o documento em linha e clicar em **Atualizar** para salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="295b1-159">You can then work with the document inline and click **Update** to save it.</span></span> <span data-ttu-id="295b1-160">Você também pode excluir o documento ou criar novos documentos ou consultas.</span><span class="sxs-lookup"><span data-stu-id="295b1-160">You can also delete the document, or create new documents or queries.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="295b1-161">Examinar SLAs no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="295b1-161">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="295b1-162">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="295b1-162">Clean up resources</span></span>

<span data-ttu-id="295b1-163">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="295b1-163">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="295b1-164">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="295b1-164">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="295b1-165">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="295b1-165">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="295b1-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="295b1-166">Next steps</span></span>

<span data-ttu-id="295b1-167">Neste início rápido, você aprendeu como criar uma conta do BD Cosmos do Azure e executar um aplicativo Golang usando a API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="295b1-167">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Golang app using the API for MongoDB.</span></span> <span data-ttu-id="295b1-168">Agora, é possível importar outros dados para sua conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="295b1-168">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="295b1-169">Importar dados no BD Cosmos do Azure para a API do MongoDB</span><span class="sxs-lookup"><span data-stu-id="295b1-169">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)
