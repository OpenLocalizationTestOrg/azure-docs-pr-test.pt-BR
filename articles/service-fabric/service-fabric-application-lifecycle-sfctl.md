---
title: Gerenciar aplicativos do Azure Service Fabric usando a CLI do Azure Service Fabric
description: Saiba como implantar e remover aplicativos de um cluster do Azure Service Fabric usando a CLI do Azure Service Fabric
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: c3a2eb3e6e54f952ef963bb2a0292d9ad7b53bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="d9dcf-103">Gerenciar um aplicativo do Azure Service Fabric usando a CLI do Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d9dcf-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="d9dcf-104">Saiba como criar e excluir os aplicativos que estão em execução em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9dcf-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9dcf-105">Prerequisites</span></span>

* <span data-ttu-id="d9dcf-106">Implantar a CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="d9dcf-107">Em seguida, selecione o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="d9dcf-108">Para obter mais informações, consulte [Introdução à CLI do Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d9dcf-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="d9dcf-109">Tenha um pacote de aplicativos do Service Fabric pronto para ser implantado.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="d9dcf-110">Para obter mais informações sobre como criar e empacotar um aplicativo, leia sobre o [modelo de aplicativo do Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="d9dcf-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="d9dcf-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d9dcf-111">Overview</span></span>

<span data-ttu-id="d9dcf-112">Para implantar um novo aplicativo, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="d9dcf-113">Faça upload de um pacote de aplicativos no repositório de imagens do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="d9dcf-114">Provisione um tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-114">Provision an application type.</span></span>
3. <span data-ttu-id="d9dcf-115">Especifique e crie um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-115">Specify and create an application.</span></span>
4. <span data-ttu-id="d9dcf-116">Especifique e crie serviços.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-116">Specify and create services.</span></span>

<span data-ttu-id="d9dcf-117">Para remover um aplicativo existente, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="d9dcf-118">Exclua o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-118">Delete the application.</span></span>
2. <span data-ttu-id="d9dcf-119">Desprovisione o tipo de aplicativo associado.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="d9dcf-120">Exclua o conteúdo do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="d9dcf-121">Implantar um novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-121">Deploy a new application</span></span>

<span data-ttu-id="d9dcf-122">Para implantar um novo aplicativo, execute as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-122">To deploy a new application, complete the following tasks:</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="d9dcf-123">Carregar um novo pacote de aplicativos no repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="d9dcf-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="d9dcf-124">Antes de criar um aplicativo, carregue o pacote de aplicativos no repositório de imagens do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span>

<span data-ttu-id="d9dcf-125">Por exemplo, se o seu pacote de aplicativos está no diretório `app_package_dir`, use os seguintes comandos para carregar o diretório:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="d9dcf-126">Para pacotes de aplicativos grandes, especifique a opção `--show-progress` para exibir o progresso do upload.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="d9dcf-127">Provisionar o tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-127">Provision the application type</span></span>

<span data-ttu-id="d9dcf-128">Quando o upload for concluído, provisione o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="d9dcf-129">Para provisionar o aplicativo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-129">To provision the application, use the following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="d9dcf-130">O valor de `application-type-build-path` é o nome do diretório em que você carregou o pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="d9dcf-131">Criar um aplicativo com base em um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-131">Create an application from an application type</span></span>

<span data-ttu-id="d9dcf-132">Depois de provisionar o aplicativo, use o seguinte comando para nomear e criar seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="d9dcf-133">`app-name` é o nome que você deseja usar para a instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="d9dcf-134">Você pode obter parâmetros adicionais no manifesto do aplicativo provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="d9dcf-135">O nome do aplicativo deve começar com o prefixo `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="d9dcf-136">Criar serviços para o novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-136">Create services for the new application</span></span>

<span data-ttu-id="d9dcf-137">Depois de criar um aplicativo, crie serviços com base no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="d9dcf-138">No exemplo a seguir, criamos um novo serviço sem estado com base em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="d9dcf-139">Os serviços que podem ser criados por meio de um aplicativo estão definidos em um manifesto do serviço dentro do pacote de aplicativos provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="d9dcf-140">Verificar a integridade e a implantação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-140">Verify application deployment and health</span></span>

<span data-ttu-id="d9dcf-141">Para verificar a integridade de todos os componentes, use os seguintes comandos de integridade:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-141">To verify everything is healthy, use the following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="d9dcf-142">Para verificar se o serviço está íntegro, use comandos semelhantes para recuperar a integridade do serviço e do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="d9dcf-143">Os serviços e aplicativos íntegros têm um valor `HealthState` igual a `Ok`.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="d9dcf-144">Remover um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="d9dcf-144">Remove an existing application</span></span>

<span data-ttu-id="d9dcf-145">Para remover um aplicativo, execute as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-145">To remove an application, complete the following tasks:</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="d9dcf-146">Excluir o aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-146">Delete the application</span></span>

<span data-ttu-id="d9dcf-147">Para excluir o aplicativo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-147">To delete the application, use the following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="d9dcf-148">Desprovisionar o tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-148">Unprovision the application type</span></span>

<span data-ttu-id="d9dcf-149">Depois de excluir o aplicativo, você pode desprovisionar o tipo de aplicativo se ele não for mais necessário.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="d9dcf-150">Para desprovisionar o tipo de aplicativo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-150">To unprovision the application type, use the following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="d9dcf-151">O nome e a versão do tipo devem corresponder ao nome e à versão no manifesto do aplicativo provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="d9dcf-152">Excluir o pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d9dcf-152">Delete the application package</span></span>

<span data-ttu-id="d9dcf-153">Depois de haver desprovisionado o tipo de aplicativo, você pode excluir o pacote de aplicativos do repositório de imagens, caso ele não seja mais necessário.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="d9dcf-154">A exclusão de pacotes de aplicativos ajuda a recuperar o espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="d9dcf-155">Para excluir o pacote de aplicativos do repositório de imagens, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="d9dcf-156">`content-path` deve ser o nome do diretório que você carregou ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="d9dcf-157">Atualizar aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9dcf-157">Upgrade application</span></span>

<span data-ttu-id="d9dcf-158">Após criar seu aplicativo, você pode repetir o mesmo conjunto de etapas para provisionar uma segunda versão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-158">After creating your application, you can repeat the same set of steps to provision a second version of your application.</span></span> <span data-ttu-id="d9dcf-159">Em seguida, com uma atualização do aplicativo do Service Fabric, você pode fazer a transição para executar a segunda versão do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-159">Then, with a Service Fabric application upgrade you can transition to running the second version of the application.</span></span> <span data-ttu-id="d9dcf-160">Para obter mais informações, consulte a documentação sobre [Atualizações de aplicativo do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="d9dcf-160">For more information, see the documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="d9dcf-161">Para realizar uma atualização, primeiro provisione a próxima versão do aplicativo usando os mesmos comandos que antes:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-161">To perform an upgrade, first provision the next version of the application using the same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="d9dcf-162">Em seguida, é recomendável realizar uma atualização automática monitorada. Inicie a atualização executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d9dcf-162">It is recommended then to perform a monitored automatic upgrade, launch the upgrade by running the following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="d9dcf-163">As atualizações substituem os parâmetros existentes por qualquer conjunto especificado.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="d9dcf-164">Parâmetros do aplicativo devem ser transmitidos como argumentos para o comando de atualização, se necessário.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-164">Application parameters should be passed as arguments to the upgrade command, if necessary.</span></span> <span data-ttu-id="d9dcf-165">Parâmetros do aplicativo devem ser codificados como um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="d9dcf-166">Para recuperar parâmetros especificados anteriormente, você pode usar o comando `sfctl application info`.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-166">To retrieve any parameters previously specified, you can use the `sfctl application info` command.</span></span>

<span data-ttu-id="d9dcf-167">Quando uma atualização de aplicativo estiver em andamento, o status poderá ser recuperado usando o comando `sfctl application upgrade-status`.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-167">When an application upgrade is in progress, the status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="d9dcf-168">Por fim, se uma atualização estiver em andamento e precisar ser cancelada, você poderá usar `sfctl application upgrade-rollback` para reverter a atualização.</span><span class="sxs-lookup"><span data-stu-id="d9dcf-168">Finally, if an upgrade is in progress and needs to be canceled, you can use the `sfctl application upgrade-rollback` to roll back the upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9dcf-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9dcf-169">Next steps</span></span>

* [<span data-ttu-id="d9dcf-170">Noções básicas do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d9dcf-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="d9dcf-171">Introdução ao Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="d9dcf-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="d9dcf-172">Iniciar uma atualização de aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d9dcf-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
