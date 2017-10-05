---
title: Tutorial de desenvolvimento de aplicativo Java usando o Azure Cosmos DB | Microsoft Docs
description: "Este tutorial de aplicativo Web Java mostra a você como usar o Azure Cosmos DB e a API de DocumentDB para armazenar e acessar dados de um aplicativo Java hospedado nos Sites do Azure."
keywords: Desenvolvimento de aplicativos, tutorial de banco de dados, aplicativo java, tutorial do aplicativo web java, banco de dados de documentos, azure, Microsoft azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="56e53-104">Compilar um aplicativo Web Java usando o Azure Cosmos DB e a API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="56e53-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56e53-105">.NET</span><span class="sxs-lookup"><span data-stu-id="56e53-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="56e53-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="56e53-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="56e53-107">Java</span><span class="sxs-lookup"><span data-stu-id="56e53-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="56e53-108">Python</span><span class="sxs-lookup"><span data-stu-id="56e53-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="56e53-109">Este tutorial de aplicativo Web Java mostra a você como usar o serviço [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) para armazenar e acessar dados de um aplicativo Java hospedado nos Aplicativos Web do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="56e53-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="56e53-110">Neste tópico, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="56e53-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="56e53-111">Como compilar um aplicativo básico do JSP (JavaServer Pages) no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="56e53-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="56e53-112">Como trabalhar com o serviço Azure Cosmos DB usando o [SDK de Java do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="56e53-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="56e53-113">Este tutorial de aplicativo Java mostra como criar um aplicativo de gerenciamento de tarefas baseado na web que permite criar, recuperar e marcar tarefas como concluídas, conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="56e53-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="56e53-114">Cada uma das tarefas na lista de tarefas é armazenada como documentos JSON no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56e53-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Aplicativo Java Minha lista de tarefas pendentes](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="56e53-116">Este tutorial de desenvolvimento de aplicativo presume que você tenha experiência anterior com o Java.</span><span class="sxs-lookup"><span data-stu-id="56e53-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="56e53-117">Se você não estiver familiarizado com Java ou com as [ferramentas de pré-requisito](#Prerequisites), recomendamos o download completo do projeto [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) do GitHub e compilação dele usando as [instruções no final deste artigo](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="56e53-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="56e53-118">Depois de compilá-lo, você poderá consultar o artigo para obter informações sobre o código no contexto do projeto.</span><span class="sxs-lookup"><span data-stu-id="56e53-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="56e53-119"><a id="Prerequisites"></a>Pré-requisitos para este tutorial de aplicativo Web Java</span><span class="sxs-lookup"><span data-stu-id="56e53-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="56e53-120">Antes de começar este tutorial de desenvolvimento de aplicativo, você deve ter:</span><span class="sxs-lookup"><span data-stu-id="56e53-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="56e53-121">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="56e53-121">An active Azure account.</span></span> <span data-ttu-id="56e53-122">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="56e53-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="56e53-123">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="56e53-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="56e53-124">OU</span><span class="sxs-lookup"><span data-stu-id="56e53-124">OR</span></span>

    <span data-ttu-id="56e53-125">Uma instalação local do [Emulador do Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="56e53-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="56e53-126">[Java Development Kit (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="56e53-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="56e53-127">Eclipse IDE para desenvolvedores de Java EE.</span><span class="sxs-lookup"><span data-stu-id="56e53-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="56e53-128">Um site do Azure com um Java runtime environment (por exemplo, Tomcat ou Jetty) habilitado.</span><span class="sxs-lookup"><span data-stu-id="56e53-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="56e53-129">Se você estiver instalando essas ferramentas pela primeira vez, o coreservlets.com fornecerá um passo a passo do processo de instalação na seção de Início rápido do artigo [Tutorial: Instalar TomCat7 e usá-lo com o Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) .</span><span class="sxs-lookup"><span data-stu-id="56e53-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="56e53-130"><a id="CreateDB"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="56e53-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="56e53-131">Vamos começar criando uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56e53-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="56e53-132">Se você já tiver uma conta ou se estiver usando o Emulador do Azure Cosmos DB para este tutorial, pule para a [Etapa 2: Criar um novo aplicativo do Java JSP](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="56e53-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="56e53-133"><a id="CreateJSP"></a>Etapa 2: criar o aplicativo JSP Java</span><span class="sxs-lookup"><span data-stu-id="56e53-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="56e53-134">Para criar o aplicativo JSP:</span><span class="sxs-lookup"><span data-stu-id="56e53-134">To create the JSP application:</span></span>

1. <span data-ttu-id="56e53-135">Primeiro, começaremos criando um projeto Java.</span><span class="sxs-lookup"><span data-stu-id="56e53-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="56e53-136">Inicie o Eclipse, clique em **Arquivo**, **Novo** e clique em **Projeto Web dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="56e53-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="56e53-137">Se você não vir o **Projeto Web Dinâmico** listado como um projeto disponível, faça o seguinte: clique em **Arquivo**, **Novo**, **Projeto...**, expanda **Web**, clique em **Projeto Web Dinâmico** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Desenvolvimento de aplicativo Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="56e53-139">Digite um nome de projeto na caixa **Nome do projeto** e no menu suspenso **Tempo de Execução de Destino**, selecione, opcionalmente, um valor (por exemplo, Apache Tomcat v 7.0) e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56e53-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="56e53-140">Selecione um tempo de execução de destino que permite que você execute seu projeto localmente por meio do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="56e53-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="56e53-141">No Eclipse, na exibição do Explorador de Projeto, expanda o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="56e53-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="56e53-142">Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="56e53-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="56e53-143">Na caixa de diálogo **Novo Arquivo JSP**, nomeie o arquivo como **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="56e53-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="56e53-144">Mantenha a pasta pai como **WebContent**, conforme mostrado na ilustração a seguir e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Criar um novo arquivo JSP — tutorial de aplicativo Web Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="56e53-146">Na caixa de diálogo **Selecionar modelo JSP**, selecione esse tutorial **Novo Arquivo JSP (html)** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56e53-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="56e53-147">Quando o arquivo index.jsp for aberto no Eclipse, adicione o texto para exibir **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="56e53-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="56e53-148">dentro do elemento existente <body>.</span><span class="sxs-lookup"><span data-stu-id="56e53-148">within the existing <body> element.</span></span> <span data-ttu-id="56e53-149">A atualização <body> do conteúdo deve se parecer com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="56e53-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="56e53-150">Salve o arquivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="56e53-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="56e53-151">Se definir um tempo de execução de destino na etapa 2, você pode clicar no **Projeto** e em **Executar** para executar o aplicativo JSP localmente:</span><span class="sxs-lookup"><span data-stu-id="56e53-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Hello World — tutorial de aplicativo Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="56e53-153"><a id="InstallSDK">
            </a>Etapa 3: Instalar o SDK do Java do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="56e53-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="56e53-154">É a maneira mais fácil de obter o SDK do Java do DocumentDB e suas dependências por meio do [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="56e53-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="56e53-155">Para fazer isso, você precisará converter o projeto para um projeto Maven concluindo as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="56e53-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="56e53-156">Clique em seu projeto no Explorador de projeto, clique em **Configurar** e em **Converter em Projeto Maven**.</span><span class="sxs-lookup"><span data-stu-id="56e53-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="56e53-157">Na janela **Criar novo POM**, aceite os padrões e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56e53-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="56e53-158">No **Explorador de projeto**, abra o arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="56e53-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="56e53-159">Na guia **Dependências**, no painel **Dependências**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="56e53-160">Na janela **Selecionar dependência** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="56e53-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="56e53-161">Na caixa **Id do Grupo**, insira com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="56e53-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="56e53-162">Na caixa **Id do Artefato**, insira azure-documentdb.</span><span class="sxs-lookup"><span data-stu-id="56e53-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="56e53-163">Na caixa **Versão**, insira 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="56e53-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![Instalar o SDK do aplicativo Java para DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="56e53-165">Ou adicione a dependência de XML para a ID do Grupo e ID do Artefato diretamente no pom.xml por meio de um editor de texto:</span><span class="sxs-lookup"><span data-stu-id="56e53-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="56e53-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="56e53-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="56e53-167">Clique em **OK** e o Maven instalará o SDK do Java do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="56e53-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="56e53-168">Salve o arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="56e53-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="56e53-169"><a id="UseService"></a>Etapa 4: Usar o serviço do Azure Cosmos DB em um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="56e53-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="56e53-170">Primeiro, vamos definir o objeto TodoItem no TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="56e53-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="56e53-171">Neste projeto, estamos usando [Project Lombok](http://projectlombok.org/) para gerar o construtor, os getters, os setters e um builder.</span><span class="sxs-lookup"><span data-stu-id="56e53-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="56e53-172">Como alternativa, você pode escrever esse código manualmente ou o IDE pode gerá-lo.</span><span class="sxs-lookup"><span data-stu-id="56e53-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="56e53-173">Para invocar o serviço Azure Cosmos DB, você deve criar um novo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="56e53-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="56e53-174">Em geral, é melhor reutilizar o **DocumentClient** - em vez de construir um novo cliente para cada solicitação subsequente.</span><span class="sxs-lookup"><span data-stu-id="56e53-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="56e53-175">O cliente pode ser reutilizado envolvendo o cliente em uma **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="56e53-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="56e53-176">No DocumentClientFactory.java, você precisa colar o valor da URI e a CHAVE PRIMÁRIA salva na área de transferência na [etapa 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="56e53-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="56e53-177">Substitua [SEU\_PONTODEEXTREMIDADE\_AQUI] pelo seu URI e substitua [SUA\_CHAVE\_AQUI] pela sua chave primária.</span><span class="sxs-lookup"><span data-stu-id="56e53-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="56e53-178">Agora, vamos criar um objeto de acesso de dados (DAO) para abstrair mantendo os itens ToDo no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56e53-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="56e53-179">Para salvar os itens das tarefas em uma coleção, o cliente precisa saber qual banco de dados e coleção manter (como referenciado por self-links).</span><span class="sxs-lookup"><span data-stu-id="56e53-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="56e53-180">Em geral, é melhor armazenar o banco de dados e a coleção em cache sempre que possível para evitar viagens adicionais ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="56e53-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="56e53-181">O código a seguir ilustra como recuperar nosso Banco de dados e Coleção, se existir, ou criar um novo se ela não existir:</span><span class="sxs-lookup"><span data-stu-id="56e53-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="56e53-182">A próxima etapa é escrever algum código para manter as TodoItems na coleção.</span><span class="sxs-lookup"><span data-stu-id="56e53-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="56e53-183">Neste exemplo, usaremos [Gson](https://code.google.com/p/google-gson/) para serializar e desserializar TodoItem Plain Old Java Objects (POJOs) para documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="56e53-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="56e53-184">Assim como os bancos de dados e coleções do Azure Cosmos DB, os documentos também são referenciados por self-links.</span><span class="sxs-lookup"><span data-stu-id="56e53-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="56e53-185">A função de auxiliar a seguir nos permite recuperar documentos por outro atributo (por exemplo, "id") em vez de self-links:</span><span class="sxs-lookup"><span data-stu-id="56e53-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="56e53-186">Podemos usar o método auxiliar na etapa 5 para recuperar um documento TodoItem JSON pela ID e, em seguida, desserializá-lo para um POJO:</span><span class="sxs-lookup"><span data-stu-id="56e53-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="56e53-187">Também podemos usar o DocumentClient para obter uma coleção ou uma lista de TodoItems usando o SQL do DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="56e53-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="56e53-188">Há muitas maneiras de atualizar um documento com o DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="56e53-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="56e53-189">Em nosso aplicativo de lista Todo, queremos poder ativar ou desativar um TodoItem ele for concluído.</span><span class="sxs-lookup"><span data-stu-id="56e53-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="56e53-190">Isso pode ser feito atualizando o atributo "concluído" dentro do documento:</span><span class="sxs-lookup"><span data-stu-id="56e53-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="56e53-191">Por fim, queremos ter a capacidade de excluir um TodoItem de nossa lista.</span><span class="sxs-lookup"><span data-stu-id="56e53-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="56e53-192">Para fazer isso, podemos usar o método auxiliar que escrevemos antes para recuperar self links e depois dizer ao cliente para excluí-lo:</span><span class="sxs-lookup"><span data-stu-id="56e53-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="56e53-193"><a id="Wire"></a>Etapa 5: Conectando por fio o restante do projeto de desenvolvimento de aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="56e53-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="56e53-194">Agora que concluímos a parte divertida - tudo que restou é criar uma interface de usuário rápida e conectá-la ao nosso DAO.</span><span class="sxs-lookup"><span data-stu-id="56e53-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="56e53-195">Primeiro, vamos começar com a criação de um Controlador para chamar nosso DAO:</span><span class="sxs-lookup"><span data-stu-id="56e53-195">First, let's start with building a controller to call our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="56e53-196">Em um aplicativo mais complexo, o Controlador pode ter uma lógica comercial complicada na parte superior do DAO.</span><span class="sxs-lookup"><span data-stu-id="56e53-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="56e53-197">Em seguida, criaremos um Servlet para rotear solicitações HTTP para o Controlador:</span><span class="sxs-lookup"><span data-stu-id="56e53-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="56e53-198">Precisaremos de uma interface do usuário da Web para a exibição ao usuário.</span><span class="sxs-lookup"><span data-stu-id="56e53-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="56e53-199">Vamos reescrever o ndex.jsp criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="56e53-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- The ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="56e53-200">E, finalmente, escrever um JavaScript do lado do cliente para unir o servlet e a interface do usuário da web:</span><span class="sxs-lookup"><span data-stu-id="56e53-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api to update todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install the TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="56e53-201">Incrível!</span><span class="sxs-lookup"><span data-stu-id="56e53-201">Awesome!</span></span> <span data-ttu-id="56e53-202">Agora tudo o que resta é testar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="56e53-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="56e53-203">Executar o aplicativo localmente e adicionar alguns itens de tarefas, preenchendo o nome do item e a categoria e clicando em **Adicionar tarefa**.</span><span class="sxs-lookup"><span data-stu-id="56e53-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="56e53-204">Quando o item aparecer, você poderá atualizar se ele está concluído alternando a caixa de seleção e clicando em **Atualizar Tarefas**.</span><span class="sxs-lookup"><span data-stu-id="56e53-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="56e53-205"><a id="Deploy"></a>Etapa 6: implantar seu aplicativo Java em sites do Azure</span><span class="sxs-lookup"><span data-stu-id="56e53-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="56e53-206">Sites do Azure tornam a implantação de aplicativos Java tão simples quanto a exportação de seu aplicativo como um arquivo WAR e por carregamento ou por meio do controle de origem (por exemplo, Git) ou FTP.</span><span class="sxs-lookup"><span data-stu-id="56e53-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="56e53-207">Para exportar seu aplicativo como um arquivo WAR, clique com o botão direito em seu projeto no **Explorador de Projeto**, clique em **Exportar** e clique em **Arquivo WAR**.</span><span class="sxs-lookup"><span data-stu-id="56e53-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="56e53-208">Na janela **Exportar WAR** , faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="56e53-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="56e53-209">Na caixa de projeto da Web, insira azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="56e53-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="56e53-210">Na caixa Destino, escolha um destino para salvar o arquivo WAR.</span><span class="sxs-lookup"><span data-stu-id="56e53-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="56e53-211">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56e53-211">Click **Finish**.</span></span>
3. <span data-ttu-id="56e53-212">Agora que tem um arquivo WAR em mãos, você pode simplesmente carregá-lo no seu diretório **webapps** do site do Azure.</span><span class="sxs-lookup"><span data-stu-id="56e53-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="56e53-213">Para obter instruções sobre como carregar o arquivo, confira [Adicionar um aplicativo Java aos Aplicativos Web do Serviço de Aplicativo do Azure](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="56e53-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="56e53-214">Uma vez carregado o arquivo WAR na pasta webapps, o ambiente de tempo de execução irá detectar que você o adicionou e o carregará automaticamente.</span><span class="sxs-lookup"><span data-stu-id="56e53-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="56e53-215">Para exibir seu produto acabado, navegue para http://SEU\_NOME\_SITE.azurewebsites.net/azure-java-sample/ e comece a adicionar suas tarefas!</span><span class="sxs-lookup"><span data-stu-id="56e53-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="56e53-216"><a id="GetProject"></a>Obtenha o projeto do GitHub</span><span class="sxs-lookup"><span data-stu-id="56e53-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="56e53-217">Todos os exemplos neste tutorial foram incluídos no projeto [tarefas](https://github.com/Azure-Samples/documentdb-java-todo-app) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="56e53-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="56e53-218">Para importar o projeto de tarefas no Eclipse, certifique-se de ter o software e os recursos listados na seção [pré-requisitos](#Prerequisites) e, em seguida, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="56e53-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="56e53-219">Instalar [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="56e53-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="56e53-220">Lombok é usado para gerar construtores, getters e setters no projeto.</span><span class="sxs-lookup"><span data-stu-id="56e53-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="56e53-221">Depois que você baixou o arquivo lombok.jar, clique duas vezes nele para instalá-lo ou instalá-lo a partir da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="56e53-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="56e53-222">Se o Eclipse estiver aberto, feche-o e reinicie-o para carregar o Lombok.</span><span class="sxs-lookup"><span data-stu-id="56e53-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="56e53-223">No Eclipse, no menu **Arquivo**, clique em **Importar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="56e53-224">Na janela **Importar**, clique em **Git**, **Projetos do Git** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="56e53-225">Na tela **Selecionar origem de repositório**, clique em **Clonar URI**.</span><span class="sxs-lookup"><span data-stu-id="56e53-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="56e53-226">Na tela **Repositório de Origem do Git**, na caixa **URI**, insira https://github.com/Azure-Samples/java-todo-app.git e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="56e53-227">Na tela **Seleção de Ramificação**, verifique se **master** está selecionado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="56e53-228">Na tela **Destino Local**, clique em **Procurar** para selecionar uma pasta onde o repositório possa ser copiado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="56e53-229">Na tela **Selecionar um assistente a ser usado para importar projetos**, verifique se **Importar projetos existentes** está selecionado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="56e53-230">Na tela **Importar projetos**, desmarque o projeto do **DocumentDB** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56e53-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="56e53-231">O projeto DocumentDB contém o SDK Java do Azure Cosmos DB, que adicionaremos como uma dependência em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="56e53-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="56e53-232">No **Gerenciador de Projetos**, navegue para azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java e substitua os valores HOST e MASTER_KEY pela URI e a CHAVE PRIMÁRIA de sua conta BD Cosmos do Azure, então, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="56e53-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="56e53-233">Para obter mais informações, consulte a [Etapa 1. Crie uma conta do banco de dados BD Cosmos do Azure](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="56e53-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="56e53-234">Em **Explorador de Projeto**, clique com o botão direito do mouse em **azure-documentdb-java-sample**, clique em **Caminho de Build** e clique em **Configurar Caminho de Build**.</span><span class="sxs-lookup"><span data-stu-id="56e53-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="56e53-235">Na tela **Caminho de Build Java**, no painel direito, selecione a guia **Bibliotecas** e clique em **Adicionar JARs Externos**.</span><span class="sxs-lookup"><span data-stu-id="56e53-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="56e53-236">Navegue até o local do arquivo lombok.jar e clique em **Abrir** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56e53-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="56e53-237">Use a Etapa 12 para abrir a janela **Propriedades** novamente e, no painel esquerdo, clique em **Tempos de Execução Direcionados**.</span><span class="sxs-lookup"><span data-stu-id="56e53-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="56e53-238">Na tela **Tempos de Execução Direcionados**, clique em **Novo**, selecione **Apache Tomcat v7.0** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56e53-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="56e53-239">Use a Etapa 12 para abrir a janela **Propriedades** novamente e, no painel esquerdo, clique em **Facetas do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="56e53-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="56e53-240">Na tela **Facetas do Projeto**, selecione **Módulo da Web Dinâmico** e **Java** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56e53-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="56e53-241">Na guia **Servidores** na parte inferior da tela, clique com o botão direito do mouse em **Servidor Tomcat v7.0 no localhost** e clique em **Adicionar e Remover**.</span><span class="sxs-lookup"><span data-stu-id="56e53-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="56e53-242">Na janela **Adicionar e Remover**, mova **azure-documentdb-java-sample** para a caixa **Configurado** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="56e53-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="56e53-243">Na guia **Servidores**, clique com o botão direito do mouse em **Servidor Tomcat v7.0 no localhost** e clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="56e53-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="56e53-244">Em um navegador, navegue para http://localhost:8080/azure-documentdb-java-sample/ e comece a adicionar sua lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="56e53-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="56e53-245">Observe que, se você alterou os valores da porta padrão, altere a 8080 para o valor selecionado.</span><span class="sxs-lookup"><span data-stu-id="56e53-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="56e53-246">Para implantar o projeto em um site do Azure, consulte a [Etapa 6. Implante o aplicativo nos Sites do Azure](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="56e53-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
