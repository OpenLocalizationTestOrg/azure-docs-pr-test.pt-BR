---
title: "aaaManage Azure DC/OS de cluster com interface de usuário maratona | Microsoft Docs"
description: "Implante o serviço de cluster do serviço de contêiner do Azure de tooan de contêineres usando a interface da web maratona hello."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="26b8e-104">Gerenciar um cluster de serviço de contêiner do Azure DC/OS por meio da interface da web maratona Olá</span><span class="sxs-lookup"><span data-stu-id="26b8e-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="26b8e-105">Controlador de domínio/sistema operacional fornece um ambiente para Implantando e dimensionando cargas de trabalho clusterizadas, enquanto a abstração de hardware subjacente hello.</span><span class="sxs-lookup"><span data-stu-id="26b8e-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="26b8e-106">Sobre o DC/OS, há uma estrutura que gerencia o agendamento e a execução das cargas de trabalho de computação.</span><span class="sxs-lookup"><span data-stu-id="26b8e-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="26b8e-107">Enquanto as estruturas estão disponíveis para várias cargas de trabalho populares, este documento descreve como tooget iniciada implantar contêineres com maratona.</span><span class="sxs-lookup"><span data-stu-id="26b8e-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="26b8e-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26b8e-108">Prerequisites</span></span>
<span data-ttu-id="26b8e-109">Antes de trabalhar nos exemplos, você precisará de um cluster DC/OS configurado no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b8e-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="26b8e-110">Você também precisa de cluster de toothis toohave conectividade remota.</span><span class="sxs-lookup"><span data-stu-id="26b8e-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="26b8e-111">Para obter mais informações sobre esses itens, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="26b8e-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="26b8e-112">Implantar um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="26b8e-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="26b8e-113">Conecte-se o cluster do serviço de contêiner do Azure tooan</span><span class="sxs-lookup"><span data-stu-id="26b8e-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="26b8e-114">Este artigo pressupõe que você está encapsulando toohello cluster de DC/OS pela sua porta local 80.</span><span class="sxs-lookup"><span data-stu-id="26b8e-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="26b8e-115">Explorar Olá DC/sistema operacional da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="26b8e-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="26b8e-116">Com um túnel de Secure Shell (SSH) [estabelecida](../container-service-connect.md), procurar toohttp://localhost/.</span><span class="sxs-lookup"><span data-stu-id="26b8e-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="26b8e-117">Isso carrega a interface da web hello DC/sistema operacional e mostra informações sobre o cluster hello, como os recursos usados, os agentes active e serviços em execução.</span><span class="sxs-lookup"><span data-stu-id="26b8e-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![Interface do usuário do DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="26b8e-119">Explorar Olá maratona da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="26b8e-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="26b8e-120">Olá toosee maratona da interface do usuário, procure toohttp://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="26b8e-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="26b8e-121">Nessa tela, você pode iniciar um novo contêiner ou outro aplicativo no cluster do serviço de contêiner do Azure DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="26b8e-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="26b8e-122">Você também pode ver informações sobre a execução de aplicativos e de contêineres.</span><span class="sxs-lookup"><span data-stu-id="26b8e-122">You can also see information about running containers and applications.</span></span>  

![Interface do usuário do Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="26b8e-124">Implantar um contêiner formatado pelo Docker</span><span class="sxs-lookup"><span data-stu-id="26b8e-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="26b8e-125">toodeploy um novo contêiner usando maratona, clique em **criar aplicativo**e digite Olá segue as informações nas guias de formulário hello:</span><span class="sxs-lookup"><span data-stu-id="26b8e-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="26b8e-126">Campo</span><span class="sxs-lookup"><span data-stu-id="26b8e-126">Field</span></span> | <span data-ttu-id="26b8e-127">Valor</span><span class="sxs-lookup"><span data-stu-id="26b8e-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="26b8e-128">ID</span><span class="sxs-lookup"><span data-stu-id="26b8e-128">ID</span></span> |<span data-ttu-id="26b8e-129">nginx</span><span class="sxs-lookup"><span data-stu-id="26b8e-129">nginx</span></span> |
| <span data-ttu-id="26b8e-130">Memória</span><span class="sxs-lookup"><span data-stu-id="26b8e-130">Memory</span></span> | <span data-ttu-id="26b8e-131">32</span><span class="sxs-lookup"><span data-stu-id="26b8e-131">32</span></span> |
| <span data-ttu-id="26b8e-132">Imagem</span><span class="sxs-lookup"><span data-stu-id="26b8e-132">Image</span></span> |<span data-ttu-id="26b8e-133">nginx</span><span class="sxs-lookup"><span data-stu-id="26b8e-133">nginx</span></span> |
| <span data-ttu-id="26b8e-134">Rede</span><span class="sxs-lookup"><span data-stu-id="26b8e-134">Network</span></span> |<span data-ttu-id="26b8e-135">Com ponte</span><span class="sxs-lookup"><span data-stu-id="26b8e-135">Bridged</span></span> |
| <span data-ttu-id="26b8e-136">Porta de host</span><span class="sxs-lookup"><span data-stu-id="26b8e-136">Host Port</span></span> |<span data-ttu-id="26b8e-137">80</span><span class="sxs-lookup"><span data-stu-id="26b8e-137">80</span></span> |
| <span data-ttu-id="26b8e-138">Protocolo</span><span class="sxs-lookup"><span data-stu-id="26b8e-138">Protocol</span></span> |<span data-ttu-id="26b8e-139">TCP</span><span class="sxs-lookup"><span data-stu-id="26b8e-139">TCP</span></span> |

![Interface do usuário do novo aplicativo – geral](./media/container-service-mesos-marathon-ui/dcos4.png)

![Interface do usuário do novo aplicativo – contêiner do Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Interface do usuário do novo aplicativo - descoberta de serviço e portas](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="26b8e-143">Se você quiser toostatically mapa Olá contêiner tooa porta no agente Olá, é necessário toouse modo JSON.</span><span class="sxs-lookup"><span data-stu-id="26b8e-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="26b8e-144">toodo então, alternar Assistente do novo aplicativo hello muito**JSON modo** usando a alternância de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b8e-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="26b8e-145">Digite hello após a configuração em Olá `portMappings` seção Olá da definição do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26b8e-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="26b8e-146">Este exemplo associa a porta 80 do tooport 80 do contêiner saudação do agente de controlador de domínio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="26b8e-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="26b8e-147">Depois de fazer essa alteração, você pode remover o assistente do Modo JSON.</span><span class="sxs-lookup"><span data-stu-id="26b8e-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Interface do usuário do novo aplicativo – exemplo de porta 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="26b8e-149">Se você quiser tooenable verificações de integridade, definir um caminho em Olá **verificações de integridade** guia.</span><span class="sxs-lookup"><span data-stu-id="26b8e-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Verificações de integridade da interface do usuário do novo aplicativo](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="26b8e-151">cluster de DC/OS de saudação é implantado com o conjunto de agentes públicos e privados.</span><span class="sxs-lookup"><span data-stu-id="26b8e-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="26b8e-152">Para aplicativos do hello cluster toobe tooaccess capaz de saudação à Internet, você precisa de agente público do toodeploy Olá aplicativos tooa.</span><span class="sxs-lookup"><span data-stu-id="26b8e-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="26b8e-153">toodo assim, marque Olá **opcional** guia do Assistente do novo aplicativo hello e digite **slave_public** para Olá **funções de recurso aceitos**.</span><span class="sxs-lookup"><span data-stu-id="26b8e-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="26b8e-154">Em seguida, clique em **Criar Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="26b8e-154">Then click **Create Application**.</span></span>

![Interface do usuário do novo aplicativo - configuração do agente público](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="26b8e-156">Novamente na página principal do maratona Olá, você pode ver o status de implantação de saudação do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b8e-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="26b8e-157">Inicialmente, você vê um status de **Implantando**.</span><span class="sxs-lookup"><span data-stu-id="26b8e-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="26b8e-158">Depois de uma implantação bem-sucedida, Olá alterações de status muito**executando**.</span><span class="sxs-lookup"><span data-stu-id="26b8e-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Interface do usuário da página principal do Marathon – status da implantação do contêiner](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="26b8e-160">Quando você alternar toohello back DC/OS IU da web (http://localhost/), você verá que uma tarefa (nesse caso, um contêiner Docker formatado) está em execução no cluster de DC/OS de saudação.</span><span class="sxs-lookup"><span data-stu-id="26b8e-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![Controlador de domínio/OS interface da web – tarefas em execução no cluster Olá](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="26b8e-162">nó de cluster de saudação toosee que Olá tarefa está em execução no, clique em Olá **nós** guia.</span><span class="sxs-lookup"><span data-stu-id="26b8e-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![Interface do usuário Web DC/OS - nó do cluster de tarefa](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="26b8e-164">Acessar o contêiner de saudação</span><span class="sxs-lookup"><span data-stu-id="26b8e-164">Reach hello container</span></span>

<span data-ttu-id="26b8e-165">Neste exemplo, o aplicativo hello está em execução em um nó de agente pública.</span><span class="sxs-lookup"><span data-stu-id="26b8e-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="26b8e-166">Acessar o aplicativo hello da saudação internet navegando toohello agente FQDN do cluster Olá: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, onde:</span><span class="sxs-lookup"><span data-stu-id="26b8e-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="26b8e-167">**DNSPREFIX** é Olá prefixo DNS que você forneceu quando você implantou o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="26b8e-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="26b8e-168">**REGIÃO** é Olá região na qual o grupo de recursos está localizado.</span><span class="sxs-lookup"><span data-stu-id="26b8e-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Nginx da Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="26b8e-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26b8e-170">Next steps</span></span>
* [<span data-ttu-id="26b8e-171">Trabalhar com o controlador de domínio/OS e Olá maratona API</span><span class="sxs-lookup"><span data-stu-id="26b8e-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="26b8e-172">Mergulho profundo na hello Azure serviço de contêiner com Mesos</span><span class="sxs-lookup"><span data-stu-id="26b8e-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
