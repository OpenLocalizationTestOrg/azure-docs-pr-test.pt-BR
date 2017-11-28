---
title: aaaManage Azure DC/OS cluster com a API de REST maratona | Microsoft Docs
description: "Implante o cluster de serviço de contêiner do Azure DC/OS contêineres tooan usando Olá maratona REST API."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="003b8-104">Gerenciamento de contêiner de DC/sistema operacional por meio de saudação maratona REST API</span><span class="sxs-lookup"><span data-stu-id="003b8-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="003b8-105">Controlador de domínio/sistema operacional fornece um ambiente para Implantando e dimensionando cargas de trabalho clusterizadas, enquanto a abstração de hardware subjacente hello.</span><span class="sxs-lookup"><span data-stu-id="003b8-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="003b8-106">Sobre o DC/OS, há uma estrutura que gerencia o agendamento e a execução das cargas de trabalho de computação.</span><span class="sxs-lookup"><span data-stu-id="003b8-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="003b8-107">Embora estruturas estão disponíveis para várias cargas de trabalho populares, este documento apresenta criando e escala de implantações de contêiner usando Olá maratona REST API.</span><span class="sxs-lookup"><span data-stu-id="003b8-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="003b8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="003b8-108">Prerequisites</span></span>

<span data-ttu-id="003b8-109">Antes de trabalhar nos exemplos, você precisará de um cluster DC/OS configurado no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="003b8-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="003b8-110">Você também precisa de cluster de toothis toohave conectividade remota.</span><span class="sxs-lookup"><span data-stu-id="003b8-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="003b8-111">Para obter mais informações sobre esses itens, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="003b8-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="003b8-112">Como implantar um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="003b8-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="003b8-113">Conectar-se o cluster do serviço de contêiner do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="003b8-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="003b8-114">Olá DC/OS APIs de acesso</span><span class="sxs-lookup"><span data-stu-id="003b8-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="003b8-115">Depois de cluster do serviço de contêiner do Azure toohello conectado, você pode acessar hello DC/sistema operacional e as APIs REST relacionadas por meio da porta http://localhost:local.</span><span class="sxs-lookup"><span data-stu-id="003b8-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="003b8-116">exemplos de saudação neste documento pressupõem que você está encapsulando na porta 80.</span><span class="sxs-lookup"><span data-stu-id="003b8-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="003b8-117">Por exemplo, os pontos de extremidade do hello maratona podem ser contatados em URIs começando com `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="003b8-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="003b8-118">Para obter mais informações sobre Olá várias APIs, consulte a documentação de Mesosphere Olá para Olá [maratona API](https://mesosphere.github.io/marathon/docs/rest-api.html) e [Chronos API](https://mesos.github.io/chronos/docs/api.html)e a documentação do Apache para Olá [Mesos API do Agendador ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="003b8-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="003b8-119">Coletar informações do DC/OS e do Marathon</span><span class="sxs-lookup"><span data-stu-id="003b8-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="003b8-120">Antes de implantar o cluster de DC/OS contêineres toohello, colete algumas informações sobre o cluster de DC/OS hello, como nomes de saudação e status de saudação DC/OS agentes.</span><span class="sxs-lookup"><span data-stu-id="003b8-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="003b8-121">toodo consulta assim, Olá `master/slaves` ponto de extremidade da saudação API REST do controlador de domínio/OS.</span><span class="sxs-lookup"><span data-stu-id="003b8-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="003b8-122">Se tudo correr bem, consulta Olá retorna uma lista de agentes do controlador de domínio/OS e várias propriedades para cada um.</span><span class="sxs-lookup"><span data-stu-id="003b8-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="003b8-123">Agora, use Olá maratona `/apps` toocheck de ponto de extremidade para aplicativo implantações toohello DC/SO o cluster atual.</span><span class="sxs-lookup"><span data-stu-id="003b8-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="003b8-124">Se esse for um cluster novo, você verá uma matriz vazia para os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="003b8-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="003b8-125">Implantar um contêiner formatado pelo Docker</span><span class="sxs-lookup"><span data-stu-id="003b8-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="003b8-126">Implantar contêineres do Docker formatado por meio de saudação maratona REST API usando um arquivo JSON que descreve a implantação Olá pretendido.</span><span class="sxs-lookup"><span data-stu-id="003b8-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="003b8-127">Olá, exemplo a seguir implanta um agente Nginx contêiner tooa privado no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="003b8-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="003b8-128">toodeploy um contêiner Docker formatado, armazene o arquivo JSON de saudação em um local acessível.</span><span class="sxs-lookup"><span data-stu-id="003b8-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="003b8-129">Próximo, toodeploy Olá contêiner, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="003b8-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="003b8-130">Especificar nome de saudação do arquivo JSON de saudação (`marathon.json` neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="003b8-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="003b8-131">saída de Hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="003b8-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="003b8-132">Agora, se você consultar maratona de aplicativos, esse novo aplicativo aparece na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="003b8-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="003b8-133">Acessar o contêiner de saudação</span><span class="sxs-lookup"><span data-stu-id="003b8-133">Reach hello container</span></span>

<span data-ttu-id="003b8-134">Você pode verificar que Olá que nginx está em execução em um contêiner em um dos agentes de saudação privada no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="003b8-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="003b8-135">host de saudação do toofind e a porta onde Olá contêiner estiver sendo executado, consultar maratona Olá tarefas em execução:</span><span class="sxs-lookup"><span data-stu-id="003b8-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="003b8-136">Localizar o valor de saudação do `host` na saída da saudação (um endereço IP semelhante muito`10.32.0.x`) e o valor de saudação do `ports`.</span><span class="sxs-lookup"><span data-stu-id="003b8-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="003b8-137">Fazer um gerenciamento de toohello de conexão terminal (não uma conexão em túnel) de SSH FQDN de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="003b8-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="003b8-138">Uma vez conectado, fazem Olá solicitação a seguir, substituindo os valores corretos de saudação do `host` e `ports`:</span><span class="sxs-lookup"><span data-stu-id="003b8-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="003b8-139">Olá Nginx saída do servidor é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="003b8-139">hello Nginx server output is similar toohello following:</span></span>

![Nginx do contêiner](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="003b8-141">Dimensionar seus contêineres</span><span class="sxs-lookup"><span data-stu-id="003b8-141">Scale your containers</span></span>
<span data-ttu-id="003b8-142">Você pode usar o hello maratona API tooscale out ou escala em implantações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="003b8-143">No exemplo anterior de saudação, você implantou uma instância de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="003b8-144">Vamos dimensionar isso toothree instâncias de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="003b8-145">Portanto, toodo criar um arquivo JSON usando Olá texto JSON a seguir e armazená-lo em um local acessível.</span><span class="sxs-lookup"><span data-stu-id="003b8-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="003b8-146">A conexão encapsulada, execute Olá comando tooscale aplicativo hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="003b8-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="003b8-147">Olá URI é http://localhost/marathon/v2/apps/ seguido por ID de saudação do hello tooscale de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="003b8-148">Se você estiver usando o exemplo de Nginx hello fornecido aqui, Olá URI seria http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="003b8-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="003b8-149">Por fim, consulte o ponto de extremidade do hello maratona para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="003b8-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="003b8-150">Você vê que agora há três contêineres Nginx.</span><span class="sxs-lookup"><span data-stu-id="003b8-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="003b8-151">Comandos equivalentes do PowerShell</span><span class="sxs-lookup"><span data-stu-id="003b8-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="003b8-152">Você pode executar essas mesmas ações usando comandos do PowerShell em um sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="003b8-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="003b8-153">informações de toogather sobre cluster de DC/OS hello, como nomes de agente e o status do agente, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="003b8-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="003b8-154">Implantar contêineres do Docker formatado por meio da maratona usando um arquivo JSON que descreve a implantação Olá pretendido.</span><span class="sxs-lookup"><span data-stu-id="003b8-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="003b8-155">Olá, exemplo a seguir implanta contêiner de Nginx hello, porta 80 do hello DC/OS agente tooport 80 do contêiner de saudação de associação.</span><span class="sxs-lookup"><span data-stu-id="003b8-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="003b8-156">toodeploy um contêiner Docker formatado, armazene o arquivo JSON de saudação em um local acessível.</span><span class="sxs-lookup"><span data-stu-id="003b8-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="003b8-157">Próximo, toodeploy Olá contêiner, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="003b8-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="003b8-158">Especifique o arquivo JSON do hello caminho toohello (`marathon.json` neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="003b8-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="003b8-159">Você também pode usar o hello maratona API tooscale out ou escala em implantações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="003b8-160">No exemplo anterior de saudação, você implantou uma instância de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="003b8-161">Vamos dimensionar isso toothree instâncias de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="003b8-162">Portanto, toodo criar um arquivo JSON usando Olá texto JSON a seguir e armazená-lo em um local acessível.</span><span class="sxs-lookup"><span data-stu-id="003b8-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="003b8-163">Execute Olá comando tooscale aplicativo hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="003b8-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="003b8-164">Olá URI é http://localhost/marathon/v2/apps/ seguido por ID de saudação do hello tooscale de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="003b8-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="003b8-165">Se você estiver usando o exemplo de Nginx Olá fornecido aqui, Olá URI seria http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="003b8-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="003b8-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="003b8-166">Next steps</span></span>
* [<span data-ttu-id="003b8-167">Leia mais sobre pontos de extremidade de HTTP Mesos Olá</span><span class="sxs-lookup"><span data-stu-id="003b8-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="003b8-168">Leia mais sobre Olá maratona REST API</span><span class="sxs-lookup"><span data-stu-id="003b8-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

