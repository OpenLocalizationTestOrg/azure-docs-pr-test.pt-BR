---
title: "Tutorial de Serviço de Contêiner do Azure – gerenciar DC/SO | Microsoft Docs"
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
ms.openlocfilehash: e93f782c26c32f97749e817ec59ee3c2ecb7e119
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="23f45-104">Tutorial de Serviço de Contêiner do Azure – gerenciar DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="23f45-105">DC/SO fornece uma plataforma distribuída para executar aplicativos modernos e em contêineres.</span><span class="sxs-lookup"><span data-stu-id="23f45-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="23f45-106">Com o Serviço de Contêiner do Azure, o provisionamento de um cluster de DC/SO pronto para produção é simples e rápido.</span><span class="sxs-lookup"><span data-stu-id="23f45-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="23f45-107">Este início rápido detalha as etapas básicas necessárias para implantar um cluster do DC/SO e executar uma carga de trabalho básica.</span><span class="sxs-lookup"><span data-stu-id="23f45-107">This quick start details basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="23f45-108">Criar um cluster de DC/SO do ACS</span><span class="sxs-lookup"><span data-stu-id="23f45-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="23f45-109">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="23f45-109">Connect to the cluster</span></span>
> * <span data-ttu-id="23f45-110">Instalar a CLI de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-110">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="23f45-111">Implantar um aplicativo para o cluster</span><span class="sxs-lookup"><span data-stu-id="23f45-111">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="23f45-112">Dimensionar um aplicativo no cluster</span><span class="sxs-lookup"><span data-stu-id="23f45-112">Scale an application on the cluster</span></span>
> * <span data-ttu-id="23f45-113">Dimensionar os nós de cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-113">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="23f45-114">Gerenciamento básico do DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="23f45-115">Excluir o cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-115">Delete the DC/OS cluster</span></span>

<span data-ttu-id="23f45-116">Este tutorial requer a CLI do Azure, versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="23f45-116">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="23f45-117">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="23f45-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="23f45-118">Se você precisar atualizar, confira [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23f45-118">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="23f45-119">Criar cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-119">Create DC/OS cluster</span></span>

<span data-ttu-id="23f45-120">Primeiro, crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="23f45-120">First, create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="23f45-121">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="23f45-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="23f45-122">O seguinte exemplo cria um grupo de recursos chamado *myResourceGroup* no local *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="23f45-122">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="23f45-123">Em seguida, crie um cluster de DC/SO com o comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="23f45-123">Next, create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="23f45-124">O exemplo a seguir cria um cluster de DC/SO chamado *myDCOSCluster* e cria as chaves de SSH se elas ainda não existirem.</span><span class="sxs-lookup"><span data-stu-id="23f45-124">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="23f45-125">Para usar um conjunto específico de chaves, use a opção `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="23f45-125">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="23f45-126">Após alguns minutos, o comando é concluído e retorna informações sobre a implantação.</span><span class="sxs-lookup"><span data-stu-id="23f45-126">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="23f45-127">Conectar-se ao cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-127">Connect to DC/OS cluster</span></span>

<span data-ttu-id="23f45-128">Quando um cluster de DC/SO tiver sido criado, ele poderá ser acessado por meio de um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="23f45-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="23f45-129">Execute o seguinte comando para retornar o endereço IP público do mestre de DC/SO.</span><span class="sxs-lookup"><span data-stu-id="23f45-129">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="23f45-130">Esse endereço IP é armazenado em uma variável e usado na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="23f45-130">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="23f45-131">Para criar o túnel SSH, execute o seguinte comando e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="23f45-131">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="23f45-132">Se a porta 80 já estiver em uso, o comando falhará.</span><span class="sxs-lookup"><span data-stu-id="23f45-132">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="23f45-133">Atualize a porta em túnel para uma que não esteja em uso, como `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="23f45-133">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="23f45-134">Instalar CLI de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-134">Install DC/OS CLI</span></span>

<span data-ttu-id="23f45-135">Instale a CLI de DC/SO usando o comando [az acs dcos install-cli](/azure/acs/dcos#install-cli).</span><span class="sxs-lookup"><span data-stu-id="23f45-135">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="23f45-136">Se você estiver usando o Azure CloudShell, a CLI do DC/SO já estará instalada.</span><span class="sxs-lookup"><span data-stu-id="23f45-136">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> <span data-ttu-id="23f45-137">Se você estiver executando a CLI do Azure em macOS ou Linux, talvez precise executar o comando com sudo.</span><span class="sxs-lookup"><span data-stu-id="23f45-137">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="23f45-138">Antes de poder usar a CLI com o cluster, ela deve ser configurada para usar o túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="23f45-138">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="23f45-139">Para fazer isso, execute o comando a seguir, ajustando a porta, se necessário.</span><span class="sxs-lookup"><span data-stu-id="23f45-139">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="23f45-140">Executar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="23f45-140">Run an application</span></span>

<span data-ttu-id="23f45-141">O mecanismo de agendamento padrão para um cluster de DC/SO do ACS é o Marathon.</span><span class="sxs-lookup"><span data-stu-id="23f45-141">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="23f45-142">O Marathon é usado para iniciar um aplicativo e gerenciar o estado do aplicativo no cluster de DC/SO.</span><span class="sxs-lookup"><span data-stu-id="23f45-142">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="23f45-143">Para agendar um aplicativo por meio do Marathon, crie um arquivo chamado **marathon-app.json** e copie o seguinte conteúdo para ele.</span><span class="sxs-lookup"><span data-stu-id="23f45-143">To schedule an application through Marathon, create a file named **marathon-app.json**, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="23f45-144">Execute o seguinte comando para agendar o aplicativo para ser executado no cluster do DC/SO.</span><span class="sxs-lookup"><span data-stu-id="23f45-144">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="23f45-145">Para ver o status da implantação para o aplicativo, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="23f45-145">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="23f45-146">Quando o valor da coluna **TAREFAS** mudar de *0/1* para *1/1*, a implantação do aplicativo terá sido concluída.</span><span class="sxs-lookup"><span data-stu-id="23f45-146">When the **TASKS** column value switches from *0/1* to *1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="23f45-147">Dimensionar aplicativo Marathon</span><span class="sxs-lookup"><span data-stu-id="23f45-147">Scale Marathon application</span></span>

<span data-ttu-id="23f45-148">No exemplo anterior, um aplicativo de instância única foi criado.</span><span class="sxs-lookup"><span data-stu-id="23f45-148">In the previous example, a single instance application was created.</span></span> <span data-ttu-id="23f45-149">Para atualizar essa implantação para que as três instâncias do aplicativo estejam disponíveis, abra o arquivo **marathon-app.json** e atualize a propriedade da instância para 3.</span><span class="sxs-lookup"><span data-stu-id="23f45-149">To update this deployment so that three instances of the application are available, open up the **marathon-app.json** file, and update the instance property to 3.</span></span>

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

<span data-ttu-id="23f45-150">Atualizar o aplicativo usando o comando `dcos marathon app update`.</span><span class="sxs-lookup"><span data-stu-id="23f45-150">Update the application using the `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="23f45-151">Para ver o status da implantação para o aplicativo, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="23f45-151">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="23f45-152">Quando o valor da coluna **TAREFAS** mudar de *1/3* para *3/1*, a implantação do aplicativo terá sido concluída.</span><span class="sxs-lookup"><span data-stu-id="23f45-152">When the **TASKS** column value switches from *1/3* to *3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="23f45-153">Execute o aplicativo acessível pela Internet</span><span class="sxs-lookup"><span data-stu-id="23f45-153">Run internet accessible app</span></span>

<span data-ttu-id="23f45-154">O cluster DC/SO do ACS consiste em dois conjuntos de nó, um público, que pode ser acessado pela Internet, e um privado, que não está acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="23f45-154">The ACS DC/OS cluster consists of two node sets, one public which is accessible on the internet, and one private which is not accessible on the internet.</span></span> <span data-ttu-id="23f45-155">O conjunto padrão é o de nós privados, que foi usado no último exemplo.</span><span class="sxs-lookup"><span data-stu-id="23f45-155">The default set is the private nodes, which was used in the last example.</span></span>

<span data-ttu-id="23f45-156">Para disponibilizar um aplicativo pela Internet, implante-o no conjunto de nós públicos.</span><span class="sxs-lookup"><span data-stu-id="23f45-156">To make an application accessible on the internet, deploy them to the public node set.</span></span> <span data-ttu-id="23f45-157">Para fazer isso, dê ao objeto `acceptedResourceRoles` um valor de `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="23f45-157">To do so, give the `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="23f45-158">Crie um arquivo chamado **nginx-public.json** e copie o seguinte conteúdo para ele.</span><span class="sxs-lookup"><span data-stu-id="23f45-158">Create a file named **nginx-public.json** and copy the following contents into it.</span></span>

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

<span data-ttu-id="23f45-159">Execute o seguinte comando para agendar o aplicativo para ser executado no cluster do DC/SO.</span><span class="sxs-lookup"><span data-stu-id="23f45-159">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="23f45-160">Obtenha o endereço IP público dos agentes de cluster público DC/SO.</span><span class="sxs-lookup"><span data-stu-id="23f45-160">Get the public IP address of the DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="23f45-161">Navegar para esse endereço retorna o site NGINX padrão.</span><span class="sxs-lookup"><span data-stu-id="23f45-161">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="23f45-163">Cluster de DC/SO de escala</span><span class="sxs-lookup"><span data-stu-id="23f45-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="23f45-164">Nos exemplos anteriores, um aplicativo foi dimensionado para várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="23f45-164">In the previous examples, an application was scaled to multiple instance.</span></span> <span data-ttu-id="23f45-165">A infraestrutura do DC/SO também pode ser dimensionada para fornecer mais ou menos capacidade de computação.</span><span class="sxs-lookup"><span data-stu-id="23f45-165">The DC/OS infrastructure can also be scaled to provide more or less compute capacity.</span></span> <span data-ttu-id="23f45-166">Isso é feito com o comando [az acs scale]().</span><span class="sxs-lookup"><span data-stu-id="23f45-166">This is done with the [az acs scale]() command.</span></span> 

<span data-ttu-id="23f45-167">Para ver a contagem atual de agentes do DC/SO, use o comando [az acs show](/cli/azure/acs#show).</span><span class="sxs-lookup"><span data-stu-id="23f45-167">To see the current count of DC/OS agents, use the [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="23f45-168">Para aumentar a contagem para 5, use o comando [az acs scale](/cli/azure/acs#scale).</span><span class="sxs-lookup"><span data-stu-id="23f45-168">To increase the count to 5, use the [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="23f45-169">Excluir cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="23f45-170">Quando não for mais necessário, você pode usar o comando [az group delete](/cli/azure/group#delete) para remover o grupo de recursos, o cluster DC/SO todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="23f45-170">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="23f45-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23f45-171">Next steps</span></span>

<span data-ttu-id="23f45-172">Neste tutorial, você aprendeu sobre a tarefa básica de gerenciamento de DC/SO, incluindo as seguintes.</span><span class="sxs-lookup"><span data-stu-id="23f45-172">In this tutorial, you have learned about basic DC/OS management task including the following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="23f45-173">Criar um cluster de DC/SO do ACS</span><span class="sxs-lookup"><span data-stu-id="23f45-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="23f45-174">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="23f45-174">Connect to the cluster</span></span>
> * <span data-ttu-id="23f45-175">Instalar a CLI de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-175">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="23f45-176">Implantar um aplicativo para o cluster</span><span class="sxs-lookup"><span data-stu-id="23f45-176">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="23f45-177">Dimensionar um aplicativo no cluster</span><span class="sxs-lookup"><span data-stu-id="23f45-177">Scale an application on the cluster</span></span>
> * <span data-ttu-id="23f45-178">Dimensionar os nós de cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-178">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="23f45-179">Excluir o cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="23f45-179">Delete the DC/OS cluster</span></span>

<span data-ttu-id="23f45-180">Avance para o próximo tutorial para saber mais sobre o aplicativo de balanceamento de carga no DC/SO no Azure.</span><span class="sxs-lookup"><span data-stu-id="23f45-180">Advance to the next tutorial to learn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="23f45-181">Aplicativos de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="23f45-181">Load balance applications</span></span>](container-service-load-balancing.md)