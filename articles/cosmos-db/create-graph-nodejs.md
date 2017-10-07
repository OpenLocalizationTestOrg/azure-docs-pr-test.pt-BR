---
title: aaaBuild um aplicativo de Node.js do Azure Cosmos banco de dados usando a API do Graph | Microsoft Docs
description: "Apresenta um exemplo de código de Node. js que você pode usar tooconnect tooand consultar o banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="340bf-103">Azure Cosmos DB: Compilar um aplicativo Node.js usando a API do Graph</span><span class="sxs-lookup"><span data-stu-id="340bf-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="340bf-104">Banco de dados do Azure Cosmos é serviço de banco de dados de vários modelos de Olá globalmente distribuída da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="340bf-104">Azure Cosmos DB is hello globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="340bf-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="340bf-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="340bf-106">Este artigo de início rápido demonstra como toocreate um banco de dados do Azure Cosmos a conta para a API do Graph (visualização), o banco de dados e o gráfico usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="340bf-106">This quick-start article demonstrates how toocreate an Azure Cosmos DB account for Graph API (preview), database, and graph by using hello Azure portal.</span></span> <span data-ttu-id="340bf-107">Em seguida, compilar e executar um aplicativo de console usando Olá código-fonte aberto [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span><span class="sxs-lookup"><span data-stu-id="340bf-107">You then build and run a console app by using hello open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="340bf-108">módulo de npm Olá `gremlin-secure` é uma versão modificada do `gremlin` módulo, com suporte para SSL e SASL necessárias para conectar-se com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="340bf-108">hello npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="340bf-109">O código-fonte está disponível no [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="340bf-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="340bf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="340bf-110">Prerequisites</span></span>

<span data-ttu-id="340bf-111">Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="340bf-111">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="340bf-112">[Node.js](https://nodejs.org/en/) versão v0.10.29 ou posterior</span><span class="sxs-lookup"><span data-stu-id="340bf-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="340bf-113">Git</span><span class="sxs-lookup"><span data-stu-id="340bf-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="340bf-114">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="340bf-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="340bf-115">Adicionar um gráfico</span><span class="sxs-lookup"><span data-stu-id="340bf-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="340bf-116">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="340bf-116">Clone hello sample application</span></span>

<span data-ttu-id="340bf-117">Agora vamos aplicativo clone uma API do Graph do GitHub, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="340bf-117">Now let's clone a Graph API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="340bf-118">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="340bf-118">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="340bf-119">Abra uma janela de terminal de Git, como o Git Bash e altere (via `cd` comando) tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="340bf-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) tooa working directory.</span></span>  

2. <span data-ttu-id="340bf-120">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="340bf-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="340bf-121">Abra o arquivo de solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="340bf-121">Open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="340bf-122">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="340bf-122">Review hello code</span></span>

<span data-ttu-id="340bf-123">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="340bf-123">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="340bf-124">Olá abrir `app.js` arquivo e você encontrará Olá linhas de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="340bf-124">Open hello `app.js` file, and you'll find hello following lines of code.</span></span> 

* <span data-ttu-id="340bf-125">cliente de Gremlin Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="340bf-125">hello Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="340bf-126">Olá configurações estão todos em `config.js`, que podemos Editar Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="340bf-126">hello configurations are all in `config.js`, which we edit in hello following section.</span></span>

* <span data-ttu-id="340bf-127">Uma série de etapas de Gremlin são executados com hello `client.execute` método.</span><span class="sxs-lookup"><span data-stu-id="340bf-127">A series of Gremlin steps are executed with hello `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="340bf-128">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="340bf-128">Update your connection string</span></span>

1. <span data-ttu-id="340bf-129">Arquivo de config.js Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="340bf-129">Open hello config.js file.</span></span> 

2. <span data-ttu-id="340bf-130">Na config.js, preencha chave config.endpoint Olá Olá **Gremlin URI** valor da saudação **visão geral** página de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="340bf-130">In config.js, fill in hello config.endpoint key with hello **Gremlin URI** value from hello **Overview** page of hello Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="340bf-132">Se hello **Gremlin URI** valor estiver em branco, você pode gerar o valor de saudação do hello **chaves** página no portal de hello, usando Olá **URI** https:// de remoção e alteração de valor toographs de documentos.</span><span class="sxs-lookup"><span data-stu-id="340bf-132">If hello **Gremlin URI** value is blank, you can generate hello value from hello **Keys** page in hello portal, using hello **URI** value, removing https://, and changing documents toographs.</span></span>

   <span data-ttu-id="340bf-133">o ponto de extremidade do Hello Gremlin deve ser somente nome de host de saudação sem número de porta do protocolo de saudação, como `mygraphdb.graphs.azure.com` (não `https://mygraphdb.graphs.azure.com` ou `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="340bf-133">hello Gremlin endpoint must be only hello host name without hello protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="340bf-134">Na config.js, preencha o valor de config.primaryKey Olá com hello **chave primária** valor da saudação **chaves** página de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="340bf-134">In config.js, fill in hello config.primaryKey value in with hello **Primary Key** value from hello **Keys** page of hello Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Olá folha de chaves de portal do Azure](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="340bf-136">Insira o nome do banco de dados de saudação e nome do gráfico (contêiner) para valor de saudação do config.database e config.collection.</span><span class="sxs-lookup"><span data-stu-id="340bf-136">Enter hello database name, and graph (container) name for hello value of config.database and config.collection.</span></span> 

<span data-ttu-id="340bf-137">Aqui está um exemplo da aparência seu arquivo config.js concluído:</span><span class="sxs-lookup"><span data-stu-id="340bf-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a><span data-ttu-id="340bf-138">Execute o aplicativo de console Olá</span><span class="sxs-lookup"><span data-stu-id="340bf-138">Run hello console app</span></span>

1. <span data-ttu-id="340bf-139">Abra uma janela do terminal e alterar (por meio de `cd` comando) toohello o diretório de instalação para o arquivo Package. JSON de Olá que está incluído no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="340bf-139">Open a terminal window and change (via `cd` command) toohello installation directory for hello package.json file that's included in hello project.</span></span>  

2. <span data-ttu-id="340bf-140">Executar `npm install` tooinstall Olá necessário npm módulos, incluindo `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="340bf-140">Run `npm install` tooinstall hello required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="340bf-141">Executar `node app.js` em um terminal toostart seu aplicativo de nó.</span><span class="sxs-lookup"><span data-stu-id="340bf-141">Run `node app.js` in a terminal toostart your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="340bf-142">Procurar com o Data Explorer</span><span class="sxs-lookup"><span data-stu-id="340bf-142">Browse with Data Explorer</span></span>

<span data-ttu-id="340bf-143">Agora você pode voltar tooData Explorer no hello tooview portal do Azure, consultar, modificar e trabalhar com os novos dados de gráfico.</span><span class="sxs-lookup"><span data-stu-id="340bf-143">You can now go back tooData Explorer in hello Azure portal tooview, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="340bf-144">No Explorador de dados, o novo banco de dados de saudação aparece no hello **gráficos** painel.</span><span class="sxs-lookup"><span data-stu-id="340bf-144">In Data Explorer, hello new database appears in hello **Graphs** pane.</span></span> <span data-ttu-id="340bf-145">Expanda o banco de dados do hello, seguido por coleção Olá, e clique em **gráfico**.</span><span class="sxs-lookup"><span data-stu-id="340bf-145">Expand hello database, followed by hello collection, then click **Graph**.</span></span>

<span data-ttu-id="340bf-146">dados Olá gerados pelo aplicativo de exemplo hello são exibidos no painel de Avançar hello dentro Olá **gráfico** guia quando você clica em **Aplicar filtro**.</span><span class="sxs-lookup"><span data-stu-id="340bf-146">hello data generated by hello sample app is displayed in hello next pane within hello **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="340bf-147">Tente concluir `g.V()` com `.has('firstName', 'Thomas')` tootest filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="340bf-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` tootest hello filter.</span></span> <span data-ttu-id="340bf-148">Observe que o valor de saudação diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="340bf-148">Do note that hello value is case sensitive.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="340bf-149">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="340bf-149">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="340bf-150">Limpar seus recursos</span><span class="sxs-lookup"><span data-stu-id="340bf-150">Clean up your resources</span></span>

<span data-ttu-id="340bf-151">Se você não planeja toocontinue usando este aplicativo, exclua todos os recursos que você criou neste artigo, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="340bf-151">If you do not plan toocontinue using this app, delete all resources that you created in this article by doing hello following:</span></span> 

1. <span data-ttu-id="340bf-152">No hello portal do Azure, no menu de navegação à esquerda do hello, clique em **grupos de recursos**e clique em nome de saudação do recurso de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="340bf-152">In hello Azure portal, on hello left navigation menu, click **Resource groups**, and then click hello name of hello resource that you created.</span></span> 
2. <span data-ttu-id="340bf-153">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toobe excluído e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="340bf-153">On your resource group page, click **Delete**, type hello name of hello resource toobe deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="340bf-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="340bf-154">Next steps</span></span>

<span data-ttu-id="340bf-155">Neste artigo, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie um gráfico usando o Explorador de dados e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="340bf-155">In this article, you've learned how toocreate an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="340bf-156">Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin.</span><span class="sxs-lookup"><span data-stu-id="340bf-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="340bf-157">Consultar usando o Gremlin</span><span class="sxs-lookup"><span data-stu-id="340bf-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
