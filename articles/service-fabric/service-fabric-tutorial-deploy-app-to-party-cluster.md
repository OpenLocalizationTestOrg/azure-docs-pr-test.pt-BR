---
title: Implantar um aplicativo do Azure Service Fabric em um Cluster Party | Microsoft Docs
description: Saiba como implantar um aplicativo em um Cluster Party.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 6624d683edb548a65d07ab4012c599faaf940ed0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-an-application-to-a-party-cluster-in-azure"></a><span data-ttu-id="175ec-103">Implantar um aplicativo em um Cluster Party no Azure</span><span class="sxs-lookup"><span data-stu-id="175ec-103">Deploy an application to a Party Cluster in Azure</span></span>
<span data-ttu-id="175ec-104">Este tutorial é a segunda parte de uma série e mostra como implantar um aplicativo do Azure Service Fabric em um Cluster Party no Azure.</span><span class="sxs-lookup"><span data-stu-id="175ec-104">This tutorial is part two of a series and shows you how to deploy an Azure Service Fabric application to a Party Cluster in Azure.</span></span>

<span data-ttu-id="175ec-105">A segunda parte da série de tutoriais, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="175ec-105">In part two of the tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="175ec-106">Implantar um aplicativo em um cluster remoto usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="175ec-106">Deploy an application to a remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="175ec-107">Remover um aplicativo de um cluster usando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="175ec-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="175ec-108">Nesta série de tutoriais, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="175ec-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="175ec-109">Criar um aplicativo .NET do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="175ec-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="175ec-110">Implantar o aplicativo em um cluster remoto</span><span class="sxs-lookup"><span data-stu-id="175ec-110">Deploy the application to a remote cluster</span></span>
> * [<span data-ttu-id="175ec-111">Configurar CI/CD usando o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="175ec-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="175ec-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="175ec-112">Prerequisites</span></span>
<span data-ttu-id="175ec-113">Antes de começar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="175ec-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="175ec-114">Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="175ec-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="175ec-115">[Instale o Visual Studio 2017](https://www.visualstudio.com/) e instale as cargas de trabalho de **desenvolvimento do Azure** e de **desenvolvimento para a Web e ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="175ec-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="175ec-116">Instalar o SDK do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="175ec-116">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-the-voting-sample-application"></a><span data-ttu-id="175ec-117">Baixar o aplicativo de exemplo Votação</span><span class="sxs-lookup"><span data-stu-id="175ec-117">Download the Voting sample application</span></span>
<span data-ttu-id="175ec-118">Se você não tiver criado o aplicativo de exemplo Votação na [parte um esta série de tutoriais](service-fabric-tutorial-create-dotnet-app.md), poderá baixá-lo.</span><span class="sxs-lookup"><span data-stu-id="175ec-118">If you did not build the Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="175ec-119">Em uma janela de comando, execute o comando a seguir para clonar o repositório de aplicativos de exemplo no computador local.</span><span class="sxs-lookup"><span data-stu-id="175ec-119">In a command window, run the following command to clone the sample app repository to your local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="175ec-120">Configurar um Cluster Party</span><span class="sxs-lookup"><span data-stu-id="175ec-120">Set up a Party Cluster</span></span>
<span data-ttu-id="175ec-121">Os clusters Party são clusters gratuitos de duração limitada do Service Fabric, hospedados no Azure e executados pela equipe do Service Fabric, nos quais qualquer pessoa pode implantar aplicativos e aprender mais sobre a plataforma.</span><span class="sxs-lookup"><span data-stu-id="175ec-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by the Service Fabric team where anyone can deploy applications and learn about the platform.</span></span> <span data-ttu-id="175ec-122">Gratuitamente!</span><span class="sxs-lookup"><span data-stu-id="175ec-122">For free!</span></span>

<span data-ttu-id="175ec-123">Para obter acesso a um Cluster Party, navegue até este site: http://aka.ms/tryservicefabric e siga as instruções para obter acesso a um cluster.</span><span class="sxs-lookup"><span data-stu-id="175ec-123">To get access to a Party Cluster, browse to this site: http://aka.ms/tryservicefabric and follow the instructions to get access to a cluster.</span></span> <span data-ttu-id="175ec-124">Você precisa de uma conta do Facebook ou GitHub para obter acesso a um Cluster Party.</span><span class="sxs-lookup"><span data-stu-id="175ec-124">You need a Facebook or GitHub account to get access to a Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="175ec-125">Os clusters Party não são protegidos, portanto seus aplicativos e os dados que você colocar neles poderão ficar visíveis para outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="175ec-125">Party clusters are not secured, so your applications and any data you put in them may be visible to others.</span></span> <span data-ttu-id="175ec-126">Não implante nada que você não queira que outras pessoas vejam.</span><span class="sxs-lookup"><span data-stu-id="175ec-126">Don't deploy anything you don't want others to see.</span></span> <span data-ttu-id="175ec-127">Certifique-se de ler nossos Termos de Uso para conhecer todos os detalhes.</span><span class="sxs-lookup"><span data-stu-id="175ec-127">Be sure to read over our Terms of Use for all the details.</span></span>

## <a name="configure-the-listening-port"></a><span data-ttu-id="175ec-128">Configurar a porta ouvinte</span><span class="sxs-lookup"><span data-stu-id="175ec-128">Configure the listening port</span></span>
<span data-ttu-id="175ec-129">Quando o serviço de front-end VotingWeb é criado, o Visual Studio seleciona aleatoriamente uma porta para o serviço ao escutar em.</span><span class="sxs-lookup"><span data-stu-id="175ec-129">When the VotingWeb front-end service is created, Visual Studio randomly selects a port for the service to listen on.</span></span>  <span data-ttu-id="175ec-130">O serviço VotingWeb age como o front-end para este aplicativo e aceita o tráfego externo, portanto queremos associar esse serviço a uma porta fixa e bem conhecida.</span><span class="sxs-lookup"><span data-stu-id="175ec-130">The VotingWeb service acts as the front-end for this application and accepts external traffic, so let's bind that service to a fixed and well-know port.</span></span> <span data-ttu-id="175ec-131">No Gerenciador de Soluções, abra *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="175ec-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="175ec-132">Localizar o **ponto de extremidade** recurso o **recursos** seção e altere o **porta** valor como 80.</span><span class="sxs-lookup"><span data-stu-id="175ec-132">Find the **Endpoint** resource in the **Resources** section and change the **Port** value to 80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="175ec-133">Também atualize o valor da propriedade URL do aplicativo no projeto de voto para que um navegador da web abre a porta correta ao depurar usando 'F5'.</span><span class="sxs-lookup"><span data-stu-id="175ec-133">Also update the Application URL property value in the Voting project so a web browser opens to the correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="175ec-134">No Gerenciador de Soluções, selecione o **votação** projeto e atualize o **URL do aplicativo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="175ec-134">In Solution Explorer, select the **Voting** project and update the **Application URL** property.</span></span>

![URL do Aplicativo](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-the-app-to-the-azure"></a><span data-ttu-id="175ec-136">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="175ec-136">Deploy the app to the Azure</span></span>
<span data-ttu-id="175ec-137">Agora que o aplicativo está pronto, você pode implantá-lo no Cluster Party diretamente do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="175ec-137">Now that the application is ready, you can deploy it to the Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="175ec-138">Clique com o botão direito do mouse em **Votação** no Gerenciador de Soluções e escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="175ec-138">Right-click **Voting** in the Solution Explorer and choose **Publish**.</span></span>

    ![Caixa de diálogo Publicar](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="175ec-140">Digite o ponto de extremidade de conexão do Cluster Party no campo **Ponto de Extremidade de Conexão** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="175ec-140">Type in the Connection Endpoint of the Party Cluster in the **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="175ec-141">Depois que a publicação for concluída, você poderá enviar uma solicitação ao aplicativo por meio de um navegador.</span><span class="sxs-lookup"><span data-stu-id="175ec-141">Once the publish has finished, you should be able to send a request to the application via a browser.</span></span>

3. <span data-ttu-id="175ec-142">Abra o navegador de sua preferência e digite o endereço do cluster (o ponto de extremidade de conexão sem as informações de porta – por exemplo, win1kw5649s.westus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="175ec-142">Open you preferred browser and type in the cluster address (the connection endpoint without the port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="175ec-143">Agora você verá o mesmo resultado que viu ao executar o aplicativo localmente.</span><span class="sxs-lookup"><span data-stu-id="175ec-143">You should now see the same result as you saw when running the application locally.</span></span>

    ![Resposta de API do Cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-the-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="175ec-145">Remover o aplicativo de um cluster usando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="175ec-145">Remove the application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="175ec-146">O Service Fabric Explorer é uma interface gráfica do usuário para explorar e gerenciar aplicativos em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="175ec-146">Service Fabric Explorer is a graphical user interface to explore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="175ec-147">Para remover o aplicativo Cluster de Terceiros:</span><span class="sxs-lookup"><span data-stu-id="175ec-147">To remove the application from the Party Cluster:</span></span>

1. <span data-ttu-id="175ec-148">Navegue até o Service Fabric Explorer usando o link fornecido pela página de entrada do Cluster Party.</span><span class="sxs-lookup"><span data-stu-id="175ec-148">Browse to the Service Fabric Explorer, using the link provided by the Party Cluster sign-up page.</span></span> <span data-ttu-id="175ec-149">Por exemplo, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="175ec-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="175ec-150">No Service Fabric Explorer, navegue até o nó **fabric://Voting** no modo de exibição em árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="175ec-150">In Service Fabric Explorer, navigate to the **fabric://Voting** node in the treeview on the left-hand side.</span></span>

3. <span data-ttu-id="175ec-151">Clique no botão **Ação** à direita do painel **Essentials** e escolha **Excluir Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="175ec-151">Click the **Action** button in the right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="175ec-152">Confirme a exclusão da instância do aplicativo, que removerá a instância do nosso aplicativo que estava em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="175ec-152">Confirm deleting the application instance, which removes the instance of our application running in the cluster.</span></span>

![Excluir aplicativo no Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-the-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="175ec-154">Remover o tipo de aplicativo de um cluster usando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="175ec-154">Remove the application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="175ec-155">Os aplicativos são implantados como tipos de aplicativos em um cluster do Service Fabric, o que permite que você tenha várias instâncias e versões do aplicativo em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="175ec-155">Applications are deployed as application types in a Service Fabric cluster, which enables you to have multiple instances and versions of the application running within the cluster.</span></span> <span data-ttu-id="175ec-156">Depois de ter removido a instância em execução do nosso aplicativo, também podemos remover o tipo, para concluir a limpeza da implantação.</span><span class="sxs-lookup"><span data-stu-id="175ec-156">After having removed the running instance of our application, we can also remove the type, to complete the cleanup of the deployment.</span></span>

<span data-ttu-id="175ec-157">Para obter mais informações sobre o modelo de aplicativo no Service Fabric, consulte [Modelar um aplicativo no Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="175ec-157">For more information about the application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="175ec-158">Navegue até o nó **VotingType** no modo de exibição de árvore.</span><span class="sxs-lookup"><span data-stu-id="175ec-158">Navigate to the **VotingType** node in the treeview.</span></span>

2. <span data-ttu-id="175ec-159">Clique no botão **Ação** à direita do painel **Essentials** e escolha **Desprovisionar o Tipo**.</span><span class="sxs-lookup"><span data-stu-id="175ec-159">Click the **Action** button in the right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="175ec-160">Confirme o desprovisionamento do tipo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="175ec-160">Confirm unprovisioning the application type.</span></span>

![Desprovisionar o tipo do aplicativo Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="175ec-162">Isso conclui o tutorial.</span><span class="sxs-lookup"><span data-stu-id="175ec-162">This concludes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="175ec-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="175ec-163">Next steps</span></span>
<span data-ttu-id="175ec-164">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="175ec-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="175ec-165">Implantar um aplicativo em um cluster remoto usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="175ec-165">Deploy an application to a remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="175ec-166">Remover um aplicativo de um cluster usando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="175ec-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="175ec-167">Prosseguir para o próximo tutorial:</span><span class="sxs-lookup"><span data-stu-id="175ec-167">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="175ec-168">Configurar a integração contínua usando o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="175ec-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)