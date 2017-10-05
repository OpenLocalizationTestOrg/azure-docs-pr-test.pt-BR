---
title: "Azure Cosmos DB: compilar um aplicativo Web com autenticação do Xamarin e do Facebook | Microsoft Docs"
description: "Apresenta um exemplo de código .NET que pode ser usado para conectar e consultar o Azure Cosmos DB"
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
ms.openlocfilehash: 4ea97c2aca6769843d0210ffeae6f95531a21f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="848fb-103">Azure Cosmos DB: compilar um aplicativo Web com autenticação do Xamarin, do Facebook e do .NET</span><span class="sxs-lookup"><span data-stu-id="848fb-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="848fb-104">O Azure Cosmos DB é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="848fb-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="848fb-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848fb-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="848fb-106">Este início rápido demonstra como criar uma conta do Azure Cosmos DB, um banco de dados de documento e uma coleção usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="848fb-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="848fb-107">Em seguida, você criará e implantará um aplicativo Web de lista de tarefas pendentes com base na [API do .NET do DocumentDB](documentdb-sdk-dotnet.md), no [Xamarin](https://www.xamarin.com/)e no mecanismo de autorização do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848fb-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and the Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="848fb-108">O aplicativo Web da lista de tarefas pendentes implementa um padrão de dados por usuário que permite que usuários façam o logon usando a Autenticação do Facebook e gerenciem seus próprios itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="848fb-108">The todo list web app implements a per-user data pattern that enables users to login using Facebook Auth and manage their own to do items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="848fb-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="848fb-109">Prerequisites</span></span>

<span data-ttu-id="848fb-110">Se você ainda não tem o Visual 2017 Studio instalado, poderá baixar e usar o **Visual Studio 2017 Community Edition** [gratuito](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="848fb-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="848fb-111">Verifique se você habilitou o **desenvolvimento do Azure** durante a instalação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="848fb-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="848fb-112">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="848fb-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="848fb-113">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="848fb-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="848fb-114">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="848fb-114">Clone the sample application</span></span>

<span data-ttu-id="848fb-115">Agora, vamos clonar um aplicativo de API do DocumentDB do GitHub, defina a cadeia de conexão e execute-o.</span><span class="sxs-lookup"><span data-stu-id="848fb-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="848fb-116">Você verá como é fácil trabalhar usando dados de forma programática.</span><span class="sxs-lookup"><span data-stu-id="848fb-116">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="848fb-117">Abra uma janela de terminal do Git, como git bash, e `cd` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="848fb-117">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="848fb-118">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="848fb-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="848fb-119">Em seguida, abra o arquivo DocumentDBTodo.sln na pasta samples/xamarin/UserItems/xamarin.forms no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="848fb-119">Then open the DocumentDBTodo.sln file from the samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="848fb-120">Examine o código</span><span class="sxs-lookup"><span data-stu-id="848fb-120">Review the code</span></span>

<span data-ttu-id="848fb-121">O código na pasta Xamarin contém:</span><span class="sxs-lookup"><span data-stu-id="848fb-121">The code in the Xamarin folder contains:</span></span>

* <span data-ttu-id="848fb-122">aplicativo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="848fb-122">Xamarin app.</span></span> <span data-ttu-id="848fb-123">O aplicativo armazena itens pendentes do usuário em uma coleção particionada chamada UserItems.</span><span class="sxs-lookup"><span data-stu-id="848fb-123">The app stores the user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="848fb-124">API do agente de token de recurso.</span><span class="sxs-lookup"><span data-stu-id="848fb-124">Resource token broker API.</span></span> <span data-ttu-id="848fb-125">Uma API Web ASP.NET simples para tokens de recurso do Azure Cosmos DB do agente para os usuários conectados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="848fb-125">A simple ASP.NET Web API to broker Azure Cosmos DB resource tokens to the logged in users of the app.</span></span> <span data-ttu-id="848fb-126">Os tokens de recurso são tokens de acesso de curta duração que fornecem o aplicativo com acesso aos dados do usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="848fb-126">Resource tokens are short-lived access tokens that provide the app with the access to the logged in user's data.</span></span>

<span data-ttu-id="848fb-127">O fluxo de dados e de autenticação está ilustrado no diagrama abaixo.</span><span class="sxs-lookup"><span data-stu-id="848fb-127">The authentication and data flow is illustrated in the diagram below.</span></span>

* <span data-ttu-id="848fb-128">A coleção UserItems foi criada com a chave de partição '/userid'.</span><span class="sxs-lookup"><span data-stu-id="848fb-128">The UserItems collection is created with the partition key '/userid'.</span></span> <span data-ttu-id="848fb-129">Especificar uma chave de partição para uma coleção permite que o Azure Cosmos DB dimensione infinitamente conforme o número de usuários e itens aumenta.</span><span class="sxs-lookup"><span data-stu-id="848fb-129">Specifying a partition key for a collection allows Azure Cosmos DB to scale infinitely as the number of users and items grows.</span></span>
* <span data-ttu-id="848fb-130">O aplicativo Xamarin permite que os usuários façam logon com as credenciais do Facebook.</span><span class="sxs-lookup"><span data-stu-id="848fb-130">The Xamarin app allows users to login with Facebook credentials.</span></span>
* <span data-ttu-id="848fb-131">O aplicativo Xamarin usa o token de acesso do Facebook para autenticar com a API do ResourceTokenBroker</span><span class="sxs-lookup"><span data-stu-id="848fb-131">The Xamarin app uses Facebook access token to authenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="848fb-132">A API do agente de token de recurso autentica a solicitação, usando o recurso de Autenticação do Serviço de Aplicativo e solicita um token de recurso do Azure Cosmos DB com acesso de leitura/gravação para todos os documentos que compartilham a chave de partição do usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="848fb-132">The resource token broker API authenticates the request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access to all documents sharing the authenticated user's partition key.</span></span>
* <span data-ttu-id="848fb-133">O agente de token de recurso retorna o token de recurso ao aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="848fb-133">Resource token broker returns the resource token to the client app.</span></span>
* <span data-ttu-id="848fb-134">O aplicativo acessa os itens pendentes do usuário por meio do token de recurso.</span><span class="sxs-lookup"><span data-stu-id="848fb-134">The app accesses the user's todo items using the resource token.</span></span>

![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="848fb-136">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="848fb-136">Update your connection string</span></span>

<span data-ttu-id="848fb-137">Agora, volte ao portal do Azure para obter informações sobre a cadeia de conexão e copiá-las para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="848fb-137">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="848fb-138">No [Portal do Azure](http://portal.azure.com/), na sua conta do Azure Cosmos DB, no painel de navegação esquerdo, clique em **Chaves** e, em seguida, clique em **Chaves de leitura/gravação**.</span><span class="sxs-lookup"><span data-stu-id="848fb-138">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="848fb-139">Você usará os botões de cópia no lado direito da tela para copiar o URI e a Chave Primária para o arquivo Web.config na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="848fb-139">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the Web.config file in the next step.</span></span>

    ![Exibir e copiar uma chave de acesso no Portal do Azure, folha Chaves](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="848fb-141">No Visual Studio de 2017, abra o arquivo Web.config na pasta azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="848fb-141">In Visual Studio 2017, open the Web.config file in the azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="848fb-142">Copie o valor do URI do portal (usando o botão de cópia) e torne-o o valor de accountUrl no Web.config.</span><span class="sxs-lookup"><span data-stu-id="848fb-142">Copy your URI value from the portal (using the copy button) and make it the value of the accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="848fb-143">Em seguida, copie o valor da CHAVE PRIMÁRIA do portal e torne-o o valor de accountKey no Web.congif.</span><span class="sxs-lookup"><span data-stu-id="848fb-143">Then copy your PRIMARY KEY value from the portal and make it the value of the accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="848fb-144">Agora, você atualizou o aplicativo com todas as informações necessárias para se comunicar com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848fb-144">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-the-web-app"></a><span data-ttu-id="848fb-145">Compilar e implantar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="848fb-145">Build and deploy the web app</span></span>

1. <span data-ttu-id="848fb-146">No Portal do Azure, crie um site do Serviço de Aplicativo para hospedar a API do agente de token de recurso.</span><span class="sxs-lookup"><span data-stu-id="848fb-146">In the Azure portal, create an App Service website to host the Resource token broker API.</span></span>
2. <span data-ttu-id="848fb-147">No Portal do Azure, abra a folha de Configurações do Aplicativo do site da API do agente de token de recurso.</span><span class="sxs-lookup"><span data-stu-id="848fb-147">In the Azure portal, open the App Settings blade of the Resource token broker API website.</span></span> <span data-ttu-id="848fb-148">Preencha as seguintes configurações de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="848fb-148">Fill in the following app settings:</span></span>

    * <span data-ttu-id="848fb-149">accountUrl – A URL da conta do Azure Cosmos DB da guia Chaves da sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848fb-149">accountUrl - The Azure Cosmos DB account URL from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="848fb-150">accountKey – A chave mestra da conta do Azure Cosmos DB da guia Chaves da sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848fb-150">accountKey - The Azure Cosmos DB account master key from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="848fb-151">databaseId e collectionId do seu banco de dados e coleção criados</span><span class="sxs-lookup"><span data-stu-id="848fb-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="848fb-152">Publique a solução ResourceTokenBroker no site criado.</span><span class="sxs-lookup"><span data-stu-id="848fb-152">Publish the ResourceTokenBroker solution to your created website.</span></span>

4. <span data-ttu-id="848fb-153">Abra o projeto do Xamarin e navegue até TodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="848fb-153">Open the Xamarin project, and navigate to TodoItemManager.cs.</span></span> <span data-ttu-id="848fb-154">Preencha os valores para accountURL, collectionId, databaseId e também para resourceTokenBrokerURL como a URL HTTPS de base para o site do agente de token de recurso.</span><span class="sxs-lookup"><span data-stu-id="848fb-154">Fill in the values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as the base https url for the resource token broker website.</span></span>

5. <span data-ttu-id="848fb-155">Conclua o tutorial [Como configurar seu aplicativo do Serviço de Aplicativo para usar o logon do Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) a fim de definir a autenticação do Facebook e configurar o site do ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="848fb-155">Complete the [How to configure your App Service application to use Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial to setup Facebook authentication and configure the ResourceTokenBroker website.</span></span>

    <span data-ttu-id="848fb-156">Execute o aplicativo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="848fb-156">Run the Xamarin app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="848fb-157">Examinar SLAs no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="848fb-157">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="848fb-158">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="848fb-158">Clean up resources</span></span>

<span data-ttu-id="848fb-159">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="848fb-159">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="848fb-160">No menu à esquerda no portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="848fb-160">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you just created.</span></span> 
2. <span data-ttu-id="848fb-161">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="848fb-161">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="848fb-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="848fb-162">Next steps</span></span>

<span data-ttu-id="848fb-163">Neste início rápido, você aprendeu a criar uma conta do Azure Cosmos DB, criar uma coleção usando o Data Explorer e compilar e implantar um aplicativo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="848fb-163">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="848fb-164">Agora, é possível importar outros dados para sua conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="848fb-164">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="848fb-165">Importar dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="848fb-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
