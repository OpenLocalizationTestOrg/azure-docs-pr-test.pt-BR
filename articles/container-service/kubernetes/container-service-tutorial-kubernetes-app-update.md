---
title: "Tutorial do Serviço de Contêiner do Azure – atualizar aplicativo"
description: "Tutorial do Serviço de Contêiner do Azure – atualizar aplicativo"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5ecaa3a79270e29ac002e91065f7df4f7e8914e7
ms.sourcegitcommit: 694e40a193980dea1e2f945471071f11030d5641
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2018
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="ca006-103">Atualizar um aplicativo no Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ca006-103">Update an application in Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="ca006-104">Depois que um aplicativo foi implantado no Kubernetes, ele pode ser atualizado especificando uma nova imagem de contêiner ou versão de imagem.</span><span class="sxs-lookup"><span data-stu-id="ca006-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="ca006-105">Ao fazer isso, a atualização é dividida em etapas para que apenas uma parte da implantação seja atualizada simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ca006-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="ca006-106">Essa atualização em etapas permite que o aplicativo continue em execução durante a atualização.</span><span class="sxs-lookup"><span data-stu-id="ca006-106">This staged update enables the application to keep running during the update.</span></span> <span data-ttu-id="ca006-107">Ela também oferece um mecanismo de reversão, caso ocorra uma falha de implantação.</span><span class="sxs-lookup"><span data-stu-id="ca006-107">It also provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="ca006-108">Neste tutorial, parte seis de sete, o aplicativo de exemplo Azure Vote é atualizado.</span><span class="sxs-lookup"><span data-stu-id="ca006-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="ca006-109">As tarefas a serem concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="ca006-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ca006-110">Atualizando o código do aplicativo front-end</span><span class="sxs-lookup"><span data-stu-id="ca006-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="ca006-111">Criando uma imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="ca006-111">Creating an updated container image</span></span>
> * <span data-ttu-id="ca006-112">Enviando a imagem de contêiner por push para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ca006-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="ca006-113">Implantando a imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="ca006-113">Deploying the updated container image</span></span>

<span data-ttu-id="ca006-114">Nos tutoriais subsequentes, o Operations Management Suite é configurado para monitorar o cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ca006-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ca006-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ca006-115">Before you begin</span></span>

<span data-ttu-id="ca006-116">Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, a imagem foi carregada no Registro de Contêiner do Azure e um cluster Kubernetes foi criado.</span><span class="sxs-lookup"><span data-stu-id="ca006-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="ca006-117">Em seguida, o aplicativo foi executado no cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ca006-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="ca006-118">Um repositório de aplicativo também foi clonado, o qual inclui o código-fonte do aplicativo e um arquivo do Docker Compose pré-criado usado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ca006-118">An application repository was also cloned which includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span></span> <span data-ttu-id="ca006-119">Verifique se você criou um clone do repositório e se você alterou os diretórios para o diretório clonado.</span><span class="sxs-lookup"><span data-stu-id="ca006-119">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span></span> <span data-ttu-id="ca006-120">Dentro está um diretório chamado `azure-vote` e um arquivo chamado `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="ca006-120">Inside is a directory named `azure-vote` and a file named `docker-compose.yml`.</span></span>

<span data-ttu-id="ca006-121">Se você ainda não completou essas etapas e deseja continuar acompanhando, retorne para [Tutorial 1 – Criar mensagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="ca006-121">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="ca006-122">Atualizar aplicativo</span><span class="sxs-lookup"><span data-stu-id="ca006-122">Update application</span></span>

<span data-ttu-id="ca006-123">Para este tutorial, é feita uma alteração no aplicativo e o aplicativo atualizado é implantado no cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ca006-123">For this tutorial, a change is made to the application, and the updated application deployed to the Kubernetes cluster.</span></span> 

<span data-ttu-id="ca006-124">O código-fonte do aplicativo pode ser encontrado no diretório `azure-vote`.</span><span class="sxs-lookup"><span data-stu-id="ca006-124">The application source code can be found inside of the `azure-vote` directory.</span></span> <span data-ttu-id="ca006-125">Abra o arquivo `config_file.cfg` com qualquer editor de texto ou de código.</span><span class="sxs-lookup"><span data-stu-id="ca006-125">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="ca006-126">Neste exemplo, `vi` é usado.</span><span class="sxs-lookup"><span data-stu-id="ca006-126">In this example `vi` is used.</span></span>

```bash
vi azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="ca006-127">Altere os valores de `VOTE1VALUE` e `VOTE2VALUE` e, em seguida, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="ca006-127">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="ca006-128">Salve e feche o arquivo.</span><span class="sxs-lookup"><span data-stu-id="ca006-128">Save and close the file.</span></span>

## <a name="update-container-image"></a><span data-ttu-id="ca006-129">Atualizar imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="ca006-129">Update container image</span></span>

<span data-ttu-id="ca006-130">Utilize [docker-compose](https://docs.docker.com/compose/) para recriar a imagem de front-end e executar o aplicativo atualizado.</span><span class="sxs-lookup"><span data-stu-id="ca006-130">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span> <span data-ttu-id="ca006-131">O argumento `--build` é usado para instruir o Docker Compose a recriar a imagem do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ca006-131">The `--build` argument is used to instruct Docker Compose to re-create the application image.</span></span>

```bash
docker-compose up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="ca006-132">Testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="ca006-132">Test application locally</span></span>

<span data-ttu-id="ca006-133">Navegue até http://localhost:8080 para ver o aplicativo atualizado.</span><span class="sxs-lookup"><span data-stu-id="ca006-133">Browse to http://localhost:8080 to see the updated application.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="ca006-135">Marcar e enviar mensagens por push</span><span class="sxs-lookup"><span data-stu-id="ca006-135">Tag and push images</span></span>

<span data-ttu-id="ca006-136">Marque a imagem `azure-vote-front` com o loginServer do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ca006-136">Tag the `azure-vote-front` image with the loginServer of the container registry.</span></span> 

<span data-ttu-id="ca006-137">Obter o nome do servidor de logon com o comando [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="ca006-137">Get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="ca006-138">Utilize a [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) para marcar a imagem.</span><span class="sxs-lookup"><span data-stu-id="ca006-138">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="ca006-139">Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure ou pelo nome do host do registro público.</span><span class="sxs-lookup"><span data-stu-id="ca006-139">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span> <span data-ttu-id="ca006-140">Note também que a versão da imagem é atualizada para `redis-v2`.</span><span class="sxs-lookup"><span data-stu-id="ca006-140">Also notice that the image version is updated to `redis-v2`.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="ca006-141">Utilize [docker push](https://docs.docker.com/engine/reference/commandline/push/) para carregar a imagem no seu registro.</span><span class="sxs-lookup"><span data-stu-id="ca006-141">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="ca006-142">Substitua `<acrLoginServer>` pelo nome do servidor de logon do Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca006-142">Replace `<acrLoginServer>` with your Azure Container Registry login server name.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="ca006-143">Implantar aplicativo de atualização</span><span class="sxs-lookup"><span data-stu-id="ca006-143">Deploy update application</span></span>

<span data-ttu-id="ca006-144">Para garantir o tempo de atividade máximo, várias instâncias do pod de aplicativos devem estar em execução.</span><span class="sxs-lookup"><span data-stu-id="ca006-144">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="ca006-145">Verifique essa configuração com o comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="ca006-145">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="ca006-146">Saída:</span><span class="sxs-lookup"><span data-stu-id="ca006-146">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="ca006-147">Se não houver vários pods executando a imagem do azure-vote-front, dimensione a implantação do `azure-vote-front`.</span><span class="sxs-lookup"><span data-stu-id="ca006-147">If you do not have multiple pods running the azure-vote-front image, scale the `azure-vote-front` deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="ca006-148">Para atualizar o aplicativo, utilize o comando [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set).</span><span class="sxs-lookup"><span data-stu-id="ca006-148">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="ca006-149">Atualize `<acrLoginServer>` com o servidor de logon ou o nome do host do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ca006-149">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="ca006-150">Para monitorar a implantação, use o comando [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="ca006-150">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="ca006-151">Conforme o aplicativo atualizado é implantado, os pods são encerrados e recriados com a nova imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ca006-151">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="ca006-152">Saída:</span><span class="sxs-lookup"><span data-stu-id="ca006-152">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="ca006-153">Testar aplicativo atualizado</span><span class="sxs-lookup"><span data-stu-id="ca006-153">Test updated application</span></span>

<span data-ttu-id="ca006-154">Obtenha o endereço IP externo do serviço `azure-vote-front`.</span><span class="sxs-lookup"><span data-stu-id="ca006-154">Get the external IP address of the `azure-vote-front` service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="ca006-155">Navegue até o endereço IP para ver o aplicativo atualizado.</span><span class="sxs-lookup"><span data-stu-id="ca006-155">Browse to the IP address to see the updated application.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="ca006-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca006-157">Next steps</span></span>

<span data-ttu-id="ca006-158">Neste tutorial, você atualizou um aplicativo e distribuiu essa atualização para um cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ca006-158">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="ca006-159">Concluímos as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="ca006-159">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ca006-160">Atualizamos o código do aplicativo front-end</span><span class="sxs-lookup"><span data-stu-id="ca006-160">Updated the front-end application code</span></span>
> * <span data-ttu-id="ca006-161">Criamos uma imagem de contêiner atualizada</span><span class="sxs-lookup"><span data-stu-id="ca006-161">Created an updated container image</span></span>
> * <span data-ttu-id="ca006-162">Enviamos a imagem de contêiner por push para o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ca006-162">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="ca006-163">Implantamos o aplicativo atualizado</span><span class="sxs-lookup"><span data-stu-id="ca006-163">Deployed the updated application</span></span>

<span data-ttu-id="ca006-164">Avance para o próximo tutorial para saber mais sobre como monitorar o Kubernetes com o Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="ca006-164">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca006-165">Monitorar o Kubernetes com o OMS</span><span class="sxs-lookup"><span data-stu-id="ca006-165">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)