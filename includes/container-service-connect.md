# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="c1fdc-101">Fazer uma conexão remota com um cluster Kubernetes, DC/OS ou Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c1fdc-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="c1fdc-102">Depois de criar um cluster do serviço de contêiner do Azure, você precisa se conectar ao cluster para implantar e gerenciar cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="c1fdc-103">Este artigo descreve como conectar-se à VM mestre do cluster de um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="c1fdc-104">Os clusters Kubernetes DC/SO e Docker Swarm fornecem pontos de extremidade HTTP localmente.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="c1fdc-105">Para Kubernetes, esse ponto de extremidade é exposto de maneira segura na Internet, e você pode acessá-lo executando a ferramenta de linha de comando `kubectl` de qualquer computador conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="c1fdc-106">Para Controlador de domínio/sistema operacional e Docker Swarm, recomendamos a criação de um túnel de shell seguro (SSH) do computador local para o sistema de gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="c1fdc-107">Depois que o túnel for estabelecido, você pode executar comandos que usam os pontos de extremidade HTTP e exibir a interface da Web do orquestrador (se disponível) do seu sistema local.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c1fdc-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c1fdc-108">Prerequisites</span></span>

* <span data-ttu-id="c1fdc-109">Um cluster Kubernetes, CD/SO ou Docker Swarm [implantado no Serviço de Contêiner do Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="c1fdc-110">Um arquivo de chave privada SSH RSA, correspondente à chave pública adicionada ao cluster durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="c1fdc-111">Esses comandos pressupõem que a chave privada do SSH esteja em `$HOME/.ssh/id_rsa` em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="c1fdc-112">Veja estas instruções para obter mais informações sobre [MacOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="c1fdc-113">Se a conexão SSH não está funcionando, você talvez precise [redefinir suas chaves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="c1fdc-114">Conectar-se a um cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c1fdc-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="c1fdc-115">Siga estas etapas para instalar e configurar `kubectl` no computador.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="c1fdc-116">No Linux ou macOS, talvez seja necessário executar os comandos nesta seção usando `sudo`.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="c1fdc-117">Instalar kubectl</span><span class="sxs-lookup"><span data-stu-id="c1fdc-117">Install kubectl</span></span>
<span data-ttu-id="c1fdc-118">Uma maneira de instalar essa ferramenta é usar o comando `az acs kubernetes install-cli` da CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="c1fdc-119">Para executar esse comando, verifique se você [instalou](/cli/azure/install-az-cli2) a CLI do Azure 2.0 mais recente e conectou-se a uma conta do Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="c1fdc-120">Como alternativa, você pode baixar o cliente `kubectl` mais recente diretamente na [página de versões do Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="c1fdc-121">Para obter mais informações, consulte [Instalando e configurando o kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="c1fdc-122">Baixar credenciais de cluster</span><span class="sxs-lookup"><span data-stu-id="c1fdc-122">Download cluster credentials</span></span>
<span data-ttu-id="c1fdc-123">Uma vez que `kubectl` esteja instalado, você precisa copiar as credenciais de cluster em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="c1fdc-124">Uma maneira de obter as credenciais é com o comando `az acs kubernetes get-credentials`.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="c1fdc-125">Passe o nome do grupo de recursos e o nome do recurso de serviço de contêiner:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="c1fdc-126">Esse comando baixa as credenciais do cluster para `$HOME/.kube/config`, em que `kubectl` espera que estejam.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="c1fdc-127">Como alternativa, você pode usar `scp` para copiar o arquivo de forma segura de `$HOME/.kube/config` para a VM mestre em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="c1fdc-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="c1fdc-129">Se estiver no Windows, você pode usar o Bash no Ubuntu no Windows, o cliente de cópia de arquivo segura PuTTy ou uma ferramenta semelhante.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="c1fdc-130">Usar kubectl</span><span class="sxs-lookup"><span data-stu-id="c1fdc-130">Use kubectl</span></span>

<span data-ttu-id="c1fdc-131">Uma vez que `kubectl` estiver configurado, teste a conexão listando os nós no cluster:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="c1fdc-132">Você pode tentar outros comandos `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="c1fdc-133">Por exemplo, você pode exibir o Painel de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="c1fdc-134">Primeiro, execute um proxy para o servidor de API Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="c1fdc-135">A interface do usuário do Kubernetes agora está disponível em: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="c1fdc-136">Para obter mais informações, confira [Início rápido do Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="c1fdc-137">Conectar-se a um cluster de DC/SO ou Swarm</span><span class="sxs-lookup"><span data-stu-id="c1fdc-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="c1fdc-138">Para usar o DC/SO e clusters Docker Swarm implantados pelo Serviço de Contêiner do Azure, siga estas instruções para criar um túnel SSH a partir do seu sistema Linux, macOS ou Windows local.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="c1fdc-139">Essas instruções se concentram no tráfego TCP de túnel via SSH.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="c1fdc-140">Você também pode iniciar uma sessão SSH interativa com um dos sistemas de gerenciamento de cluster interno, mas não recomendamos isso.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="c1fdc-141">Trabalhar diretamente em um sistema interno acarreta o risco de alterações de configuração acidentais</span><span class="sxs-lookup"><span data-stu-id="c1fdc-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="c1fdc-142">Criar um túnel SSH no Linux ou no macOS</span><span class="sxs-lookup"><span data-stu-id="c1fdc-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="c1fdc-143">A primeira coisa que você faz quando cria um túnel SSH no Linux ou no macOS é localizar o nome DNS público de mestres de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="c1fdc-144">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-144">Follow these steps:</span></span>


1. <span data-ttu-id="c1fdc-145">No [portal do Azure](https://portal.azure.com), navegue até o grupo de recursos que contém o cluster de serviço do contêiner.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="c1fdc-146">Expanda o grupo de recursos para que todos os recursos sejam exibidos.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="c1fdc-147">Clique no recurso de **Serviço de contêiner** e, em seguida, clique em **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="c1fdc-148">O **FQDN mestre** do cluster aparece nos **Conceitos básicos**.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="c1fdc-149">Salve o nome para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-149">Save this name for later use.</span></span> 

    ![Nome DNS público](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="c1fdc-151">Como alternativa, execute o comando `az acs show` em seu serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="c1fdc-152">Procure a propriedade **Master Profile:fqdn** na saída do comando.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="c1fdc-153">Agora abra um shell e execute o comando `ssh` especificando os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="c1fdc-154">**LOCAL_PORT** é a porta TCP no lado do serviço do túnel com o qual se conectar.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="c1fdc-155">Para Swarm, defina para 2375.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="c1fdc-156">Para DC/SO, defina para 80.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="c1fdc-157">**REMOTE_PORT** é a porta do ponto de extremidade que você deseja expor.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="c1fdc-158">Para a nuvem, use a porta 2375.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="c1fdc-159">Para o DC/OS, use a porta 80.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="c1fdc-160">**NOME DE USUÁRIO** é o nome de usuário fornecido quando você implantou o cluster.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="c1fdc-161">**PREFIXODEDNS** é o prefixo de DNS que você forneceu ao implantar o cluster.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="c1fdc-162">**REGIÃO** é a região em que o grupo de recursos está localizado.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="c1fdc-163">**CAMINHO_PARA_CHAVE_PRIVADA** [OPCIONAL] é o caminho para a chave privada correspondente à chave pública que você forneceu ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="c1fdc-164">Use essa opção com o sinalizador `-i`.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="c1fdc-165">A porta de conexão SSH é 2200, e não a porta 22 padrão.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="c1fdc-166">Em um cluster com mais de uma VM mestre, essa é a porta de conexão para a primeira VM mestre.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="c1fdc-167">O comando retorna sem saída.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-167">The command returns without output.</span></span>

<span data-ttu-id="c1fdc-168">Confira os exemplos de DC/SO e nuvem nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="c1fdc-169">Túnel DC/OS</span><span class="sxs-lookup"><span data-stu-id="c1fdc-169">DC/OS tunnel</span></span>
<span data-ttu-id="c1fdc-170">Para abrir um túnel para pontos de extremidade do DC/SO, execute um comando semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="c1fdc-171">Certifique-se de que você não tem outro processo local que associa a porta 80.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="c1fdc-172">Se necessário, você pode especificar uma porta local diferente da porta 80, como a porta 8080.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="c1fdc-173">No entanto, alguns links da interface do usuário da Web podem não funcionar quando você usa essa porta.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="c1fdc-174">Agora você pode acessar os pontos de extremidade do DC/SO do seu sistema local por meio das URLs a seguir (supondo que a porta local é a 80):</span><span class="sxs-lookup"><span data-stu-id="c1fdc-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="c1fdc-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="c1fdc-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="c1fdc-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="c1fdc-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="c1fdc-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="c1fdc-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="c1fdc-178">Da mesma forma, as APIs rest para cada aplicativo podem ser acessadas por este túnel.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="c1fdc-179">Túnel do Swarm</span><span class="sxs-lookup"><span data-stu-id="c1fdc-179">Swarm tunnel</span></span>
<span data-ttu-id="c1fdc-180">Para abrir um túnel para o ponto de extremidade do Swarn, execute um comando semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="c1fdc-181">Certifique-se de que você não tem outro processo local que associa a porta 2375.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="c1fdc-182">Por exemplo, se você estiver executando o daemon do Docker localmente, ele é definido por padrão para usar a porta 2375.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="c1fdc-183">Se necessário, você pode especificar uma porta local diferente da porta 2375.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="c1fdc-184">Agora você pode acessar o cluster do Docker Swarm usando a interface de linha de comando do Docker (CLI do Docker) no seu sistema local.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="c1fdc-185">Para as instruções de instalação, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="c1fdc-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="c1fdc-186">Defina sua variável de ambiente DOCKER_HOST para a porta local configurada para o túnel.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="c1fdc-187">Execute os comandos do Docker que fazem o túnel para o cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="c1fdc-188">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="c1fdc-189">Criar um túnel SSH no Windows</span><span class="sxs-lookup"><span data-stu-id="c1fdc-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="c1fdc-190">Há várias opções para a criação de túneis SSH no Windows.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="c1fdc-191">Se você estiver executando Bash no Ubuntu no Windows ou uma ferramenta semelhante, você pode seguir as instruções de túnel SSH mostradas anteriormente neste artigo para macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="c1fdc-192">Como alternativa no Windows, esta seção descreve como usar PuTTY para criar o túnel.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="c1fdc-193">[Baixe o PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) para o sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="c1fdc-194">Execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-194">Run the application.</span></span>

3. <span data-ttu-id="c1fdc-195">Insira um nome de host que consista no nome de usuário do administrador do cluster e no nome DNS público do primeiro mestre no cluster.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="c1fdc-196">O **Nome do Host** é semelhante a `azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="c1fdc-197">Insira 2200 em **Porta**.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-197">Enter 2200 for the **Port**.</span></span>

    ![Configuração do PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="c1fdc-199">Selecione **SSH > Auth**.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="c1fdc-200">Adicione um caminho para o arquivo de chave privada (formato .ppk) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="c1fdc-201">Você pode usar uma ferramenta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) para gerar esse arquivo da chave SSH usada para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![Configuração do PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="c1fdc-203">Selecione **SSH > Túnel** e configure as seguintes portas encaminhadas:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="c1fdc-204">**Porta de Origem:** use 80 para DC/SO ou 2375 para nuvem.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="c1fdc-205">**Destino:** use localhost:80 para o DC/OS ou localhost:2375 para o Swarm.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="c1fdc-206">O exemplo a seguir é configurado para o DC/OS, mas seria semelhante para o Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c1fdc-207">A porta 80 não deve estar em uso quando você criar esse túnel.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configuração do PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="c1fdc-209">Quando terminar, clique em **Sessão > Salvar** para salvar a configuração de conexão.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="c1fdc-210">Para se conectar à sessão do PuTTY, clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="c1fdc-211">Quando você se conectar, poderá ver a configuração da porta no log de eventos do PuTTY.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![Log de eventos do PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="c1fdc-213">Após configurar o túnel para o DC/SO, você poderá acessar os pontos de extremidade relacionados em:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="c1fdc-214">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="c1fdc-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="c1fdc-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="c1fdc-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="c1fdc-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="c1fdc-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="c1fdc-217">Depois de configurar o túnel de Docker Swarm, abra as configurações do Windows para configurar uma variável de ambiente do sistema denominada `DOCKER_HOST` com um valor de `:2375`.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="c1fdc-218">Em seguida, você pode acessar o cluster do Swarm por meio da CLI do Docker.</span><span class="sxs-lookup"><span data-stu-id="c1fdc-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1fdc-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1fdc-219">Next steps</span></span>
<span data-ttu-id="c1fdc-220">Implantar e gerenciar contêineres no cluster:</span><span class="sxs-lookup"><span data-stu-id="c1fdc-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="c1fdc-221">Trabalhar com o Serviço de Contêiner do Azure e o Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c1fdc-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="c1fdc-222">Trabalhar com o Serviço de Contêiner do Azure e o DC/SO</span><span class="sxs-lookup"><span data-stu-id="c1fdc-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="c1fdc-223">Trabalhar com o Serviço de Contêiner do Azure e o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="c1fdc-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

