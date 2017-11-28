---
title: "aaaCreate um banco de dados do gráfico de banco de dados do Azure Cosmos com Java | Microsoft Docs"
description: "Apresenta um Java código de exemplo que você pode usar dados do gráfico tooconnect tooand consulta no banco de dados do Cosmos do Azure usando Gremlin."
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
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="0279a-103">Banco de dados do Azure do Cosmos: Criar um banco de dados do gráfico usando Java e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0279a-103">Azure Cosmos DB: Create a graph database using Java and hello Azure portal</span></span>

<span data-ttu-id="0279a-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0279a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0279a-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0279a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="0279a-106">Este guia de início rápido cria um gráfico de banco de dados usando Olá ferramentas portais do Azure para o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0279a-106">This quickstart creates a graph database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="0279a-107">Este guia de início rápido também mostra como tooquickly criar um aplicativo de console de Java usando um banco de dados do gráfico usando Olá OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span><span class="sxs-lookup"><span data-stu-id="0279a-107">This quickstart also shows you how tooquickly create a Java console app using a graph database using hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="0279a-108">instruções Olá este guia de início rápido podem ser seguidas em qualquer sistema operacional que é capaz de executar Java.</span><span class="sxs-lookup"><span data-stu-id="0279a-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="0279a-109">Este guia de início rápido familiariza você com a criação e modificação de recursos de gráfico em Olá da interface do usuário ou programaticamente, o que for sua preferência.</span><span class="sxs-lookup"><span data-stu-id="0279a-109">This quickstart familiarizes you with creating and modifying graph resources in either hello UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0279a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0279a-110">Prerequisites</span></span>

* [<span data-ttu-id="0279a-111">Java Development Kit (JDK) 1.7 +</span><span class="sxs-lookup"><span data-stu-id="0279a-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="0279a-112">No Ubuntu, execute `apt-get install default-jdk` tooinstall Olá JDK.</span><span class="sxs-lookup"><span data-stu-id="0279a-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="0279a-113">Ser toohello tooset se Olá JAVA_HOME ambiente variável toopoint pasta onde Olá JDK está instalado.</span><span class="sxs-lookup"><span data-stu-id="0279a-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="0279a-114">[Baixar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) um armazenamento binário [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="0279a-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="0279a-115">No Ubuntu, você pode executar `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="0279a-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="0279a-116">Git</span><span class="sxs-lookup"><span data-stu-id="0279a-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="0279a-117">No Ubuntu, você pode executar `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="0279a-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="0279a-118">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="0279a-118">Create a database account</span></span>

<span data-ttu-id="0279a-119">Antes de criar um banco de dados do gráfico, você precisa toocreate uma conta de banco de dados Gremlin (gráfico) com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0279a-119">Before you can create a graph database, you need toocreate a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="0279a-120">Adicionar um gráfico</span><span class="sxs-lookup"><span data-stu-id="0279a-120">Add a graph</span></span>

<span data-ttu-id="0279a-121">Agora você pode usar a ferramenta de Gerenciador de dados de saudação em Olá toocreate portal do Azure um banco de dados do gráfico.</span><span class="sxs-lookup"><span data-stu-id="0279a-121">You can now use hello Data Explorer tool in hello Azure portal toocreate a graph database.</span></span> 

1. <span data-ttu-id="0279a-122">No hello portal do Azure, no menu de navegação à esquerda do hello, clique em **Gerenciador de dados (visualização)**.</span><span class="sxs-lookup"><span data-stu-id="0279a-122">In hello Azure portal, in hello left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="0279a-123">Em Olá **Gerenciador de dados (visualização)** folha, clique em **novo gráfico**, em seguida, preencha a página hello usando Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="0279a-123">In hello **Data Explorer (Preview)** blade, click **New Graph**, then fill in hello page using hello following information:</span></span>

    ![Gerenciador de dados no hello portal do Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="0279a-125">Configuração</span><span class="sxs-lookup"><span data-stu-id="0279a-125">Setting</span></span>|<span data-ttu-id="0279a-126">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="0279a-126">Suggested value</span></span>|<span data-ttu-id="0279a-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="0279a-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="0279a-128">ID do banco de dados</span><span class="sxs-lookup"><span data-stu-id="0279a-128">Database ID</span></span>|<span data-ttu-id="0279a-129">banco de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="0279a-129">sample-database</span></span>|<span data-ttu-id="0279a-130">ID de saudação do novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0279a-130">hello ID for your new database.</span></span> <span data-ttu-id="0279a-131">Os nomes de banco de dados devem ter entre um e 255 caracteres e não podem conter `/ \ # ?` nem espaços à direita.</span><span class="sxs-lookup"><span data-stu-id="0279a-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="0279a-132">ID do Gráfico</span><span class="sxs-lookup"><span data-stu-id="0279a-132">Graph ID</span></span>|<span data-ttu-id="0279a-133">gráfico de exemplo</span><span class="sxs-lookup"><span data-stu-id="0279a-133">sample-graph</span></span>|<span data-ttu-id="0279a-134">ID de saudação para seu novo gráfico.</span><span class="sxs-lookup"><span data-stu-id="0279a-134">hello ID for your new graph.</span></span> <span data-ttu-id="0279a-135">Nomes de gráfico tem Olá mesmo caractere requisitos como ids de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0279a-135">Graph names have hello same character requirements as database ids.</span></span>
    <span data-ttu-id="0279a-136">Capacidade de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="0279a-136">Storage Capacity</span></span>| <span data-ttu-id="0279a-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="0279a-137">10 GB</span></span>|<span data-ttu-id="0279a-138">Deixe o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-138">Leave hello default value.</span></span> <span data-ttu-id="0279a-139">Isso é a capacidade de armazenamento de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-139">This is hello storage capacity of hello database.</span></span>
    <span data-ttu-id="0279a-140">Taxa de transferência</span><span class="sxs-lookup"><span data-stu-id="0279a-140">Throughput</span></span>|<span data-ttu-id="0279a-141">400 RUs</span><span class="sxs-lookup"><span data-stu-id="0279a-141">400 RUs</span></span>|<span data-ttu-id="0279a-142">Deixe o valor padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-142">Leave hello default value.</span></span> <span data-ttu-id="0279a-143">Você pode dimensionar a taxa de transferência hello mais tarde se você quiser tooreduce latência.</span><span class="sxs-lookup"><span data-stu-id="0279a-143">You can scale up hello throughput later if you want tooreduce latency.</span></span>
    <span data-ttu-id="0279a-144">Chave de partição</span><span class="sxs-lookup"><span data-stu-id="0279a-144">Partition key</span></span>|<span data-ttu-id="0279a-145">Deixar em branco</span><span class="sxs-lookup"><span data-stu-id="0279a-145">Leave blank</span></span>|<span data-ttu-id="0279a-146">Para finalidade Olá este guia de início rápido, chave de partição Olá deixe em branco.</span><span class="sxs-lookup"><span data-stu-id="0279a-146">For hello purpose of this quickstart, leave hello partition key blank.</span></span>

3. <span data-ttu-id="0279a-147">Depois de preencher o formulário Olá, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0279a-147">Once hello form is filled out, click **OK**.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="0279a-148">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="0279a-148">Clone hello sample application</span></span>

<span data-ttu-id="0279a-149">Agora vamos, clonar um aplicativo gráfico do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="0279a-149">Now let's clone a graph app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="0279a-150">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="0279a-150">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="0279a-151">Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0279a-151">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="0279a-152">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="0279a-152">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="0279a-153">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="0279a-153">Review hello code</span></span>

<span data-ttu-id="0279a-154">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0279a-154">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="0279a-155">Olá abrir `Program.java` arquivo da pasta de \src\GetStarted hello e encontrar essas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="0279a-155">Open hello `Program.java` file from hello \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="0279a-156">Olá Gremlin `Client` é inicializada de configuração de saudação no `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="0279a-156">hello Gremlin `Client` is initialized from hello configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="0279a-157">Uma série de etapas de Gremlin são executadas usando Olá `client.submit` método.</span><span class="sxs-lookup"><span data-stu-id="0279a-157">A series of Gremlin steps are executed using hello `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="0279a-158">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="0279a-158">Update your connection string</span></span>

1. <span data-ttu-id="0279a-159">Arquivo de src/remote.yaml Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="0279a-159">Open hello src/remote.yaml file.</span></span> 

3. <span data-ttu-id="0279a-160">Preencha o *hosts*, *username*, e *senha* valores no arquivo de src/remote.yaml hello.</span><span class="sxs-lookup"><span data-stu-id="0279a-160">Fill in your *hosts*, *username*, and *password* values in hello src/remote.yaml file.</span></span> <span data-ttu-id="0279a-161">rest Olá das configurações de saudação não é necessário toobe alterado.</span><span class="sxs-lookup"><span data-stu-id="0279a-161">hello rest of hello settings do not need toobe changed.</span></span>

    <span data-ttu-id="0279a-162">Configuração</span><span class="sxs-lookup"><span data-stu-id="0279a-162">Setting</span></span>|<span data-ttu-id="0279a-163">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="0279a-163">Suggested value</span></span>|<span data-ttu-id="0279a-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="0279a-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="0279a-165">Hosts</span><span class="sxs-lookup"><span data-stu-id="0279a-165">Hosts</span></span>|<span data-ttu-id="0279a-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="0279a-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="0279a-167">Consulte a captura de tela de saudação após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="0279a-167">See hello screenshot following this table.</span></span> <span data-ttu-id="0279a-168">Esse valor é Olá Gremlin URI na página de visão geral de saudação do hello portal do Azure, entre colchetes, com hello à direita: 443 / removido.</span><span class="sxs-lookup"><span data-stu-id="0279a-168">This value is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="0279a-169">Esse valor também pode ser recuperado do guia de chaves hello, usando o valor URI Olá removendo https://, alterando toographs documentos e remoção de saudação à direita: 443 /.</span><span class="sxs-lookup"><span data-stu-id="0279a-169">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="0279a-170">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0279a-170">Username</span></span>|<span data-ttu-id="0279a-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="0279a-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="0279a-172">Olá recursos do formulário de saudação `/dbs/<db>/colls/<coll>` onde `<db>` é o nome do banco de dados existente e `<coll>` é o nome de coleção existente.</span><span class="sxs-lookup"><span data-stu-id="0279a-172">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="0279a-173">Senha</span><span class="sxs-lookup"><span data-stu-id="0279a-173">Password</span></span>|<span data-ttu-id="0279a-174">*Sua chave mestra principal*</span><span class="sxs-lookup"><span data-stu-id="0279a-174">*Your primary master key*</span></span>|<span data-ttu-id="0279a-175">Consulte a captura de tela segundo Olá após esta tabela.</span><span class="sxs-lookup"><span data-stu-id="0279a-175">See hello second screenshot following this table.</span></span> <span data-ttu-id="0279a-176">Esse valor é a chave primária, o que você pode recuperar da página de chaves de saudação do hello portal do Azure, na caixa de chave primária de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-176">This value is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="0279a-177">Copie o valor de saudação usando o botão de cópia de Olá Olá direita da caixa de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-177">Copy hello value using hello copy button on hello right side of hello box.</span></span>

    <span data-ttu-id="0279a-178">Valor de Hosts hello, copie Olá **Gremlin URI** valor da saudação **visão geral** página.</span><span class="sxs-lookup"><span data-stu-id="0279a-178">For hello Hosts value, copy hello **Gremlin URI** value from hello **Overview** page.</span></span> <span data-ttu-id="0279a-179">Se ela estiver vazia, consulte as instruções de saudação em linha Hosts Olá Olá anterior tabela sobre a criação de saudação Gremlin URI da folha de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-179">If it's empty, see hello instructions in hello Hosts row in hello preceding table about creating hello Gremlin URI from hello Keys blade.</span></span>
<span data-ttu-id="0279a-180">![Exibir e copiar valor de URI Gremlin Olá página de visão geral de saudação do hello portal do Azure](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="0279a-180">![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="0279a-181">Olá valor da senha, copiar Olá **chave primária** de saudação **chaves** folha: ![exibir e copiar a chave primária na Olá portal do Azure, chaves de página](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="0279a-181">For hello Password value, copy hello **Primary key** from hello **Keys** blade: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-hello-console-app"></a><span data-ttu-id="0279a-182">Execute o aplicativo de console Olá</span><span class="sxs-lookup"><span data-stu-id="0279a-182">Run hello console app</span></span>

1. <span data-ttu-id="0279a-183">Na janela do terminal Olá git, `cd` pasta azure-cosmos-db-graph-java-getting-started toohello.</span><span class="sxs-lookup"><span data-stu-id="0279a-183">In hello git terminal window, `cd` toohello azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="0279a-184">Na janela do terminal Olá git, digite `mvn package` tooinstall Olá necessário pacotes Java.</span><span class="sxs-lookup"><span data-stu-id="0279a-184">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="0279a-185">Na janela do terminal Olá git, execute `mvn exec:java -D exec.mainClass=GetStarted.Program` no hello janela do terminal toostart seu aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="0279a-185">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

<span data-ttu-id="0279a-186">janela do terminal Olá exibe vértices hello está sendo adicionados toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="0279a-186">hello terminal window displays hello vertices being added toohello graph.</span></span> <span data-ttu-id="0279a-187">Após a conclusão do programa hello, alterne back toohello portal do Azure no seu navegador da internet.</span><span class="sxs-lookup"><span data-stu-id="0279a-187">Once hello program completes, switch back toohello Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="0279a-188">Revisar e adicionar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="0279a-188">Review and add sample data</span></span>

<span data-ttu-id="0279a-189">Agora você pode voltar tooData Explorer e consulte vértices Olá adicionado toohello gráfico e adicionar pontos de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="0279a-189">You can now go back tooData Explorer and see hello vertices added toohello graph, and add additional data points.</span></span>

1. <span data-ttu-id="0279a-190">No Explorador de dados, expanda Olá **banco de dados de exemplo**/**exemplo de gráfico**, clique em **gráfico**e, em seguida, clique em **Aplicar filtro**.</span><span class="sxs-lookup"><span data-stu-id="0279a-190">In Data Explorer, expand hello **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Criar novos documentos no Explorador de dados no hello portal do Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="0279a-192">Em Olá **resultados** lista, observe a saudação novos usuários adicionados toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="0279a-192">In hello **Results** list, notice hello new users added toohello graph.</span></span> <span data-ttu-id="0279a-193">Selecione **ben** e observe que ele se conectou toorobin.</span><span class="sxs-lookup"><span data-stu-id="0279a-193">Select **ben** and notice that he's connected toorobin.</span></span> <span data-ttu-id="0279a-194">Mover os vértices Olá no Gerenciador de gráficos hello, ampliar e reduzir e expandir Olá tamanho da superfície do hello graph explorer.</span><span class="sxs-lookup"><span data-stu-id="0279a-194">You can move hello vertices around on hello graph explorer, zoom in and out, and expand hello size of hello graph explorer surface.</span></span> 

   ![Novo vértices no gráfico de saudação no Explorador de dados em Olá portal do Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="0279a-196">Vamos adicionar alguns novo gráfico de usuários toohello usando Olá Explorador de dados.</span><span class="sxs-lookup"><span data-stu-id="0279a-196">Let's add a few new users toohello graph using hello Data Explorer.</span></span> <span data-ttu-id="0279a-197">Clique em Olá **novo vértice** gráfico do botão tooadd dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="0279a-197">Click hello **New Vertex** button tooadd data tooyour graph.</span></span>

   ![Criar novos documentos no Explorador de dados no hello portal do Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="0279a-199">Digite um rótulo de *pessoa* , em seguida, digite Olá seguir as chaves e valores toocreate Olá primeiro vértice no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-199">Enter a label of *person* then enter hello following keys and values toocreate hello first vertex in hello graph.</span></span> <span data-ttu-id="0279a-200">Observe que você pode criar propriedades exclusivas para cada pessoa no gráfico.</span><span class="sxs-lookup"><span data-stu-id="0279a-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="0279a-201">Chave de id de saudação só é necessária.</span><span class="sxs-lookup"><span data-stu-id="0279a-201">Only hello id key is required.</span></span>

    <span data-ttu-id="0279a-202">chave</span><span class="sxs-lookup"><span data-stu-id="0279a-202">key</span></span>|<span data-ttu-id="0279a-203">valor</span><span class="sxs-lookup"><span data-stu-id="0279a-203">value</span></span>|<span data-ttu-id="0279a-204">Observações</span><span class="sxs-lookup"><span data-stu-id="0279a-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="0279a-205">ID</span><span class="sxs-lookup"><span data-stu-id="0279a-205">id</span></span>|<span data-ttu-id="0279a-206">ashley</span><span class="sxs-lookup"><span data-stu-id="0279a-206">ashley</span></span>|<span data-ttu-id="0279a-207">Identificador exclusivo do Hello vértice hello.</span><span class="sxs-lookup"><span data-stu-id="0279a-207">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="0279a-208">Se você não especificar uma ID, ela será gerada para você.</span><span class="sxs-lookup"><span data-stu-id="0279a-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="0279a-209">gender</span><span class="sxs-lookup"><span data-stu-id="0279a-209">gender</span></span>|<span data-ttu-id="0279a-210">feminino</span><span class="sxs-lookup"><span data-stu-id="0279a-210">female</span></span>| 
    <span data-ttu-id="0279a-211">técnico</span><span class="sxs-lookup"><span data-stu-id="0279a-211">tech</span></span> | <span data-ttu-id="0279a-212">java</span><span class="sxs-lookup"><span data-stu-id="0279a-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="0279a-213">Neste início rápido, criamos uma coleção não particionada.</span><span class="sxs-lookup"><span data-stu-id="0279a-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="0279a-214">No entanto, se você criar uma coleção particionada com a especificação de uma chave de partição durante a criação de coleção de saudação, em seguida, você precisa tooinclude Olá partição chave como uma chave em cada novo vértice.</span><span class="sxs-lookup"><span data-stu-id="0279a-214">However, if you create a partitioned collection by specifying a partition key during hello collection creation, then you need tooinclude hello partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="0279a-215">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0279a-215">Click **OK**.</span></span> <span data-ttu-id="0279a-216">Talvez seja necessário tooexpand toosee sua tela **Okey** na parte inferior de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="0279a-216">You may need tooexpand your screen toosee **OK** on hello bottom of hello screen.</span></span>

6. <span data-ttu-id="0279a-217">Clique em **Novo Vértice** novamente e acrescente um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="0279a-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="0279a-218">Digite um rótulo de *pessoa* digite Olá seguinte chaves e valores:</span><span class="sxs-lookup"><span data-stu-id="0279a-218">Enter a label of *person* then enter hello following keys and values:</span></span>

    <span data-ttu-id="0279a-219">chave</span><span class="sxs-lookup"><span data-stu-id="0279a-219">key</span></span>|<span data-ttu-id="0279a-220">valor</span><span class="sxs-lookup"><span data-stu-id="0279a-220">value</span></span>|<span data-ttu-id="0279a-221">Observações</span><span class="sxs-lookup"><span data-stu-id="0279a-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="0279a-222">ID</span><span class="sxs-lookup"><span data-stu-id="0279a-222">id</span></span>|<span data-ttu-id="0279a-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="0279a-223">rakesh</span></span>|<span data-ttu-id="0279a-224">Identificador exclusivo do Hello vértice hello.</span><span class="sxs-lookup"><span data-stu-id="0279a-224">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="0279a-225">Se você não especificar uma ID, ela será gerada para você.</span><span class="sxs-lookup"><span data-stu-id="0279a-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="0279a-226">gender</span><span class="sxs-lookup"><span data-stu-id="0279a-226">gender</span></span>|<span data-ttu-id="0279a-227">masculino</span><span class="sxs-lookup"><span data-stu-id="0279a-227">male</span></span>| 
    <span data-ttu-id="0279a-228">escola</span><span class="sxs-lookup"><span data-stu-id="0279a-228">school</span></span>|<span data-ttu-id="0279a-229">MIT</span><span class="sxs-lookup"><span data-stu-id="0279a-229">MIT</span></span>| 

7. <span data-ttu-id="0279a-230">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0279a-230">Click **OK**.</span></span> 

8. <span data-ttu-id="0279a-231">Clique em **Aplicar filtro** com padrão de saudação `g.V()` filtro.</span><span class="sxs-lookup"><span data-stu-id="0279a-231">Click **Apply Filter** with hello default `g.V()` filter.</span></span> <span data-ttu-id="0279a-232">Todos os usuários Olá mostram em Olá **resultados** lista.</span><span class="sxs-lookup"><span data-stu-id="0279a-232">All of hello users now show in hello **Results** list.</span></span> <span data-ttu-id="0279a-233">Conforme você adiciona mais dados, você pode usar filtros toolimit seus resultados.</span><span class="sxs-lookup"><span data-stu-id="0279a-233">As you add more data, you can use filters toolimit your results.</span></span> <span data-ttu-id="0279a-234">Por padrão, o Gerenciador de dados usa `g.V()` tooretrieve todos os vértices em um gráfico, mas você podem alterar esse tooa diferente [consulta graph](tutorial-query-graph.md), como `g.V().count()`, tooreturn uma contagem de todos os vértices de saudação no gráfico de saudação no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0279a-234">By default, Data Explorer uses `g.V()` tooretrieve all vertices in a graph, but you can change that tooa different [graph query](tutorial-query-graph.md), such as `g.V().count()`, tooreturn a count of all hello vertices in hello graph in JSON format.</span></span>

9. <span data-ttu-id="0279a-235">Agora, podemos conectar rakesh e ashley.</span><span class="sxs-lookup"><span data-stu-id="0279a-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="0279a-236">Certifique-se de **Carlos** em selecionado na Olá **resultados** lista, clique botão de edição Olá Avançar muito**destinos** no lado inferior direito.</span><span class="sxs-lookup"><span data-stu-id="0279a-236">Ensure **ashley** in selected in hello **Results** list, then click hello edit button next too**Targets** on lower right side.</span></span> <span data-ttu-id="0279a-237">Talvez seja necessário toowiden Olá de toosee sua janela **propriedades** área.</span><span class="sxs-lookup"><span data-stu-id="0279a-237">You may need toowiden your window toosee hello **Properties** area.</span></span>

   ![Alterar o destino de saudação de um vértice em um gráfico](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="0279a-239">Em Olá **destino** caixa tipo *rakesh*e em Olá **rótulo de borda** caixa tipo *sabe*e, em seguida, clique em caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="0279a-239">In hello **Target** box type *rakesh*, and in hello **Edge label** box type *knows*, and then click hello check box.</span></span>

   ![Adicionar uma conexão entre ashley e rakesh no Data Explorer](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="0279a-241">Agora selecione **rakesh** na lista de resultados de saudação e veja se Carlos e rakesh estão conectados.</span><span class="sxs-lookup"><span data-stu-id="0279a-241">Now select **rakesh** from hello results list and see that ashley and rakesh are connected.</span></span> 

   ![Dois vértices conectados no Data Explorer](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="0279a-243">Você também pode usar procedimentos de toocreate armazenado no Explorador de dados, UDFs e lógica de negócios do lado do servidor de tooperform de gatilhos, bem como a taxa de transferência de escala.</span><span class="sxs-lookup"><span data-stu-id="0279a-243">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="0279a-244">No Explorador de dados expõe todos acesso a dados através de programação interno Olá disponível no hello APIs, mas fornece acesso fácil tooyour dados em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0279a-244">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>



## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="0279a-245">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0279a-245">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="0279a-246">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="0279a-246">Clean up resources</span></span>

<span data-ttu-id="0279a-247">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0279a-247">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="0279a-248">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="0279a-248">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="0279a-249">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="0279a-249">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0279a-250">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0279a-250">Next steps</span></span>

<span data-ttu-id="0279a-251">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, criar um gráfico usando Olá Explorador de dados e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0279a-251">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="0279a-252">Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin.</span><span class="sxs-lookup"><span data-stu-id="0279a-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0279a-253">Consultar usando o Gremlin</span><span class="sxs-lookup"><span data-stu-id="0279a-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

