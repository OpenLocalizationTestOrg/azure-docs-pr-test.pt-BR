---
title: "tutorial de serviço de contêiner aaaAzure - gerenciar DC/OS | Microsoft Docs"
description: "Tutorial de Serviço de Contêiner do Azure – gerenciar DC/SO"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="4021c-104">Tutorial de Serviço de Contêiner do Azure – gerenciar DC/SO</span><span class="sxs-lookup"><span data-stu-id="4021c-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="4021c-105">DC/SO fornece uma plataforma distribuída para executar aplicativos modernos e em contêineres.</span><span class="sxs-lookup"><span data-stu-id="4021c-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="4021c-106">Com o Serviço de Contêiner do Azure, o provisionamento de um cluster de DC/SO pronto para produção é simples e rápido.</span><span class="sxs-lookup"><span data-stu-id="4021c-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="4021c-107">Esse início rápido detalhes as etapas básicas necessárias toodeploy um cluster de DC/OS e execução de carga de trabalho básica.</span><span class="sxs-lookup"><span data-stu-id="4021c-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4021c-108">Criar um cluster de DC/SO do ACS</span><span class="sxs-lookup"><span data-stu-id="4021c-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="4021c-109">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="4021c-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="4021c-110">Instalar Olá CLI DC/OS</span><span class="sxs-lookup"><span data-stu-id="4021c-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="4021c-111">Implantar um cluster de toohello do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4021c-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="4021c-112">Dimensionar um aplicativo no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="4021c-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="4021c-113">Expandir nós de cluster Olá DC/OS</span><span class="sxs-lookup"><span data-stu-id="4021c-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="4021c-114">Gerenciamento básico do DC/SO</span><span class="sxs-lookup"><span data-stu-id="4021c-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="4021c-115">Excluir Olá DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="4021c-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="4021c-116">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4021c-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4021c-117">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4021c-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4021c-118">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4021c-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="4021c-119">Criar cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="4021c-119">Create DC/OS cluster</span></span>

<span data-ttu-id="4021c-120">Primeiro, crie um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="4021c-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4021c-121">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4021c-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="4021c-122">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.</span><span class="sxs-lookup"><span data-stu-id="4021c-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="4021c-123">Em seguida, criar um cluster de DC/SO com hello [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="4021c-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="4021c-124">Olá, exemplo a seguir cria um cluster de DC/OS denominado *myDCOSCluster* e cria as chaves de SSH se eles ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="4021c-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="4021c-125">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="4021c-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="4021c-126">Após alguns minutos, o comando de Olá for concluída e retorna informações sobre a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4021c-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="4021c-127">Conecte-se o cluster tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="4021c-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="4021c-128">Quando um cluster de DC/SO tiver sido criado, ele poderá ser acessado por meio de um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="4021c-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="4021c-129">Execute Olá comando tooreturn Olá endereço IP público do mestre de controlador de domínio/OS Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="4021c-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="4021c-130">Esse endereço IP é armazenado em uma variável e usado na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="4021c-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="4021c-131">toocreate Olá túnel SSH, executar Olá comando a seguir e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="4021c-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="4021c-132">Se a porta 80 já está em uso, Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="4021c-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="4021c-133">Saudação de atualização encapsulado tooone de porta não está em uso, como `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="4021c-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="4021c-134">Instalar CLI de DC/SO</span><span class="sxs-lookup"><span data-stu-id="4021c-134">Install DC/OS CLI</span></span>

<span data-ttu-id="4021c-135">Instalar a cli do hello DC/OS usando Olá [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="4021c-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="4021c-136">Se você estiver usando o Azure CloudShell, Olá CLI DC/sistema operacional já está instalado.</span><span class="sxs-lookup"><span data-stu-id="4021c-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="4021c-137">Se você estiver executando Olá CLI do Azure em macOS ou Linux, talvez seja necessário um comando de saudação toorun com sudo.</span><span class="sxs-lookup"><span data-stu-id="4021c-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="4021c-138">Antes de Olá que CLI pode ser usado com cluster hello, deve ser túnel SSH Olá toouse configurado.</span><span class="sxs-lookup"><span data-stu-id="4021c-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="4021c-139">toodo assim, executar Olá comando a seguir, ajustando porta hello, se necessário.</span><span class="sxs-lookup"><span data-stu-id="4021c-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="4021c-140">Executar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="4021c-140">Run an application</span></span>

<span data-ttu-id="4021c-141">padrão de saudação mecanismo para um cluster ACS DC/OS de agendamento é maratona.</span><span class="sxs-lookup"><span data-stu-id="4021c-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="4021c-142">Maratona é toostart usado um aplicativo e gerenciar o estado de saudação do aplicativo hello no cluster de DC/OS de saudação.</span><span class="sxs-lookup"><span data-stu-id="4021c-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="4021c-143">tooschedule um aplicativo por meio da maratona, crie um arquivo chamado **app.json maratona**, e Olá cópia seguindo o conteúdo nele.</span><span class="sxs-lookup"><span data-stu-id="4021c-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="4021c-144">Execute Olá após o comando tooschedule Olá aplicativo toorun no cluster de DC/OS de saudação.</span><span class="sxs-lookup"><span data-stu-id="4021c-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="4021c-145">status da implantação toosee Olá para o aplicativo hello, executar Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4021c-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="4021c-146">Olá quando **tarefas** alterna o valor da coluna de *0/1* muito*1/1*, implantação do aplicativo foi concluída.</span><span class="sxs-lookup"><span data-stu-id="4021c-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="4021c-147">Dimensionar aplicativo Marathon</span><span class="sxs-lookup"><span data-stu-id="4021c-147">Scale Marathon application</span></span>

<span data-ttu-id="4021c-148">No exemplo anterior de saudação, um aplicativo de instância única foi criado.</span><span class="sxs-lookup"><span data-stu-id="4021c-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="4021c-149">tooupdate essa implantação para que as três instâncias do aplicativo hello estão disponíveis, abra o hello **maratona app.json** de arquivos e atualizar Olá too3 de propriedade de instância.</span><span class="sxs-lookup"><span data-stu-id="4021c-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="4021c-150">Atualizar o aplicativo hello usando Olá `dcos marathon app update` comando.</span><span class="sxs-lookup"><span data-stu-id="4021c-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="4021c-151">status da implantação toosee Olá para o aplicativo hello, executar Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4021c-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="4021c-152">Olá quando **tarefas** alterna o valor da coluna de *1/3* muito*3/1*, implantação do aplicativo foi concluída.</span><span class="sxs-lookup"><span data-stu-id="4021c-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="4021c-153">Execute o aplicativo acessível pela Internet</span><span class="sxs-lookup"><span data-stu-id="4021c-153">Run internet accessible app</span></span>

<span data-ttu-id="4021c-154">Olá ACS DC/OS cluster consiste em dois conjuntos de nó, Olá a um público que pode ser acessado na internet e um particular que não é acessível em Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="4021c-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="4021c-155">conjunto padrão de saudação é nós particular do hello, que foi usado no exemplo última hello.</span><span class="sxs-lookup"><span data-stu-id="4021c-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="4021c-156">toomake um aplicativo acessível na Olá da internet, implantá-los toohello conjunto de nós públicos.</span><span class="sxs-lookup"><span data-stu-id="4021c-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="4021c-157">toodo portanto, conceder Olá `acceptedResourceRoles` o valor do objeto `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="4021c-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="4021c-158">Crie um arquivo chamado **nginx public.json** e Olá cópia seguindo o conteúdo nele.</span><span class="sxs-lookup"><span data-stu-id="4021c-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="4021c-159">Execute Olá após o comando tooschedule Olá aplicativo toorun no cluster de DC/OS de saudação.</span><span class="sxs-lookup"><span data-stu-id="4021c-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="4021c-160">Obter o endereço IP público de Olá Olá DC/OS públicos de agentes do cluster.</span><span class="sxs-lookup"><span data-stu-id="4021c-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="4021c-161">Procurando toothis endereço retorna o site NGINX saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="4021c-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="4021c-163">Cluster de DC/SO de escala</span><span class="sxs-lookup"><span data-stu-id="4021c-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="4021c-164">Nos exemplos anteriores do hello, um aplicativo foi dimensionado toomultiple instância.</span><span class="sxs-lookup"><span data-stu-id="4021c-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="4021c-165">infraestrutura de DC/OS Olá também pode ser dimensionado tooprovide mais ou menos de capacidade de computação.</span><span class="sxs-lookup"><span data-stu-id="4021c-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="4021c-166">Isso é feito com hello [az acs dimensionar]() comando.</span><span class="sxs-lookup"><span data-stu-id="4021c-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="4021c-167">contagem atual do hello toosee dos agentes de DC/sistema operacional, use Olá [az acs Mostrar](/cli/azure/acs#show) comando.</span><span class="sxs-lookup"><span data-stu-id="4021c-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="4021c-168">tooincrease Olá too5 contagem, use Olá [az acs dimensionar](/cli/azure/acs#scale) comando.</span><span class="sxs-lookup"><span data-stu-id="4021c-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="4021c-169">Excluir cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="4021c-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="4021c-170">Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, cluster de DC/OS e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4021c-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="4021c-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4021c-171">Next steps</span></span>

<span data-ttu-id="4021c-172">Neste tutorial, você aprendeu sobre tarefas básicas de gerenciamento DC/sistema operacional incluindo Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="4021c-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4021c-173">Criar um cluster de DC/SO do ACS</span><span class="sxs-lookup"><span data-stu-id="4021c-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="4021c-174">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="4021c-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="4021c-175">Instalar Olá CLI DC/OS</span><span class="sxs-lookup"><span data-stu-id="4021c-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="4021c-176">Implantar um cluster de toohello do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4021c-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="4021c-177">Dimensionar um aplicativo no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="4021c-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="4021c-178">Expandir nós de cluster Olá DC/OS</span><span class="sxs-lookup"><span data-stu-id="4021c-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="4021c-179">Excluir Olá DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="4021c-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="4021c-180">Toohello antecipada próxima toolearn tutorial sobre como carregar o aplicativo balanceamento no controlador de domínio/sistema operacional no Azure.</span><span class="sxs-lookup"><span data-stu-id="4021c-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="4021c-181">Aplicativos de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="4021c-181">Load balance applications</span></span>](container-service-load-balancing.md)