---
title: "Balancear a carga de contêineres em um cluster do Azure DC/OS | Microsoft Docs"
description: "Balancear a carga entre vários contêineres em um cluster do Serviço de Contêiner do Azure DC/OS."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, Microsserviços, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 78725c9d23e13d307821a188028ef573d1def038
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="c209f-104">Balancear a carga de contêineres em um cluster do Serviço de Contêiner do Azure DC/OS</span><span class="sxs-lookup"><span data-stu-id="c209f-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="c209f-105">Neste artigo, exploramos como criar um balanceador de carga interno em um Serviço de Contêiner do Azure gerenciado por DC/SO usando o Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="c209f-105">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="c209f-106">Essa configuração permite que você dimensione seus aplicativos horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="c209f-106">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="c209f-107">Também permite que você aproveite os clusters de agentes públicos e privados colocando seus balanceadores de carga no cluster público e seus contêineres de aplicativo no cluster privado.</span><span class="sxs-lookup"><span data-stu-id="c209f-107">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="c209f-108">Neste tutorial, você:</span><span class="sxs-lookup"><span data-stu-id="c209f-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c209f-109">Configurar um balanceador de carga do Marathon</span><span class="sxs-lookup"><span data-stu-id="c209f-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="c209f-110">Implantar um aplicativo usando o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c209f-110">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="c209f-111">Configurar um Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c209f-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="c209f-112">É necessário um cluster de DC/SO do ACS para concluir as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="c209f-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="c209f-113">Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.</span><span class="sxs-lookup"><span data-stu-id="c209f-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="c209f-114">Este tutorial requer a CLI do Azure, versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c209f-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c209f-115">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="c209f-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="c209f-116">Se você precisar atualizar, confira [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c209f-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="c209f-117">Visão geral do balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="c209f-117">Load balancing overview</span></span>

<span data-ttu-id="c209f-118">Há duas camadas de balanceamento de carga em um cluster de DC/SO do Serviço de Contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="c209f-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="c209f-119">O **Azure Load Balancer** fornece pontos de entrada públicos (aqueles que os usuários finais acessarão).</span><span class="sxs-lookup"><span data-stu-id="c209f-119">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="c209f-120">Um Azure LB é fornecido automaticamente pelo Serviço de Contêiner do Azure e, por padrão, é configurado para exibir as portas 80, 443 e 8080.</span><span class="sxs-lookup"><span data-stu-id="c209f-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="c209f-121">O **Balanceador de Carga Marathon** (marathon-lb) encaminha as solicitações de entrada às instâncias do contêiner que atendem a essas solicitações.</span><span class="sxs-lookup"><span data-stu-id="c209f-121">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="c209f-122">Conforme dimensionamos os contêineres fornecendo nosso serviço Web, o marathon-lb adapta-se dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="c209f-122">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="c209f-123">Esse balanceador de carga não é fornecido por padrão em seu Serviço de Contêiner, mas é muito fácil de instalar.</span><span class="sxs-lookup"><span data-stu-id="c209f-123">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="c209f-124">Configurar Balanceador de Carga Marathon</span><span class="sxs-lookup"><span data-stu-id="c209f-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="c209f-125">O Balanceador de Carga do Marathon reconfigura dinamicamente baseado nos contêineres que você implantou.</span><span class="sxs-lookup"><span data-stu-id="c209f-125">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="c209f-126">Ele também é resistente à perda de um contêiner ou de um agente. Se isso ocorrer, o Apache Mesos reiniciará o contêiner em outro lugar e o marathon-lb se adaptará.</span><span class="sxs-lookup"><span data-stu-id="c209f-126">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="c209f-127">Execute o seguinte comando para instalar o balanceador de carga Marathon no cluster do agente público.</span><span class="sxs-lookup"><span data-stu-id="c209f-127">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="c209f-128">Implantar aplicativo com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="c209f-128">Deploy load balanced application</span></span>

<span data-ttu-id="c209f-129">Agora que temos o pacote marathon-lb, podemos implantar um contêiner de aplicativo para o qual desejamos balancear a carga.</span><span class="sxs-lookup"><span data-stu-id="c209f-129">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="c209f-130">Primeiro, obtenha o FQDN dos agentes expostos publicamente.</span><span class="sxs-lookup"><span data-stu-id="c209f-130">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="c209f-131">Em seguida, crie um arquivo chamado *hello-web.json* e copie o seguinte conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c209f-131">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="c209f-132">O rótulo `HAPROXY_0_VHOST` precisa ser atualizado com o FQDN dos agentes DC/SO.</span><span class="sxs-lookup"><span data-stu-id="c209f-132">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
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
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="c209f-133">Use a CLI do DC/SO para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c209f-133">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="c209f-134">Por padrão, o Marathon implanta o aplicativo no cluster privado.</span><span class="sxs-lookup"><span data-stu-id="c209f-134">By default Marathon deploys the the applicaton to the private cluster.</span></span> <span data-ttu-id="c209f-135">Isso significa que a implantação acima está acessível apenas por meio do balanceador de carga, que geralmente é o comportamento desejado.</span><span class="sxs-lookup"><span data-stu-id="c209f-135">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="c209f-136">Depois que o aplicativo tiver sido implantado, navegue até o FQDN do cluster do agente para exibir o aplicativo com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="c209f-136">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![Imagem do aplicativo com balanceamento de carga](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="c209f-138">Configurar o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c209f-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="c209f-139">Por padrão, o Azure Load Balancer expõe as portas 80, 8080 e 443.</span><span class="sxs-lookup"><span data-stu-id="c209f-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="c209f-140">Se você estiver usando uma dessas três portas (como ocorre no exemplo acima), não haverá mais nada a fazer.</span><span class="sxs-lookup"><span data-stu-id="c209f-140">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="c209f-141">Você deve conseguir atingir o FQDN do balanceador de carga do agente e, cada vez que atualizar, encontrará um dos três servidores Web em round robin.</span><span class="sxs-lookup"><span data-stu-id="c209f-141">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="c209f-142">Se você usar uma porta diferente, precisará adicionar uma regra de round robin e uma investigação ao balanceador de carga para a porta usada.</span><span class="sxs-lookup"><span data-stu-id="c209f-142">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="c209f-143">Você pode fazer isso na [CLI do Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md) com os comandos `azure network lb rule create` e `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="c209f-143">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c209f-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c209f-144">Next steps</span></span>

<span data-ttu-id="c209f-145">Neste tutorial, você aprendeu sobre balanceamento de carga no ACS com os maratona balanceadores de carga Marathon e Azure, incluindo as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="c209f-145">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c209f-146">Configurar um balanceador de carga do Marathon</span><span class="sxs-lookup"><span data-stu-id="c209f-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="c209f-147">Implantar um aplicativo usando o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c209f-147">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="c209f-148">Configurar um Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c209f-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="c209f-149">Avance para o próximo tutorial para saber mais sobre como integrar o armazenamento do Azure ao DC/SO no Azure.</span><span class="sxs-lookup"><span data-stu-id="c209f-149">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c209f-150">Montar o compartilhamento de arquivos do Azure no cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="c209f-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)