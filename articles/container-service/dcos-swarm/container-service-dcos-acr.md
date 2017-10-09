---
title: "aaaUsing ACR com um cluster de SO/controlador de domínio do Azure | Microsoft Docs"
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
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="21531-104">Usar ACR com toodeploy de cluster um controlador de domínio/SO seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="21531-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="21531-105">Neste artigo, exploraremos como toouse registro de contêiner do Azure com um cluster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="21531-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="21531-106">Usando ACR permite tooprivately repositório e gerenciar imagens de contêiner.</span><span class="sxs-lookup"><span data-stu-id="21531-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="21531-107">Este tutorial aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="21531-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="21531-108">Implantar o Registro de Contêiner do Azure (se necessário)</span><span class="sxs-lookup"><span data-stu-id="21531-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="21531-109">Configurar a autenticação do ACR em um cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="21531-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="21531-110">Carregar uma imagem toohello registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="21531-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="21531-111">Executar uma imagem de contêiner de saudação do registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="21531-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="21531-112">Você precisa de um controlador de domínio/SO ACS saudação do cluster toocomplete as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="21531-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="21531-113">Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.</span><span class="sxs-lookup"><span data-stu-id="21531-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="21531-114">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="21531-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="21531-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="21531-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="21531-116">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="21531-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="21531-117">Implantar o Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="21531-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="21531-118">Se necessário, crie um registro de contêiner do Azure com hello [criar acr az](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="21531-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="21531-119">Olá, exemplo a seguir cria um registro com um nome de gerar aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="21531-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="21531-120">registro de saudação também é configurado com uma conta de administrador usando Olá `--admin-enabled` argumento.</span><span class="sxs-lookup"><span data-stu-id="21531-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="21531-121">Quando o registro de saudação tiver sido criado, Olá CLI do Azure gera dados semelhantes toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="21531-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="21531-122">Anote Olá `name` e `loginServer`, eles são usados em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="21531-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

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

<span data-ttu-id="21531-123">Obter credenciais de registro de contêiner hello usando Olá [Mostrar de credencial de acr az](/cli/azure/acr/credential) comando.</span><span class="sxs-lookup"><span data-stu-id="21531-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="21531-124">Olá substituto `--name` com hello um observado na última etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="21531-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="21531-125">Anote uma senha, ela será necessária em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="21531-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="21531-126">Para obter mais informações sobre o registro de contêiner do Azure, consulte [registros de contêiner de Docker Introdução tooprivate](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="21531-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="21531-127">Gerenciar a autenticação do ACR</span><span class="sxs-lookup"><span data-stu-id="21531-127">Manage ACR authentication</span></span>

<span data-ttu-id="21531-128">Olá convencional forma imagem toopush e recepção de um registro particular toofirst autenticar com o registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="21531-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="21531-129">toodo assim, você usaria Olá `docker login` comando em qualquer cliente que precisa do Registro particular do tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="21531-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="21531-130">Como um cluster de DC/OS pode conter muitos nós, todos precisam toobe autenticado com hello ACR, é útil tooautomate esse processo em cada nó.</span><span class="sxs-lookup"><span data-stu-id="21531-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="21531-131">Criar um armazenamento compartilhado</span><span class="sxs-lookup"><span data-stu-id="21531-131">Create shared storage</span></span>

<span data-ttu-id="21531-132">Esse processo usa um compartilhamento de arquivos do Azure que foi montado em cada nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="21531-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="21531-133">Se você ainda não definiu o armazenamento compartilhado, consulte [Criar e montar um compartilhamento de arquivos em um cluster de controlador de domínio/sistema operacional](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="21531-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="21531-134">Configurar a autenticação do ACR</span><span class="sxs-lookup"><span data-stu-id="21531-134">Configure ACR authentication</span></span>

<span data-ttu-id="21531-135">Primeiro, obtenha Olá FQDN do hello DC/SO mestre e armazená-lo em uma variável.</span><span class="sxs-lookup"><span data-stu-id="21531-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="21531-136">Crie uma conexão SSH com hello mestre (ou Olá primeiro mestre) do cluster baseado no controlador de domínio/sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="21531-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="21531-137">Atualize o nome de usuário de saudação se um valor padrão não foi usado durante a criação de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="21531-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="21531-138">Olá execução após o comando toologin toohello registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="21531-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="21531-139">Substituir saudação `--username` com o nome de saudação do registro de contêiner hello e hello `--password` com uma das senhas Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="21531-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="21531-140">Substituir o último argumento de saudação *mycontainerregistry.azurecr.io* no exemplo hello com o nome de loginServer de saudação do registro de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="21531-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="21531-141">Este comando armazena valores de autenticação Olá localmente em hello `~/.docker` caminho.</span><span class="sxs-lookup"><span data-stu-id="21531-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="21531-142">Crie um arquivo compactado que contém valores de autenticação Olá contêiner do registro.</span><span class="sxs-lookup"><span data-stu-id="21531-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="21531-143">Copie esse armazenamento de cluster compartilhado do arquivo toohello.</span><span class="sxs-lookup"><span data-stu-id="21531-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="21531-144">Esta etapa disponibiliza arquivo hello em todos os nós do cluster do hello DC/OS.</span><span class="sxs-lookup"><span data-stu-id="21531-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="21531-145">Carregar imagem tooACR</span><span class="sxs-lookup"><span data-stu-id="21531-145">Upload image tooACR</span></span>

<span data-ttu-id="21531-146">Agora um computador de desenvolvimento, ou qualquer outro sistema com o Docker instalado, crie uma imagem e carregá-lo toohello registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="21531-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="21531-147">Crie um recipiente de imagem do Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="21531-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="21531-148">Agora captura Olá contêiner em uma nova imagem.</span><span class="sxs-lookup"><span data-stu-id="21531-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="21531-149">nome da imagem Olá precisa Olá tooinclude `loginServer` nome da saudação contêiner registrywith um formato de `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="21531-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="21531-150">Faça logon em Olá registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="21531-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="21531-151">Substituir nome hello com o nome de loginServer hello, Olá - nome de usuário com o nome da saudação de registro de contêiner hello e hello – senha com uma das senhas Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="21531-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="21531-152">Por fim, carregue o registro da saudação imagem toohello ACR.</span><span class="sxs-lookup"><span data-stu-id="21531-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="21531-153">Este exemplo carrega uma imagem chamada dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="21531-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="21531-154">Execute uma imagem do ACR</span><span class="sxs-lookup"><span data-stu-id="21531-154">Run an image from ACR</span></span>

<span data-ttu-id="21531-155">toouse uma imagem do registro ACR hello, crie um arquivo de nomes de *acrDemo.json* e Olá cópia após o texto nela.</span><span class="sxs-lookup"><span data-stu-id="21531-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="21531-156">Substitua o nome de imagem Olá Olá contêiner do registro loginServer nome e imagem, por exemplo `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="21531-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="21531-157">Anote Olá `uris` propriedade.</span><span class="sxs-lookup"><span data-stu-id="21531-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="21531-158">Esta propriedade contém o local de saudação do arquivo autenticação do hello contêiner do registro, que nesse caso é o compartilhamento de arquivos do Azure de saudação montado em cada nó no cluster de DC/OS de saudação.</span><span class="sxs-lookup"><span data-stu-id="21531-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

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

<span data-ttu-id="21531-159">Implante o aplicativo de saudação com hello DC/OC CLI.</span><span class="sxs-lookup"><span data-stu-id="21531-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="21531-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21531-160">Next steps</span></span>

<span data-ttu-id="21531-161">Neste tutorial, você tem configurar toouse DC/OS registro de contêiner do Azure incluindo Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="21531-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="21531-162">Implantar o Registro de Contêiner do Azure (se necessário)</span><span class="sxs-lookup"><span data-stu-id="21531-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="21531-163">Configurar a autenticação do ACR em um cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="21531-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="21531-164">Carregar uma imagem toohello registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="21531-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="21531-165">Executar uma imagem de contêiner de saudação do registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="21531-165">Run a container image from hello Azure Container Registry</span></span>
