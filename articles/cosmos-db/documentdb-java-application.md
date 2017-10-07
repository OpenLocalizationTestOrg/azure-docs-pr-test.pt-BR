---
title: tutorial de desenvolvimento de aplicativo aaaJava usando o banco de dados do Azure Cosmos | Microsoft Docs
description: "Este tutorial de aplicativo web Java mostra como toouse hello Azure Cosmos DB Olá toostore API DocumentDB e acessar dados de um aplicativo Java hospedado em sites do Azure."
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
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="ff8c0-104">Criar um aplicativo da web de Java usando o banco de dados do Azure Cosmos e hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ff8c0-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff8c0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ff8c0-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="ff8c0-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ff8c0-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="ff8c0-107">Java</span><span class="sxs-lookup"><span data-stu-id="ff8c0-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="ff8c0-108">Python</span><span class="sxs-lookup"><span data-stu-id="ff8c0-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="ff8c0-109">Este tutorial de aplicativo web Java mostra como Olá toouse [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) toostore e acessar dados de um aplicativo Java hospedado em aplicativos de Web do serviço de aplicativo do Azure service.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="ff8c0-110">Neste tópico, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="ff8c0-111">Como toobuild um aplicativo básico do JavaServer Pages (JSP) no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="ff8c0-112">Como toowork com hello Azure Cosmos DB serviço usando Olá [SDK de Java do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="ff8c0-113">Este tutorial de aplicativo Java mostra como o aplicativo de gerenciamento de tarefas de toocreate baseado na web, que permite marcar, recuperar e você toocreate tarefas como concluída, conforme mostrado no Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="ff8c0-114">Cada uma das tarefas de saudação na lista de tarefas de saudação são armazenadas como documentos JSON no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Aplicativo Java Minha lista de tarefas pendentes](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="ff8c0-116">Este tutorial de desenvolvimento de aplicativo presume que você tenha experiência anterior com o Java.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="ff8c0-117">Se você for novo tooJava ou Olá [ferramentas pré-requisito](#Prerequisites), recomendamos o download Olá completa [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projeto do GitHub e compilá-lo usando [Olá instruções no final da saudação deste artigo](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="ff8c0-118">Depois de criado, você pode examinar informações de toogain artigo Olá no código Olá no contexto de saudação do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="ff8c0-119"><a id="Prerequisites"></a>Pré-requisitos para este tutorial de aplicativo Web Java</span><span class="sxs-lookup"><span data-stu-id="ff8c0-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="ff8c0-120">Antes de começar este tutorial de desenvolvimento de aplicativo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="ff8c0-121">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-121">An active Azure account.</span></span> <span data-ttu-id="ff8c0-122">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ff8c0-123">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="ff8c0-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="ff8c0-124">OU</span><span class="sxs-lookup"><span data-stu-id="ff8c0-124">OR</span></span>

    <span data-ttu-id="ff8c0-125">Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="ff8c0-126">[Java Development Kit (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="ff8c0-127">Eclipse IDE para desenvolvedores de Java EE.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="ff8c0-128">Um site do Azure com um Java runtime environment (por exemplo, Tomcat ou Jetty) habilitado.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="ff8c0-129">Se você estiver instalando essas ferramentas para Olá a primeira vez, coreservlets.com fornece uma passo a passo do processo de instalação de saudação na seção de início rápido de saudação do seu [Tutorial: Instalando TomCat7 e usá-lo com o Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artigo.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="ff8c0-130"><a id="CreateDB"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ff8c0-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="ff8c0-131">Vamos começar criando uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="ff8c0-132">Se você já tiver uma conta ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[etapa 2: criar o aplicativo de Java JSP hello](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="ff8c0-133"><a id="CreateJSP"></a>Etapa 2: Criar um aplicativo de Java JSP hello</span><span class="sxs-lookup"><span data-stu-id="ff8c0-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="ff8c0-134">Olá toocreate aplicativo JSP:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="ff8c0-135">Primeiro, começaremos criando um projeto Java.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="ff8c0-136">Inicie o Eclipse, clique em **Arquivo**, **Novo** e clique em **Projeto Web dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="ff8c0-137">Se você não vir **projeto Web dinâmico** listado como um projeto disponível, Olá a seguir: clique em **arquivo**, clique em **novo**, clique em **projeto**..., expanda **Web**, clique em **projeto Web dinâmico**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Desenvolvimento de aplicativo Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="ff8c0-139">Insira um nome de projeto em Olá **nome do projeto** caixa e em Olá **tempo de execução de destino** menu suspenso, selecione, opcionalmente, um valor (por exemplo, Apache Tomcat v 7.0) e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="ff8c0-140">Selecionar um destino de tempo de execução permite que você toorun seu projeto localmente por meio do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="ff8c0-141">No Eclipse, na exibição do Explorador de projeto hello, expanda seu projeto.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="ff8c0-142">Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="ff8c0-143">Em Olá **novo arquivo JSP** caixa de diálogo, o arquivo de saudação do nome **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="ff8c0-144">Mantenha a pasta pai Olá **WebContent**, conforme mostrado no Olá a ilustração a seguir e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Criar um novo arquivo JSP — tutorial de aplicativo Web Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="ff8c0-146">Em Olá **Selecionar modelo JSP** caixa de diálogo para finalidade de saudação deste tutorial, selecione **novo arquivo JSP (html)**e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="ff8c0-147">Quando o arquivo do hello index.jsp for aberto no Eclipse, adicionar texto toodisplay **Olá, mundo!**</span><span class="sxs-lookup"><span data-stu-id="ff8c0-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="ff8c0-148">dentro de saudação existente <body> elemento.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-148">within hello existing <body> element.</span></span> <span data-ttu-id="ff8c0-149">Seu atualizada <body> conteúdo deve ter aparência Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="ff8c0-150">Salve o arquivo index.jsp de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="ff8c0-151">Se você definir um tempo de execução de destino na etapa 2, você pode clicar em **projeto** e **executar** toorun aplicativo JSP localmente:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Hello World — tutorial de aplicativo Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="ff8c0-153"><a id="InstallSDK"></a>Etapa 3: Instalar Olá SDK de Java do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ff8c0-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="ff8c0-154">Olá toopull de maneira mais fácil no hello SDK de Java do DocumentDB e suas dependências é por meio de [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="ff8c0-155">toodo isso, você precisará tooconvert seu projeto do projeto tooa maven Concluindo Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="ff8c0-156">Seu projeto no hello Explorador de projeto, clique **configurar**, clique em **converter tooMaven projeto**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="ff8c0-157">Em Olá **criar novo POM** janela, aceite os padrões de saudação e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="ff8c0-158">Em **Explorador de projeto**, abrir arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="ff8c0-159">Em Olá **dependências** guia Olá **dependências** painel, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="ff8c0-160">Em Olá **selecione dependência** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="ff8c0-161">Em Olá **Id do grupo** , digite com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="ff8c0-162">Em Olá **Id do artefato** , digite documentdb do azure.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="ff8c0-163">Em Olá **versão** , digite 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![Instalar o SDK do aplicativo Java para DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="ff8c0-165">Ou Adicionar dependência Olá XML para o Id de grupo e a Id de artefato diretamente toohello pom.xml por meio de um editor de texto:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="ff8c0-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="ff8c0-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="ff8c0-167">Clique em **Okey** e Maven instalará Olá SDK de Java do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="ff8c0-168">Salve o arquivo de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="ff8c0-169"><a id="UseService"></a>Etapa 4: Usando o serviço de banco de dados do Azure Cosmos Olá em um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="ff8c0-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="ff8c0-170">Primeiro, vamos definir objeto de TodoItem Olá em TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="ff8c0-171">Este projeto, estamos usando [Lombok projeto](http://projectlombok.org/) toogenerate Olá construtor, getters, setters e um construtor.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="ff8c0-172">Como alternativa, você pode gravar este código manualmente ou ter Olá IDE gerá-lo.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="ff8c0-173">serviço de banco de dados do Azure Cosmos de saudação tooinvoke, você deve criar um novo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="ff8c0-174">Em geral, é melhor Olá de tooreuse **DocumentClient** - em vez de criar um novo cliente para cada solicitação subsequente.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="ff8c0-175">Cliente Olá pode ser reutilizado por quebra automática de cliente de saudação em uma **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="ff8c0-176">Em DocumentClientFactory.java, você precisa toopaste Olá URI e chave primária valor salvo tooyour a área de transferência em [etapa 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="ff8c0-177">Substitua [SEU\_PONTODEEXTREMIDADE\_AQUI] pelo seu URI e substitua [SUA\_CHAVE\_AQUI] pela sua chave primária.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="ff8c0-178">Agora vamos criar um tooabstract Data Access Object (DAO) persistentes nosso tooAzure de itens de ToDo banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="ff8c0-179">Em ordem de itens de tarefas toosave tooa coleção, Olá cliente precisa toopersist qual banco de dados e coleção de tooknow muito (como referenciada por links automáticos).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="ff8c0-180">Em geral, é o banco de dados do melhor toocache hello e coleção quando possível tooavoid banco de dados de toohello de ida e volta adicionais.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="ff8c0-181">Olá código a seguir ilustra como tooretrieve nosso banco de dados e a coleção, se ele existir, ou crie um novo se não existir:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="ff8c0-182">próxima etapa do Hello é toowrite alguns hello de toopersist de código TodoItems na coleção toohello.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="ff8c0-183">Neste exemplo, usaremos [Gson](https://code.google.com/p/google-gson/) tooserialize e desserializar documentos de tooJSON TodoItem POJOs Plain Old Java Objects ().</span><span class="sxs-lookup"><span data-stu-id="ff8c0-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="ff8c0-184">Assim como os bancos de dados e coleções do Azure Cosmos DB, os documentos também são referenciados por self-links.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="ff8c0-185">Olá permite a função auxiliar a seguir nos recuperar documentos por outro atributo (por exemplo, "id") em vez de vínculo automático:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
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
6. <span data-ttu-id="ff8c0-186">Podemos usar o método auxiliar de saudação na etapa 5 tooretrieve um documento JSON TodoItem por id e desserializá-la tooa POJO:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="ff8c0-187">Também podemos usar Olá DocumentClient tooget uma coleção ou uma lista de TodoItems usando SQL do DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="ff8c0-188">Há tooupdate de muitas maneiras de um documento com hello DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="ff8c0-189">Em nosso aplicativo de lista de tarefas, queremos tootoggle capaz de toobe se um TodoItem é concluído.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="ff8c0-190">Isso pode ser feito atualizando o atributo "concluído" no documento de saudação do hello:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="ff8c0-191">Por fim, queremos Olá capacidade toodelete um TodoItem de nossa lista.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="ff8c0-192">toodo isso, podemos usar o método auxiliar de saudação escrevemos anteriormente tooretrieve Olá vínculo automático e, em seguida, diga Olá cliente toodelete-lo:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="ff8c0-193"><a id="Wire"></a>Etapa 5: Fiação restante Olá Olá do projeto de desenvolvimento de aplicativos Java em conjunto</span><span class="sxs-lookup"><span data-stu-id="ff8c0-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="ff8c0-194">Agora que concluímos fun Olá bits - resta é toobuild uma interface do usuário rápida e conectá-lo tooour DAO.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="ff8c0-195">Primeiro, vamos começar com a criação de um controlador toocall nosso DAO:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-195">First, let's start with building a controller toocall our DAO:</span></span>
   
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
   
    <span data-ttu-id="ff8c0-196">Em um aplicativo mais complexo, controlador Olá pode hospedar a lógica de negócios complicado sobre Olá DAO.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="ff8c0-197">Em seguida, vamos criar um controlador de toohello solicitações HTTP do servlet tooroute:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
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
3. <span data-ttu-id="ff8c0-198">Precisaremos de usuário da web usuário interface toodisplay toohello.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="ff8c0-199">Vamos reescrever Olá JSP criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
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
   
            <!-- hello ToDo List -->
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
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="ff8c0-200">Por fim, gravar alguma interface de usuário do lado do cliente JavaScript tootie Olá web e Olá servlet juntos:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
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
   
              // Call api tooupdate todo items.
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
           * Install hello TodoApp
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
5. <span data-ttu-id="ff8c0-201">Incrível!</span><span class="sxs-lookup"><span data-stu-id="ff8c0-201">Awesome!</span></span> <span data-ttu-id="ff8c0-202">Agora tudo o que resta é aplicativo de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="ff8c0-203">Execute o aplicativo hello localmente e adicione alguns itens de tarefas, preenchendo a categoria e o nome do item hello e clicando em **adicionar tarefa**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="ff8c0-204">Depois que o item de saudação aparece, você pode atualizar seja concluída, alternando a caixa de seleção hello e clicando em **atualizar tarefas**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="ff8c0-205"><a id="Deploy"></a>Etapa 6: Implantar seu aplicativo de Java tooAzure Sites da Web</span><span class="sxs-lookup"><span data-stu-id="ff8c0-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="ff8c0-206">Sites do Azure tornam a implantação de aplicativos Java tão simples quanto a exportação de seu aplicativo como um arquivo WAR e por carregamento ou por meio do controle de origem (por exemplo, Git) ou FTP.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="ff8c0-207">tooexport seu aplicativo como um arquivo WAR, com o botão direito no seu projeto no **Explorador de projeto**, clique em **exportar**e, em seguida, clique em **arquivo WAR**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="ff8c0-208">Em Olá **WAR exportar** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="ff8c0-209">Na caixa do projeto Web hello, insira documentdb do azure-exemplo java.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="ff8c0-210">Na caixa de destino hello, escolha um arquivo WAR do destino toosave hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="ff8c0-211">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-211">Click **Finish**.</span></span>
3. <span data-ttu-id="ff8c0-212">Agora que você tem um arquivo WAR lado, você pode simplesmente carregá-lo tooyour Site do Azure **webapps** directory.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="ff8c0-213">Para obter instruções sobre como carregar o arquivo hello, consulte [adicionar um aplicativo de Java tooAzure aplicativos de Web do serviço de aplicativo](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="ff8c0-214">Depois de saudação WAR arquivo carregado toohello webapps diretório, o ambiente de tempo de execução de saudação detectará que você adicionou a ele e automaticamente carregará.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="ff8c0-215">tooview seu produto final, navegar toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ e começar a adicionar tarefas!</span><span class="sxs-lookup"><span data-stu-id="ff8c0-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="ff8c0-216"><a id="GetProject"></a>Obter o projeto de saudação do GitHub</span><span class="sxs-lookup"><span data-stu-id="ff8c0-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="ff8c0-217">Todos os exemplos de saudação neste tutorial são incluídos no hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projeto no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="ff8c0-218">projeto de todo tooimport Olá no Eclipse, certifique-se de ter software hello e recursos listados em Olá [pré-requisitos](#Prerequisites) seção e, em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff8c0-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="ff8c0-219">Instalar [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="ff8c0-220">Lombok é toogenerate usados construtores, getters, setters no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="ff8c0-221">Depois que você baixou o arquivo de lombok.jar hello, clique duas vezes nele tooinstall-lo ou instalá-lo na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="ff8c0-222">Se o Eclipse estiver aberto, fechá-la e reiniciá-lo tooload Lombok.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="ff8c0-223">No Eclipse, no hello **arquivo** menu, clique em **importação**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="ff8c0-224">Em Olá **importação** janela, clique em **Git**, clique em **projetos do Git**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="ff8c0-225">Em Olá **Selecionar origem de repositório** tela, clique em **Clone URI**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="ff8c0-226">Em Olá **repositório Git de origem** tela hello **URI** caixa, digite https://github.com/Azure-Samples/java-todo-app.git e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="ff8c0-227">Em Olá **seleção ramificação** tela, verifique se **mestre** está selecionado e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="ff8c0-228">Em Olá **destino Local** tela, clique em **procurar** tooselect uma pasta onde Olá repositório pode ser copiada e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="ff8c0-229">Em Olá **selecione toouse um Assistente para importar projetos** tela, verifique se **importar projetos existentes** está selecionado e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="ff8c0-230">Em Olá **importar projetos** tela, desmarque Olá **DocumentDB** do projeto e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="ff8c0-231">projeto de documentos Olá contém hello Azure Cosmos DB Java SDK, vamos adicionar como uma dependência em vez disso.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="ff8c0-232">Em **Explorador de projeto**, navegue tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java e substitua os valores HOST e MASTER_KEY Olá Olá URI e a chave primária para sua conta do banco de dados do Azure Cosmos e salvar Olá arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="ff8c0-233">Para obter mais informações, consulte a [Etapa 1. Crie uma conta do banco de dados BD Cosmos do Azure](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="ff8c0-234">Em **Explorador de projeto**, Olá clique com botão direito **documentdb do azure-exemplo java**, clique em **caminho de compilação de**e, em seguida, clique em **configurar o caminho de compilação**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="ff8c0-235">Em Olá **caminho de compilação de Java** tela, no painel direito da saudação, selecione Olá **bibliotecas** guia e, em seguida, clique em **adicionar JARs externo**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="ff8c0-236">Navegue toohello local do arquivo de lombok.jar hello e, em seguida, clique em **abrir**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="ff8c0-237">Saudação do uso etapa 12 tooopen **propriedades** janela novamente e, no painel esquerdo do hello, clique em **tempos de execução de destino**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="ff8c0-238">Em Olá **tempos de execução de destino** tela, clique em **novo**, selecione **versão 7.0 do Apache Tomcat**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="ff8c0-239">Saudação do uso etapa 12 tooopen **propriedades** janela novamente e, no painel esquerdo do hello, clique em **facetas de projeto**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="ff8c0-240">Em Olá **projeto facetas** tela, selecione **módulo Web dinâmico** e **Java**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="ff8c0-241">Em Olá **servidores** guia na parte inferior da saudação da tela hello, clique no **Tomcat versão 7.0 do servidor no localhost** e, em seguida, clique em **adicionar e remover**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="ff8c0-242">Em Olá **adicionar e remover** janela, mover **documentdb do azure-exemplo java** toohello **configurado** caixa e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="ff8c0-243">Em Olá **servidores** guia, clique no **Tomcat versão 7.0 do servidor no localhost**e, em seguida, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="ff8c0-244">Em um navegador, navegue toohttp://localhost:8080 / azure-documentdb-exemplo de java / e comece a adicionar tooyour lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="ff8c0-245">Observe que se você tiver alterado os valores de porta padrão, alterar 8080 toohello valor selecionado.</span><span class="sxs-lookup"><span data-stu-id="ff8c0-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="ff8c0-246">toodeploy tooan seu projeto site do Azure, consulte [etapa 6. Implantar seu aplicativo tooAzure Sites da Web](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="ff8c0-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
