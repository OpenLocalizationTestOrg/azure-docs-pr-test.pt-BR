# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="3fc42-101">Criar um cluster de conexão remota tooa Kubernetes, o controlador de domínio/sistema operacional ou o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="3fc42-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="3fc42-102">Depois de criar um cluster do serviço de contêiner do Azure, você precisa tooconnect toohello cluster toodeploy e gerenciar cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3fc42-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="3fc42-103">Este artigo descreve como tooconnect toohello mestre VM de saudação do cluster de um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="3fc42-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="3fc42-104">clusters de Kubernetes, o controlador de domínio/sistema operacional e o Docker Swarm Olá fornecem pontos de extremidade HTTP localmente.</span><span class="sxs-lookup"><span data-stu-id="3fc42-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="3fc42-105">Para Kubernetes, esse ponto de extremidade é exposto de maneira segura em Olá internet e você pode acessá-lo executando Olá `kubectl` ferramenta de linha de comando de qualquer computador conectado à internet.</span><span class="sxs-lookup"><span data-stu-id="3fc42-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="3fc42-106">Para o controlador de domínio/OS e Docker Swarm, recomendamos que você cria um túnel SSH (secure shell) de seu sistema de gerenciamento de cluster de toohello do computador local.</span><span class="sxs-lookup"><span data-stu-id="3fc42-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="3fc42-107">Depois de saudação túnel é estabelecido, você pode executar comandos que usam pontos de extremidade HTTP hello e interface da web do modo de exibição Olá orchestrator (se disponível) do seu sistema local.</span><span class="sxs-lookup"><span data-stu-id="3fc42-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3fc42-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3fc42-108">Prerequisites</span></span>

* <span data-ttu-id="3fc42-109">Um cluster Kubernetes, CD/SO ou Docker Swarm [implantado no Serviço de Contêiner do Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3fc42-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="3fc42-110">SSH RSA arquivo de chave privada correspondente toohello toohello adicional de chave pública cluster durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="3fc42-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="3fc42-111">Esses comandos pressupõem a chave privada SSH hello está em `$HOME/.ssh/id_rsa` em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3fc42-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="3fc42-112">Veja estas instruções para obter mais informações sobre [MacOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3fc42-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="3fc42-113">Se Olá conexão SSH não estiver funcionando, talvez seja necessário muito [redefinir suas chaves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3fc42-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="3fc42-114">Conecte-se tooa Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="3fc42-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="3fc42-115">Siga estas etapas tooinstall e configurar `kubectl` no seu computador.</span><span class="sxs-lookup"><span data-stu-id="3fc42-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="3fc42-116">No Linux ou macOS, talvez seja necessário comandos Olá toorun essa seção usando `sudo`.</span><span class="sxs-lookup"><span data-stu-id="3fc42-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="3fc42-117">Instalar kubectl</span><span class="sxs-lookup"><span data-stu-id="3fc42-117">Install kubectl</span></span>
<span data-ttu-id="3fc42-118">Uma maneira tooinstall essa ferramenta é Olá toouse `az acs kubernetes install-cli` comando 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="3fc42-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="3fc42-119">toorun esse comando, verifique se você [instalado](/cli/azure/install-az-cli2) Olá 2.0 mais recentes de CLI do Azure e registrado no tooan conta do Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="3fc42-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="3fc42-120">Como alternativa, você pode baixar hello mais recente `kubectl` cliente diretamente do hello [Kubernetes libera página](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="3fc42-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="3fc42-121">Para obter mais informações, consulte [Instalando e configurando o kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="3fc42-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="3fc42-122">Baixar credenciais de cluster</span><span class="sxs-lookup"><span data-stu-id="3fc42-122">Download cluster credentials</span></span>
<span data-ttu-id="3fc42-123">Uma vez que `kubectl` instalada, você precisará de máquina de tooyour toocopy Olá cluster credenciais.</span><span class="sxs-lookup"><span data-stu-id="3fc42-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="3fc42-124">Credenciais de saudação get toodo unidirecional é com hello `az acs kubernetes get-credentials` comando.</span><span class="sxs-lookup"><span data-stu-id="3fc42-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="3fc42-125">Passe o nome de Olá Olá do grupo de recursos e nome de saudação do recurso de serviço de contêiner hello:</span><span class="sxs-lookup"><span data-stu-id="3fc42-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="3fc42-126">Esse comando baixa credenciais de cluster Olá muito`$HOME/.kube/config`, onde `kubectl` espera toobe localizado.</span><span class="sxs-lookup"><span data-stu-id="3fc42-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="3fc42-127">Como alternativa, você pode usar `scp` toosecurely copie o arquivo hello de `$HOME/.kube/config` Olá mestre VM tooyour do computador local.</span><span class="sxs-lookup"><span data-stu-id="3fc42-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="3fc42-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3fc42-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="3fc42-129">Se você estiver usando o Windows, você pode usar Bash no Ubuntu no Windows, o cliente de cópia de arquivos seguro PuTTy hello ou uma ferramenta semelhante.</span><span class="sxs-lookup"><span data-stu-id="3fc42-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="3fc42-130">Usar kubectl</span><span class="sxs-lookup"><span data-stu-id="3fc42-130">Use kubectl</span></span>

<span data-ttu-id="3fc42-131">Uma vez que `kubectl` configurado, testar conexão Olá lista Olá nós no cluster:</span><span class="sxs-lookup"><span data-stu-id="3fc42-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="3fc42-132">Você pode tentar outros comandos `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="3fc42-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="3fc42-133">Por exemplo, você pode exibir hello Kubernetes painel.</span><span class="sxs-lookup"><span data-stu-id="3fc42-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="3fc42-134">Primeiro, execute um proxy do servidor de API Kubernetes toohello:</span><span class="sxs-lookup"><span data-stu-id="3fc42-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="3fc42-135">Olá Kubernetes UI agora está disponível em: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="3fc42-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="3fc42-136">Para obter mais informações, consulte Olá [início rápido Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="3fc42-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="3fc42-137">Conecte-se o cluster de DC/sistema operacional ou por nuvem tooa</span><span class="sxs-lookup"><span data-stu-id="3fc42-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="3fc42-138">Olá toouse DC/OS e clusters de Docker Swarm implantados pelo serviço de contêiner do Azure, siga toocreate essas instruções um túnel SSH do seu sistema Linux, macOS ou Windows local.</span><span class="sxs-lookup"><span data-stu-id="3fc42-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="3fc42-139">Essas instruções se concentram no tráfego TCP de túnel via SSH.</span><span class="sxs-lookup"><span data-stu-id="3fc42-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="3fc42-140">Você também pode iniciar uma sessão interativa do SSH com um dos sistemas de gerenciamento de cluster interno hello, mas não recomendamos isso.</span><span class="sxs-lookup"><span data-stu-id="3fc42-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="3fc42-141">Trabalhar diretamente em um sistema interno acarreta o risco de alterações de configuração acidentais</span><span class="sxs-lookup"><span data-stu-id="3fc42-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="3fc42-142">Criar um túnel SSH no Linux ou no macOS</span><span class="sxs-lookup"><span data-stu-id="3fc42-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="3fc42-143">Olá primeira coisa que você faz quando você criar um túnel SSH no Linux ou macOS é toolocate Olá nome DNS público de mestres de balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc42-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="3fc42-144">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3fc42-144">Follow these steps:</span></span>


1. <span data-ttu-id="3fc42-145">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello grupo de recursos que contém o cluster do serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="3fc42-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="3fc42-146">Expanda o grupo de recursos de saudação para que cada recurso é exibido.</span><span class="sxs-lookup"><span data-stu-id="3fc42-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="3fc42-147">Clique em Olá **serviço de contêiner** recurso e clique em **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="3fc42-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="3fc42-148">Olá **FQDN mestre** de saudação cluster aparece sob **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="3fc42-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="3fc42-149">Salve o nome para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="3fc42-149">Save this name for later use.</span></span> 

    ![Nome DNS público](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="3fc42-151">Como alternativa, executar Olá `az acs show` comando no seu serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="3fc42-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="3fc42-152">Procure Olá **mestre perfil: fqdn** propriedade na saída do comando hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="3fc42-153">Agora, abra um shell e execute Olá `ssh` comando especificando Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc42-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="3fc42-154">**LOCAL_PORT** é a porta TCP no lado do serviço de saudação do hello túnel tooconnect para hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="3fc42-155">Para por nuvem, defina este too2375.</span><span class="sxs-lookup"><span data-stu-id="3fc42-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="3fc42-156">Para DC/OS, defina este too80.</span><span class="sxs-lookup"><span data-stu-id="3fc42-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="3fc42-157">**REMOTE_PORT** é a porta de saudação do ponto de extremidade de saudação que você deseja tooexpose.</span><span class="sxs-lookup"><span data-stu-id="3fc42-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="3fc42-158">Para a nuvem, use a porta 2375.</span><span class="sxs-lookup"><span data-stu-id="3fc42-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="3fc42-159">Para o DC/OS, use a porta 80.</span><span class="sxs-lookup"><span data-stu-id="3fc42-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="3fc42-160">**Nome de usuário** é Olá nome de usuário fornecido quando você implantou o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="3fc42-161">**DNSPREFIX** é Olá prefixo DNS que você forneceu quando você implantou o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="3fc42-162">**REGIÃO** é Olá região na qual o grupo de recursos está localizado.</span><span class="sxs-lookup"><span data-stu-id="3fc42-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="3fc42-163">**PATH_TO_PRIVATE_KEY** [opcional] é Olá caminho toohello chave privada correspondente toohello chave pública que você forneceu ao criar cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="3fc42-164">Use essa opção com hello `-i` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="3fc42-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="3fc42-165">Olá porta de conexão SSH é 2200 e não Olá 22 de porta padrão.</span><span class="sxs-lookup"><span data-stu-id="3fc42-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="3fc42-166">Em um cluster com mais de uma VM mestre, isso é o mestre de primeira toohello VM de porta de conexão hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="3fc42-167">comando Olá retorna sem saída.</span><span class="sxs-lookup"><span data-stu-id="3fc42-167">hello command returns without output.</span></span>

<span data-ttu-id="3fc42-168">Consulte exemplos de saudação DC/sistema operacional e por nuvem Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="3fc42-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="3fc42-169">Túnel DC/OS</span><span class="sxs-lookup"><span data-stu-id="3fc42-169">DC/OS tunnel</span></span>
<span data-ttu-id="3fc42-170">tooopen um encapsulamento para pontos de extremidade do controlador de domínio/OS, execute um comando como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc42-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="3fc42-171">Certifique-se de que você não tem outro processo local que associa a porta 80.</span><span class="sxs-lookup"><span data-stu-id="3fc42-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="3fc42-172">Se necessário, você pode especificar uma porta local diferente da porta 80, como a porta 8080.</span><span class="sxs-lookup"><span data-stu-id="3fc42-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="3fc42-173">No entanto, alguns links da interface do usuário da Web podem não funcionar quando você usa essa porta.</span><span class="sxs-lookup"><span data-stu-id="3fc42-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="3fc42-174">Agora você pode acessar os pontos de extremidade de DC/OS de saudação do seu sistema local por meio de saudação seguintes URLs (supondo que a porta local 80):</span><span class="sxs-lookup"><span data-stu-id="3fc42-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="3fc42-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="3fc42-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="3fc42-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="3fc42-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="3fc42-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="3fc42-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="3fc42-178">Da mesma forma, você pode acessar as APIs de rest Olá para cada aplicativo por esse túnel.</span><span class="sxs-lookup"><span data-stu-id="3fc42-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="3fc42-179">Túnel do Swarm</span><span class="sxs-lookup"><span data-stu-id="3fc42-179">Swarm tunnel</span></span>
<span data-ttu-id="3fc42-180">tooopen um toohello por nuvem ponto de extremidade, execute um comando como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3fc42-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="3fc42-181">Certifique-se de que você não tem outro processo local que associa a porta 2375.</span><span class="sxs-lookup"><span data-stu-id="3fc42-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="3fc42-182">Por exemplo, se você estiver executando o daemon do Docker Olá localmente, ele é definido como padrão a porta 2375 toouse.</span><span class="sxs-lookup"><span data-stu-id="3fc42-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="3fc42-183">Se necessário, você pode especificar uma porta local diferente da porta 2375.</span><span class="sxs-lookup"><span data-stu-id="3fc42-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="3fc42-184">Agora você pode acessar o cluster de Docker Swarm de saudação usando a interface de linha de comando Docker hello (CLI do Docker) em seu sistema local.</span><span class="sxs-lookup"><span data-stu-id="3fc42-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="3fc42-185">Para as instruções de instalação, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="3fc42-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="3fc42-186">Defina sua toohello de variável de ambiente DOCKER_HOST porta local configurado para túnel hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="3fc42-187">Execute os comandos cluster túnel toohello Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="3fc42-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="3fc42-188">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3fc42-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="3fc42-189">Criar um túnel SSH no Windows</span><span class="sxs-lookup"><span data-stu-id="3fc42-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="3fc42-190">Há várias opções para a criação de túneis SSH no Windows.</span><span class="sxs-lookup"><span data-stu-id="3fc42-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="3fc42-191">Se você estiver executando Bash no Ubuntu no Windows ou uma ferramenta semelhante, você pode seguir as instruções de túnel de SSH do hello mostradas anteriormente neste artigo para macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="3fc42-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="3fc42-192">Como alternativa no Windows, esta seção descreve como túnel de saudação do toouse toocreate PuTTY.</span><span class="sxs-lookup"><span data-stu-id="3fc42-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="3fc42-193">[Baixar o PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="3fc42-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="3fc42-194">Execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-194">Run hello application.</span></span>

3. <span data-ttu-id="3fc42-195">Insira um nome de host que é composto de nome de usuário do administrador de cluster de saudação e o nome DNS público de saudação do mestre de saudação primeiro cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3fc42-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="3fc42-196">Olá **nome de Host** parece muito`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="3fc42-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="3fc42-197">Insira 2200 Olá **porta**.</span><span class="sxs-lookup"><span data-stu-id="3fc42-197">Enter 2200 for hello **Port**.</span></span>

    ![Configuração do PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="3fc42-199">Selecione **SSH > Auth**. Adicione um caminho tooyour arquivo de chave privada (formato *.ppk) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="3fc42-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="3fc42-200">Você pode usar uma ferramenta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate esse arquivo hello cluster de saudação toocreate usado chave SSH.</span><span class="sxs-lookup"><span data-stu-id="3fc42-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![Configuração do PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="3fc42-202">Selecione **SSH > túneis** e configure o seguinte Olá encaminhados portas:</span><span class="sxs-lookup"><span data-stu-id="3fc42-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="3fc42-203">**Porta de Origem:** use 80 para DC/SO ou 2375 para nuvem.</span><span class="sxs-lookup"><span data-stu-id="3fc42-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="3fc42-204">**Destino:** use localhost:80 para o DC/OS ou localhost:2375 para o Swarm.</span><span class="sxs-lookup"><span data-stu-id="3fc42-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="3fc42-205">saudação de exemplo a seguir está configurada para o controlador de domínio/SO, mas será semelhante para Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="3fc42-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3fc42-206">A porta 80 não deve estar em uso quando você criar esse túnel.</span><span class="sxs-lookup"><span data-stu-id="3fc42-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configuração do PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="3fc42-208">Quando tiver terminado, clique em **sessão > Salvar** toosave configuração de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3fc42-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="3fc42-209">tooconnect toohello PuTTY sessão, clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="3fc42-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="3fc42-210">Quando você se conectar, você pode ver a configuração da porta Olá no log de eventos PuTTY Olá.</span><span class="sxs-lookup"><span data-stu-id="3fc42-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![Log de eventos do PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="3fc42-212">Depois de configurar o túnel Olá para o controlador de domínio/sistema operacional, você pode acessar Olá relacionadas a pontos de extremidade em:</span><span class="sxs-lookup"><span data-stu-id="3fc42-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="3fc42-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="3fc42-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="3fc42-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="3fc42-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="3fc42-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="3fc42-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="3fc42-216">Depois de configurar o túnel de saudação para Docker Swarm, abra seu tooconfigure de configurações do Windows uma variável de ambiente de sistema chamada `DOCKER_HOST` com um valor de `:2375`.</span><span class="sxs-lookup"><span data-stu-id="3fc42-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="3fc42-217">Em seguida, você pode acessar o cluster de por nuvem Olá através de Olá CLI do Docker.</span><span class="sxs-lookup"><span data-stu-id="3fc42-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fc42-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3fc42-218">Next steps</span></span>
<span data-ttu-id="3fc42-219">Implantar e gerenciar contêineres no cluster:</span><span class="sxs-lookup"><span data-stu-id="3fc42-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="3fc42-220">Trabalhar com o Serviço de Contêiner do Azure e o Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3fc42-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="3fc42-221">Trabalhar com o Serviço de Contêiner do Azure e o DC/SO</span><span class="sxs-lookup"><span data-stu-id="3fc42-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="3fc42-222">Trabalhar com hello Azure serviço de contêiner e o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="3fc42-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

