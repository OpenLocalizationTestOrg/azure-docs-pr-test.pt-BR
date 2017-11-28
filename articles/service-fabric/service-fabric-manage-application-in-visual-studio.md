---
title: aaaManage seus aplicativos no Visual Studio | Microsoft Docs
description: "Usar o Visual Studio toocreate, desenvolver, pacotes, implantar e depurar seus aplicativos de serviço de malha e serviços."
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
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="ff81c-103">Use a gravação de toosimplify do Visual Studio e gerenciar seus aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff81c-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="ff81c-104">É possível gerenciar os serviços e aplicativos do Service Fabric do Azure por meio do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff81c-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="ff81c-105">Depois que você [configurar seu ambiente de desenvolvimento](service-fabric-get-started.md), usar os aplicativos do Visual Studio toocreate Service Fabric, adicionar um registro de serviços ou pacote e implantar aplicativos em seu cluster de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="ff81c-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="ff81c-106">Implantar o aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff81c-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="ff81c-107">Por padrão, implantando um aplicativo combina Olá seguindo as etapas em uma operação simple:</span><span class="sxs-lookup"><span data-stu-id="ff81c-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="ff81c-108">Criar pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ff81c-108">Creating hello application package</span></span>
2. <span data-ttu-id="ff81c-109">Carregando o repositório de imagens toohello do pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ff81c-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="ff81c-110">Registrando o tipo de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ff81c-110">Registering hello application type</span></span>
4. <span data-ttu-id="ff81c-111">Remover as instâncias de aplicativo em execução</span><span class="sxs-lookup"><span data-stu-id="ff81c-111">Removing any running application instances</span></span>
5. <span data-ttu-id="ff81c-112">Criando uma instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ff81c-112">Creating an application instance</span></span>

<span data-ttu-id="ff81c-113">No Visual Studio, pressionando **F5** anexar instâncias do aplicativo hello depurador tooall e implanta seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff81c-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="ff81c-114">Você pode usar **Ctrl + F5** toodeploy um aplicativo sem depuração ou você pode publicar tooa local ou cluster remoto usando Olá perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="ff81c-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="ff81c-115">Para obter mais informações, consulte [publicar um cluster remoto de tooa do aplicativo usando o Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ff81c-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="ff81c-116">Modo de Depuração do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ff81c-116">Application Debug Mode</span></span>
<span data-ttu-id="ff81c-117">Visual Studio fornece uma propriedade chamada **o modo de depuração de aplicativo**, que controla como deseja que a implantação de aplicativos do Visual estúdios toohandle como parte da depuração.</span><span class="sxs-lookup"><span data-stu-id="ff81c-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="ff81c-118">Olá tooset propriedade modo de depuração de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ff81c-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="ff81c-119">Em Olá Service Fabric do projeto de aplicação (*. sfproj) menu de atalho, escolha **propriedades** (ou pressione hello **F4** chave).</span><span class="sxs-lookup"><span data-stu-id="ff81c-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="ff81c-120">Em Olá **propriedades** janela, Olá conjunto **o modo de depuração de aplicativo** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ff81c-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Definir a Propriedade Modo de Depuração do Aplicativo][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="ff81c-122">Modos de depuração do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ff81c-122">Application Debug Modes</span></span>

1. <span data-ttu-id="ff81c-123">**Atualizar aplicativo** esse modo permite que você altere tooquickly e depurar seu código e dá suporte à edição de arquivos de estático da web durante a depuração.</span><span class="sxs-lookup"><span data-stu-id="ff81c-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="ff81c-124">Esse modo funciona apenas se o cluster de desenvolvimento local está em [Modo 1 Nó](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="ff81c-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="ff81c-125">**Remover aplicativo** causas Olá toobe aplicativo removido quando a sessão de depuração Olá termina.</span><span class="sxs-lookup"><span data-stu-id="ff81c-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="ff81c-126">**Auto atualização** aplicativo hello continua toorun quando a sessão de depuração Olá termina.</span><span class="sxs-lookup"><span data-stu-id="ff81c-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="ff81c-127">Olá próxima sessão de depuração tratará implantação hello como uma atualização.</span><span class="sxs-lookup"><span data-stu-id="ff81c-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="ff81c-128">o processo de atualização Olá preserva todos os dados inseridos em uma sessão de depuração anterior.</span><span class="sxs-lookup"><span data-stu-id="ff81c-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="ff81c-129">**Manter o aplicativo** Olá aplicativo mantém em execução no cluster hello quando hello término da sessão de depuração.</span><span class="sxs-lookup"><span data-stu-id="ff81c-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="ff81c-130">Olá começo da saudação próxima sessão de depuração, aplicativo hello será removido.</span><span class="sxs-lookup"><span data-stu-id="ff81c-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="ff81c-131">Para **atualização automática** os dados são preservados, aplicando a capacidade de atualização de aplicativo hello do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ff81c-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="ff81c-132">Para obter mais informações sobre como atualizar aplicativos e como executar uma atualização em um ambiente real, confira [Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="ff81c-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="ff81c-133">Adicionar um serviço tooyour aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff81c-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="ff81c-134">Você pode adicionar novos serviços tooyour aplicativo tooextend sua funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="ff81c-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="ff81c-135">tooensure que o serviço de saudação está incluído em seu pacote de aplicativo, adicione o serviço de Olá por meio de saudação **novo Service Fabric...**  item de menu.</span><span class="sxs-lookup"><span data-stu-id="ff81c-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Adicionar um novo serviço Service Fabric][newservice]

<span data-ttu-id="ff81c-137">Selecione um aplicativo do Service Fabric projetos tipo tooadd tooyour e especifique um nome para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff81c-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="ff81c-138">Consulte [escolher uma estrutura para seu serviço](service-fabric-choose-framework.md) toohelp decidir qual serviço digite toouse.</span><span class="sxs-lookup"><span data-stu-id="ff81c-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Selecione um aplicativo do Service Fabric service projeto tipo tooadd tooyour][addserviceproject]

<span data-ttu-id="ff81c-140">novo serviço de saudação é adicionado à solução tooyour e pacote de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="ff81c-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="ff81c-141">Olá referências de serviço e uma instância de serviço padrão será adicionado toohello o manifesto do aplicativo, causando toobe de serviço Olá criada e iniciada Olá próxima vez que você implantar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ff81c-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![Olá novo serviço é adicionado, o manifesto do aplicativo tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="ff81c-143">Empacotar o aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff81c-143">Package your Service Fabric application</span></span>
<span data-ttu-id="ff81c-144">aplicativo de hello toodeploy e seu cluster tooa de serviços, é necessário toocreate um pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff81c-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="ff81c-145">pacote de saudação organiza o manifesto do aplicativo hello, manifestos do serviço e outros arquivos necessários em um layout específico.</span><span class="sxs-lookup"><span data-stu-id="ff81c-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="ff81c-146">Visual Studio configura e gerencia Olá pacote na pasta do projeto de aplicativo hello, no diretório de 'pkg' hello.</span><span class="sxs-lookup"><span data-stu-id="ff81c-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="ff81c-147">Clicando em **pacote** de saudação **aplicativo** cria do menu de contexto ou atualizações Olá pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff81c-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="ff81c-148">Remover aplicativos e tipos de aplicativo usando o Gerenciador de Nuvem</span><span class="sxs-lookup"><span data-stu-id="ff81c-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="ff81c-149">Você pode executar operações de gerenciamento de cluster básico do Visual Studio usando o Gerenciador de nuvem, que você pode iniciar de saudação **exibição** menu.</span><span class="sxs-lookup"><span data-stu-id="ff81c-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="ff81c-150">Por exemplo, você pode excluir aplicativos e desprovisionar tipos de aplicativos em clusters locais ou remotos.</span><span class="sxs-lookup"><span data-stu-id="ff81c-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Remover um aplicativo][removeapplication]

> [!TIP]
> <span data-ttu-id="ff81c-152">Para funcionalidade de gerenciamento de cluster mais avançada, confira [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ff81c-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="ff81c-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff81c-153">Next steps</span></span>
* [<span data-ttu-id="ff81c-154">Modelo de aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="ff81c-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="ff81c-155">Implantação de aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="ff81c-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="ff81c-156">Gerenciando parâmetros do aplicativo para vários ambientes</span><span class="sxs-lookup"><span data-stu-id="ff81c-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="ff81c-157">Depurando o aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="ff81c-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="ff81c-158">Visualização do cluster usando o Gerenciador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff81c-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png