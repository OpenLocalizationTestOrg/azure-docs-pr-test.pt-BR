---
title: "Balancear a carga de contêineres Kubernetes no Azure | Microsoft Docs"
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
ms.openlocfilehash: ab46bb204f14424e394ced499ffbc0ef1cada15b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="907a8-104">Balancear a carga de contêineres em um cluster Kubernetes no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="907a8-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="907a8-105">Este artigo apresenta o balanceamento de carga em um cluster Kubernetes no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="907a8-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="907a8-106">O balanceamento de carga fornece um endereço IP acessível externamente para o serviço e distribui o tráfego de rede entre os pods em execução em VMs do agente.</span><span class="sxs-lookup"><span data-stu-id="907a8-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span></span>

<span data-ttu-id="907a8-107">Você pode configurar um serviço Kubernetes para usar o [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) para gerenciar o tráfego de rede externo (TCP).</span><span class="sxs-lookup"><span data-stu-id="907a8-107">You can set up a Kubernetes service to use [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) to manage external network (TCP) traffic.</span></span> <span data-ttu-id="907a8-108">Com uma configuração adicional, o balanceamento de carga e roteamento de tráfego HTTP ou HTTPS ou cenários mais avançados são possíveis.</span><span class="sxs-lookup"><span data-stu-id="907a8-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="907a8-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="907a8-109">Prerequisites</span></span>
* <span data-ttu-id="907a8-110">[Implantar um cluster Kubernetes](container-service-kubernetes-walkthrough.md) no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="907a8-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="907a8-111">[Conectar o cliente](../container-service-connect.md) ao cluster</span><span class="sxs-lookup"><span data-stu-id="907a8-111">[Connect your client](../container-service-connect.md) to your cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="907a8-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="907a8-112">Azure load balancer</span></span>

<span data-ttu-id="907a8-113">Por padrão, um cluster Kubernetes implantado no Serviço de Contêiner do Azure inclui um Azure Load Balancer voltado para a Internet para VMs do agente.</span><span class="sxs-lookup"><span data-stu-id="907a8-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span></span> <span data-ttu-id="907a8-114">(Um recurso de balanceador de carga separado é configurado para as VMs mestres.) O Azure Load Balancer é um balanceador de carga de Camada 4.</span><span class="sxs-lookup"><span data-stu-id="907a8-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="907a8-115">No momento, o balanceador de carga dá suporte apenas a tráfego TCP em Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="907a8-115">Currently, the load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="907a8-116">Ao criar um serviço Kubernetes, você pode configurar automaticamente o Azure Load Balancer para permitir o acesso ao serviço.</span><span class="sxs-lookup"><span data-stu-id="907a8-116">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span></span> <span data-ttu-id="907a8-117">Para configurar o balanceador de carga, defina o serviço `type` como `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="907a8-117">To configure the load balancer, set the service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="907a8-118">O balanceador de carga cria uma regra para mapear um endereço IP público e o número da porta do tráfego do serviço de entrada para os endereços IP privados e números de porta dos pods nas VMs do agente (e vice-versa para o tráfego de resposta).</span><span class="sxs-lookup"><span data-stu-id="907a8-118">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="907a8-119">A seguir estão dois exemplos que mostram como configurar o serviço Kubernetes `type` como `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="907a8-119">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="907a8-120">(Depois de experimentar os exemplos, exclua as implantações se não precisar mais delas.)</span><span class="sxs-lookup"><span data-stu-id="907a8-120">(After trying the examples, delete the deployments if you no longer need them.)</span></span>

### <a name="example-use-the-kubectl-expose-command"></a><span data-ttu-id="907a8-121">Exemplo: use o comando `kubectl expose`</span><span class="sxs-lookup"><span data-stu-id="907a8-121">Example: Use the `kubectl expose` command</span></span> 
<span data-ttu-id="907a8-122">O [passo a passo do Kubernetes](container-service-kubernetes-walkthrough.md) inclui um exemplo de como expor um serviço com o comando `kubectl expose` e seu sinalizador `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="907a8-122">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="907a8-123">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="907a8-123">Here are the steps :</span></span>

1. <span data-ttu-id="907a8-124">Inicie uma nova implantação do contêiner.</span><span class="sxs-lookup"><span data-stu-id="907a8-124">Start a new container deployment.</span></span> <span data-ttu-id="907a8-125">Por exemplo, o comando a seguir inicia uma nova implantação chamada `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="907a8-125">For example, the following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="907a8-126">A implantação consiste em três contêineres com base na imagem do Docker para o servidor Web Nginx.</span><span class="sxs-lookup"><span data-stu-id="907a8-126">The deployment consists of three containers based on the Docker image for the Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="907a8-127">Verifique se os contêineres estão em execução.</span><span class="sxs-lookup"><span data-stu-id="907a8-127">Verify that the containers are running.</span></span> <span data-ttu-id="907a8-128">Por exemplo, se você consultar os contêineres com `kubectl get pods`, verá uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="907a8-128">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span></span>

    ![Obter contêineres Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="907a8-130">Para configurar o balanceador de carga para aceitar tráfego externo para a implantação, execute `kubectl expose` com `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="907a8-130">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="907a8-131">O comando a seguir expõe o servidor Nginx na porta 80:</span><span class="sxs-lookup"><span data-stu-id="907a8-131">The following command exposes the Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="907a8-132">Digite `kubectl get svc` para ver o estado dos serviços no cluster.</span><span class="sxs-lookup"><span data-stu-id="907a8-132">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="907a8-133">Enquanto o balanceador de carga configura a regra, o `EXTERNAL-IP` do serviço aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="907a8-133">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span></span> <span data-ttu-id="907a8-134">Depois de alguns minutos, o endereço IP externo está configurado:</span><span class="sxs-lookup"><span data-stu-id="907a8-134">After a few minutes, the external IP address is configured:</span></span> 

    ![Configurar o Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="907a8-136">Verifique se você pode acessar o serviço no endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="907a8-136">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="907a8-137">Por exemplo, abra um navegador da Web para o endereço IP exibido.</span><span class="sxs-lookup"><span data-stu-id="907a8-137">For example, open a web browser to the IP address shown.</span></span> <span data-ttu-id="907a8-138">O navegador mostra servidor Web Nginx em execução em um dos contêineres.</span><span class="sxs-lookup"><span data-stu-id="907a8-138">The browser shows the Nginx web server running in one of the containers.</span></span> <span data-ttu-id="907a8-139">Ou execute o comando `curl` ou `wget`.</span><span class="sxs-lookup"><span data-stu-id="907a8-139">Or, run the `curl` or `wget` command.</span></span> <span data-ttu-id="907a8-140">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="907a8-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="907a8-141">Você deve ver uma saída semelhante a:</span><span class="sxs-lookup"><span data-stu-id="907a8-141">You should see output similar to:</span></span>

    ![Acessar o Nginx com curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="907a8-143">Para ver a configuração do Azure Load Balancer, acesse o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="907a8-143">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="907a8-144">Navegue até o grupo de recursos para o cluster do serviço de contêiner e selecione o balanceador de carga para VMs do agente.</span><span class="sxs-lookup"><span data-stu-id="907a8-144">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span></span> <span data-ttu-id="907a8-145">Seu nome deve ser igual ao do serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="907a8-145">Its name should be the same as the container service.</span></span> <span data-ttu-id="907a8-146">(Não escolha o balanceador de carga para os nós mestres, aquele cujo nome inclui **master-lb**.)</span><span class="sxs-lookup"><span data-stu-id="907a8-146">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span></span> 

    ![Balanceador de carga no grupo de recursos](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="907a8-148">Para ver os detalhes de configuração do balanceador de carga, clique em **Regras de balanceamento de carga** e no nome da regra que foi configurada.</span><span class="sxs-lookup"><span data-stu-id="907a8-148">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span></span>

    ![Regras do balanceador de carga](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a><span data-ttu-id="907a8-150">Exemplo: especifique `type: LoadBalancer` no arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="907a8-150">Example: Specify `type: LoadBalancer` in the service configuration file</span></span>

<span data-ttu-id="907a8-151">Se você implantar um aplicativo de contêiner Kubernetes de [arquivo de configuração de serviço](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file) JSON ou YAML, especifique um balanceador externo de carga adicionando a seguinte linha à especificação do serviço:</span><span class="sxs-lookup"><span data-stu-id="907a8-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="907a8-152">As etapas a seguir usam o [exemplo Guestbook](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook) do Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="907a8-152">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="907a8-153">Este exemplo é um aplicativo Web de várias camadas com base em imagens do Docker PHP e Redis.</span><span class="sxs-lookup"><span data-stu-id="907a8-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="907a8-154">Você pode especificar no arquivo de configuração de serviço que o servidor PHP front-end usa o Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="907a8-154">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span></span>

1. <span data-ttu-id="907a8-155">Baixe o arquivo `guestbook-all-in-one.yaml` do [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="907a8-155">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="907a8-156">Procure o `spec` para o serviço `frontend`.</span><span class="sxs-lookup"><span data-stu-id="907a8-156">Browse for the `spec` for the `frontend` service.</span></span>
3. <span data-ttu-id="907a8-157">Remova a marca de comentário da linha `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="907a8-157">Uncomment the line `type: LoadBalancer`.</span></span>

    ![Balanceador de carga na configuração de serviço](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="907a8-159">Salve o arquivo e implante o aplicativo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="907a8-159">Save the file, and deploy the app by running the following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="907a8-160">Digite `kubectl get svc` para ver o estado dos serviços no cluster.</span><span class="sxs-lookup"><span data-stu-id="907a8-160">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="907a8-161">Enquanto o balanceador de carga configura a regra, o `EXTERNAL-IP` do serviço `frontend` aparece como `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="907a8-161">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="907a8-162">Depois de alguns minutos, o endereço IP externo está configurado:</span><span class="sxs-lookup"><span data-stu-id="907a8-162">After a few minutes, the external IP address is configured:</span></span> 

    ![Configurar o Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="907a8-164">Verifique se você pode acessar o serviço no endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="907a8-164">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="907a8-165">Por exemplo, você pode abrir um navegador da Web para o endereço IP externo do serviço.</span><span class="sxs-lookup"><span data-stu-id="907a8-165">For example, you can open a web browser to the external IP address of the service.</span></span>

    ![Acessar a página de recados externamente](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="907a8-167">Você pode adicionar entradas da página de recados.</span><span class="sxs-lookup"><span data-stu-id="907a8-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="907a8-168">Para ver a configuração do Azure Load Balancer, navegue até o recurso de balanceador de carga para o cluster no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="907a8-168">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="907a8-169">Consulte as etapas no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="907a8-169">See the steps in the previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="907a8-170">Considerações</span><span class="sxs-lookup"><span data-stu-id="907a8-170">Considerations</span></span>

* <span data-ttu-id="907a8-171">A criação da regra do balanceador de carga ocorre de maneira assíncrona e as informações sobre o balanceador provisionado são publicadas no campo `status.loadBalancer` do servidor.</span><span class="sxs-lookup"><span data-stu-id="907a8-171">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="907a8-172">Cada serviço recebe automaticamente a atribuição de seu próprio endereço IP virtual no balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="907a8-172">Every service is automatically assigned its own virtual IP address in the load balancer.</span></span>
* <span data-ttu-id="907a8-173">Se você deseja alcançar o balanceador de carga por um nome DNS, trabalhe com seu provedor de serviços de domínio para criar um nome DNS para o endereço IP da regra.</span><span class="sxs-lookup"><span data-stu-id="907a8-173">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="907a8-174">Tráfego HTTP ou HTTPS</span><span class="sxs-lookup"><span data-stu-id="907a8-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="907a8-175">Para balancear a carga do tráfego HTTP ou HTTPS para aplicativos Web de contêiner e gerenciar os certificados para o protocolo TLS, você pode usar o recurso de [Entrada](https://kubernetes.io/docs/user-guide/ingress/) Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="907a8-175">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="907a8-176">Uma Entrada é uma coleção de regras que permite que conexões de entrada alcançar os serviços de cluster.</span><span class="sxs-lookup"><span data-stu-id="907a8-176">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="907a8-177">Para um recurso de Entrada funcionar, o cluster Kubernetes deve ter uma [Controlador de entrada](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) em execução.</span><span class="sxs-lookup"><span data-stu-id="907a8-177">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="907a8-178">O Serviço de Contêiner do Azure não implementa um controlador de Entrada Kubernetes automaticamente.</span><span class="sxs-lookup"><span data-stu-id="907a8-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="907a8-179">Existem várias implementações de controlador disponíveis.</span><span class="sxs-lookup"><span data-stu-id="907a8-179">Several controller implementations are available.</span></span> <span data-ttu-id="907a8-180">Atualmente, o [controlador de Entrada Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) é recomendado para configurar regras de Entrada e balancear a carga do tráfego HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="907a8-180">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="907a8-181">Para saber mais, consulte a [Documentação do controlador de entrada Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="907a8-181">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="907a8-182">Ao usar o controlador de Entrada Nginx no Serviço de Contêiner do Azure, você deve expor a implantação do controlador como um serviço com `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="907a8-182">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="907a8-183">Isso configura o Azure Load Balancer para rotear o tráfego para o controlador.</span><span class="sxs-lookup"><span data-stu-id="907a8-183">This configures the Azure load balancer to route traffic to the controller.</span></span> <span data-ttu-id="907a8-184">Para obter mais informações, consulte a seção anterior.</span><span class="sxs-lookup"><span data-stu-id="907a8-184">For more information, see the previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="907a8-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="907a8-185">Next steps</span></span>

* <span data-ttu-id="907a8-186">Consulte a [documentação do balanceador de carga Kubernetes](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="907a8-186">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="907a8-187">Saiba mais sobre [controladores de Entrada e Entrada Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="907a8-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="907a8-188">Consulte [exemplos do Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="907a8-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

