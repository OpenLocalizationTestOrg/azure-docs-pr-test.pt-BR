---
title: aplicativos do Azure Service Fabric aaaManage usando 2.0 do CLI do Azure
description: Saiba como toodeploy e remova os aplicativos do Service Fabric do Azure de cluster usando o Azure CLI 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="8f7d6-103">Gerenciar um aplicativo do Azure Service Fabric usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8f7d6-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="8f7d6-104">Saiba como toocreate e exclua os aplicativos em execução em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f7d6-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f7d6-105">Prerequisites</span></span>

* <span data-ttu-id="8f7d6-106">Instale a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="8f7d6-107">Em seguida, selecione o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="8f7d6-108">Para obter mais informações, consulte [Introdução à CLI do Azure 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="8f7d6-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="8f7d6-109">Ter uma malha de serviço aplicativo pacote pronto toobe implantado.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="8f7d6-110">Para obter mais informações sobre como tooauthor e pacote de um aplicativo, leia sobre Olá [o modelo de aplicativo do Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="8f7d6-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="8f7d6-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8f7d6-111">Overview</span></span>

<span data-ttu-id="8f7d6-112">toodeploy um novo aplicativo, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="8f7d6-113">Carregar um repositório de imagem do aplicativo pacote toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="8f7d6-114">Provisione um tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-114">Provision an application type.</span></span>
3. <span data-ttu-id="8f7d6-115">Especifique e crie um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-115">Specify and create an application.</span></span>
4. <span data-ttu-id="8f7d6-116">Especifique e crie serviços.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-116">Specify and create services.</span></span>

<span data-ttu-id="8f7d6-117">tooremove um aplicativo existente, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="8f7d6-118">Exclua aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-118">Delete hello application.</span></span>
2. <span data-ttu-id="8f7d6-119">Olá desconfiguração associados tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="8f7d6-120">Exclua conteúdo do repositório de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="8f7d6-121">Implantar um novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f7d6-121">Deploy a new application</span></span>

<span data-ttu-id="8f7d6-122">toodeploy um novo aplicativo, completo Olá tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="8f7d6-123">Carregar um novo repositório de imagem de toohello de pacote de aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f7d6-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="8f7d6-124">Antes de criar um aplicativo, carregue o repositório de imagens do hello aplicativo pacote toohello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="8f7d6-125">Por exemplo, se o seu pacote de aplicativo está em Olá `app_package_dir` diretório, use Olá diretório de saudação tooupload comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="8f7d6-126">Para grandes pacotes de aplicativos, você pode especificar Olá `--show-progress` opção toodisplay progresso de saudação do carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="8f7d6-127">Tipo de aplicativo hello provisão</span><span class="sxs-lookup"><span data-stu-id="8f7d6-127">Provision hello application type</span></span>

<span data-ttu-id="8f7d6-128">Quando terminar de carregar Olá, provisione o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="8f7d6-129">aplicativo de hello tooprovision, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="8f7d6-130">Olá valor `application-type-build-path` é Olá nome do diretório de saudação em que você carregou o pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="8f7d6-131">Criar um aplicativo com base em um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f7d6-131">Create an application from an application type</span></span>

<span data-ttu-id="8f7d6-132">Depois de provisionar o aplicativo hello, use Olá tooname de comando a seguir e crie seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="8f7d6-133">`app-name`é o nome de saudação que você deseja toouse para instância do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="8f7d6-134">Você pode obter parâmetros adicionais do manifesto de aplicativo provisionado anteriormente hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="8f7d6-135">nome do aplicativo Hello deve começar com o prefixo Olá `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="8f7d6-136">Criar serviços para o novo aplicativo de saudação</span><span class="sxs-lookup"><span data-stu-id="8f7d6-136">Create services for hello new application</span></span>

<span data-ttu-id="8f7d6-137">Depois de criar um aplicativo, crie serviços de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="8f7d6-138">Saudação de exemplo a seguir, criamos um novo serviço sem monitoração de estado do nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="8f7d6-139">Serviços de saudação que você pode criar a partir de um aplicativo são definidos em um manifesto de serviço no pacote de aplicativo provisionado anteriormente hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="8f7d6-140">Verificar a integridade e a implantação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f7d6-140">Verify application deployment and health</span></span>

<span data-ttu-id="8f7d6-141">tooverify que um aplicativo e o serviço foram implantados com êxito, verifique se o serviço e aplicativo hello estão listados:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="8f7d6-142">tooverify que serviço Olá esteja íntegro, use semelhante integridade de saudação tooretrieve de comandos de serviço hello e o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="8f7d6-143">Os serviços e aplicativos íntegros têm um valor `HealthState` igual a `Ok`.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="8f7d6-144">Remover um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="8f7d6-144">Remove an existing application</span></span>

<span data-ttu-id="8f7d6-145">tooremove um aplicativo hello concluir tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="8f7d6-146">Excluir aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="8f7d6-146">Delete hello application</span></span>

<span data-ttu-id="8f7d6-147">aplicativo de hello toodelete, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="8f7d6-148">Desconfigurar o tipo de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="8f7d6-148">Unprovision hello application type</span></span>

<span data-ttu-id="8f7d6-149">Depois de excluir o aplicativo hello, você pode desconfigurar o tipo de aplicativo hello se você não precisar mais dela.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="8f7d6-150">tipo de aplicativo toounprovision hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="8f7d6-151">versão de nome e o tipo do tipo Hello deve coincidir nome hello e versão no manifesto de aplicativo provisionado anteriormente hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="8f7d6-152">Excluir o pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="8f7d6-152">Delete hello application package</span></span>

<span data-ttu-id="8f7d6-153">Após cancelou o provisionamento de tipo de aplicativo hello, você pode excluir o pacote de aplicativo hello saudação do repositório de imagens se você não precisar mais dela.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="8f7d6-154">A exclusão de pacotes de aplicativos ajuda a recuperar o espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="8f7d6-155">pacote de aplicativo toodelete Olá Olá do repositório de imagens, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f7d6-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="8f7d6-156">`content-path`deve ser o nome de saudação do diretório Olá carregado quando você criou o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f7d6-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="8f7d6-157">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="8f7d6-157">Related articles</span></span>

* [<span data-ttu-id="8f7d6-158">Introdução ao Service Fabric e à CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8f7d6-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="8f7d6-159">Introdução à CLI XPlat do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8f7d6-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
