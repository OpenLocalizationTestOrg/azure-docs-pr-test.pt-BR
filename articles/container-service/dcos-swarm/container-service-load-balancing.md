---
title: "contêineres de saldo de aaaLoad no cluster do Azure DC/sistema operacional | Microsoft Docs"
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
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="dc22f-104">Balancear a carga de contêineres em um cluster do Serviço de Contêiner do Azure DC/OS</span><span class="sxs-lookup"><span data-stu-id="dc22f-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="dc22f-105">Neste artigo, vamos explorar como toocreate um balanceador de carga interno em um controlador de domínio/sistema operacional gerenciado usando maratona balanceamento de carga de serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc22f-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="dc22f-106">Essa configuração permite a você tooscale seus aplicativos horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="dc22f-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="dc22f-107">Ele também permite tootake vantagem de clusters de agente públicas e privadas de saudação colocando seu balanceadores de carga no cluster público hello e seus contêineres de aplicativos em cluster privada hello.</span><span class="sxs-lookup"><span data-stu-id="dc22f-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="dc22f-108">Neste tutorial, você:</span><span class="sxs-lookup"><span data-stu-id="dc22f-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc22f-109">Configurar um balanceador de carga do Marathon</span><span class="sxs-lookup"><span data-stu-id="dc22f-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="dc22f-110">Implantar um aplicativo usando Olá balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="dc22f-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="dc22f-111">Configurar um Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="dc22f-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="dc22f-112">Você precisa de um controlador de domínio/SO ACS saudação do cluster toocomplete as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="dc22f-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="dc22f-113">Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.</span><span class="sxs-lookup"><span data-stu-id="dc22f-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="dc22f-114">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="dc22f-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dc22f-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc22f-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dc22f-116">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dc22f-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="dc22f-117">Visão geral do balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="dc22f-117">Load balancing overview</span></span>

<span data-ttu-id="dc22f-118">Há duas camadas de balanceamento de carga em um cluster de DC/SO do Serviço de Contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="dc22f-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="dc22f-119">**O balanceador de carga do Azure** fornece pontos de entrada pública (Olá aqueles que os usuários finais acessar).</span><span class="sxs-lookup"><span data-stu-id="dc22f-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="dc22f-120">Um balanceamento de carga do Azure é fornecido automaticamente pelo serviço de contêiner do Azure e é, por padrão, a porta configurada tooexpose 80, 443 e 8080.</span><span class="sxs-lookup"><span data-stu-id="dc22f-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="dc22f-121">**Olá maratona balanceador de carga (lb maratona)** rotas instâncias de toocontainer solicitações que atendem a essas solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="dc22f-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="dc22f-122">Como podemos dimensionar contêineres Olá fornecendo nosso serviço web, Olá maratona lb se adapta dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="dc22f-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="dc22f-123">Esse balanceador de carga não é fornecida por padrão em seu serviço de contêiner, mas é fácil tooinstall.</span><span class="sxs-lookup"><span data-stu-id="dc22f-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="dc22f-124">Configurar Balanceador de Carga Marathon</span><span class="sxs-lookup"><span data-stu-id="dc22f-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="dc22f-125">Balanceador de carga maratona reconfigura dinamicamente com base em contêineres de saudação que você implantou.</span><span class="sxs-lookup"><span data-stu-id="dc22f-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="dc22f-126">Também é toohello resiliente perda de um contêiner ou um agente - se isso ocorrer, Apache Mesos reinicia o contêiner de saudação em outro lugar e se adapta maratona balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="dc22f-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="dc22f-127">Execute Olá seguindo o balanceador de carga do comando tooinstall Olá maratona no cluster do agente do hello pública.</span><span class="sxs-lookup"><span data-stu-id="dc22f-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="dc22f-128">Implantar aplicativo com balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="dc22f-128">Deploy load balanced application</span></span>

<span data-ttu-id="dc22f-129">Agora que temos o pacote de balanceamento de carga maratona hello, podemos implantar um contêiner de aplicativo que desejamos que o saldo de tooload.</span><span class="sxs-lookup"><span data-stu-id="dc22f-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="dc22f-130">Primeiro, obtenha Olá FQDN de agentes Olá exposto publicamente.</span><span class="sxs-lookup"><span data-stu-id="dc22f-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="dc22f-131">Em seguida, crie um arquivo chamado *web.json Olá* e cópia em Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="dc22f-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="dc22f-132">Olá `HAPROXY_0_VHOST` toobe atualizado com hello FQDN de agentes do controlador de domínio/OS Olá precisa de rótulo.</span><span class="sxs-lookup"><span data-stu-id="dc22f-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

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

<span data-ttu-id="dc22f-133">Use Olá CLI DC/OS toorun Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dc22f-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="dc22f-134">Por padrão, maratona implanta Olá Olá aplicativo toohello privada de cluster.</span><span class="sxs-lookup"><span data-stu-id="dc22f-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="dc22f-135">Isso significa que Olá acima implantação somente é acessível por meio do balanceador de carga, que geralmente é o comportamento de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="dc22f-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="dc22f-136">Quando o aplicativo hello tiver sido implantado, procure toohello FQDN do aplicativo com balanceamento de carga do hello agente cluster tooview.</span><span class="sxs-lookup"><span data-stu-id="dc22f-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Imagem do aplicativo com balanceamento de carga](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="dc22f-138">Configurar o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="dc22f-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="dc22f-139">Por padrão, o Azure Load Balancer expõe as portas 80, 8080 e 443.</span><span class="sxs-lookup"><span data-stu-id="dc22f-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="dc22f-140">Se você estiver usando um destes três portas (como fazemos em Olá exemplo acima) e nada que é necessário toodo.</span><span class="sxs-lookup"><span data-stu-id="dc22f-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="dc22f-141">Você deve ser capaz de toohit FQDN do balanceador de carga do seu agente, e cada vez que você atualizar, você encontrará um de seus servidores três web em um modo de rodízio.</span><span class="sxs-lookup"><span data-stu-id="dc22f-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="dc22f-142">Se você usar uma porta diferente, você precisa tooadd round robin regra e uma investigação do balanceador de carga Olá para porta Olá que você usou.</span><span class="sxs-lookup"><span data-stu-id="dc22f-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="dc22f-143">Você pode fazer isso de saudação [CLI do Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), com comandos Olá `azure network lb rule create` e `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="dc22f-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc22f-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc22f-144">Next steps</span></span>

<span data-ttu-id="dc22f-145">Neste tutorial, você aprendeu sobre balanceamento de carga no ACS com hello maratona e carga do Azure balanceadores incluindo Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc22f-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc22f-146">Configurar um balanceador de carga do Marathon</span><span class="sxs-lookup"><span data-stu-id="dc22f-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="dc22f-147">Implantar um aplicativo usando Olá balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="dc22f-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="dc22f-148">Configurar um Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="dc22f-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="dc22f-149">Avançar toohello toolearn próximo de tutorial sobre como integrar o armazenamento do Azure com o controlador de domínio/sistema operacional no Azure.</span><span class="sxs-lookup"><span data-stu-id="dc22f-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc22f-150">Montar o compartilhamento de arquivos do Azure no cluster de DC/SO</span><span class="sxs-lookup"><span data-stu-id="dc22f-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)