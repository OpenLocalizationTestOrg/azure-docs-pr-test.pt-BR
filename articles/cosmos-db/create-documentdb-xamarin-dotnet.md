---
title: "Azure Cosmos DB: compilar um aplicativo Web com autenticação do Xamarin e do Facebook | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET podem usar tooconnect tooand consultar o banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="52ef1-103">Azure Cosmos DB: compilar um aplicativo Web com autenticação do Xamarin, do Facebook e do .NET</span><span class="sxs-lookup"><span data-stu-id="52ef1-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="52ef1-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52ef1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="52ef1-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="52ef1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="52ef1-106">Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ef1-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="52ef1-107">Você, em seguida, criar e implantar um aplicativo da web lista todo baseado Olá [API .NET do DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)e o mecanismo de autorização do Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="52ef1-108">aplicativo de web de lista de tarefas Olá implementa um padrão de dados por usuário que permite que os usuários toologin usando o Facebook Auth e gerenciar seus próprios itens toodo.</span><span class="sxs-lookup"><span data-stu-id="52ef1-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52ef1-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="52ef1-109">Prerequisites</span></span>

<span data-ttu-id="52ef1-110">Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="52ef1-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="52ef1-111">Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="52ef1-112">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="52ef1-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="52ef1-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="52ef1-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="52ef1-114">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="52ef1-114">Clone hello sample application</span></span>

<span data-ttu-id="52ef1-115">Agora vamos clone uma API de documentos de aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="52ef1-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="52ef1-116">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="52ef1-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="52ef1-117">Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="52ef1-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="52ef1-118">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="52ef1-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="52ef1-119">Em seguida, abra o arquivo de DocumentDBTodo.sln de saudação da pasta de samples/xamarin/UserItems/xamarin.forms de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52ef1-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="52ef1-120">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="52ef1-120">Review hello code</span></span>

<span data-ttu-id="52ef1-121">código de saudação na pasta de Xamarin Olá contém:</span><span class="sxs-lookup"><span data-stu-id="52ef1-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="52ef1-122">aplicativo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="52ef1-122">Xamarin app.</span></span> <span data-ttu-id="52ef1-123">aplicativo Hello armazena itens de tarefas do usuário Olá em uma coleção particionada chamada UserItems.</span><span class="sxs-lookup"><span data-stu-id="52ef1-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="52ef1-124">API do agente de token de recurso.</span><span class="sxs-lookup"><span data-stu-id="52ef1-124">Resource token broker API.</span></span> <span data-ttu-id="52ef1-125">Um recurso de banco de dados do Azure Cosmos toobroker API da Web ASP.NET simples tokens toohello os usuários do aplicativo hello conectado.</span><span class="sxs-lookup"><span data-stu-id="52ef1-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="52ef1-126">Tokens de recurso são tokens de acesso de curta duração que fornecem aplicativo Olá Olá acesso toohello registrada nos dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="52ef1-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="52ef1-127">Olá autenticação e fluxo de dados é ilustrado no diagrama de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="52ef1-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="52ef1-128">Olá UserItems coleção é criada com a chave de partição Olá ' / userid'.</span><span class="sxs-lookup"><span data-stu-id="52ef1-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="52ef1-129">Especificar uma chave de partição para uma coleção permite que o banco de dados do Azure Cosmos tooscale infinitamente como número de saudação de usuários e itens cresce.</span><span class="sxs-lookup"><span data-stu-id="52ef1-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="52ef1-130">Olá Xamarin aplicativo permite toologin de usuários com credenciais do Facebook.</span><span class="sxs-lookup"><span data-stu-id="52ef1-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="52ef1-131">Olá Xamarin aplicativo usa tooauthenticate de token de acesso do Facebook com o API ResourceTokenBroker</span><span class="sxs-lookup"><span data-stu-id="52ef1-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="52ef1-132">broker API do token de recurso de Olá autentica Olá solicitação usando o recurso de autenticação do serviço de aplicativo e solicita um token de recurso do banco de dados do Azure Cosmos com documentos de tooall de acesso de leitura/gravação compartilhar a chave de partição de saudação do usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="52ef1-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="52ef1-133">Agente de token de recurso retorna Olá recurso token toohello cliente aplicativo.</span><span class="sxs-lookup"><span data-stu-id="52ef1-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="52ef1-134">aplicativo Hello acessa os itens de tarefas do usuário hello usando o token de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="52ef1-136">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="52ef1-136">Update your connection string</span></span>

<span data-ttu-id="52ef1-137">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="52ef1-138">Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="52ef1-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="52ef1-139">Você usará botões de cópia Olá Olá direita da saudação toocopy da tela hello URI e a chave primária no arquivo Web. config de saudação na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="52ef1-141">No Visual Studio de 2017, abra Web. config Olá na pasta do azure-documentdb-dotnet/exemplos/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="52ef1-142">Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá valor Olá accountUrl em Web. config.</span><span class="sxs-lookup"><span data-stu-id="52ef1-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="52ef1-143">Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá accountKey em Web.congif.</span><span class="sxs-lookup"><span data-stu-id="52ef1-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="52ef1-144">Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="52ef1-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="52ef1-145">Criar e implantar o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="52ef1-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="52ef1-146">No portal do Azure de Olá, crie um serviço de aplicativo site toohost Olá recurso token broker API.</span><span class="sxs-lookup"><span data-stu-id="52ef1-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="52ef1-147">No hello portal do Azure, abra a folha de configurações do aplicativo de saudação do broker site da API do token de recurso de hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="52ef1-148">Preencha Olá configurações do aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ef1-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="52ef1-149">accountUrl - URL de conta de banco de dados do Azure Cosmos Olá na guia de chaves de saudação da sua conta de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="52ef1-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="52ef1-150">accountKey - chave de mestre de guia de chaves de saudação da sua conta de banco de dados do Azure Cosmos do hello Azure Cosmos DB conta.</span><span class="sxs-lookup"><span data-stu-id="52ef1-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="52ef1-151">databaseId e collectionId do seu banco de dados e coleção criados</span><span class="sxs-lookup"><span data-stu-id="52ef1-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="52ef1-152">Publica Olá ResourceTokenBroker solução tooyour criado site da Web.</span><span class="sxs-lookup"><span data-stu-id="52ef1-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="52ef1-153">Abra o projeto do Xamarin hello e navegue tooTodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="52ef1-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="52ef1-154">Preencha valores hello para accountURL, collectionId, databaseId, bem como resourceTokenBrokerURL como Olá base https url para o site de broker token de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="52ef1-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="52ef1-155">Olá completa [como tooconfigure seu logon do Facebook do serviço de aplicativo aplicativo toouse](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup tutorial a autenticação do Facebook e configurar Olá ResourceTokenBroker site.</span><span class="sxs-lookup"><span data-stu-id="52ef1-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="52ef1-156">Execute o aplicativo Xamarin de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ef1-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="52ef1-157">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="52ef1-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="52ef1-158">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="52ef1-158">Clean up resources</span></span>

<span data-ttu-id="52ef1-159">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ef1-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="52ef1-160">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="52ef1-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="52ef1-161">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="52ef1-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52ef1-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52ef1-162">Next steps</span></span>

<span data-ttu-id="52ef1-163">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e criar e implantar um aplicativo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="52ef1-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="52ef1-164">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="52ef1-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="52ef1-165">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="52ef1-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
