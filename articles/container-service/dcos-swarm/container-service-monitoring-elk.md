---
title: aaaMonitor um cluster Azure DC/OS - ELK pilha | Microsoft Docs
description: "Monitore um cluster de SO/DC no cluster do serviço de contêiner do Azure com ELK (Elasticsearch, Logstash e Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, CD/OS, Azure, monitoramento, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="de98a-104">Monitorar um cluster do Serviço de Contêiner do Azure com ELK</span><span class="sxs-lookup"><span data-stu-id="de98a-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="de98a-105">Neste artigo, demonstraremos como toodeploy Olá ELK (Elasticsearch, Logstash, Kibana) de pilha em um cluster de SO/controlador de domínio no serviço de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="de98a-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="de98a-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="de98a-106">Prerequisites</span></span>
<span data-ttu-id="de98a-107">[Implantar](container-service-deployment.md) e [conectar](../container-service-connect.md) um cluster DC/OS configurado pelo Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="de98a-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="de98a-108">Explorar o painel de DC/OS hello e serviços maratona [aqui](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="de98a-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="de98a-109">Também instalar Olá [balanceador de carga maratona](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="de98a-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="de98a-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="de98a-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="de98a-111">Pilha ELK é uma combinação de Elasticsearch, Logstash, e Kibana que fornece uma pilha de tooend final que pode ser usado toomonitor e analise logs em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="de98a-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="de98a-112">Configurar a pilha ELK Olá em um cluster de DC/OS</span><span class="sxs-lookup"><span data-stu-id="de98a-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="de98a-113">Interface de usuário do controlador de domínio/OS por meio de acesso [http://localhost:80 /](http://localhost:80/) uma vez no hello navegue de interface do usuário do controlador de domínio/OS muito**universo**.</span><span class="sxs-lookup"><span data-stu-id="de98a-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="de98a-114">Pesquisar e instalar Elasticsearch, Logstash e Kibana da saudação universo de DC/OS e na ordem específica.</span><span class="sxs-lookup"><span data-stu-id="de98a-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="de98a-115">Você pode aprender mais sobre a configuração se você for toohello **instalação avançada** link.</span><span class="sxs-lookup"><span data-stu-id="de98a-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="de98a-119">Uma vez Olá contêineres ELK e estão em funcionamento, você precisa tooenable Kibana toobe acessado por meio de balanceamento de carga maratona.</span><span class="sxs-lookup"><span data-stu-id="de98a-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="de98a-120">Navegue muito **serviços** > **kibana**e clique em **editar** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="de98a-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="de98a-122">Alternar muito**modo JSON** e role para baixo toohello seção de rótulos.</span><span class="sxs-lookup"><span data-stu-id="de98a-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="de98a-123">Você precisa tooadd um `"HAPROXY_GROUP": "external"` entrada aqui conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="de98a-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="de98a-124">Depois que você clicar em **Implantar alterações**, seu contêiner será reinicializado.</span><span class="sxs-lookup"><span data-stu-id="de98a-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="de98a-126">Se você quiser tooverify que Kibana está registrado como um serviço no painel HAPROXY hello, você precisa tooopen porta 9090 no cluster de agente hello como HAPROXY é executado na porta 9090.</span><span class="sxs-lookup"><span data-stu-id="de98a-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="de98a-127">Por padrão, é abrir as portas 80, 8080 e 443 em Olá cluster do agente de controlador de domínio/OS.</span><span class="sxs-lookup"><span data-stu-id="de98a-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="de98a-128">Instruções tooopen uma porta e fornecer público avaliar são fornecidos [aqui](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="de98a-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="de98a-129">tooaccess Olá painel HAPROXY, interface do administrador abrir Olá maratona LB em: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="de98a-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="de98a-130">Quando você navegar toohello URL, você deve ver o painel HAPROXY Olá conforme mostrado abaixo e você deverá ver uma entrada de serviço para Kibana.</span><span class="sxs-lookup"><span data-stu-id="de98a-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="de98a-132">Painel de Kibana de saudação tooaccess, que é implantado na porta 5601, é necessário tooopen porta 5601.</span><span class="sxs-lookup"><span data-stu-id="de98a-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="de98a-133">Siga as instruções [aqui](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="de98a-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="de98a-134">Em seguida, abra o painel de Kibana de saudação em: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="de98a-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de98a-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="de98a-135">Next steps</span></span>

* <span data-ttu-id="de98a-136">Para configuração e encaminhamento de log de aplicativo e sistema, confira [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Gerenciamento de Log no DC/SO com ELK).</span><span class="sxs-lookup"><span data-stu-id="de98a-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="de98a-137">toofilter logs, consulte [filtragem de Logs com ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="de98a-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

