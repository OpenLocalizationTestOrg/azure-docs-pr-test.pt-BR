---
title: aplicativos do Azure Service Fabric aaaManage usando a CLI do Azure Service Fabric
description: Saiba como toodeploy e remova os aplicativos do Service Fabric do Azure de cluster usando a CLI do Azure Service Fabric
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="495b4-103">Gerenciar um aplicativo do Azure Service Fabric usando a CLI do Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="495b4-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="495b4-104">Saiba como toocreate e exclua os aplicativos em execução em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="495b4-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="495b4-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="495b4-105">Prerequisites</span></span>

* <span data-ttu-id="495b4-106">Implantar a CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="495b4-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="495b4-107">Em seguida, selecione o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="495b4-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="495b4-108">Para obter mais informações, consulte [Introdução à CLI do Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="495b4-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="495b4-109">Ter uma malha de serviço aplicativo pacote pronto toobe implantado.</span><span class="sxs-lookup"><span data-stu-id="495b4-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="495b4-110">Para obter mais informações sobre como tooauthor e pacote de um aplicativo, leia sobre Olá [o modelo de aplicativo do Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="495b4-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="495b4-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="495b4-111">Overview</span></span>

<span data-ttu-id="495b4-112">toodeploy um novo aplicativo, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="495b4-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="495b4-113">Carregar um repositório de imagem do aplicativo pacote toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="495b4-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="495b4-114">Provisione um tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="495b4-114">Provision an application type.</span></span>
3. <span data-ttu-id="495b4-115">Especifique e crie um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="495b4-115">Specify and create an application.</span></span>
4. <span data-ttu-id="495b4-116">Especifique e crie serviços.</span><span class="sxs-lookup"><span data-stu-id="495b4-116">Specify and create services.</span></span>

<span data-ttu-id="495b4-117">tooremove um aplicativo existente, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="495b4-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="495b4-118">Exclua aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-118">Delete hello application.</span></span>
2. <span data-ttu-id="495b4-119">Olá desconfiguração associados tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="495b4-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="495b4-120">Exclua conteúdo do repositório de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="495b4-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="495b4-121">Implantar um novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="495b4-121">Deploy a new application</span></span>

<span data-ttu-id="495b4-122">toodeploy um novo aplicativo, completo Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="495b4-123">Carregar um novo repositório de imagem de toohello de pacote de aplicativo</span><span class="sxs-lookup"><span data-stu-id="495b4-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="495b4-124">Antes de criar um aplicativo, carregue o repositório de imagens do hello aplicativo pacote toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="495b4-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="495b4-125">Por exemplo, se o seu pacote de aplicativo está em Olá `app_package_dir` diretório, use Olá diretório de saudação tooupload comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="495b4-126">Para grandes pacotes de aplicativos, você pode especificar Olá `--show-progress` opção toodisplay progresso de saudação do carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="495b4-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="495b4-127">Tipo de aplicativo hello provisão</span><span class="sxs-lookup"><span data-stu-id="495b4-127">Provision hello application type</span></span>

<span data-ttu-id="495b4-128">Quando terminar de carregar Olá, provisione o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="495b4-129">aplicativo de hello tooprovision, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="495b4-130">Olá valor `application-type-build-path` é Olá nome do diretório de saudação em que você carregou o pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="495b4-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="495b4-131">Criar um aplicativo com base em um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="495b4-131">Create an application from an application type</span></span>

<span data-ttu-id="495b4-132">Depois de provisionar o aplicativo hello, use Olá tooname de comando a seguir e crie seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="495b4-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="495b4-133">`app-name`é o nome de saudação que você deseja toouse para instância do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="495b4-134">Você pode obter parâmetros adicionais no manifesto do aplicativo provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="495b4-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="495b4-135">nome do aplicativo Hello deve começar com o prefixo Olá `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="495b4-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="495b4-136">Criar serviços para o novo aplicativo de saudação</span><span class="sxs-lookup"><span data-stu-id="495b4-136">Create services for hello new application</span></span>

<span data-ttu-id="495b4-137">Depois de criar um aplicativo, crie serviços de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="495b4-138">Saudação de exemplo a seguir, criamos um novo serviço sem monitoração de estado do nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="495b4-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="495b4-139">Serviços de saudação que você pode criar a partir de um aplicativo são definidos em um manifesto de serviço no pacote de aplicativo provisionado anteriormente hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="495b4-140">Verificar a integridade e a implantação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="495b4-140">Verify application deployment and health</span></span>

<span data-ttu-id="495b4-141">tooverify tudo está íntegro, use Olá comandos de integridade a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="495b4-142">tooverify que serviço Olá esteja íntegro, use semelhante integridade de saudação tooretrieve de comandos do serviço de saudação e do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="495b4-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="495b4-143">Os serviços e aplicativos íntegros têm um valor `HealthState` igual a `Ok`.</span><span class="sxs-lookup"><span data-stu-id="495b4-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="495b4-144">Remover um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="495b4-144">Remove an existing application</span></span>

<span data-ttu-id="495b4-145">tooremove um aplicativo hello concluir tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="495b4-146">Excluir aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="495b4-146">Delete hello application</span></span>

<span data-ttu-id="495b4-147">aplicativo de hello toodelete, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="495b4-148">Desconfigurar o tipo de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="495b4-148">Unprovision hello application type</span></span>

<span data-ttu-id="495b4-149">Depois de excluir o aplicativo hello, você pode desconfigurar o tipo de aplicativo hello se você não precisar mais dela.</span><span class="sxs-lookup"><span data-stu-id="495b4-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="495b4-150">tipo de aplicativo toounprovision hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="495b4-151">versão de nome e o tipo do tipo Hello deve coincidir nome hello e versão no manifesto de aplicativo provisionado anteriormente hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="495b4-152">Excluir o pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="495b4-152">Delete hello application package</span></span>

<span data-ttu-id="495b4-153">Após cancelou o provisionamento de tipo de aplicativo hello, você pode excluir o pacote de aplicativo hello saudação do repositório de imagens se você não precisar mais dela.</span><span class="sxs-lookup"><span data-stu-id="495b4-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="495b4-154">A exclusão de pacotes de aplicativos ajuda a recuperar o espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="495b4-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="495b4-155">pacote de aplicativo toodelete Olá Olá do repositório de imagens, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="495b4-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="495b4-156">`content-path`deve ser o nome de saudação do diretório Olá carregado quando você criou o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="495b4-157">Atualizar aplicativo</span><span class="sxs-lookup"><span data-stu-id="495b4-157">Upgrade application</span></span>

<span data-ttu-id="495b4-158">Depois de criar seu aplicativo, você pode repetir Olá mesmo conjunto de etapas tooprovision uma segunda versão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="495b4-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="495b4-159">Em seguida, com uma atualização de aplicativo do Service Fabric transição toorunning Olá segunda versão do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="495b4-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="495b4-160">Para obter mais informações, consulte a documentação do hello em [atualizações de aplicativo do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="495b4-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="495b4-161">tooperform uma atualização, primeiro provisionar Olá próxima versão do aplicativo usando a saudação Olá comandos mesmo de antes:</span><span class="sxs-lookup"><span data-stu-id="495b4-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="495b4-162">É recomendável tooperform uma atualização automática monitorada, reinicie a atualização Olá executando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="495b4-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="495b4-163">As atualizações substituem os parâmetros existentes por qualquer conjunto especificado.</span><span class="sxs-lookup"><span data-stu-id="495b4-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="495b4-164">Parâmetros do aplicativo devem ser passados como um comando de atualização de toohello de argumentos, se necessário.</span><span class="sxs-lookup"><span data-stu-id="495b4-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="495b4-165">Parâmetros do aplicativo devem ser codificados como um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="495b4-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="495b4-166">tooretrieve todos os parâmetros especificados anteriormente, você pode usar o hello `sfctl application info` comando.</span><span class="sxs-lookup"><span data-stu-id="495b4-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="495b4-167">Quando uma atualização do aplicativo está em andamento, o status de saudação podem ser recuperados usando o `sfctl application upgrade-status` comando.</span><span class="sxs-lookup"><span data-stu-id="495b4-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="495b4-168">Finalmente, se uma atualização está em andamento e precisa toobe cancelada, você pode usar Olá `sfctl application upgrade-rollback` tooroll volta Olá atualização.</span><span class="sxs-lookup"><span data-stu-id="495b4-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="495b4-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="495b4-169">Next steps</span></span>

* [<span data-ttu-id="495b4-170">Noções básicas do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="495b4-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="495b4-171">Introdução ao Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="495b4-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="495b4-172">Iniciar uma atualização de aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="495b4-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
