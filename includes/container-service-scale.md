# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="1b108-101">Escalar nós de agente em um cluster do Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="1b108-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="1b108-102">Depois de [Implantando um cluster do serviço de contêiner do Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), talvez seja necessário um número de saudação do toochange de nós de agente.</span><span class="sxs-lookup"><span data-stu-id="1b108-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="1b108-103">Por exemplo, mais agentes podem ser necessários para que você possa executar mais aplicativos ou instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="1b108-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="1b108-104">Você pode alterar o número de saudação de nós de agente em um cluster de DC/OS, o Docker Swarm ou Kubernetes usando Olá portal do Azure ou Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b108-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="1b108-105">Dimensionar com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1b108-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="1b108-106">Em Olá [portal do Azure](https://portal.azure.com), procurar **serviços de contêiner**e, em seguida, clique em serviço de contêiner de saudação que você deseja toomodify.</span><span class="sxs-lookup"><span data-stu-id="1b108-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="1b108-107">Em Olá **serviço de contêiner** folha, clique em **agentes**.</span><span class="sxs-lookup"><span data-stu-id="1b108-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="1b108-108">Em **contagem de VM**, insira o número desejado de saudação de nós de agentes.</span><span class="sxs-lookup"><span data-stu-id="1b108-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Dimensionar um pool no portal de saudação](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="1b108-110">configuração de saudação toosave, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="1b108-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="1b108-111">Dimensionar com hello 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1b108-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="1b108-112">Verifique se você [instalado](/cli/azure/install-az-cli2) Olá 2.0 mais recentes de CLI do Azure e registrado no tooan conta do azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="1b108-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="1b108-113">Consulte a contagem atual de agente Olá</span><span class="sxs-lookup"><span data-stu-id="1b108-113">See hello current agent count</span></span>
<span data-ttu-id="1b108-114">número de saudação do toosee de agentes no momento em cluster Olá, executar Olá `az acs show` comando.</span><span class="sxs-lookup"><span data-stu-id="1b108-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="1b108-115">Isso mostra a configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b108-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="1b108-116">Por exemplo, Olá mostra Olá a configuração do serviço de contêiner Olá chamado de comando a seguir `containerservice-myACSName` no grupo de recursos de saudação `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="1b108-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="1b108-117">comando Olá retorna o número de saudação de agentes em Olá `Count` valor em `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="1b108-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="1b108-118">Use Olá az comando de escala do acs</span><span class="sxs-lookup"><span data-stu-id="1b108-118">Use hello az acs scale command</span></span>
<span data-ttu-id="1b108-119">número de saudação toochange de nós de agente, executar Olá `az acs scale` Olá comando e forneça **grupo de recursos**, **nome do serviço de contêiner**e hello desejado **nova contagem de agente**.</span><span class="sxs-lookup"><span data-stu-id="1b108-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="1b108-120">Ao usar um número menor ou maior, você pode reduzir e escalar verticalmente, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="1b108-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="1b108-121">Por exemplo, número de saudação toochange de agentes na saudação anterior too10 de cluster, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b108-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="1b108-122">Olá 2.0 do CLI do Azure retorna uma cadeia de caracteres JSON que representa a nova configuração de saudação do serviço de contêiner hello, incluindo a nova contagem de agente hello.</span><span class="sxs-lookup"><span data-stu-id="1b108-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="1b108-123">Para obter mais opções de comando, execute `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="1b108-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="1b108-124">Considerações de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="1b108-124">Scaling considerations</span></span>

* <span data-ttu-id="1b108-125">número de saudação de nós de agente deve estar entre 1 e 100, inclusive.</span><span class="sxs-lookup"><span data-stu-id="1b108-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="1b108-126">Sua cota de núcleos pode limitar o número de saudação de nós de agente em um cluster.</span><span class="sxs-lookup"><span data-stu-id="1b108-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="1b108-127">Operações de dimensionamento de nó do agente são aplicadas tooan conjunto de escala de máquina virtual do Azure que contém o pool de agente hello.</span><span class="sxs-lookup"><span data-stu-id="1b108-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="1b108-128">Em um cluster de DC/OS, somente nós de agente no pool privada Olá são dimensionados pelas operações de saudação mostradas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="1b108-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="1b108-129">Dependendo orchestrator Olá que implantar em seu cluster, você pode dimensionar separadamente número Olá de instâncias de um contêiner em execução no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1b108-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="1b108-130">Por exemplo, em um cluster de DC/sistema operacional, use Olá [maratona UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange número de saudação de instâncias de um aplicativo de contêiner.</span><span class="sxs-lookup"><span data-stu-id="1b108-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="1b108-131">Atualmente, não há suporte para o dimensionamento automático dos nós de agente em um cluster do serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="1b108-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b108-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b108-132">Next steps</span></span>
* <span data-ttu-id="1b108-133">Confira [mais exemplos](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) de como usar os comandos da CLI 2.0 do Azure com o Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b108-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="1b108-134">Saiba mais sobre os [pools de agentes DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b108-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

