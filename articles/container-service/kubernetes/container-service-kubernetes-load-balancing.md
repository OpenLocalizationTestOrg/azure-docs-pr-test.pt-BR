---
title: "aaaLoad equilibrar Kubernetes contêineres no Azure | Microsoft Docs"
description: "Conecte-se externamente e balanceie a carga em vários contêineres em um cluster Kubernetes no Serviço de Contêiner do Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, Microsserviços, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="65e81-104">Balancear a carga de contêineres em um cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="65e81-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="65e81-105">Este artigo apresenta o balanceamento de carga em um cluster Kubernetes no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="65e81-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="65e81-106">Balanceamento de carga fornece um endereço IP acessível externamente para serviço de saudação e distribui o tráfego de rede entre os compartimentos de saudação em execução no agente de VMs.</span><span class="sxs-lookup"><span data-stu-id="65e81-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="65e81-107">Você pode configurar um toouse de serviço Kubernetes [balanceador de carga do Azure](../../load-balancer/load-balancer-overview.md) toomanage tráfego de rede (TCP) externo.</span><span class="sxs-lookup"><span data-stu-id="65e81-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="65e81-108">Com uma configuração adicional, o balanceamento de carga e roteamento de tráfego HTTP ou HTTPS ou cenários mais avançados são possíveis.</span><span class="sxs-lookup"><span data-stu-id="65e81-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65e81-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="65e81-109">Prerequisites</span></span>
* <span data-ttu-id="65e81-110">[Implantar um cluster Kubernetes](container-service-kubernetes-walkthrough.md) no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="65e81-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="65e81-111">[Conecte o cliente](../container-service-connect.md) tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="65e81-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="65e81-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="65e81-112">Azure load balancer</span></span>

<span data-ttu-id="65e81-113">Por padrão, um cluster Kubernetes implantado no serviço de contêiner do Azure inclui um balanceador de carga do Azure voltado para a Internet para agente Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="65e81-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="65e81-114">(Um recurso de Balanceador de carga separado é configurado para mestre Olá VMs.) O Azure Load Balancer é um balanceador de carga de Camada 4.</span><span class="sxs-lookup"><span data-stu-id="65e81-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="65e81-115">No momento, o balanceador de carga de saudação suporta apenas o tráfego TCP em Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="65e81-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="65e81-116">Ao criar um serviço Kubernetes, pode configurar automaticamente o serviço de toohello acesso do tooallow de Balanceador de carga do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="65e81-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="65e81-117">Balanceador de carga tooconfigure hello, serviço de saudação do conjunto `type` muito`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="65e81-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="65e81-118">Balanceador de carga Olá cria uma regra toomap um endereço IP público e o número da porta de entrada serviço tráfego toohello endereços IP privados e números de porta de compartimentos de saudação no agente de VMs (e vice-versa para o tráfego de resposta).</span><span class="sxs-lookup"><span data-stu-id="65e81-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="65e81-119">Estes são dois exemplos que mostram como tooset Olá Kubernetes serviço `type` muito`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="65e81-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="65e81-120">(Depois de tentar exemplos de hello, excluir Olá implantações se você não precisar mais deles.)</span><span class="sxs-lookup"><span data-stu-id="65e81-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="65e81-121">Exemplo: Saudação de uso `kubectl expose` comando</span><span class="sxs-lookup"><span data-stu-id="65e81-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="65e81-122">Olá [Kubernetes passo a passo](container-service-kubernetes-walkthrough.md) inclui um exemplo de como tooexpose um serviço com hello `kubectl expose` comando e sua `--type=LoadBalancer` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="65e81-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="65e81-123">Aqui estão as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="65e81-123">Here are hello steps :</span></span>

1. <span data-ttu-id="65e81-124">Inicie uma nova implantação do contêiner.</span><span class="sxs-lookup"><span data-stu-id="65e81-124">Start a new container deployment.</span></span> <span data-ttu-id="65e81-125">Olá, por exemplo, após o comando inicia uma nova implantação chamada `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="65e81-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="65e81-126">Olá implantação consiste em três contêineres com base na imagem do Docker Olá Olá Nginx servidor de web.</span><span class="sxs-lookup"><span data-stu-id="65e81-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="65e81-127">Verificar se os contêineres de saudação estão em execução.</span><span class="sxs-lookup"><span data-stu-id="65e81-127">Verify that hello containers are running.</span></span> <span data-ttu-id="65e81-128">Por exemplo, se você consultar para contêineres de saudação com `kubectl get pods`, você vê saída semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="65e81-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Obter contêineres Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="65e81-130">tooconfigure Olá carga tooaccept tráfego externo toohello implantação de Balanceador, execute `kubectl expose` com `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="65e81-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="65e81-131">Olá seguinte comando expõe servidor de Nginx Olá na porta 80:</span><span class="sxs-lookup"><span data-stu-id="65e81-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="65e81-132">Tipo `kubectl get svc` estado de saudação do toosee dos serviços de Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="65e81-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="65e81-133">Enquanto o balanceador de carga Olá configura regra hello, Olá `EXTERNAL-IP` de saudação serviço aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="65e81-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="65e81-134">Após alguns minutos, o endereço IP externo de saudação é configurado:</span><span class="sxs-lookup"><span data-stu-id="65e81-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurar o Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="65e81-136">Verifique se que você pode acessar o serviço de saudação no endereço IP externo de saudação.</span><span class="sxs-lookup"><span data-stu-id="65e81-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="65e81-137">Por exemplo, abra um endereço IP do web navegador toohello mostrado.</span><span class="sxs-lookup"><span data-stu-id="65e81-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="65e81-138">navegador de saudação mostra o servidor de web Nginx Olá em execução em um dos contêineres de saudação.</span><span class="sxs-lookup"><span data-stu-id="65e81-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="65e81-139">Ou então, Olá execução `curl` ou `wget` comando.</span><span class="sxs-lookup"><span data-stu-id="65e81-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="65e81-140">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="65e81-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="65e81-141">Você deve ver uma saída semelhante a:</span><span class="sxs-lookup"><span data-stu-id="65e81-141">You should see output similar to:</span></span>

    ![Acessar o Nginx com curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="65e81-143">configuração de saudação toosee hello Azure do balanceador de carga, vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65e81-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="65e81-144">Procurar o grupo de recursos Olá para o cluster do serviço de contêiner e selecione o balanceador de carga Olá para agente Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="65e81-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="65e81-145">Seu nome deve ser Olá mesmo que o serviço de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="65e81-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="65e81-146">(Não escolher Olá balanceador de carga de nós mestres hello, Olá um cujo nome inclui **lb mestre**.)</span><span class="sxs-lookup"><span data-stu-id="65e81-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Balanceador de carga no grupo de recursos](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="65e81-148">toosee Olá detalhes de configuração de Balanceador de carga hello, clique em **regras de balanceamento de carga** e o nome de saudação da regra de saudação que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="65e81-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Regras do balanceador de carga](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="65e81-150">Exemplo: Especificar `type: LoadBalancer` no arquivo de configuração de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="65e81-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="65e81-151">Se você implantar um aplicativo de contêiner Kubernetes de um YAML ou JSON [arquivo de configuração de serviço](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), especifique um balanceador externo adicionando Olá especificação do serviço toohello linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="65e81-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="65e81-152">Olá, etapas a seguir usam Olá Kubernetes [convidados exemplo](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="65e81-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="65e81-153">Este exemplo é um aplicativo Web de várias camadas com base em imagens do Docker PHP e Redis.</span><span class="sxs-lookup"><span data-stu-id="65e81-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="65e81-154">Você pode especificar no arquivo de configuração de serviço Olá que servidor Olá front-end PHP usa o balanceador de carga do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="65e81-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="65e81-155">Baixe o arquivo hello `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="65e81-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="65e81-156">Procurar Olá `spec` para Olá `frontend` serviço.</span><span class="sxs-lookup"><span data-stu-id="65e81-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="65e81-157">Descomente a linha hello `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="65e81-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Balanceador de carga na configuração de serviço](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="65e81-159">Salvar arquivo hello e implante o aplicativo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="65e81-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="65e81-160">Tipo `kubectl get svc` estado de saudação do toosee dos serviços de Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="65e81-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="65e81-161">Enquanto o balanceador de carga Olá configura regra hello, Olá `EXTERNAL-IP` de saudação `frontend` serviço aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="65e81-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="65e81-162">Após alguns minutos, o endereço IP externo de saudação é configurado:</span><span class="sxs-lookup"><span data-stu-id="65e81-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Configurar o Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="65e81-164">Verifique se que você pode acessar o serviço de saudação no endereço IP externo de saudação.</span><span class="sxs-lookup"><span data-stu-id="65e81-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="65e81-165">Por exemplo, você pode abrir um web navegador toohello endereço IP externo do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="65e81-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Acessar a página de recados externamente](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="65e81-167">Você pode adicionar entradas da página de recados.</span><span class="sxs-lookup"><span data-stu-id="65e81-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="65e81-168">configuração de saudação toosee hello Azure do balanceador de carga, navegue para o recurso de Balanceador de carga Olá para cluster Olá Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65e81-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="65e81-169">Consulte as etapas no exemplo anterior Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="65e81-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="65e81-170">Considerações</span><span class="sxs-lookup"><span data-stu-id="65e81-170">Considerations</span></span>

* <span data-ttu-id="65e81-171">Criação de regra de Balanceador de carga Olá ocorre de maneira assíncrona e informações sobre balanceador Olá provisionado são publicadas no serviço de saudação `status.loadBalancer` campo.</span><span class="sxs-lookup"><span data-stu-id="65e81-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="65e81-172">Cada serviço é automaticamente atribuído a seu próprio endereço IP virtual no balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="65e81-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="65e81-173">Se você quiser balanceador de carga Olá tooreach por um nome DNS, trabalhe com seu toocreate de provedor de serviços de domínio um nome DNS para o endereço IP da regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="65e81-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="65e81-174">Tráfego HTTP ou HTTPS</span><span class="sxs-lookup"><span data-stu-id="65e81-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="65e81-175">Saldo de tooload HTTP ou HTTPS tráfego toocontainer aplicativos web e gerenciar certificados de segurança de camada de transporte (TLS), você pode usar o hello Kubernetes [entrada](https://kubernetes.io/docs/user-guide/ingress/) recursos.</span><span class="sxs-lookup"><span data-stu-id="65e81-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="65e81-176">Uma entrada é uma coleção de regras que permitem conexões de entrada de serviços de cluster tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="65e81-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="65e81-177">Para um toowork de recurso de entrada, o cluster de Kubernetes de saudação deve ter uma [controlador entrada](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) em execução.</span><span class="sxs-lookup"><span data-stu-id="65e81-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="65e81-178">O Serviço de Contêiner do Azure não implementa um controlador de Entrada Kubernetes automaticamente.</span><span class="sxs-lookup"><span data-stu-id="65e81-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="65e81-179">Existem várias implementações de controlador disponíveis.</span><span class="sxs-lookup"><span data-stu-id="65e81-179">Several controller implementations are available.</span></span> <span data-ttu-id="65e81-180">Atualmente, Olá [controlador Nginx entrada](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) é recomendável tooconfigure regras de entrada e balanceamento de carga de tráfego HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="65e81-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="65e81-181">Para obter mais informações, consulte Olá [documentação do controlador de entrada Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="65e81-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65e81-182">Ao usar o hello controlador Nginx entrada no serviço de contêiner do Azure, você deve expor na implantação do controlador hello como um serviço com `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="65e81-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="65e81-183">Isso configura o controlador de toohello tráfego do tooroute de Balanceador de carga do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="65e81-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="65e81-184">Para obter mais informações, consulte a seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="65e81-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="65e81-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65e81-185">Next steps</span></span>

* <span data-ttu-id="65e81-186">Consulte Olá [Kubernetes LoadBalancer documentação](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="65e81-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="65e81-187">Saiba mais sobre [controladores de Entrada e Entrada Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="65e81-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="65e81-188">Consulte [exemplos do Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="65e81-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

