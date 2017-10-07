---
title: "versão de aaaCanary com Vamp no cluster do Azure DC/sistema operacional | Microsoft Docs"
description: "Como toouse Vamp toocanary versão serviços e aplicar a filtragem em um cluster do serviço de contêiner do Azure DC/OS de tráfego inteligente"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="6c7c7-103">Microsserviços da versão canário com Vamp no cluster de DC/SO do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="6c7c7-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="6c7c7-104">Neste passo a passo, configuramos o Vamp no Serviço de Contêiner do Azure com um cluster de DC/SO.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="6c7c7-105">Lançamos canary serviço demonstração de Vamp hello "sava" e, em seguida, resolver uma incompatibilidade de serviço Olá com o Firefox, aplicando a filtragem inteligente.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="6c7c7-106">Neste passo a passo Vamp é executado em um cluster de DC/sistema operacional, mas você também pode usar Vamp com Kubernetes como orchestrator hello.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="6c7c7-107">Sobre versões canário e Vamp</span><span class="sxs-lookup"><span data-stu-id="6c7c7-107">About canary releases and Vamp</span></span>


<span data-ttu-id="6c7c7-108">A [versão canário](https://martinfowler.com/bliki/CanaryRelease.html) é uma estratégia de implantação inteligente adotada por organizações inovadoras como Netflix, Facebook e Spotify.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="6c7c7-109">É uma abordagem que faz sentido, porque reduz problemas, introduz redes de segurança e aumenta a inovação.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="6c7c7-110">Então, por que nem todas as empresas estão usando?</span><span class="sxs-lookup"><span data-stu-id="6c7c7-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="6c7c7-111">Estender um tooinclude do pipeline de CI/CD estratégias canary adiciona complexidade e exige experiência e devops extenso conhecimento.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="6c7c7-112">É suficiente tooblock pequenas empresas e empresas semelhantes antes de eles mesmo começar.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="6c7c7-113">[Vamp](http://vamp.io/) é um sistema de código-fonte aberto criado tooease essa transição e coloque canary liberar recursos tooyour preferido contêiner do Agendador.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="6c7c7-114">Funcionalidade de canário do Vamp vai além de distribuições baseadas em percentual.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="6c7c7-115">Tráfego pode ser filtrado e dividido em uma ampla variedade de condições, por exemplo, usuários específicos tootarget, intervalos de IP ou dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="6c7c7-116">Vamp monitora e analisa as métricas de desempenho, permitindo a automação baseada em dados reais.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="6c7c7-117">Você pode configurar a reversão automática em caso de erros ou dimensionar variantes de serviço individuais com base na carga ou na latência.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="6c7c7-118">Configurar o Serviço de Contêiner do Azure com o DC/SO</span><span class="sxs-lookup"><span data-stu-id="6c7c7-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="6c7c7-119">[Implantar um cluster de DC/SO](container-service-deployment.md) com um mestre e dois agentes de tamanho padrão.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="6c7c7-120">[Criar um túnel SSH](../container-service-connect.md) cluster do tooconnect toohello DC/OS.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="6c7c7-121">Este artigo pressupõe que você criar um túnel de cluster toohello na porta local 80.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="6c7c7-122">Configurar o Vamp</span><span class="sxs-lookup"><span data-stu-id="6c7c7-122">Set up Vamp</span></span>

<span data-ttu-id="6c7c7-123">Agora que você tem um cluster de DC/sistema operacional em execução, você pode instalar Vamp de saudação da interface do usuário do controlador de domínio/OS (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![Interface do usuário do DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="6c7c7-125">A instalação é feita em duas etapas:</span><span class="sxs-lookup"><span data-stu-id="6c7c7-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="6c7c7-126">**Implantar Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="6c7c7-127">Em seguida, **implantar Vamp** instalando o pacote de universo Olá Vamp DC/OS.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="6c7c7-128">Implantar Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="6c7c7-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="6c7c7-129">O Vamp requer Elasticsearch para coleta e agregação de métricas.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="6c7c7-130">Você pode usar o hello [imagens do Docker magneticio](https://hub.docker.com/r/magneticio/elastic/) toodeploy uma pilha Vamp Elasticsearch compatível.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="6c7c7-131">Olá DC/sistema operacional da interface do usuário, vá muito**serviços** e clique em **implantar serviço**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="6c7c7-132">Selecione **modo JSON** de saudação **implantar novo serviço** pop-up.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![Selecione o modo JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="6c7c7-134">Cole Olá JSON a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-134">Paste in hello following JSON.</span></span> <span data-ttu-id="6c7c7-135">Essa configuração é executado contêiner Olá com 1 GB de RAM e uma verificação básica de integridade na porta de Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="6c7c7-136">Clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-136">Click **Deploy**.</span></span>

  <span data-ttu-id="6c7c7-137">Controlador de domínio/OS implanta contêiner de Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="6c7c7-138">Você pode acompanhar o progresso na Olá **serviços** página.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-138">You can track progress on hello **Services** page.</span></span>  

  ![implantar e?Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="6c7c7-140">Implantar o Vamp</span><span class="sxs-lookup"><span data-stu-id="6c7c7-140">Deploy Vamp</span></span>

<span data-ttu-id="6c7c7-141">Depois de Elasticsearch informa como **executando**, você pode adicionar Olá Vamp universo de DC/OS pacote.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="6c7c7-142">Vá muito**universo** e procure **vamp**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="6c7c7-143">![Vamp no DC/SO universal](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="6c7c7-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="6c7c7-144">Clique em **instalar** toohello próximo vamp pacote e escolha **instalação avançada**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="6c7c7-145">Role para baixo e insira Olá elasticsearch url a seguir: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Digitar a URL de Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="6c7c7-147">Clique em **Examine e instale**, em seguida, clique em **instalar** toostart implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="6c7c7-148">O DC/SO implanta todos os componentes necessários do Vamp.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="6c7c7-149">Você pode acompanhar o progresso na Olá **serviços** página.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-149">You can track progress on hello **Services** page.</span></span>
  
  ![Implantar Vamp como um pacote universal](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="6c7c7-151">Depois que a implantação for concluída, você pode acessar Olá Vamp da interface do usuário:</span><span class="sxs-lookup"><span data-stu-id="6c7c7-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![Serviço Vamp no DC/SO](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interface do usuário do Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="6c7c7-154">Implantar seu primeiro serviço</span><span class="sxs-lookup"><span data-stu-id="6c7c7-154">Deploy your first service</span></span>

<span data-ttu-id="6c7c7-155">Agora que o Vamp está em execução, implante um serviço de um plano gráfico.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="6c7c7-156">Em sua forma mais simples, uma [Vamp planta](http://vamp.io/documentation/using-vamp/blueprints/) descreve os pontos de extremidade da saudação (gateways), clusters e toodeploy de serviços.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="6c7c7-157">Vamp usa clusters toogroup variantes diferentes Olá mesmo serviço em grupos lógicos para liberar canary ou A / B teste.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="6c7c7-158">Esse cenário usa um aplicativo monolítico de exemplo chamado [ **sava**](https://github.com/magneticio/sava), que está na versão 1.0.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="6c7c7-159">monolito Olá é empacotado em um contêiner do Docker, que está no Hub do Docker em magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="6c7c7-160">Olá aplicativo normalmente é executado na porta 8080, mas você deseja tooexpose na porta 9050 neste caso.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="6c7c7-161">Implante o aplicativo de saudação por meio de Vamp usando uma estrutura simple.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="6c7c7-162">Vá muito**implantações**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="6c7c7-163">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-163">Click **Add**.</span></span>

3. <span data-ttu-id="6c7c7-164">Colar em Olá seguindo plano gráfico YAML.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="6c7c7-165">Esse plano gráfico contém um cluster com apenas uma variante de serviço, que podemos alterar em uma etapa posterior:</span><span class="sxs-lookup"><span data-stu-id="6c7c7-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="6c7c7-166">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-166">Click **Save**.</span></span> <span data-ttu-id="6c7c7-167">Vamp inicia a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="6c7c7-168">implantação Hello está listada no hello **implantações** página.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="6c7c7-169">Clique em Olá implantação toomonitor seu status.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-169">Click hello deployment toomonitor its status.</span></span>

![Interface do usuário do Vamp – implantação de sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![serviço sava na interface do usuário do Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="6c7c7-172">São criados dois gateways, que são listados em Olá **Gateways** página:</span><span class="sxs-lookup"><span data-stu-id="6c7c7-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="6c7c7-173">uma saudação de tooaccess estável do ponto de extremidade que está executando o serviço (porta 9050)</span><span class="sxs-lookup"><span data-stu-id="6c7c7-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="6c7c7-174">um gateway interno gerenciado pelo Vamp (mais informações sobre este gateway mais tarde).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Interface do usuário do Vamp – gateways de sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="6c7c7-176">serviço de sava Olá implantou, mas você não pode acessá-lo externamente porque Olá balanceador de carga do Azure não sabe tooforward tráfego tooit ainda.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="6c7c7-177">serviço de saudação tooaccess, Olá de atualização de configuração de rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="6c7c7-178">Atualizar a configuração de rede do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="6c7c7-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="6c7c7-179">Serviço de sava vamp implantado Olá em nós de agente do DC/OS hello, expor um ponto de extremidade estável na porta 9050.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="6c7c7-180">tooaccess serviço de saudação do cluster fora do DC/OS hello, verifique Olá seguinte configuração de rede do Azure toohello alterações em sua implantação de cluster:</span><span class="sxs-lookup"><span data-stu-id="6c7c7-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="6c7c7-181">**Configurar Olá balanceador de carga do Azure** para agentes hello (Olá recurso denominado **dcos-agente lb xxxx**) com um teste de integridade e o tráfego de tooforward uma regra em instâncias de sava toohello 9050 porta.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="6c7c7-182">**Grupo de segurança de rede atualização Olá** para agentes pública hello (Olá recurso denominado **XXXX-agente-público-nsg-XXXX**) tooallow o tráfego na porta 9050.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="6c7c7-183">Para obter etapas detalhadas toocomplete essas tarefas usando hello Azure portal, consulte [ativar o aplicativo de serviço de contêiner do Azure do acesso público tooan](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="6c7c7-184">Especifique a porta 9050 para todas as configurações de porta.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="6c7c7-185">Quando tudo o que tiver sido criado, acesse toohello **visão geral** folha Olá DC/OS agente de Balanceador de carga (Olá recurso denominado **dcos-agente lb xxxx**).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="6c7c7-186">Localize Olá **endereço IP público**e usar o hello endereço tooaccess sava na porta 9050.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Portal do Azure – obter endereço IP público](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="6c7c7-189">Executar uma versão canário</span><span class="sxs-lookup"><span data-stu-id="6c7c7-189">Run a canary release</span></span>

<span data-ttu-id="6c7c7-190">Suponha que você tenha uma nova versão do aplicativo que você deseja que a versão toocanary em produção.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="6c7c7-191">Você tem em contêineres como magneticio/sava:1.1.0 e toogo pronto.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="6c7c7-192">Vamp permite adicionar novos toohello de serviços em execução de implantação.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="6c7c7-193">Esses serviços "mesclados" são implantados junto com os serviços existentes no cluster Olá Olá e recebe um peso de 0%.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="6c7c7-194">Nenhum tráfego é o serviço de tooa roteados recentemente mesclada até que você ajustar a distribuição de tráfego hello.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="6c7c7-195">controle deslizante de peso de saudação no hello Vamp da interface do usuário lhe dá controle total sobre a distribuição hello, permitindo ajustes incrementais (versão canary) ou uma reversão de instantâneo.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="6c7c7-196">Mesclar uma nova variante do serviço</span><span class="sxs-lookup"><span data-stu-id="6c7c7-196">Merge a new service variant</span></span>

<span data-ttu-id="6c7c7-197">toomerge Olá novo sava 1.1 serviço com hello executando implantação:</span><span class="sxs-lookup"><span data-stu-id="6c7c7-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="6c7c7-198">No hello Vamp da interface do usuário, clique em **plantas**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="6c7c7-199">Clique em **adicionar** e colar em Olá seguindo plano gráfico YAML: Este diagrama descreve um novo toodeploy de variante (sava: 1.1.0) do serviço em cluster existente da saudação (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="6c7c7-200">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-200">Click **Save**.</span></span> <span data-ttu-id="6c7c7-201">esquema de saudação é armazenada e listada no hello **plantas** página.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="6c7c7-202">Menu de ação Olá aberta no esquema de sava: 1.1 hello e clique em **Mesclar para**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Interface do usuário do Vamp – planos gráficos](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="6c7c7-204">Selecione Olá **sava** implantação e clique em **mesclar**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Vamp da interface do usuário - toodeployment plano gráfico de mesclagem](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="6c7c7-206">Vamp implanta Olá nova sava: 1.1.0 serviço variante descrito no esquema Olá junto com sava: 1.0.0 em Olá **sava_cluster** de saudação executando a implantação.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Interface do usuário do Vamp – implantação sava atualizada](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="6c7c7-208">Olá **sava_cluster/sava/webport** gateway (ponto de extremidade de cluster Olá) também é atualizada, adicionar uma rota toohello recentemente implantado sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="6c7c7-209">Neste momento, nenhum tráfego é roteado aqui (Olá **peso** é definido % too0).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Interface do usuário do Vamp – gateway do cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="6c7c7-211">Versão canário</span><span class="sxs-lookup"><span data-stu-id="6c7c7-211">Canary release</span></span>

<span data-ttu-id="6c7c7-212">Nas versões do sava implantados em Olá mesmo cluster, ajustar a distribuição de saudação do tráfego entre elas, movendo Olá **peso** controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="6c7c7-213">Clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avançar muito**peso**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="6c7c7-214">Defina Olá peso distribuição too50%/50% e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Interface do usuário do Vamp – controle deslizante de peso de gateway](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="6c7c7-216">Voltar tooyour navegador e atualize a página de sava de saudação mais algumas vezes.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="6c7c7-217">aplicativo de sava Hello agora alterna entre uma página sava: 1.0 e uma página de sava: 1.1.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![alternando os serviços sava1.0 e sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="6c7c7-219">Essa alternância de página Olá funciona melhor com hello "Incógnita" ou "Anonymous" modo do navegador devido ao caching Olá ativos estático.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="6c7c7-220">Filtrar o tráfego</span><span class="sxs-lookup"><span data-stu-id="6c7c7-220">Filter traffic</span></span>

<span data-ttu-id="6c7c7-221">Suponha que, depois da implantação, você descobriu uma incompatibilidade no sava:1.1.0 que causa problemas de exibição em navegadores Firefox.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="6c7c7-222">Você pode definir Vamp toofilter o tráfego de entrada e direcionar a todos os usuários do Firefox fazer toohello conhecido sava: 1.0.0 estável.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="6c7c7-223">Esse filtro instantaneamente resolve Olá interrupção para usuários do Firefox, enquanto todos os outros continua tooenjoy benefícios Olá Olá aprimorado sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="6c7c7-224">Vamp usa **condições** toofilter o tráfego entre as rotas de um gateway.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="6c7c7-225">O tráfego é filtrado pela primeira vez e direcionadas acordo toohello condições aplicadas tooeach rota.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="6c7c7-226">Todo o tráfego restante é distribuído de acordo com a configuração de peso de gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="6c7c7-227">Você pode criar uma condição toofilter todos os usuários do Firefox e encaminhá-los sava: 1.0.0 toohello antigo:</span><span class="sxs-lookup"><span data-stu-id="6c7c7-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="6c7c7-228">Em Olá sava_cluster/sava/webport **Gateways** , clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd um **condição** toohello rota sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="6c7c7-229">Insira a condição de saudação **agente do usuário = = Firefox** e clique em ![Vamp UI - salvar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="6c7c7-230">Vamp adiciona a condição de saudação com um nível padrão de 0%.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="6c7c7-231">toostart o tráfego de filtragem, você precisa de intensidade de condição de saudação tooadjust.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="6c7c7-232">Clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange Olá **força** aplicada toohello condição.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="6c7c7-233">Saudação de conjunto **força** too100% e clique em ![Vamp UI - salvar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="6c7c7-234">Vamp agora envia todo o tráfego correspondente Olá condição (todos os usuários Firefox) toosava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp da interface do usuário - aplicar toogateway condição](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="6c7c7-236">Por fim, ajuste todos os demais tráfego (todos os usuários não Firefox) toohello novo sava: 1.1.0 Olá toosend de peso de gateway.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="6c7c7-237">Clique em ![Vamp UI - editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avançar muito**peso** e definir a distribuição de peso Olá para 100% seja direcionado toohello rota sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="6c7c7-238">Todo o tráfego não filtrado pela condição Olá agora é direcionado toohello novo sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="6c7c7-239">filtro de saudação toosee em ação, abra dois navegadores diferentes (um Firefox e um outro navegador) e acessar o serviço de sava de saudação do.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="6c7c7-240">Todas as solicitações de Firefox são enviadas toosava:1.0.0, enquanto todos os outros navegadores estão toosava:1.1.0 direcionado.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Interface do usuário do Vamp – filtrar tráfego](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="6c7c7-242">Resumindo</span><span class="sxs-lookup"><span data-stu-id="6c7c7-242">Summing up</span></span>

<span data-ttu-id="6c7c7-243">Este artigo foi tooVamp uma rápida introdução em um cluster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="6c7c7-244">Para começar, você obteve Vamp para cima e em execução em seu contêiner de serviço DC/sistema operacional do Azure cluster, implantado um serviço com um esquema Vamp acessou no ponto de extremidade exposto de saudação (gateway).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="6c7c7-245">Também abordamos na alguns recursos avançados do Vamp: mesclagem de um novo serviço variant toohello executando a implantação e apresentando-lo incrementalmente, filtragem de tráfego tooresolve uma incompatibilidade conhecida.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6c7c7-246">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c7c7-246">Next steps</span></span>

* <span data-ttu-id="6c7c7-247">Saiba como gerenciar Vamp ações por meio de saudação [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="6c7c7-248">Crie scripts de automação do Vamp no Node.js e execute-os como [Fluxos de trabalho do Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="6c7c7-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="6c7c7-249">Consulte [Tutoriais do VAMP](http://vamp.io/documentation/tutorials/overview/) adicionais.</span><span class="sxs-lookup"><span data-stu-id="6c7c7-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

