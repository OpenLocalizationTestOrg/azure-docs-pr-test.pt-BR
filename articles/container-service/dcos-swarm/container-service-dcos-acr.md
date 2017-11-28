---
title: Usando ACR com um cluster DC/OS do Azure | Microsoft Docs
description: "Usar um Registro de Contêiner do Azure com um cluster DC/OS no Serviço de Contêiner do Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 618d32ca919e50d41b85c800225fe72c3b94e537
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="c360a-104">Usar ACR com um cluster DC/OS para implantar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c360a-104">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="c360a-105">Neste artigo, exploraremos como usar o Registro de Contêiner do Azure com um cluster de DC/SO.</span><span class="sxs-lookup"><span data-stu-id="c360a-105">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="c360a-106">Usar o ACR permite armazenar e gerenciar imagens de contêiner de forma privada.</span><span class="sxs-lookup"><span data-stu-id="c360a-106">Using ACR allows you to privately store and manage container images.</span></span> <span data-ttu-id="c360a-107">Este tutorial cobre as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="c360a-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c360a-108">Implantar o Registro de Contêiner do Azure (se necessário)</span><span class="sxs-lookup"><span data-stu-id="c360a-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="c360a-109">Configurar a autenticação do ACR em um cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="c360a-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="c360a-110">Uma imagem carregada no Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="c360a-110">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="c360a-111">Executar uma imagem de contêiner do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="c360a-111">Run a container image from the Azure Container Registry</span></span>

<span data-ttu-id="c360a-112">É necessário um cluster de DC/SO do ACS para concluir as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="c360a-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="c360a-113">Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.</span><span class="sxs-lookup"><span data-stu-id="c360a-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="c360a-114">Este tutorial requer a CLI do Azure, versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c360a-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c360a-115">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="c360a-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="c360a-116">Se você precisar atualizar, confira [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c360a-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="c360a-117">Implantar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="c360a-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="c360a-118">Se necessário, crie um Registro de Contêiner do Azure com o comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="c360a-118">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="c360a-119">O exemplo a seguir cria um registro com um nome gerado aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="c360a-119">The following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="c360a-120">O registro também é configurado com uma conta do administrador usando o argumento `--admin-enabled`.</span><span class="sxs-lookup"><span data-stu-id="c360a-120">The registry is also configured with an admin account using the `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="c360a-121">Quando o registro tiver sido criado, a CLI do Azure gerará dados semelhantes aos seguintes.</span><span class="sxs-lookup"><span data-stu-id="c360a-121">Once the registry has been created, the Azure CLI outputs data similar to the following.</span></span> <span data-ttu-id="c360a-122">Anote `name` e `loginServer`, eles serão usados em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="c360a-122">Take note of the `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="c360a-123">Obtenha as credenciais de registro de contêiner usando o comando [az acr credential show](/cli/azure/acr/credential).</span><span class="sxs-lookup"><span data-stu-id="c360a-123">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="c360a-124">Substitua o `--name` pelo anotado na última etapa.</span><span class="sxs-lookup"><span data-stu-id="c360a-124">Substitute the `--name` with the one noted in the last step.</span></span> <span data-ttu-id="c360a-125">Anote uma senha, ela será necessária em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="c360a-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="c360a-126">Para obter mais informações sobre o Registro de Contêiner do Azure, consulte [Introdução aos registros de contêiner do Docker privado](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="c360a-126">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="c360a-127">Gerenciar a autenticação do ACR</span><span class="sxs-lookup"><span data-stu-id="c360a-127">Manage ACR authentication</span></span>

<span data-ttu-id="c360a-128">A maneira convencional de enviar uma imagem por push e de efetuar pull dela de um registro privado é primeiro autenticar no registro.</span><span class="sxs-lookup"><span data-stu-id="c360a-128">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span></span> <span data-ttu-id="c360a-129">Para fazer isso, use o comando `docker login` em qualquer cliente que precise acessar o registro privado.</span><span class="sxs-lookup"><span data-stu-id="c360a-129">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span></span> <span data-ttu-id="c360a-130">Como um cluster de DC/SO pode conter muitos nós que precisam ser autenticados com o ACR, é útil automatizar esse processo em cada nó.</span><span class="sxs-lookup"><span data-stu-id="c360a-130">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="c360a-131">Criar um armazenamento compartilhado</span><span class="sxs-lookup"><span data-stu-id="c360a-131">Create shared storage</span></span>

<span data-ttu-id="c360a-132">Esse processo usa um compartilhamento de arquivos do Azure que foi montado em cada nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="c360a-132">This process uses an Azure file share that has been mounted on each node in the cluster.</span></span> <span data-ttu-id="c360a-133">Se você ainda não definiu o armazenamento compartilhado, consulte [Criar e montar um compartilhamento de arquivos em um cluster de controlador de domínio/sistema operacional](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="c360a-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="c360a-134">Configurar a autenticação do ACR</span><span class="sxs-lookup"><span data-stu-id="c360a-134">Configure ACR authentication</span></span>

<span data-ttu-id="c360a-135">Primeiro, obtenha o FQDN do mestre de DC/SO e armazene-o em uma variável.</span><span class="sxs-lookup"><span data-stu-id="c360a-135">First, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="c360a-136">Crie uma conexão SSH com o mestre (ou o primeiro mestre) do cluster baseado no DC/SO.</span><span class="sxs-lookup"><span data-stu-id="c360a-136">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="c360a-137">Atualize o nome de usuário se um valor não padrão tiver sido usado ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="c360a-137">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="c360a-138">Execute o seguinte comando para fazer logon no Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="c360a-138">Run the following command to login to the Azure Container Registry.</span></span> <span data-ttu-id="c360a-139">Substitua `--username` pelo o nome do registro de contêiner e `--password` por uma das senhas fornecidas.</span><span class="sxs-lookup"><span data-stu-id="c360a-139">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span></span> <span data-ttu-id="c360a-140">Substitua o último argumento *mycontainerregistry.azurecr.io* no exemplo pelo nome de loginServer de registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="c360a-140">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span></span> 

<span data-ttu-id="c360a-141">Este comando armazena os valores de autenticação localmente no caminho `~/.docker`.</span><span class="sxs-lookup"><span data-stu-id="c360a-141">This command stores the authentication values locally under the `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="c360a-142">Crie um arquivo compactado que contenha os valores de autenticação do registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="c360a-142">Create a compressed file that contains the container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="c360a-143">Copie esse arquivo no armazenamento de cluster compartilhado.</span><span class="sxs-lookup"><span data-stu-id="c360a-143">Copy this file to the cluster shared storage.</span></span> <span data-ttu-id="c360a-144">Esta etapa disponibiliza o arquivo em todos os nós de cluster de DC/SO.</span><span class="sxs-lookup"><span data-stu-id="c360a-144">This step makes the file available on all nodes of the DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-to-acr"></a><span data-ttu-id="c360a-145">Carregar imagem no ACR</span><span class="sxs-lookup"><span data-stu-id="c360a-145">Upload image to ACR</span></span>

<span data-ttu-id="c360a-146">Agora de um computador de desenvolvimento ou de qualquer outro sistema com o Docker instalado, crie uma imagem e carregue-a no Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="c360a-146">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span></span>

<span data-ttu-id="c360a-147">Crie um contêiner da imagem do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c360a-147">Create a container from the Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="c360a-148">Agora, capture o contêiner em uma nova imagem.</span><span class="sxs-lookup"><span data-stu-id="c360a-148">Now capture the container into a new image.</span></span> <span data-ttu-id="c360a-149">O nome da imagem precisa incluir o nome do `loginServer` do registro de contêiner com o formato `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="c360a-149">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="c360a-150">Faça logon no Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="c360a-150">Login into the Azure Container Registry.</span></span> <span data-ttu-id="c360a-151">Substitua o nome pelo nome de loginServer, --username pelo o nome do registro de contêiner e --password por uma das senhas fornecidas.</span><span class="sxs-lookup"><span data-stu-id="c360a-151">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="c360a-152">Por fim, carregue a imagem no registro do ACR.</span><span class="sxs-lookup"><span data-stu-id="c360a-152">Finally, upload the image to the ACR registry.</span></span> <span data-ttu-id="c360a-153">Este exemplo carrega uma imagem chamada dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="c360a-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="c360a-154">Execute uma imagem do ACR</span><span class="sxs-lookup"><span data-stu-id="c360a-154">Run an image from ACR</span></span>

<span data-ttu-id="c360a-155">Para usar uma imagem do registro ACR, crie um arquivo chamado *acrDemo.json* e copie o seguinte texto nele.</span><span class="sxs-lookup"><span data-stu-id="c360a-155">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span></span> <span data-ttu-id="c360a-156">Substitua o nome da imagem pelo nome de loginServer do registro de contêiner e pelo nome da imagem, por exemplo `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="c360a-156">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="c360a-157">Anote a propriedade `uris`.</span><span class="sxs-lookup"><span data-stu-id="c360a-157">Take note of the `uris` property.</span></span> <span data-ttu-id="c360a-158">Esta propriedade contém o local do arquivo de autenticação do registro de contêiner, que nesse caso é o compartilhamento de arquivos do Azure que está montado em cada nó do cluster de DC/SO.</span><span class="sxs-lookup"><span data-stu-id="c360a-158">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="c360a-159">Implante o aplicativo com a CLI do DC/OC.</span><span class="sxs-lookup"><span data-stu-id="c360a-159">Deploy the application with the DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="c360a-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c360a-160">Next steps</span></span>

<span data-ttu-id="c360a-161">Neste tutorial, você configurou o DC/SO para usar o Registro de Contêiner do Azure, incluindo as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="c360a-161">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c360a-162">Implantar o Registro de Contêiner do Azure (se necessário)</span><span class="sxs-lookup"><span data-stu-id="c360a-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="c360a-163">Configurar a autenticação do ACR em um cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="c360a-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="c360a-164">Uma imagem carregada no Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="c360a-164">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="c360a-165">Executar uma imagem de contêiner do Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="c360a-165">Run a container image from the Azure Container Registry</span></span>
