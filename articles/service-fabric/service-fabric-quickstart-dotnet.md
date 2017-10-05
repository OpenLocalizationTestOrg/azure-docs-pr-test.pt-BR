---
title: Criar um aplicativo .NET do Service Fabric no Azure | Microsoft Docs
description: "Crie um aplicativo .NET para o Azure usando a amostra de início rápido do Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: d11b9af982112db8ba94b62110c18be843f1abb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="e90fa-103">Criar um aplicativo .NET do Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="e90fa-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="e90fa-104">O Azure Service Fabric é uma plataforma de sistemas distribuídos para implantação e gerenciamento de contêineres e microsserviços escalonáveis e confiáveis.</span><span class="sxs-lookup"><span data-stu-id="e90fa-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="e90fa-105">Este guia de início rápido mostra como implantar seu primeiro aplicativo .NET no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e90fa-105">This quickstart shows how to deploy your first .NET application to Service Fabric.</span></span> <span data-ttu-id="e90fa-106">Quando terminar, você terá um aplicativo de votação com um front-end da Web do ASP.NET Core que salva os resultados da votação em um serviço de back-end com estado do cluster.</span><span class="sxs-lookup"><span data-stu-id="e90fa-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span>

![Captura de tela do aplicativo](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="e90fa-108">Com esse aplicativo, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="e90fa-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e90fa-109">Criar um aplicativo usando o .NET e o Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e90fa-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="e90fa-110">Usar o ASP.NET Core como um front-end da Web</span><span class="sxs-lookup"><span data-stu-id="e90fa-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="e90fa-111">Armazenar dados de aplicativo em um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="e90fa-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="e90fa-112">Depurar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="e90fa-112">Debug your application locally</span></span>
> * <span data-ttu-id="e90fa-113">Implantar o aplicativo em um cluster no Azure</span><span class="sxs-lookup"><span data-stu-id="e90fa-113">Deploy the application to a cluster in Azure</span></span>
> * <span data-ttu-id="e90fa-114">Expandir o aplicativo para vários nós</span><span class="sxs-lookup"><span data-stu-id="e90fa-114">Scale-out the application across multiple nodes</span></span>
> * <span data-ttu-id="e90fa-115">Executar um upgrade sem interrupção do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e90fa-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e90fa-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e90fa-116">Prerequisites</span></span>
<span data-ttu-id="e90fa-117">Para concluir este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="e90fa-117">To complete this quickstart:</span></span>
1. <span data-ttu-id="e90fa-118">[Instale o Visual Studio 2017](https://www.visualstudio.com/) com as cargas de trabalho de **desenvolvimento do Azure** e de **desenvolvimento para a Web e ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with the **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. [<span data-ttu-id="e90fa-119">Instalar o Git</span><span class="sxs-lookup"><span data-stu-id="e90fa-119">Install Git</span></span>](https://git-scm.com/)
3. [<span data-ttu-id="e90fa-120">Instalar o SDK do Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e90fa-120">Install the Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="e90fa-121">Execute o seguinte comando para habilitar o Visual Studio a implantar no cluster local do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="e90fa-121">Run the following command to enable Visual Studio to deploy to the local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-the-sample"></a><span data-ttu-id="e90fa-122">Baixar o exemplo</span><span class="sxs-lookup"><span data-stu-id="e90fa-122">Download the sample</span></span>
<span data-ttu-id="e90fa-123">Em uma janela de comando, execute o comando a seguir para clonar o repositório de aplicativos de exemplo no computador local.</span><span class="sxs-lookup"><span data-stu-id="e90fa-123">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-the-application-locally"></a><span data-ttu-id="e90fa-124">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="e90fa-124">Run the application locally</span></span>
<span data-ttu-id="e90fa-125">Clique com o botão direito do mouse no ícone do Visual Studio no Menu Iniciar e escolha **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-125">Right-click the Visual Studio icon in the Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="e90fa-126">Para anexar o depurador aos serviços, você precisa executar o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="e90fa-126">In order to attach the debugger to your services, you need to run Visual Studio as administrator.</span></span>

<span data-ttu-id="e90fa-127">Abra a solução **Voting.sln** do Visual Studio no repositório clonado.</span><span class="sxs-lookup"><span data-stu-id="e90fa-127">Open the **Voting.sln** Visual Studio solution from the repository you cloned.</span></span>

<span data-ttu-id="e90fa-128">Para implantar o aplicativo, pressione **F5**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-128">To deploy the application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="e90fa-129">Na primeira vez que você executar e implantar o aplicativo, o Visual Studio cria um cluster local para depuração.</span><span class="sxs-lookup"><span data-stu-id="e90fa-129">The first time you run and deploy the application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="e90fa-130">Essa operação pode levar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="e90fa-130">This operation may take some time.</span></span> <span data-ttu-id="e90fa-131">O status de criação do cluster é exibido na janela de saída do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e90fa-131">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="e90fa-132">Quando a implantação for concluída, inicie um navegador e abra esta página: `http://localhost:8080` – o front-end da Web do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e90fa-132">When the deployment is complete, launch a browser and open this page: `http://localhost:8080` - the web front-end of the application.</span></span>

![Front-end do aplicativo](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="e90fa-134">Agora, você pode adicionar um conjunto de opções de votação e começar a votar.</span><span class="sxs-lookup"><span data-stu-id="e90fa-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="e90fa-135">O aplicativo é executado e armazena todos os dados no cluster do Service Fabric, sem a necessidade de um banco de dados separado.</span><span class="sxs-lookup"><span data-stu-id="e90fa-135">The application runs and stores all data in your Service Fabric cluster, without the need for a separate database.</span></span>

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="e90fa-136">Percorrer o aplicativo de exemplo de votação</span><span class="sxs-lookup"><span data-stu-id="e90fa-136">Walk through the voting sample application</span></span>
<span data-ttu-id="e90fa-137">O aplicativo de votação consiste em dois serviços:</span><span class="sxs-lookup"><span data-stu-id="e90fa-137">The voting application consists of two services:</span></span>
- <span data-ttu-id="e90fa-138">Serviço de front-end da Web (VotingWeb) – um serviço de front-end da Web do ASP.NET Core, que fornece a página da Web e expõe APIs Web para se comunicar com o serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="e90fa-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="e90fa-139">Serviço de back-end (VotingData) – um serviço Web do ASP.NET Core, que expõe uma API para armazenar os resultados da votação em um dicionário confiável persistido em disco.</span><span class="sxs-lookup"><span data-stu-id="e90fa-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![Diagrama de aplicativo](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="e90fa-141">Quando você vota no aplicativo, os seguintes eventos ocorrem:</span><span class="sxs-lookup"><span data-stu-id="e90fa-141">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="e90fa-142">Um JavaScript envia a solicitação de votação para a API Web no serviço de front-end da Web como uma solicitação HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="e90fa-142">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="e90fa-143">O serviço de front-end da Web usa um proxy para localizar e encaminhar uma solicitação HTTP PUT para o serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="e90fa-143">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="e90fa-144">O serviço de back-end recebe a solicitação de entrada e armazena o resultado atualizado em um dicionário confiável, que é replicado em vários nós no cluster e persistido em disco.</span><span class="sxs-lookup"><span data-stu-id="e90fa-144">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="e90fa-145">Todos os dados do aplicativo são armazenados no cluster e, portanto, nenhum banco de dados é necessário.</span><span class="sxs-lookup"><span data-stu-id="e90fa-145">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="e90fa-146">Depuração no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e90fa-146">Debug in Visual Studio</span></span>
<span data-ttu-id="e90fa-147">Ao depurar o aplicativo no Visual Studio, você usa um cluster de desenvolvimento local do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e90fa-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="e90fa-148">Você tem a opção de ajustar sua experiência de depuração para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="e90fa-148">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="e90fa-149">Neste aplicativo, armazenamos dados em nosso serviço de back-end, usando um dicionário confiável.</span><span class="sxs-lookup"><span data-stu-id="e90fa-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="e90fa-150">O Visual Studio remove o aplicativo por padrão quando você interrompe o depurador.</span><span class="sxs-lookup"><span data-stu-id="e90fa-150">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="e90fa-151">A remoção do aplicativo faz com que os dados no serviço de back-end também sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="e90fa-151">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="e90fa-152">Para persistir os dados entre as sessões de depuração, altere o **Modo de Depuração de Aplicativo** como uma propriedade no projeto **Votação** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e90fa-152">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="e90fa-153">Para ver o que acontece no código, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e90fa-153">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="e90fa-154">Abra o arquivo **VotesController.cs** e defina um ponto de interrupção no método **Put** da API Web (linha 47). Pesquise o arquivo no Gerenciador de Soluções no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e90fa-154">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="e90fa-155">Abra o arquivo **VoteDataController.cs** e defina um ponto de interrupção no método **Put** dessa API Web (linha 50).</span><span class="sxs-lookup"><span data-stu-id="e90fa-155">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="e90fa-156">Volte para o navegador e clique em uma opção de votação ou adicione uma nova opção de votação.</span><span class="sxs-lookup"><span data-stu-id="e90fa-156">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="e90fa-157">Você chegou ao primeiro ponto de interrupção no controlador de API do front-end da Web.</span><span class="sxs-lookup"><span data-stu-id="e90fa-157">You hit the first breakpoint in the web front-end's api controller.</span></span>
    - <span data-ttu-id="e90fa-158">Esse é o local em que o JavaScript no navegador envia uma solicitação para o controlador da API Web no serviço de front-end.</span><span class="sxs-lookup"><span data-stu-id="e90fa-158">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![Adicionar Serviço de Front-end de Voto](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="e90fa-160">Primeiro, construímos a URL para o ReverseProxy para nosso serviço de back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-160">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="e90fa-161">Então, podemos enviar a Solicitação PUT HTTP para o ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-161">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="e90fa-162">Por fim, retornamos a resposta do serviço de back-end para o cliente **(3)**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-162">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="e90fa-163">Pressione **F5** para continuar</span><span class="sxs-lookup"><span data-stu-id="e90fa-163">Press **F5** to continue</span></span>
    - <span data-ttu-id="e90fa-164">Agora você está no ponto de interrupção no serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="e90fa-164">You are now at the break point in the back-end service.</span></span>
    
    ![Adicionar Serviço de Back-End de Voto](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="e90fa-166">Na primeira linha do método **(1)**, estamos usando o `StateManager` para obter ou adicionar um dicionário confiável chamado `counts`.</span><span class="sxs-lookup"><span data-stu-id="e90fa-166">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="e90fa-167">Todas as interações com valores em um dicionário confiável exigem uma transação e, portanto, o uso da instrução **(2)** cria essa transação.</span><span class="sxs-lookup"><span data-stu-id="e90fa-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="e90fa-168">Na transação, depois, atualizamos o valor da chave relevante para a opção de votação e confirmamos a operação **(3)**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-168">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="e90fa-169">Depois que o método de confirmação for retornado, os dados serão atualizados no dicionário e replicados em outros nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="e90fa-169">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="e90fa-170">Os dados agora estão armazenados com segurança no cluster e o serviço de back-end pode fazer failover para outros nós, ainda tendo os dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e90fa-170">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="e90fa-171">Pressione **F5** para continuar</span><span class="sxs-lookup"><span data-stu-id="e90fa-171">Press **F5** to continue</span></span>

<span data-ttu-id="e90fa-172">Para interromper a sessão de depuração, pressione **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-172">To stop the debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="e90fa-173">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="e90fa-173">Deploy the application to Azure</span></span>
<span data-ttu-id="e90fa-174">Para implantar o aplicativo em um cluster do Azure, você pode optar por criar seu próprio cluster ou usar um Cluster de Entidade.</span><span class="sxs-lookup"><span data-stu-id="e90fa-174">To deploy the application to a cluster in Azure, you can either choose to create your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="e90fa-175">Os clusters de entidade são clusters gratuitos de duração limitada do Service Fabric, hospedados no Azure e executados pela equipe do Service Fabric, nos quais qualquer pessoa pode implantar aplicativos e aprender mais sobre a plataforma.</span><span class="sxs-lookup"><span data-stu-id="e90fa-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by the Service Fabric team where anyone can deploy applications and learn about the platform.</span></span> <span data-ttu-id="e90fa-176">Para obter acesso a um Cluster de Terceiros, [siga as instruções](http://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="e90fa-176">To get access to a Party Cluster, [follow the instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="e90fa-177">Para obter informações sobre como criar seu próprio cluster, consulte [Criar seu primeiro cluster do Service Fabric no Azure](service-fabric-get-started-azure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e90fa-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="e90fa-178">O serviço de front-end da Web está configurado para escutar o tráfego de entrada na porta 8080.</span><span class="sxs-lookup"><span data-stu-id="e90fa-178">The web front-end service is configured to listen on port 8080 for incoming traffic.</span></span> <span data-ttu-id="e90fa-179">Verifique se a porta está aberta no cluster.</span><span class="sxs-lookup"><span data-stu-id="e90fa-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="e90fa-180">Se você estiver usando o Cluster de Entidade, essa porta estará aberta.</span><span class="sxs-lookup"><span data-stu-id="e90fa-180">If you are using the Party Cluster, this port is open.</span></span>
>

### <a name="deploy-the-application-using-visual-studio"></a><span data-ttu-id="e90fa-181">Implantar o aplicativo usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e90fa-181">Deploy the application using Visual Studio</span></span>
<span data-ttu-id="e90fa-182">Agora que o aplicativo está pronto, você poderá implantá-lo no cluster diretamente por meio do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e90fa-182">Now that the application is ready, you can deploy it to a cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="e90fa-183">Clique com o botão direito do mouse em **Votação** no Gerenciador de Soluções e escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-183">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="e90fa-184">A caixa de diálogo Publicar será exibida.</span><span class="sxs-lookup"><span data-stu-id="e90fa-184">The Publish dialog appears.</span></span>

    ![Caixa de diálogo Publicar](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="e90fa-186">Digite o Ponto de Extremidade de Conexão do cluster no campo **Ponto de Extremidade de Conexão** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-186">Type in the Connection Endpoint of the cluster in the **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="e90fa-187">Ao se inscrever no Cluster de Entidade, o Ponto de Extremidade de Conexão será fornecido no navegador.</span><span class="sxs-lookup"><span data-stu-id="e90fa-187">When signing up for the Party Cluster, the Connection Endpoint is provided in the browser.</span></span> <span data-ttu-id="e90fa-188">– por exemplo, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span><span class="sxs-lookup"><span data-stu-id="e90fa-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="e90fa-189">Abra um navegador e digite o endereço do cluster – por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="e90fa-189">Open a browser and type in the cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="e90fa-190">Agora, você deverá ver o aplicativo em execução no cluster no Azure.</span><span class="sxs-lookup"><span data-stu-id="e90fa-190">You should now see the application running in the cluster in Azure.</span></span>

![Front-end do aplicativo](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="e90fa-192">Dimensionar aplicativos e serviços em um cluster</span><span class="sxs-lookup"><span data-stu-id="e90fa-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="e90fa-193">Os serviços do Service Fabric podem ser facilmente dimensionados em um cluster para acomodar uma alteração na carga dos serviços.</span><span class="sxs-lookup"><span data-stu-id="e90fa-193">Service Fabric services can easily be scaled across a cluster to accommodate for a change in the load on the services.</span></span> <span data-ttu-id="e90fa-194">Dimensione um serviço alterando o número de instâncias em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="e90fa-194">You scale a service by changing the number of instances running in the cluster.</span></span> <span data-ttu-id="e90fa-195">Você tem vários modos de dimensionar seus serviços usando scripts ou comandos do PowerShell ou a CLI do Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="e90fa-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="e90fa-196">Neste exemplo, estamos usando o Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e90fa-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="e90fa-197">O Service Fabric Explorer é executado em todos os clusters do Service Fabric e pode ser acessado em um navegador, navegando para a porta de gerenciamento HTTP dos de clusters (19080), por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="e90fa-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing to the clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="e90fa-198">Para dimensionar o serviço de front-end da Web, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e90fa-198">To scale the web front-end service, do the following steps:</span></span>

1. <span data-ttu-id="e90fa-199">Abra o Service Fabric Explorer no cluster – por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="e90fa-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="e90fa-200">Clique nas reticências (três pontos) ao lado do nó **fabric:/Voting/VotingWeb** no modo de exibição de árvore e escolha **Dimensionar Serviço**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-200">Click on the ellipsis (three dots) next to the **fabric:/Voting/VotingWeb** node in the treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="e90fa-202">Agora, você pode optar por dimensionar o número de instâncias do serviço de front-end da Web.</span><span class="sxs-lookup"><span data-stu-id="e90fa-202">You can now choose to scale the number of instances of the web front-end service.</span></span>

3. <span data-ttu-id="e90fa-203">Altere o número para **2** e clique em **Dimensionar Serviço**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-203">Change the number to **2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="e90fa-204">Clique no nó **fabric:/Voting/VotingWeb** do modo de exibição de árvore e expanda o nó de partição (representado por um GUID).</span><span class="sxs-lookup"><span data-stu-id="e90fa-204">Click on the **fabric:/Voting/VotingWeb** node in the tree-view and expand the partition node (represented by a GUID).</span></span>

    ![Dimensionar Serviço do Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="e90fa-206">Agora, você pode ver que o serviço tem duas instâncias e no modo de exibição de árvore, você vê em quais nós as instâncias são executadas.</span><span class="sxs-lookup"><span data-stu-id="e90fa-206">You can now see that the service has two instances, and in the tree view you see which nodes the instances run on.</span></span>

<span data-ttu-id="e90fa-207">Com essa tarefa de gerenciamento simples, dobramos o número de recursos disponíveis para nosso serviço de front-end para processar a carga do usuário.</span><span class="sxs-lookup"><span data-stu-id="e90fa-207">By this simple management task, we doubled the resources available for our front-end service to process user load.</span></span> <span data-ttu-id="e90fa-208">É importante entender que você não precisa de várias instâncias de um serviço para que ele seja executado de forma confiável.</span><span class="sxs-lookup"><span data-stu-id="e90fa-208">It's important to understand that you do not need multiple instances of a service to have it run reliably.</span></span> <span data-ttu-id="e90fa-209">Se um serviço falhar, o Service Fabric garantirá que uma nova instância de serviço seja executada no cluster.</span><span class="sxs-lookup"><span data-stu-id="e90fa-209">If a service fails, Service Fabric makes sure a new service instance runs in the cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="e90fa-210">Executar um upgrade sem interrupção do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e90fa-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="e90fa-211">Ao implantar novas atualizações no aplicativo, o Service Fabric distribui a atualização com segurança.</span><span class="sxs-lookup"><span data-stu-id="e90fa-211">When deploying new updates to your application, Service Fabric rolls out the update in a safe way.</span></span> <span data-ttu-id="e90fa-212">As atualizações sem interrupção fornecem tempo de inatividade zero durante a atualização, bem como a reversão automática no caso de erros.</span><span class="sxs-lookup"><span data-stu-id="e90fa-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="e90fa-213">Para fazer upgrade do aplicativo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e90fa-213">To upgrade the application, do the following:</span></span>

1. <span data-ttu-id="e90fa-214">Abra o arquivo **Index.cshtml** no Visual Studio – pesquise o arquivo no Gerenciador de Soluções no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e90fa-214">Open the **Index.cshtml** file in Visual Studio - You can search for the file in the Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="e90fa-215">Altere o cabeçalho da página adicionando um texto – por exemplo.</span><span class="sxs-lookup"><span data-stu-id="e90fa-215">Change the heading on the page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="e90fa-216">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e90fa-216">Save the file.</span></span>
4. <span data-ttu-id="e90fa-217">Clique com o botão direito do mouse em **Votação** no Gerenciador de Soluções e escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-217">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="e90fa-218">A caixa de diálogo Publicar será exibida.</span><span class="sxs-lookup"><span data-stu-id="e90fa-218">The Publish dialog appears.</span></span>
5. <span data-ttu-id="e90fa-219">Clique no botão **Versão do Manifesto** para alterar a versão do serviço e do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e90fa-219">Click the **Manifest Version** button to change the version of the service and application.</span></span>
6. <span data-ttu-id="e90fa-220">Altere a versão do elemento **Código** sob **VotingWebPkg** para “2.0.0”, por exemplo, e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-220">Change the version of the **Code** element under **VotingWebPkg** to "2.0.0", for example, and click **Save**.</span></span>

    ![Caixa de diálogo Alterar Versão](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="e90fa-222">Na caixa de diálogo **Publicar Aplicativo do Service Fabric**, marque a caixa de seleção Fazer Upgrade do Aplicativo e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="e90fa-222">In the **Publish Service Fabric Application** dialog, check the Upgrade the Application checkbox, and click **Publish**.</span></span>

    ![Configuração de Upgrade da caixa de diálogo Publicar](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="e90fa-224">Abra o navegador e navegue para o endereço do cluster na porta 19080 – por exemplo, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="e90fa-224">Open your browser and browse to the cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="e90fa-225">Clique no nó **Aplicativos** do modo de exibição de árvore e, em seguida, em **Upgrades em Andamento** no painel à direita.</span><span class="sxs-lookup"><span data-stu-id="e90fa-225">Click on the **Applications** node in the tree view, and then **Upgrades in Progress** in the right-hand pane.</span></span> <span data-ttu-id="e90fa-226">Você verá como o upgrade é distribuído pelos domínios de upgrade no cluster, garantindo que cada domínio está íntegro antes de continuar com o próximo.</span><span class="sxs-lookup"><span data-stu-id="e90fa-226">You see how the upgrade rolls through the upgrade domains in your cluster, making sure each domain is healthy before proceeding to the next.</span></span>
    <span data-ttu-id="e90fa-227">![Modo de Exibição de Upgrade no Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="e90fa-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="e90fa-228">O Service Fabric faz upgrades com segurança, aguardando dois minutos após o upgrade do serviço em cada nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="e90fa-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading the service on each node in the cluster.</span></span> <span data-ttu-id="e90fa-229">Espere que toda a atualização leve aproximadamente oito minutos.</span><span class="sxs-lookup"><span data-stu-id="e90fa-229">Expect the entire update to take approximately eight minutes.</span></span>

10. <span data-ttu-id="e90fa-230">Enquanto o upgrade está em execução, você ainda poderá usar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e90fa-230">While the upgrade is running, you can still use the application.</span></span> <span data-ttu-id="e90fa-231">Como você tem duas instâncias do serviço em execução no cluster, algumas das solicitações poderão obter uma versão atualizada do aplicativo, enquanto outras ainda poderão obter a versão antiga.</span><span class="sxs-lookup"><span data-stu-id="e90fa-231">Because you have two instances of the service running in the cluster, some of your requests may get an upgraded version of the application, while others may still get the old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e90fa-232">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e90fa-232">Next steps</span></span>
<span data-ttu-id="e90fa-233">Neste guia de início rápido, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="e90fa-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e90fa-234">Criar um aplicativo usando o .NET e o Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e90fa-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="e90fa-235">Usar o ASP.NET Core como um front-end da Web</span><span class="sxs-lookup"><span data-stu-id="e90fa-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="e90fa-236">Armazenar dados de aplicativo em um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="e90fa-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="e90fa-237">Depurar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="e90fa-237">Debug your application locally</span></span>
> * <span data-ttu-id="e90fa-238">Implantar o aplicativo em um cluster no Azure</span><span class="sxs-lookup"><span data-stu-id="e90fa-238">Deploy the application to a cluster in Azure</span></span>
> * <span data-ttu-id="e90fa-239">Expandir o aplicativo para vários nós</span><span class="sxs-lookup"><span data-stu-id="e90fa-239">Scale-out the application across multiple nodes</span></span>
> * <span data-ttu-id="e90fa-240">Executar um upgrade sem interrupção do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e90fa-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="e90fa-241">Para saber mais sobre o Service Fabric e o .NET, confira este tutorial:</span><span class="sxs-lookup"><span data-stu-id="e90fa-241">To learn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e90fa-242">Aplicativo .NET no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e90fa-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)