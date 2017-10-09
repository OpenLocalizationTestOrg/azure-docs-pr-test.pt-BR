---
title: aaaQuickly implantar um cluster existente do aplicativo tooan Azure Service Fabric
description: Use um cluster de Azure Service Fabric toohost um aplicativo Node. js existente com o Visual Studio.
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
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="f298f-103">Hospedar um aplicativo Node.js no Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f298f-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="f298f-104">Este guia de início rápido o ajuda a implantar um cluster existente de malha do serviço tooa (Node. js neste exemplo) do aplicativo em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="f298f-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f298f-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f298f-105">Prerequisites</span></span>

<span data-ttu-id="f298f-106">Antes de começar, verifique se você [configurou o ambiente de desenvolvimento](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f298f-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="f298f-107">Que inclui a instalação Olá SDK do Service Fabric e 2017 do Visual Studio ou 2015.</span><span class="sxs-lookup"><span data-stu-id="f298f-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="f298f-108">Você também precisa toohave um aplicativo Node. js existente para a implantação.</span><span class="sxs-lookup"><span data-stu-id="f298f-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="f298f-109">Este guia de início rápido usa um site Node.js simples que pode ser baixado [aqui][download-sample].</span><span class="sxs-lookup"><span data-stu-id="f298f-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="f298f-110">Extrair esse arquivo tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` pasta depois de criar o projeto de saudação na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="f298f-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="f298f-111">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita][create-account].</span><span class="sxs-lookup"><span data-stu-id="f298f-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="f298f-112">Criar serviço Olá</span><span class="sxs-lookup"><span data-stu-id="f298f-112">Create hello service</span></span>

<span data-ttu-id="f298f-113">Inicie o Visual Studio como um **administrador**.</span><span class="sxs-lookup"><span data-stu-id="f298f-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="f298f-114">Criar um projeto com `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="f298f-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="f298f-115">Em Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicativo de malha do serviço**.</span><span class="sxs-lookup"><span data-stu-id="f298f-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="f298f-116">Nome do aplicativo hello **MyGuestApp** e pressione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f298f-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f298f-117">Node. js facilmente pode quebrar o limite de caracteres 260 Olá para caminhos com windows.</span><span class="sxs-lookup"><span data-stu-id="f298f-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="f298f-118">Usar um caminho curto para o próprio projeto hello como **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="f298f-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Caixa de diálogo Novo projeto no Visual Studio][new-project]

<span data-ttu-id="f298f-120">Você pode criar qualquer tipo de serviço de malha do serviço na próxima caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f298f-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="f298f-121">Para este guia de início rápido, escolha **Executável Convidado**.</span><span class="sxs-lookup"><span data-stu-id="f298f-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="f298f-122">Nome do serviço de saudação **MyGuestService** e definir opções de saudação em toohello direita Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="f298f-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="f298f-123">Configuração</span><span class="sxs-lookup"><span data-stu-id="f298f-123">Setting</span></span>                   | <span data-ttu-id="f298f-124">Valor</span><span class="sxs-lookup"><span data-stu-id="f298f-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="f298f-125">Pasta do Pacote de Código</span><span class="sxs-lookup"><span data-stu-id="f298f-125">Code Package Folder</span></span>       | <span data-ttu-id="f298f-126">_&lt;pasta de saudação com seu aplicativo Node. js&gt;_</span><span class="sxs-lookup"><span data-stu-id="f298f-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="f298f-127">Comportamento do Pacote de Código</span><span class="sxs-lookup"><span data-stu-id="f298f-127">Code Package Behavior</span></span>     | <span data-ttu-id="f298f-128">Copie a pasta conteúdo tooproject</span><span class="sxs-lookup"><span data-stu-id="f298f-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="f298f-129">Programa</span><span class="sxs-lookup"><span data-stu-id="f298f-129">Program</span></span>                   | <span data-ttu-id="f298f-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="f298f-130">node.exe</span></span> |
| <span data-ttu-id="f298f-131">Argumentos</span><span class="sxs-lookup"><span data-stu-id="f298f-131">Arguments</span></span>                 | <span data-ttu-id="f298f-132">server.js</span><span class="sxs-lookup"><span data-stu-id="f298f-132">server.js</span></span> |
| <span data-ttu-id="f298f-133">Pasta de trabalho</span><span class="sxs-lookup"><span data-stu-id="f298f-133">Working Folder</span></span>            | <span data-ttu-id="f298f-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="f298f-134">CodePackage</span></span> |

<span data-ttu-id="f298f-135">Pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f298f-135">Press **OK**.</span></span>

![Caixa de diálogo Novo serviço no Visual Studio][new-service]

<span data-ttu-id="f298f-137">Visual Studio cria o projeto de aplicativo hello e projeto de serviço de ator hello e exibe-os no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="f298f-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="f298f-138">projeto de aplicativo Hello (**MyGuestApp**) não contém qualquer código diretamente.</span><span class="sxs-lookup"><span data-stu-id="f298f-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="f298f-139">Em vez disso, ele faz referência a um conjunto de projetos de serviço.</span><span class="sxs-lookup"><span data-stu-id="f298f-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="f298f-140">Além disso, ele contém três outros tipos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="f298f-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="f298f-141">**Perfis de publicação**</span><span class="sxs-lookup"><span data-stu-id="f298f-141">**Publish profiles**</span></span>  
<span data-ttu-id="f298f-142">Preferências de ferramentas para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="f298f-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="f298f-143">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="f298f-143">**Scripts**</span></span>  
<span data-ttu-id="f298f-144">Script do PowerShell para a implantação/atualização de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f298f-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="f298f-145">**Definição de aplicativo**</span><span class="sxs-lookup"><span data-stu-id="f298f-145">**Application definition**</span></span>  
<span data-ttu-id="f298f-146">Inclui o manifesto do aplicativo hello em *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="f298f-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="f298f-147">Arquivos de parâmetro de aplicativo associados estão sob *ApplicationParameters*, que definem o aplicativo hello e permitem que você tooconfigure especificamente para um determinado ambiente.</span><span class="sxs-lookup"><span data-stu-id="f298f-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="f298f-148">Para obter uma visão geral do conteúdo de saudação do projeto de serviço hello, consulte [Introdução aos serviços confiável](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="f298f-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="f298f-149">Configurar a rede</span><span class="sxs-lookup"><span data-stu-id="f298f-149">Set up networking</span></span>

<span data-ttu-id="f298f-150">exemplo Hello aplicativo Node. js que esteja implantando usa a porta **80** e precisamos tootell Service Fabric é necessário que a porta expostos.</span><span class="sxs-lookup"><span data-stu-id="f298f-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="f298f-151">Olá abrir **ServiceManifest.xml** arquivo no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f298f-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="f298f-152">Na parte inferior de saudação do manifesto hello, há um `<Resources> \ <Endpoints>` com uma entrada já definida.</span><span class="sxs-lookup"><span data-stu-id="f298f-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="f298f-153">Modificar essa entrada tooadd `Port`, `Protocol`, e `Type`.</span><span class="sxs-lookup"><span data-stu-id="f298f-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="f298f-154">Implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="f298f-154">Deploy tooAzure</span></span>

<span data-ttu-id="f298f-155">Se você pressionar **F5** e executar o projeto Olá, é cluster local toohello implantado.</span><span class="sxs-lookup"><span data-stu-id="f298f-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="f298f-156">No entanto, vamos implantar tooAzure em vez disso.</span><span class="sxs-lookup"><span data-stu-id="f298f-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="f298f-157">Clique com botão direito no projeto hello e escolha **publicar...**  que abre um tooAzure de toopublish da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f298f-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Caixa de diálogo tooazure para um serviço de malha publicar][publish]

<span data-ttu-id="f298f-159">Selecione Olá **PublishProfiles\Cloud.xml** perfil de destino.</span><span class="sxs-lookup"><span data-stu-id="f298f-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="f298f-160">Se você ainda não anteriormente, escolha um toodeploy de conta do Azure para.</span><span class="sxs-lookup"><span data-stu-id="f298f-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="f298f-161">Se você ainda não tiver uma conta, [inscreva-se][create-account].</span><span class="sxs-lookup"><span data-stu-id="f298f-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="f298f-162">Em **ponto de extremidade de Conexão**, selecione Olá toodeploy de cluster do Service Fabric para.</span><span class="sxs-lookup"><span data-stu-id="f298f-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="f298f-163">Se você não tiver um, selecione  **&lt;criar novo Cluster... &gt;**  que abre a toohello de janela de navegador da web portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f298f-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="f298f-164">Para obter mais informações, consulte [criar um cluster no portal de saudação](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f298f-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="f298f-165">Quando você cria o cluster do Service Fabric hello, fazer se Olá de tooset **pontos de extremidade personalizado** configuração muito**80**.</span><span class="sxs-lookup"><span data-stu-id="f298f-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Configuração de tipo de nó do Service Fabric com o ponto de extremidade personalizado][custom-endpoint]

<span data-ttu-id="f298f-167">Criar um novo cluster do Service Fabric leva alguns toocomplete de tempo.</span><span class="sxs-lookup"><span data-stu-id="f298f-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="f298f-168">Depois que ele tiver sido criado, vá toohello back caixa de diálogo Publicar e selecione  **&lt;atualizar&gt;**.</span><span class="sxs-lookup"><span data-stu-id="f298f-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="f298f-169">cluster novo Hello está listado na caixa de lista suspensa Olá; Selecione-o.</span><span class="sxs-lookup"><span data-stu-id="f298f-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="f298f-170">Pressione **publicar** e aguarde Olá toofinish de implantação.</span><span class="sxs-lookup"><span data-stu-id="f298f-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="f298f-171">Isso pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f298f-171">This may take a few minutes.</span></span> <span data-ttu-id="f298f-172">Depois que ele for concluído, ele pode levar alguns minutos para Olá aplicativo toobe totalmente disponível.</span><span class="sxs-lookup"><span data-stu-id="f298f-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="f298f-173">Site de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="f298f-173">Test hello website</span></span>

<span data-ttu-id="f298f-174">Depois que o serviço foi publicado, teste-o em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="f298f-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="f298f-175">Primeiro, abra Olá portal do Azure e localizar seu serviço de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="f298f-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="f298f-176">Verifique a folha de visão geral de Olá Olá do endereço do serviço.</span><span class="sxs-lookup"><span data-stu-id="f298f-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="f298f-177">Use o nome de domínio Olá da saudação _ponto de extremidade de conexão de cliente_ propriedade.</span><span class="sxs-lookup"><span data-stu-id="f298f-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="f298f-178">Por exemplo: `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="f298f-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Folha de visão geral de malha do serviço no hello portal do Azure][overview]

<span data-ttu-id="f298f-180">Navegue toothis endereço onde você verá Olá `HELLO WORLD` resposta.</span><span class="sxs-lookup"><span data-stu-id="f298f-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="f298f-181">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="f298f-181">Delete hello cluster</span></span>

<span data-ttu-id="f298f-182">Não se esqueça de toodelete todos os recursos de saudação que você criou para este guia de início rápido, como você são cobrados por esses recursos.</span><span class="sxs-lookup"><span data-stu-id="f298f-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f298f-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f298f-183">Next steps</span></span>
<span data-ttu-id="f298f-184">Leia mais sobre [executáveis convidados](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="f298f-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F