---
title: "Tutorial do Serviço de Contêiner do Azure – atualizar aplicativo | Microsoft Docs"
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
ms.openlocfilehash: db580da3e2d70892bc37305394df5be609ebb8a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="bc750-104">Atualizar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bc750-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="bc750-105">Após implantar um aplicativo em Kubernetes, ele poderá ser atualizado especificando uma nova imagem de contêiner ou versão de imagem.</span><span class="sxs-lookup"><span data-stu-id="bc750-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="bc750-106">Quando você atualizar um aplicativo, a distribuição de atualização é realizada em etapas para que apenas uma parte da implantação seja atualizada simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="bc750-106">When you update an application, the update rollout is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="bc750-107">Essa atualização em etapas permite que o aplicativo permaneça em execução durante a atualização e fornece um mecanismo de reversão, caso ocorra alguma falha de implantação.</span><span class="sxs-lookup"><span data-stu-id="bc750-107">This staged update enables the application to keep running during the update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="bc750-108">Neste tutorial, parte seis de sete, o aplicativo de exemplo Azure Vote é atualizado.</span><span class="sxs-lookup"><span data-stu-id="bc750-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="bc750-109">As tarefas a serem concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="bc750-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bc750-110">Atualizando o código do aplicativo front-end</span><span class="sxs-lookup"><span data-stu-id="bc750-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="bc750-111">Criando uma imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="bc750-111">Creating an updated container image</span></span>
> * <span data-ttu-id="bc750-112">Enviando a imagem de contêiner por push para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="bc750-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="bc750-113">Implantando a imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="bc750-113">Deploying the updated container image</span></span>

<span data-ttu-id="bc750-114">Nos tutoriais subsequentes, o Operations Management Suite é configurado para monitorar o cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bc750-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bc750-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bc750-115">Before you begin</span></span>

<span data-ttu-id="bc750-116">Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, a imagem foi carregada no Registro de Contêiner do Azure e um cluster Kubernetes foi criado.</span><span class="sxs-lookup"><span data-stu-id="bc750-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="bc750-117">Em seguida, o aplicativo foi executado no cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bc750-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="bc750-118">Se você ainda não completou essas etapas e deseja continuar acompanhando, retorne para [Tutorial 1 – Criar mensagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="bc750-118">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="bc750-119">Atualizar aplicativo</span><span class="sxs-lookup"><span data-stu-id="bc750-119">Update application</span></span>

<span data-ttu-id="bc750-120">Para concluir as etapas neste tutorial, você deve clonar uma cópia do aplicativo Voto do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc750-120">To complete the steps in this tutorial, you must have cloned a copy of the Azure Vote application.</span></span> <span data-ttu-id="bc750-121">Se necessário, crie essa cópia clonada com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bc750-121">If necessary, create this cloned copy with the following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="bc750-122">Abra o arquivo `config_file.cfg` com qualquer editor de texto ou de código.</span><span class="sxs-lookup"><span data-stu-id="bc750-122">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="bc750-123">Você pode encontrar esse arquivo no seguinte diretório do repositório clonado.</span><span class="sxs-lookup"><span data-stu-id="bc750-123">You can find this file under the following directory of the cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="bc750-124">Altere os valores de `VOTE1VALUE` e `VOTE2VALUE` e, em seguida, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="bc750-124">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="bc750-125">Utilize [docker-compose](https://docs.docker.com/compose/) para recriar a imagem de front-end e executar o aplicativo atualizado.</span><span class="sxs-lookup"><span data-stu-id="bc750-125">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="bc750-126">Testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="bc750-126">Test application locally</span></span>

<span data-ttu-id="bc750-127">Navegue até `http://localhost:8080` para ver o aplicativo atualizado.</span><span class="sxs-lookup"><span data-stu-id="bc750-127">Browse to `http://localhost:8080` to see the updated application.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="bc750-129">Marcar e enviar mensagens por push</span><span class="sxs-lookup"><span data-stu-id="bc750-129">Tag and push images</span></span>

<span data-ttu-id="bc750-130">Marque a imagem *azure-vote-front* com o loginServer do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="bc750-130">Tag the *azure-vote-front* image with the loginServer of the container registry.</span></span>

<span data-ttu-id="bc750-131">Se você estiver usando o Registro de Contêiner do Azure, obtenha o nome do servidor de logon com o comando [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="bc750-131">If you're using Azure Container Registry, get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="bc750-132">Utilize a [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) para marcar a imagem.</span><span class="sxs-lookup"><span data-stu-id="bc750-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="bc750-133">Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure ou pelo nome do host do registro público.</span><span class="sxs-lookup"><span data-stu-id="bc750-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="bc750-134">Utilize [docker push](https://docs.docker.com/engine/reference/commandline/push/) para carregar a imagem no seu registro.</span><span class="sxs-lookup"><span data-stu-id="bc750-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="bc750-135">Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure ou pelo nome do host do registro público.</span><span class="sxs-lookup"><span data-stu-id="bc750-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="bc750-136">Implantar aplicativo de atualização</span><span class="sxs-lookup"><span data-stu-id="bc750-136">Deploy update application</span></span>

<span data-ttu-id="bc750-137">Para garantir o tempo de atividade máximo, várias instâncias do pod de aplicativos devem estar em execução.</span><span class="sxs-lookup"><span data-stu-id="bc750-137">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="bc750-138">Verifique essa configuração com o comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="bc750-138">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="bc750-139">Saída:</span><span class="sxs-lookup"><span data-stu-id="bc750-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="bc750-140">Se não houver vários pods executando a imagem do azure-vote-front, dimensione a implantação do *azure-vote-front*.</span><span class="sxs-lookup"><span data-stu-id="bc750-140">If you don't have multiple pods running the azure-vote-front image, scale the *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="bc750-141">Para atualizar o aplicativo, utilize o comando [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set).</span><span class="sxs-lookup"><span data-stu-id="bc750-141">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="bc750-142">Atualize `<acrLoginServer>` com o servidor de logon ou o nome do host do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="bc750-142">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="bc750-143">Para monitorar a implantação, use o comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="bc750-143">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="bc750-144">Conforme o aplicativo atualizado é implantado, os pods são encerrados e recriados com a nova imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="bc750-144">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="bc750-145">Saída:</span><span class="sxs-lookup"><span data-stu-id="bc750-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="bc750-146">Testar aplicativo atualizado</span><span class="sxs-lookup"><span data-stu-id="bc750-146">Test updated application</span></span>

<span data-ttu-id="bc750-147">Obtenha o endereço IP externo do serviço *azure-vote-front*.</span><span class="sxs-lookup"><span data-stu-id="bc750-147">Get the external IP address of the *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="bc750-148">Navegue até o endereço IP para ver o aplicativo atualizado.</span><span class="sxs-lookup"><span data-stu-id="bc750-148">Browse to the IP address to see the updated application.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="bc750-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc750-150">Next steps</span></span>

<span data-ttu-id="bc750-151">Neste tutorial, você atualizou um aplicativo e distribuiu essa atualização para um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bc750-151">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="bc750-152">Concluímos as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="bc750-152">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bc750-153">Atualizamos o código do aplicativo front-end</span><span class="sxs-lookup"><span data-stu-id="bc750-153">Updated the front-end application code</span></span>
> * <span data-ttu-id="bc750-154">Criamos uma imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="bc750-154">Created an updated container image</span></span>
> * <span data-ttu-id="bc750-155">Enviamos a imagem de contêiner por push para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="bc750-155">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="bc750-156">Implantamos o aplicativo atualizado</span><span class="sxs-lookup"><span data-stu-id="bc750-156">Deployed the updated application</span></span>

<span data-ttu-id="bc750-157">Avance para o próximo tutorial para saber mais sobre como monitorar o Kubernetes com o Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="bc750-157">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc750-158">Monitorar o Kubernetes com o OMS</span><span class="sxs-lookup"><span data-stu-id="bc750-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)