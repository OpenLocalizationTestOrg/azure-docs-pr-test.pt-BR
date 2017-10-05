---
title: Gerenciar aplicativos do Azure Service Fabric usando a CLI do Azure 2.0
description: Saiba como implantar e remover aplicativos de um cluster do Azure Service Fabric usando a CLI do Azure 2.0.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="88004-103">Gerenciar um aplicativo do Azure Service Fabric usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="88004-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="88004-104">Saiba como criar e excluir os aplicativos que estão em execução em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88004-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88004-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88004-105">Prerequisites</span></span>

* <span data-ttu-id="88004-106">Instale a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="88004-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="88004-107">Em seguida, selecione o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88004-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="88004-108">Para obter mais informações, consulte [Introdução à CLI do Azure 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="88004-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="88004-109">Tenha um pacote de aplicativos do Service Fabric pronto para ser implantado.</span><span class="sxs-lookup"><span data-stu-id="88004-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="88004-110">Para obter mais informações sobre como criar e empacotar um aplicativo, leia sobre o [modelo de aplicativo do Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="88004-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="88004-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="88004-111">Overview</span></span>

<span data-ttu-id="88004-112">Para implantar um novo aplicativo, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="88004-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="88004-113">Faça upload de um pacote de aplicativos no repositório de imagens do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88004-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="88004-114">Provisione um tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-114">Provision an application type.</span></span>
3. <span data-ttu-id="88004-115">Especifique e crie um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-115">Specify and create an application.</span></span>
4. <span data-ttu-id="88004-116">Especifique e crie serviços.</span><span class="sxs-lookup"><span data-stu-id="88004-116">Specify and create services.</span></span>

<span data-ttu-id="88004-117">Para remover um aplicativo existente, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="88004-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="88004-118">Exclua o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-118">Delete the application.</span></span>
2. <span data-ttu-id="88004-119">Desprovisione o tipo de aplicativo associado.</span><span class="sxs-lookup"><span data-stu-id="88004-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="88004-120">Exclua o conteúdo do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="88004-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="88004-121">Implantar um novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="88004-121">Deploy a new application</span></span>

<span data-ttu-id="88004-122">Para implantar um novo aplicativo, execute as seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="88004-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="88004-123">Carregar um novo pacote de aplicativos no repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="88004-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="88004-124">Antes de criar um aplicativo, carregue o pacote de aplicativos no repositório de imagens do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="88004-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="88004-125">Por exemplo, se o seu pacote de aplicativos está no diretório `app_package_dir`, use os seguintes comandos para carregar o diretório:</span><span class="sxs-lookup"><span data-stu-id="88004-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="88004-126">Para pacotes de aplicativos grandes, especifique a opção `--show-progress` para exibir o progresso do upload.</span><span class="sxs-lookup"><span data-stu-id="88004-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="88004-127">Provisionar o tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="88004-127">Provision the application type</span></span>

<span data-ttu-id="88004-128">Quando o upload for concluído, provisione o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="88004-129">Para provisionar o aplicativo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="88004-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="88004-130">O valor de `application-type-build-path` é o nome do diretório em que você carregou o pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="88004-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="88004-131">Criar um aplicativo com base em um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="88004-131">Create an application from an application type</span></span>

<span data-ttu-id="88004-132">Depois de provisionar o aplicativo, use o seguinte comando para nomear e criar seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="88004-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="88004-133">`app-name` é o nome que você deseja usar para a instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="88004-134">Você pode obter parâmetros adicionais no manifesto do aplicativo provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="88004-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="88004-135">O nome do aplicativo deve começar com o prefixo `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="88004-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="88004-136">Criar serviços para o novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="88004-136">Create services for the new application</span></span>

<span data-ttu-id="88004-137">Depois de criar um aplicativo, crie serviços com base no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="88004-138">No exemplo a seguir, criamos um novo serviço sem estado com base em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="88004-139">Os serviços que podem ser criados por meio de um aplicativo estão definidos em um manifesto do serviço dentro do pacote de aplicativos provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="88004-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="88004-140">Verificar a integridade e a implantação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="88004-140">Verify application deployment and health</span></span>

<span data-ttu-id="88004-141">Para verificar se um aplicativo e um serviço foram implantados com êxito, verifique se o aplicativo e o serviço estão listados:</span><span class="sxs-lookup"><span data-stu-id="88004-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="88004-142">Para verificar se o serviço está íntegro, use comandos semelhantes para recuperar a integridade do serviço e do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="88004-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="88004-143">Os serviços e aplicativos íntegros têm um valor `HealthState` igual a `Ok`.</span><span class="sxs-lookup"><span data-stu-id="88004-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="88004-144">Remover um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="88004-144">Remove an existing application</span></span>

<span data-ttu-id="88004-145">Para remover um aplicativo, execute as seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="88004-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="88004-146">Excluir o aplicativo</span><span class="sxs-lookup"><span data-stu-id="88004-146">Delete the application</span></span>

<span data-ttu-id="88004-147">Para excluir o aplicativo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="88004-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="88004-148">Desprovisionar o tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="88004-148">Unprovision the application type</span></span>

<span data-ttu-id="88004-149">Depois de excluir o aplicativo, você pode desprovisionar o tipo de aplicativo se ele não for mais necessário.</span><span class="sxs-lookup"><span data-stu-id="88004-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="88004-150">Para desprovisionar o tipo de aplicativo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="88004-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="88004-151">O nome e a versão do tipo devem corresponder ao nome e à versão no manifesto do aplicativo provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="88004-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="88004-152">Excluir o pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="88004-152">Delete the application package</span></span>

<span data-ttu-id="88004-153">Depois de haver desprovisionado o tipo de aplicativo, você pode excluir o pacote de aplicativos do repositório de imagens, caso ele não seja mais necessário.</span><span class="sxs-lookup"><span data-stu-id="88004-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="88004-154">A exclusão de pacotes de aplicativos ajuda a recuperar o espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="88004-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="88004-155">Para excluir o pacote de aplicativos do repositório de imagens, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="88004-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="88004-156">`content-path` deve ser o nome do diretório que você carregou ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88004-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="88004-157">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="88004-157">Related articles</span></span>

* [<span data-ttu-id="88004-158">Introdução ao Service Fabric e à CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="88004-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="88004-159">Introdução à CLI XPlat do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88004-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
