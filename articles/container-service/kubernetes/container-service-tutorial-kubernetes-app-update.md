---
title: "tutorial de serviço de contêiner aaaAzure - aplicativo de atualização | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – atualizar aplicativo"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="0d487-104">Atualizar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0d487-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="0d487-105">Após implantar um aplicativo em Kubernetes, ele poderá ser atualizado especificando uma nova imagem de contêiner ou versão de imagem.</span><span class="sxs-lookup"><span data-stu-id="0d487-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="0d487-106">Quando você atualizar um aplicativo, distribuição de atualização de saudação preparada para que apenas uma parte da implantação de saudação é atualizada simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="0d487-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="0d487-107">Essa atualização em etapas permite Olá tookeep de aplicativo em execução durante a atualização de saudação e fornece um mecanismo de reversão se ocorrer uma falha de implantação.</span><span class="sxs-lookup"><span data-stu-id="0d487-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="0d487-108">Neste tutorial, parte seis sete, aplicativo de voto do Azure de exemplo hello é atualizado.</span><span class="sxs-lookup"><span data-stu-id="0d487-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="0d487-109">As tarefas a serem concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="0d487-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0d487-110">Atualizando o código do aplicativo front-end Olá</span><span class="sxs-lookup"><span data-stu-id="0d487-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="0d487-111">Criando uma imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="0d487-111">Creating an updated container image</span></span>
> * <span data-ttu-id="0d487-112">Enviar por push tooAzure de imagem de contêiner Olá registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="0d487-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="0d487-113">Implantação de imagem de contêiner atualizadas Olá</span><span class="sxs-lookup"><span data-stu-id="0d487-113">Deploying hello updated container image</span></span>

<span data-ttu-id="0d487-114">Em tutoriais subsequentes, Operations Management Suite é cluster de Kubernetes Olá toomonitor configurado.</span><span class="sxs-lookup"><span data-stu-id="0d487-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0d487-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0d487-115">Before you begin</span></span>

<span data-ttu-id="0d487-116">Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, imagem Olá carregado tooAzure registro de contêiner e um cluster Kubernetes criado.</span><span class="sxs-lookup"><span data-stu-id="0d487-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="0d487-117">aplicativo Hello, em seguida, foi executado no cluster de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="0d487-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="0d487-118">Se você não concluir essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="0d487-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="0d487-119">Atualizar aplicativo</span><span class="sxs-lookup"><span data-stu-id="0d487-119">Update application</span></span>

<span data-ttu-id="0d487-120">toocomplete Olá etapas deste tutorial, você deve ter uma cópia clonada de saudação aplicativo voto do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d487-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="0d487-121">Se necessário, crie essa cópia clonada com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d487-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="0d487-122">Olá abrir `config_file.cfg` arquivo com qualquer editor de texto ou código.</span><span class="sxs-lookup"><span data-stu-id="0d487-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="0d487-123">Você pode encontrar esse arquivo em Olá seguindo o diretório de repositório de saudação clonado.</span><span class="sxs-lookup"><span data-stu-id="0d487-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="0d487-124">Alterar valores de saudação do `VOTE1VALUE` e `VOTE2VALUE`e, em seguida, salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="0d487-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="0d487-125">Use [compor docker](https://docs.docker.com/compose/) toore-criar imagem de front-end hello e aplicativo hello execução atualizado.</span><span class="sxs-lookup"><span data-stu-id="0d487-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="0d487-126">Testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="0d487-126">Test application locally</span></span>

<span data-ttu-id="0d487-127">Procurar muito`http://localhost:8080` toosee Olá atualizado o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d487-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="0d487-129">Marcar e enviar mensagens por push</span><span class="sxs-lookup"><span data-stu-id="0d487-129">Tag and push images</span></span>

<span data-ttu-id="0d487-130">Saudação de marca *front do azure-voto* imagem com loginServer de saudação do registro de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d487-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="0d487-131">Se você estiver usando o registro de contêiner do Azure, obter o nome do servidor de logon de saudação com hello [lista de acr az](/cli/azure/acr#list) comando.</span><span class="sxs-lookup"><span data-stu-id="0d487-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="0d487-132">Use [marca docker](https://docs.docker.com/engine/reference/commandline/tag/) tootag imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d487-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="0d487-133">Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure ou pelo nome do host do registro público.</span><span class="sxs-lookup"><span data-stu-id="0d487-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="0d487-134">Use [push do docker](https://docs.docker.com/engine/reference/commandline/push/) tooyour registro da imagem de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="0d487-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="0d487-135">Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure ou pelo nome do host do registro público.</span><span class="sxs-lookup"><span data-stu-id="0d487-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="0d487-136">Implantar aplicativo de atualização</span><span class="sxs-lookup"><span data-stu-id="0d487-136">Deploy update application</span></span>

<span data-ttu-id="0d487-137">tempo de atividade máximo tooensure, devem estar executando várias instâncias do pod de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0d487-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="0d487-138">Verifique se essa configuração com hello [kubectl obter pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="0d487-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="0d487-139">Saída:</span><span class="sxs-lookup"><span data-stu-id="0d487-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="0d487-140">Se você não tiver vários compartimentos executando Olá front do azure-voto imagem, dimensionar Olá *front do azure-voto* implantação.</span><span class="sxs-lookup"><span data-stu-id="0d487-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="0d487-141">aplicativo de hello tooupdate, use Olá [kubectl conjunto](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) comando.</span><span class="sxs-lookup"><span data-stu-id="0d487-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="0d487-142">Atualização `<acrLoginServer>` com o nome de host ou servidor de logon de saudação do registro do contêiner.</span><span class="sxs-lookup"><span data-stu-id="0d487-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="0d487-143">implantação de saudação toomonitor, use Olá [kubectl obter pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="0d487-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="0d487-144">Como o aplicativo hello atualizado é implantado, seus compartimentos são encerrados e criados novamente com a nova imagem de contêiner Olá.</span><span class="sxs-lookup"><span data-stu-id="0d487-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="0d487-145">Saída:</span><span class="sxs-lookup"><span data-stu-id="0d487-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="0d487-146">Testar aplicativo atualizado</span><span class="sxs-lookup"><span data-stu-id="0d487-146">Test updated application</span></span>

<span data-ttu-id="0d487-147">Obter o endereço IP externo de saudação do hello *front do azure-voto* serviço.</span><span class="sxs-lookup"><span data-stu-id="0d487-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="0d487-148">Procurar toohello IP endereço toosee Olá atualizar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d487-148">Browse toohello IP address toosee hello updated application.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="0d487-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d487-150">Next steps</span></span>

<span data-ttu-id="0d487-151">Neste tutorial, você atualizou um aplicativo e distribuiu este cluster de Kubernetes tooa atualização.</span><span class="sxs-lookup"><span data-stu-id="0d487-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="0d487-152">Olá tarefas a seguir foram concluída:</span><span class="sxs-lookup"><span data-stu-id="0d487-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0d487-153">Código do aplicativo front-end Olá atualizado</span><span class="sxs-lookup"><span data-stu-id="0d487-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="0d487-154">Criamos uma imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="0d487-154">Created an updated container image</span></span>
> * <span data-ttu-id="0d487-155">Enviado por push tooAzure de imagem de contêiner Olá registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="0d487-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="0d487-156">Aplicativo implantado hello atualizado</span><span class="sxs-lookup"><span data-stu-id="0d487-156">Deployed hello updated application</span></span>

<span data-ttu-id="0d487-157">Avançar toohello toolearn próximo de tutorial sobre como toomonitor Kubernetes com o Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="0d487-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d487-158">Monitorar o Kubernetes com o OMS</span><span class="sxs-lookup"><span data-stu-id="0d487-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)