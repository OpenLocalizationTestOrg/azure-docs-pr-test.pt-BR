# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="fd13c-101">Escalar nós de agente em um cluster do Serviço de Contêiner</span><span class="sxs-lookup"><span data-stu-id="fd13c-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="fd13c-102">Depois de [implantar um cluster do Serviço de Contêiner do Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), talvez você precise alterar o número de nós do agente.</span><span class="sxs-lookup"><span data-stu-id="fd13c-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="fd13c-103">Por exemplo, mais agentes podem ser necessários para que você possa executar mais aplicativos ou instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="fd13c-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="fd13c-104">É possível alterar o número de nós de agente em um cluster DC/OS, Docker Swarm ou Kubernetes usando o Portal do Azure ou a CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd13c-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="fd13c-105">Dimensionar com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fd13c-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="fd13c-106">No [Portal do Azure](https://portal.azure.com), procure **Serviços de contêiner** e clique no serviço de contêiner que você quer modificar.</span><span class="sxs-lookup"><span data-stu-id="fd13c-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="fd13c-107">Na folha **Serviço de contêiner**, clique em **Agentes**.</span><span class="sxs-lookup"><span data-stu-id="fd13c-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="fd13c-108">Em **Contagem de VM**, insira o número desejado de nós de agentes.</span><span class="sxs-lookup"><span data-stu-id="fd13c-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![Dimensionar um pool no portal](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="fd13c-110">Para salvar a configuração, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fd13c-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="fd13c-111">Dimensionar com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="fd13c-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="fd13c-112">Verifique se você [instalou](/cli/azure/install-az-cli2) a CLI 2.0 do Azure mais recente e conectou-se a uma conta do Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="fd13c-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="fd13c-113">Conferir a conta do agente atual</span><span class="sxs-lookup"><span data-stu-id="fd13c-113">See the current agent count</span></span>
<span data-ttu-id="fd13c-114">Para ver o número de agentes atualmente no cluster, execute o comando `az acs show`.</span><span class="sxs-lookup"><span data-stu-id="fd13c-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="fd13c-115">Isso mostra a configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="fd13c-115">This shows the cluster configuration.</span></span> <span data-ttu-id="fd13c-116">Por exemplo, o seguinte comando mostra a configuração do serviço de contêiner chamado `containerservice-myACSName` no grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="fd13c-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="fd13c-117">O comando retorna o número de agentes no valor `Count` em `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="fd13c-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="fd13c-118">Usar o comando az acs scale</span><span class="sxs-lookup"><span data-stu-id="fd13c-118">Use the az acs scale command</span></span>
<span data-ttu-id="fd13c-119">Para alterar o número de nós de agente, execute o comando `az acs scale` e forneça o **grupo de recursos**, o **nome do serviço de contêiner** e a **nova contagem de agente** desejada.</span><span class="sxs-lookup"><span data-stu-id="fd13c-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="fd13c-120">Ao usar um número menor ou maior, você pode reduzir e escalar verticalmente, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fd13c-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="fd13c-121">Por exemplo, para alterar o número de agentes no cluster anterior para 10, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="fd13c-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="fd13c-122">A CLI 2.0 do Azure retorna uma cadeia de caracteres JSON que representa a nova configuração do serviço de contêiner, incluindo a nova contagem de agentes.</span><span class="sxs-lookup"><span data-stu-id="fd13c-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="fd13c-123">Para obter mais opções de comando, execute `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="fd13c-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="fd13c-124">Considerações de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="fd13c-124">Scaling considerations</span></span>

* <span data-ttu-id="fd13c-125">O número de nós de agente deve estar entre 1 e 100, inclusive.</span><span class="sxs-lookup"><span data-stu-id="fd13c-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="fd13c-126">A cota de núcleos pode limitar o número de nós de agente em um cluster.</span><span class="sxs-lookup"><span data-stu-id="fd13c-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="fd13c-127">As operações de dimensionamento do nó de agente são aplicadas a um conjunto de dimensionamento de máquinas virtuais do Azure que contém o pool de agentes.</span><span class="sxs-lookup"><span data-stu-id="fd13c-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="fd13c-128">Em um cluster DC/OS, somente nós de agente no pool privado são dimensionados pelas operações mostradas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fd13c-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="fd13c-129">Dependendo do orquestrador que você implanta no cluster, é possível dimensionar separadamente o número de instâncias de um contêiner em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="fd13c-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="fd13c-130">Por exemplo, em um cluster DC/OS, use o [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) para alterar o número de instâncias de um aplicativo contêiner.</span><span class="sxs-lookup"><span data-stu-id="fd13c-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="fd13c-131">Atualmente, não há suporte para o dimensionamento automático dos nós de agente em um cluster do serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="fd13c-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd13c-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd13c-132">Next steps</span></span>
* <span data-ttu-id="fd13c-133">Confira [mais exemplos](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) de como usar os comandos da CLI 2.0 do Azure com o Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd13c-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="fd13c-134">Saiba mais sobre os [pools de agentes DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) no Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd13c-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

