---
title: Implantar rapidamente um aplicativo existente em um cluster do Azure Service Fabric
description: Use um cluster do Azure Service Fabric para hospedar um aplicativo Node.js existente com o Visual Studio.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 3601b73872bbea4b4e5324382eb97b7384ca6e13
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="e3744-103">Hospedar um aplicativo Node.js no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e3744-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="e3744-104">Este guia de início rápido ajuda a implantar um aplicativo existente (Node.js neste exemplo) em um cluster do Service Fabric em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3744-104">This quickstart helps you deploy an existing application (Node.js in this example) to a Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3744-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3744-105">Prerequisites</span></span>

<span data-ttu-id="e3744-106">Antes de começar, verifique se você [configurou o ambiente de desenvolvimento](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e3744-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="e3744-107">O que inclui instalar o SDK do Service Fabric e o Visual Studio 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="e3744-107">Which includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="e3744-108">Você também precisa ter um aplicativo Node.js existente para a implantação.</span><span class="sxs-lookup"><span data-stu-id="e3744-108">You also need to have an existing Node.js application for deployment.</span></span> <span data-ttu-id="e3744-109">Este guia de início rápido usa um site Node.js simples que pode ser baixado [aqui][download-sample].</span><span class="sxs-lookup"><span data-stu-id="e3744-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="e3744-110">Extraia esse arquivo para a pasta `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` depois de criar o projeto na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e3744-110">Extract this file to your `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create the project in the next step.</span></span>

<span data-ttu-id="e3744-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita][create-account].</span><span class="sxs-lookup"><span data-stu-id="e3744-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-the-service"></a><span data-ttu-id="e3744-112">Criar o serviço</span><span class="sxs-lookup"><span data-stu-id="e3744-112">Create the service</span></span>

<span data-ttu-id="e3744-113">Inicie o Visual Studio como um **administrador**.</span><span class="sxs-lookup"><span data-stu-id="e3744-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="e3744-114">Criar um projeto com `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="e3744-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="e3744-115">No diálogo **Novo Projeto**, escolha **Cloud > Aplicativo do Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="e3744-115">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="e3744-116">Nomeie o aplicativo **MyGuestApp** e pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3744-116">Name the application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="e3744-117">O Node.js pode interromper o limite de 260 caracteres para caminhos do Windows facilmente.</span><span class="sxs-lookup"><span data-stu-id="e3744-117">Node.js can easily break the 260 character limit for paths that windows has.</span></span> <span data-ttu-id="e3744-118">Use um caminho curto para o projeto, como **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="e3744-118">Use a short path for the project itself such as **c:\code\svc1**.</span></span>
   
![Caixa de diálogo Novo projeto no Visual Studio][new-project]

<span data-ttu-id="e3744-120">Você pode criar qualquer tipo de serviço Service Fabric na próxima caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3744-120">You can create any type of Service Fabric service from the next dialog.</span></span> <span data-ttu-id="e3744-121">Para este guia de início rápido, escolha **Executável Convidado**.</span><span class="sxs-lookup"><span data-stu-id="e3744-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="e3744-122">Nomeie o serviço **MyGuestService** e defina as opções à direita com os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="e3744-122">Name the service **MyGuestService** and set the options on the right to the following values:</span></span>

| <span data-ttu-id="e3744-123">Configuração</span><span class="sxs-lookup"><span data-stu-id="e3744-123">Setting</span></span>                   | <span data-ttu-id="e3744-124">Valor</span><span class="sxs-lookup"><span data-stu-id="e3744-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="e3744-125">Pasta do Pacote de Código</span><span class="sxs-lookup"><span data-stu-id="e3744-125">Code Package Folder</span></span>       | <span data-ttu-id="e3744-126">_&lt;a pasta com seu aplicativo Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="e3744-126">_&lt;the folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="e3744-127">Comportamento do Pacote de Código</span><span class="sxs-lookup"><span data-stu-id="e3744-127">Code Package Behavior</span></span>     | <span data-ttu-id="e3744-128">Copiar o conteúdo da pasta para o projeto</span><span class="sxs-lookup"><span data-stu-id="e3744-128">Copy folder contents to project</span></span> |
| <span data-ttu-id="e3744-129">Programa</span><span class="sxs-lookup"><span data-stu-id="e3744-129">Program</span></span>                   | <span data-ttu-id="e3744-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="e3744-130">node.exe</span></span> |
| <span data-ttu-id="e3744-131">Argumentos</span><span class="sxs-lookup"><span data-stu-id="e3744-131">Arguments</span></span>                 | <span data-ttu-id="e3744-132">server.js</span><span class="sxs-lookup"><span data-stu-id="e3744-132">server.js</span></span> |
| <span data-ttu-id="e3744-133">Pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="e3744-133">Working Folder</span></span>            | <span data-ttu-id="e3744-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="e3744-134">CodePackage</span></span> |

<span data-ttu-id="e3744-135">Pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3744-135">Press **OK**.</span></span>

![Caixa de diálogo Novo serviço no Visual Studio][new-service]

<span data-ttu-id="e3744-137">O Visual Studio cria o projeto de aplicativo e o projeto de serviço ator e os exibe no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="e3744-137">Visual Studio creates the application project and the actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="e3744-138">O projeto de aplicativo (**MyGuestApp**) não contém qualquer código diretamente.</span><span class="sxs-lookup"><span data-stu-id="e3744-138">The application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="e3744-139">Em vez disso, ele faz referência a um conjunto de projetos de serviço.</span><span class="sxs-lookup"><span data-stu-id="e3744-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="e3744-140">Além disso, ele contém três outros tipos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="e3744-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="e3744-141">**Perfis de publicação**</span><span class="sxs-lookup"><span data-stu-id="e3744-141">**Publish profiles**</span></span>  
<span data-ttu-id="e3744-142">Preferências de ferramentas para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="e3744-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="e3744-143">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="e3744-143">**Scripts**</span></span>  
<span data-ttu-id="e3744-144">Script do PowerShell para a implantação/atualização de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3744-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="e3744-145">**Definição de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="e3744-145">**Application definition**</span></span>  
<span data-ttu-id="e3744-146">Inclui o manifesto do aplicativo em *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="e3744-146">Includes the application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="e3744-147">Os arquivos de parâmetros do aplicativo associados estão em *ApplicationParameters*, que definem o aplicativo e permitem que você o configure especificamente para determinado ambiente.</span><span class="sxs-lookup"><span data-stu-id="e3744-147">Associated application parameter files are under *ApplicationParameters*, which define the application and allow you to configure it specifically for a given environment.</span></span>
    
<span data-ttu-id="e3744-148">Para obter uma visão geral do conteúdo do projeto de serviço, confira [Introdução aos Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="e3744-148">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="e3744-149">Configurar a rede</span><span class="sxs-lookup"><span data-stu-id="e3744-149">Set up networking</span></span>

<span data-ttu-id="e3744-150">O exemplo de aplicativo Node.js que estamos implantando usa a porta **80**, e precisamos dizer ao Service Fabric que precisamos dessa porta exposta.</span><span class="sxs-lookup"><span data-stu-id="e3744-150">The example Node.js app we're deploying uses port **80** and we need to tell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="e3744-151">Abra o arquivo **ServiceManifest.xml** no projeto.</span><span class="sxs-lookup"><span data-stu-id="e3744-151">Open the **ServiceManifest.xml** file in the project.</span></span> <span data-ttu-id="e3744-152">Na parte inferior do manifesto, há `<Resources> \ <Endpoints>` com uma entrada já definida.</span><span class="sxs-lookup"><span data-stu-id="e3744-152">At the bottom of the manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="e3744-153">Modifique a entrada para adicionar `Port`, `Protocol` e `Type`.</span><span class="sxs-lookup"><span data-stu-id="e3744-153">Modify that entry to add `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-to-azure"></a><span data-ttu-id="e3744-154">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="e3744-154">Deploy to Azure</span></span>

<span data-ttu-id="e3744-155">Se você pressionar **F5** e executar o projeto, ele será implantado no cluster local.</span><span class="sxs-lookup"><span data-stu-id="e3744-155">If you press **F5** and run the project, it is deployed to the local cluster.</span></span> <span data-ttu-id="e3744-156">No entanto, vamos implantar no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3744-156">However, let's deploy to Azure instead.</span></span>

<span data-ttu-id="e3744-157">Clique com botão direito do mouse no projeto e escolha **Publicar...**  para abrir um diálogo Publicar no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3744-157">Right-click on the project and choose **Publish...** which opens a dialog to publish to Azure.</span></span>

![Diálogo Publicar no Azure para um serviço Service Fabric][publish]

<span data-ttu-id="e3744-159">Selecione o perfil de destino **PublishProfiles\Cloud.xml**.</span><span class="sxs-lookup"><span data-stu-id="e3744-159">Select the **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="e3744-160">Se você já não fez isso, escolha uma conta do Azure para implantação.</span><span class="sxs-lookup"><span data-stu-id="e3744-160">If you haven't previously, choose an Azure account to deploy to.</span></span> <span data-ttu-id="e3744-161">Se você ainda não tiver uma conta, [inscreva-se][create-account].</span><span class="sxs-lookup"><span data-stu-id="e3744-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="e3744-162">Em **Ponto de Extremidade de Conexão**, selecione o cluster do Service Fabric para implantação.</span><span class="sxs-lookup"><span data-stu-id="e3744-162">Under **Connection Endpoint**, select the Service Fabric cluster to deploy to.</span></span> <span data-ttu-id="e3744-163">Se você não tiver um, selecione  **&lt;Criar Novo Cluster... &gt;** , o que abrirá a janela do navegador da Web no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3744-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window to the Azure portal.</span></span> <span data-ttu-id="e3744-164">Para saber mais, confira [Criar um cluster no portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="e3744-164">For more information, see [create a cluster in the portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="e3744-165">Quando você cria o cluster do Service Fabric, defina a configuração **Pontos de extremidade personalizados** como **80**.</span><span class="sxs-lookup"><span data-stu-id="e3744-165">When you create the Service Fabric cluster, make sure to set the **Custom endpoints** setting to **80**.</span></span>

![Configuração de tipo de nó do Service Fabric com o ponto de extremidade personalizado][custom-endpoint]

<span data-ttu-id="e3744-167">A criação de um novo cluster do Service Fabric leva algum tempo para concluir.</span><span class="sxs-lookup"><span data-stu-id="e3744-167">Creating a new Service Fabric cluster takes some time to complete.</span></span> <span data-ttu-id="e3744-168">Depois que o cluster for criado, acesse o diálogo Publicar e selecione  **&lt;Atualizar&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e3744-168">Once it has been created, go back to the publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="e3744-169">O novo cluster está listado na caixa suspensa. Selecione-o.</span><span class="sxs-lookup"><span data-stu-id="e3744-169">The new cluster is listed in the drop-down box; select it.</span></span>

<span data-ttu-id="e3744-170">Pressione **Publicar** e aguarde até que a implantação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="e3744-170">Press **Publish** and wait for the deployment to finish.</span></span>

<span data-ttu-id="e3744-171">Isso pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e3744-171">This may take a few minutes.</span></span> <span data-ttu-id="e3744-172">Depois de concluído, pode levar alguns minutos para o aplicativo ficar totalmente disponível.</span><span class="sxs-lookup"><span data-stu-id="e3744-172">After it completes, it may take a few more minutes for the application to be fully available.</span></span>

## <a name="test-the-website"></a><span data-ttu-id="e3744-173">Testar o site</span><span class="sxs-lookup"><span data-stu-id="e3744-173">Test the website</span></span>

<span data-ttu-id="e3744-174">Depois que o serviço foi publicado, teste-o em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="e3744-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="e3744-175">Primeiro, abra o portal do Azure e localize seu serviço Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e3744-175">First, open the Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="e3744-176">Verifique a folha de visão geral do endereço do serviço.</span><span class="sxs-lookup"><span data-stu-id="e3744-176">Check the overview blade of the service address.</span></span> <span data-ttu-id="e3744-177">Use o nome de domínio da propriedade _Ponto de extremidade de conexão de cliente_.</span><span class="sxs-lookup"><span data-stu-id="e3744-177">Use the domain name from the _Client connection endpoint_ property.</span></span> <span data-ttu-id="e3744-178">Por exemplo: `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="e3744-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Folha de visão geral do Service Fabric no portal do Azure][overview]

<span data-ttu-id="e3744-180">Navegue até esse endereço, onde você verá a resposta `HELLO WORLD`.</span><span class="sxs-lookup"><span data-stu-id="e3744-180">Navigate to this address where you will see the `HELLO WORLD` response.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="e3744-181">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="e3744-181">Delete the cluster</span></span>

<span data-ttu-id="e3744-182">Não se esqueça de excluir todos os recursos que criou para este guia de início rápido, pois você será cobrado por esses recursos.</span><span class="sxs-lookup"><span data-stu-id="e3744-182">Do not forget to delete all of the resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3744-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3744-183">Next steps</span></span>
<span data-ttu-id="e3744-184">Leia mais sobre [executáveis convidados](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="e3744-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F