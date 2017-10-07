---
title: "aaaAzure início rápido de serviço de contêiner - implantar DC/OS Cluster | Microsoft Docs"
description: "Início rápido do Serviço de Contêiner do Azure – implantar cluster de DC/SO"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="6b49f-104">Implantar um cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="6b49f-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="6b49f-105">DC/SO fornece uma plataforma distribuída para executar aplicativos modernos e em contêineres.</span><span class="sxs-lookup"><span data-stu-id="6b49f-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="6b49f-106">Com o Serviço de Contêiner do Azure, o provisionamento de um cluster de DC/SO pronto para produção é simples e rápido.</span><span class="sxs-lookup"><span data-stu-id="6b49f-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="6b49f-107">Este guia rápido detalhes Olá as etapas básicas necessárias toodeploy um cluster de DC/OS e execução de carga de trabalho básica.</span><span class="sxs-lookup"><span data-stu-id="6b49f-107">This quick start details hello basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="6b49f-108">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="6b49f-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="6b49f-109">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6b49f-109">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6b49f-110">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b49f-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6b49f-111">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b49f-111">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="6b49f-112">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b49f-112">Log in tooAzure</span></span> 

<span data-ttu-id="6b49f-113">Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="6b49f-113">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="6b49f-114">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6b49f-114">Create a resource group</span></span>

<span data-ttu-id="6b49f-115">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6b49f-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6b49f-116">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6b49f-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="6b49f-117">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="6b49f-117">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="6b49f-118">Criar cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="6b49f-118">Create DC/OS cluster</span></span>

<span data-ttu-id="6b49f-119">Criar um cluster de DC/SO com hello [az acs criar](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6b49f-119">Create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="6b49f-120">Olá, exemplo a seguir cria um cluster de DC/OS denominado *myDCOSCluster* e cria as chaves de SSH se eles ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="6b49f-120">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="6b49f-121">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="6b49f-121">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="6b49f-122">Após alguns minutos, o comando de Olá for concluída e retorna informações sobre a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b49f-122">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="6b49f-123">Conecte-se o cluster tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="6b49f-123">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="6b49f-124">Quando um cluster de DC/SO tiver sido criado, ele poderá ser acessado por meio de um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="6b49f-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="6b49f-125">Execute Olá comando tooreturn Olá endereço IP público do mestre de controlador de domínio/OS Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b49f-125">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="6b49f-126">Esse endereço IP é armazenado em uma variável e usado na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="6b49f-126">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="6b49f-127">toocreate Olá túnel SSH, executar Olá comando a seguir e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="6b49f-127">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="6b49f-128">Se a porta 80 já está em uso, Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="6b49f-128">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="6b49f-129">Saudação de atualização encapsulado tooone de porta não está em uso, como `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="6b49f-129">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="6b49f-130">túnel SSH Olá pode ser testado navegando muito`http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="6b49f-130">hello SSH tunnel can be tested by browsing too`http://localhost`.</span></span> <span data-ttu-id="6b49f-131">Se uma porta outros que 80 foi usada, ajustar Olá local toomatch.</span><span class="sxs-lookup"><span data-stu-id="6b49f-131">If a port other that 80 has been used, adjust hello location toomatch.</span></span> 

<span data-ttu-id="6b49f-132">Se o túnel SSH Olá foi criado com êxito, portal de DC/OS de saudação é retornado.</span><span class="sxs-lookup"><span data-stu-id="6b49f-132">If hello SSH tunnel was successfully created, hello DC/OS portal is returned.</span></span>

![INTERFACE DO USUÁRIO DE DC/SO](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="6b49f-134">Instalar CLI de DC/SO</span><span class="sxs-lookup"><span data-stu-id="6b49f-134">Install DC/OS CLI</span></span>

<span data-ttu-id="6b49f-135">interface de linha de comando Olá DC/sistema operacional é usada toomanage um cluster de DC/OS de saudação de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="6b49f-135">hello DC/OS command line interface is used toomanage a DC/OS cluster from hello command-line.</span></span> <span data-ttu-id="6b49f-136">Instalar a cli do hello DC/OS usando Olá [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="6b49f-136">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="6b49f-137">Se você estiver usando o Azure CloudShell, Olá CLI DC/sistema operacional já está instalado.</span><span class="sxs-lookup"><span data-stu-id="6b49f-137">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="6b49f-138">Se você estiver executando Olá CLI do Azure em macOS ou Linux, talvez seja necessário um comando de saudação toorun com sudo.</span><span class="sxs-lookup"><span data-stu-id="6b49f-138">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="6b49f-139">Antes de Olá que CLI pode ser usado com cluster hello, deve ser túnel SSH Olá toouse configurado.</span><span class="sxs-lookup"><span data-stu-id="6b49f-139">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="6b49f-140">toodo assim, executar Olá comando a seguir, ajustando porta hello, se necessário.</span><span class="sxs-lookup"><span data-stu-id="6b49f-140">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="6b49f-141">Executar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="6b49f-141">Run an application</span></span>

<span data-ttu-id="6b49f-142">padrão de saudação mecanismo para um cluster ACS DC/OS de agendamento é maratona.</span><span class="sxs-lookup"><span data-stu-id="6b49f-142">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="6b49f-143">Maratona é toostart usado um aplicativo e gerenciar o estado de saudação do aplicativo hello no cluster de DC/OS de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b49f-143">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="6b49f-144">tooschedule um aplicativo por meio da maratona, crie um arquivo chamado *app.json maratona*, e Olá cópia seguindo o conteúdo nele.</span><span class="sxs-lookup"><span data-stu-id="6b49f-144">tooschedule an application through Marathon, create a file named *marathon-app.json*, and copy hello following contents into it.</span></span> 

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

<span data-ttu-id="6b49f-145">Execute Olá após o comando tooschedule Olá aplicativo toorun no cluster de DC/OS de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b49f-145">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="6b49f-146">status da implantação toosee Olá para o aplicativo hello, executar Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b49f-146">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="6b49f-147">Olá quando **ESPERANDO** alterna o valor da coluna de *True* muito*False*, implantação do aplicativo foi concluída.</span><span class="sxs-lookup"><span data-stu-id="6b49f-147">When hello **WAITING** column value switches from *True* too*False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="6b49f-148">Obter o endereço IP público de Olá Olá DC/OS de agentes do cluster.</span><span class="sxs-lookup"><span data-stu-id="6b49f-148">Get hello public IP address of hello DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="6b49f-149">Procurando toothis endereço retorna o site NGINX saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="6b49f-149">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="6b49f-151">Excluir cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="6b49f-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="6b49f-152">Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, cluster de DC/OS e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6b49f-152">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="6b49f-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b49f-153">Next steps</span></span>

<span data-ttu-id="6b49f-154">Esse início rápido, você implantou um cluster de DC/OS e executar um simple contêiner do Docker no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b49f-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on hello cluster.</span></span> <span data-ttu-id="6b49f-155">toolearn mais sobre o serviço de contêiner do Azure, continuar toohello ACS tutoriais.</span><span class="sxs-lookup"><span data-stu-id="6b49f-155">toolearn more about Azure Container Service, continue toohello ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b49f-156">Gerenciar um cluster de DC/SO do ACS</span><span class="sxs-lookup"><span data-stu-id="6b49f-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)