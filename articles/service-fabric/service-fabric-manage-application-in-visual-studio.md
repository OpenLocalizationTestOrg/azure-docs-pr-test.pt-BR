---
title: Gerenciar seus aplicativos no Visual Studio | Microsoft Docs
description: "Use o Visual Studio para criar, desenvolver, empacotar, implantar e depurar seus aplicativos e serviços do Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: 3f6a47a15b74a7ceb6504b2834be62e76ab70bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="7d574-103">Usar o Visual Studio para simplificar a escrita e o gerenciamento de seus aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7d574-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="7d574-104">É possível gerenciar os serviços e aplicativos do Service Fabric do Azure por meio do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d574-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="7d574-105">Depois de [configurar o ambiente de desenvolvimento](service-fabric-get-started.md),você pode usar o Visual Studio para criar aplicativos do Service Fabric, adicionar serviços, ou pacotes, registrar e implantar aplicativos no cluster de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="7d574-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="7d574-106">Implantar o aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7d574-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="7d574-107">Por padrão, a implantação de um aplicativo combina as etapas a seguir em uma única operação:</span><span class="sxs-lookup"><span data-stu-id="7d574-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="7d574-108">Criar o pacote de aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d574-108">Creating the application package</span></span>
2. <span data-ttu-id="7d574-109">Carregar o pacote de aplicativo no repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="7d574-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="7d574-110">Registrar o tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d574-110">Registering the application type</span></span>
4. <span data-ttu-id="7d574-111">Remover as instâncias de aplicativo em execução</span><span class="sxs-lookup"><span data-stu-id="7d574-111">Removing any running application instances</span></span>
5. <span data-ttu-id="7d574-112">Criando uma instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d574-112">Creating an application instance</span></span>

<span data-ttu-id="7d574-113">No Visual Studio, pressionar **F5** também implanta seu aplicativo e anexa o depurador a todas as instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d574-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="7d574-114">Você pode usar **Ctrl + F5** para implantar um aplicativo sem depuração ou pode publicar um cluster local ou remoto usando o perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="7d574-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="7d574-115">Para saber mais, confira [Publicar um aplicativo em um cluster remoto usando o Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7d574-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="7d574-116">Modo de Depuração do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d574-116">Application Debug Mode</span></span>
<span data-ttu-id="7d574-117">O Visual Studio fornece uma propriedade chamada **Modo de Depuração de Aplicativo**, que controla como você deseja que o Visual Studio trate da implantação de aplicativo como parte da depuração.</span><span class="sxs-lookup"><span data-stu-id="7d574-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="7d574-118">Para definir a propriedade Modo de Depuração do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d574-118">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="7d574-119">No menu de atalho do projeto de aplicativo do Service Fabric (*.sfproj), escolha **Propriedades** (ou pressione a tecla **F4**).</span><span class="sxs-lookup"><span data-stu-id="7d574-119">On the Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="7d574-120">Na janela **Propriedades**, defina a propriedade **Modo de Depuração do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="7d574-120">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![Definir a Propriedade Modo de Depuração do Aplicativo][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="7d574-122">Modos de depuração do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7d574-122">Application Debug Modes</span></span>

1. <span data-ttu-id="7d574-123">**Atualizar aplicativo** Esse modo permite que você altere e depurar seu código rapidamente e dá suporte à edição de arquivos da Web estáticos durante a depuração.</span><span class="sxs-lookup"><span data-stu-id="7d574-123">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="7d574-124">Esse modo funciona apenas se o cluster de desenvolvimento local está em [Modo 1 Nó](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="7d574-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="7d574-125">**Remover Aplicativo** faz com que o aplicativo seja removido quando a sessão de depuração termina.</span><span class="sxs-lookup"><span data-stu-id="7d574-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="7d574-126">**Atualização Automática**: o aplicativo continua em execução quando a sessão de depuração termina.</span><span class="sxs-lookup"><span data-stu-id="7d574-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="7d574-127">A próxima sessão de depuração tratará a implantação como uma atualização.</span><span class="sxs-lookup"><span data-stu-id="7d574-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="7d574-128">O processo de atualização preserva todos os dados inseridos em uma sessão de depuração anterior.</span><span class="sxs-lookup"><span data-stu-id="7d574-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="7d574-129">**Manter Aplicativo** O aplicativo é mantido em execução no cluster quando a sessão de depuração termina.</span><span class="sxs-lookup"><span data-stu-id="7d574-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="7d574-130">No início da próxima sessão de depuração, o aplicativo será removido.</span><span class="sxs-lookup"><span data-stu-id="7d574-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="7d574-131">Na **Atualização Automática** , os dados são preservados com a aplicação dos recursos de atualização de aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7d574-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="7d574-132">Para obter mais informações sobre como atualizar aplicativos e como executar uma atualização em um ambiente real, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="7d574-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="7d574-133">Adicione um serviço ao aplicativo da Malha de Serviços</span><span class="sxs-lookup"><span data-stu-id="7d574-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="7d574-134">Você pode adicionar novos serviços a seu aplicativo para estender sua funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7d574-134">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="7d574-135">Para garantir que o serviço esteja incluído no seu pacote de aplicativos, adicione o serviço usando o item de menu **Novo Serviço de Malha...** .</span><span class="sxs-lookup"><span data-stu-id="7d574-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![Adicionar um novo serviço Service Fabric][newservice]

<span data-ttu-id="7d574-137">Selecione um tipo de projeto da Malha do Serviço para adicionar ao aplicativo e especifique um nome para o serviço.</span><span class="sxs-lookup"><span data-stu-id="7d574-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="7d574-138">Confira [Como escolher uma estrutura para o serviço](service-fabric-choose-framework.md) para ajudar com a decisão de que tipo de serviço usar.</span><span class="sxs-lookup"><span data-stu-id="7d574-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![Selecionar um tipo de projeto do serviço Service Fabric para adicionar ao aplicativo][addserviceproject]

<span data-ttu-id="7d574-140">O novo serviço é adicionado à solução e ao pacote de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="7d574-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="7d574-141">As referências de serviço e uma instância de serviço padrão serão adicionados ao manifesto do aplicativo, fazendo com que o serviço seja criado e iniciado na próxima vez em que você implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d574-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![O novo serviço é adicionado ao manifesto do aplicativo][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="7d574-143">Empacotar o aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7d574-143">Package your Service Fabric application</span></span>
<span data-ttu-id="7d574-144">Para implantar o aplicativo e seu serviço em um cluster, você precisa criar um pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7d574-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="7d574-145">O pacote organiza o manifesto do aplicativo, os manifestos do serviço e outros arquivos necessários em um layout específico.</span><span class="sxs-lookup"><span data-stu-id="7d574-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="7d574-146">O Visual Studio configura e gerencia o pacote na pasta do projeto do aplicativo, no diretório 'pkg'.</span><span class="sxs-lookup"><span data-stu-id="7d574-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="7d574-147">Clicar em **Pacote** no menu de contexto **Aplicativo** cria ou atualiza o pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7d574-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="7d574-148">Remover aplicativos e tipos de aplicativo usando o Gerenciador de Nuvem</span><span class="sxs-lookup"><span data-stu-id="7d574-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="7d574-149">Você pode executar operações de gerenciamento de cluster básico no Visual Studio usando o Cloud Explorer, que pode ser iniciado pelo menu **Exibir** .</span><span class="sxs-lookup"><span data-stu-id="7d574-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="7d574-150">Por exemplo, você pode excluir aplicativos e desprovisionar tipos de aplicativos em clusters locais ou remotos.</span><span class="sxs-lookup"><span data-stu-id="7d574-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Remover um aplicativo][removeapplication]

> [!TIP]
> <span data-ttu-id="7d574-152">Para funcionalidade de gerenciamento de cluster mais avançada, confira [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7d574-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="7d574-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d574-153">Next steps</span></span>
* [<span data-ttu-id="7d574-154">Modelo de aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="7d574-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="7d574-155">Implantação de aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="7d574-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="7d574-156">Gerenciando parâmetros do aplicativo para vários ambientes</span><span class="sxs-lookup"><span data-stu-id="7d574-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="7d574-157">Depurando o aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="7d574-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="7d574-158">Visualização do cluster usando o Gerenciador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7d574-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png