
* [<span data-ttu-id="9e187-101">Criar rapidamente uma máquina virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="9e187-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="9e187-102">Implantar uma máquina virtual no Azure com base em um modelo</span><span class="sxs-lookup"><span data-stu-id="9e187-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="9e187-103">Criar uma máquina virtual com base em uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="9e187-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="9e187-104">Implantar uma máquina virtual que usa uma rede virtual e um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="9e187-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="9e187-105">Remover um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e187-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="9e187-106">Mostrar log Olá para uma implantação de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e187-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="9e187-107">Exibir informações sobre uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9e187-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="9e187-108">Conecte-se a máquina virtual baseados em Linux de tooa</span><span class="sxs-lookup"><span data-stu-id="9e187-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="9e187-109">Parar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9e187-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="9e187-110">Iniciar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9e187-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="9e187-111">Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="9e187-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="9e187-112">Preparando-se</span><span class="sxs-lookup"><span data-stu-id="9e187-112">Getting ready</span></span>
<span data-ttu-id="9e187-113">Antes de usar Olá CLI do Azure com grupos de recursos do Azure, você precisará versão toohave Olá de direito CLI do Azure e uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e187-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="9e187-114">Se você não tiver Olá CLI do Azure, [instalá-lo](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9e187-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="9e187-115">Atualizar seu too0.9.0 de versão da CLI do Azure ou posterior</span><span class="sxs-lookup"><span data-stu-id="9e187-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="9e187-116">Tipo `azure --version` toosee se você já tiver instalado a versão 0.9.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9e187-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="9e187-117">Se sua versão não é 0.9.0 ou posterior, você precisa tooupdate-lo usando um dos Olá instaladores nativo ou por meio **npm** digitando `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="9e187-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="9e187-118">Você também pode executar CLI do Azure como um contêiner do Docker usando o seguinte Olá [imagem Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="9e187-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="9e187-119">Em um host Docker, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e187-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="9e187-120">Definir sua conta e assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="9e187-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="9e187-121">Se ainda não tiver uma assinatura do Azure, mas tiver uma assinatura do MSDN, você poderá ativar seus [benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="9e187-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="9e187-122">Ou então, você poderá se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e187-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="9e187-123">Agora [login tooyour conta do Azure interativamente](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) digitando `azure login` e seguir Olá solicitará uma experiência de logon interativo tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e187-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="9e187-124">Se você tem um trabalho ou de estudante ID e você sabe que você não tenha habilitada de autenticação de dois fatores, você pode **também** usar `azure login -u` juntamente com hello ou de estudante toolog ID em *sem* uma sessão interativa.</span><span class="sxs-lookup"><span data-stu-id="9e187-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="9e187-125">Se você não tem um trabalho ou de estudante ID, você pode [criar uma id de trabalho ou da escola de sua conta pessoal da Microsoft](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog em Olá mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="9e187-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="9e187-126">Sua conta pode ter mais de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="9e187-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="9e187-127">Você pode listar suas assinaturas digitando `azure account list`, que pode ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="9e187-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="9e187-128">Você pode definir a assinatura do Azure Olá digitando o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="9e187-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="9e187-129">Use Olá nome ou hello ID de assinatura que tem recursos de saudação deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="9e187-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="9e187-130">Alternar o modo de grupo de recursos toohello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9e187-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="9e187-131">Por padrão, a saudação CLI do Azure inicia no modo de gerenciamento de serviço de saudação (**asm** modo).</span><span class="sxs-lookup"><span data-stu-id="9e187-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="9e187-132">Digite hello modo de grupo de tooresource tooswitch a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e187-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="9e187-133">Noções básicas sobre grupos de recursos e modelos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="9e187-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="9e187-134">A maioria dos aplicativos é criada a partir de uma combinação de diferentes tipos de recursos (como uma ou mais VMs e contas de Armazenamento, um banco de dados SQL, uma Rede Virtual ou uma rede de transmissão de conteúdo).</span><span class="sxs-lookup"><span data-stu-id="9e187-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="9e187-135">Olá API de gerenciamento de serviço do Azure padrão e hello portal clássico do Azure representado esses itens usando uma abordagem pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="9e187-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="9e187-136">Essa abordagem requer que você toodeploy e gerenciar serviços individuais Olá individualmente (ou localizar outras ferramentas que fazem-lo) e não como uma única unidade lógica de implantação.</span><span class="sxs-lookup"><span data-stu-id="9e187-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="9e187-137">*Modelos do Gerenciador de recursos do Azure*, no entanto, possibilitam que você toodeploy e gerenciar esses recursos diferentes, como uma unidade lógica de implantação de forma declarativa.</span><span class="sxs-lookup"><span data-stu-id="9e187-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="9e187-138">Em vez de imperativa informando do Azure que toodeploy um comando após o outro, você descreve sua implantação completa em um arquivo JSON – todos os recursos de saudação e configurações associadas e parâmetros de implantação – e informar o Azure toodeploy esses recursos como um grupo.</span><span class="sxs-lookup"><span data-stu-id="9e187-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="9e187-139">Você pode gerenciar Olá ciclo de vida geral de recursos do grupo hello usando comandos de gerenciamento de recursos de CLI do Azure para:</span><span class="sxs-lookup"><span data-stu-id="9e187-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="9e187-140">Parar, iniciar ou excluir todos os recursos de saudação dentro do grupo de saudação de uma vez.</span><span class="sxs-lookup"><span data-stu-id="9e187-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="9e187-141">Aplique toolock de regras de controle de acesso baseado em função (RBAC) permissões de segurança-los.</span><span class="sxs-lookup"><span data-stu-id="9e187-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="9e187-142">Auditar operações.</span><span class="sxs-lookup"><span data-stu-id="9e187-142">Audit operations.</span></span>
* <span data-ttu-id="9e187-143">Marcar recursos com metadados extras para ter melhor acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="9e187-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="9e187-144">Você pode aprender muito mais sobre grupos de recursos do Azure e o que eles podem fazer para você no hello [visão geral do Gerenciador de recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e187-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="9e187-145">Se você estiver interessado na criação de modelos, confira [Criando modelos do Gerenciador de Recursos do Azure](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9e187-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="9e187-146"><a id="quick-create-a-vm-in-azure"></a>Tarefa: Criar rapidamente uma VM no Azure</span><span class="sxs-lookup"><span data-stu-id="9e187-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="9e187-147">Às vezes, você sabe quais imagem que você precisa, e você precisa de uma VM da imagem agora e não se preocupar muito infraestrutura Olá - talvez você tenha tootest algo em uma VM limpa.</span><span class="sxs-lookup"><span data-stu-id="9e187-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="9e187-148">Ou seja, quando você deseja Olá toouse `azure vm quick-create` de comando e passe Olá argumentos necessários toocreate uma máquina virtual e sua infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="9e187-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="9e187-149">Em primeiro lugar, crie o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9e187-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9e187-150">Em segundo lugar, você precisará de uma imagem.</span><span class="sxs-lookup"><span data-stu-id="9e187-150">Second, you'll need an image.</span></span> <span data-ttu-id="9e187-151">toofind uma imagem com hello CLI do Azure, consulte [Navegando e selecionando imagens de máquina virtual do Azure com o PowerShell e Olá CLI do Azure](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e187-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9e187-152">Porém, para este artigo, aqui está uma pequena lista de imagens populares.</span><span class="sxs-lookup"><span data-stu-id="9e187-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="9e187-153">Vamos usar a imagem estável do CoreOS para esta criação rápida.</span><span class="sxs-lookup"><span data-stu-id="9e187-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="9e187-154">Para ComputeImageVersion, você pode simplesmente fornecer 'último' como Olá parâmetro em ambas as linguagem de modelo Olá em Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e187-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="9e187-155">Isso permitirá que você tooalways usar hello mais recente e corrigida versão da imagem de saudação sem ter que toomodify seus scripts ou modelos.</span><span class="sxs-lookup"><span data-stu-id="9e187-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="9e187-156">Isso é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9e187-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="9e187-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="9e187-157">PublisherName</span></span> | <span data-ttu-id="9e187-158">Oferta</span><span class="sxs-lookup"><span data-stu-id="9e187-158">Offer</span></span> | <span data-ttu-id="9e187-159">Sku</span><span class="sxs-lookup"><span data-stu-id="9e187-159">Sku</span></span> | <span data-ttu-id="9e187-160">Versão</span><span class="sxs-lookup"><span data-stu-id="9e187-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9e187-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9e187-161">OpenLogic</span></span> |<span data-ttu-id="9e187-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="9e187-162">CentOS</span></span> |<span data-ttu-id="9e187-163">7</span><span class="sxs-lookup"><span data-stu-id="9e187-163">7</span></span> |<span data-ttu-id="9e187-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="9e187-164">7.0.201503</span></span> |
| <span data-ttu-id="9e187-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9e187-165">OpenLogic</span></span> |<span data-ttu-id="9e187-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="9e187-166">CentOS</span></span> |<span data-ttu-id="9e187-167">7.1</span><span class="sxs-lookup"><span data-stu-id="9e187-167">7.1</span></span> |<span data-ttu-id="9e187-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="9e187-168">7.1.201504</span></span> |
| <span data-ttu-id="9e187-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9e187-169">CoreOS</span></span> |<span data-ttu-id="9e187-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9e187-170">CoreOS</span></span> |<span data-ttu-id="9e187-171">Beta</span><span class="sxs-lookup"><span data-stu-id="9e187-171">Beta</span></span> |<span data-ttu-id="9e187-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="9e187-172">647.0.0</span></span> |
| <span data-ttu-id="9e187-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9e187-173">CoreOS</span></span> |<span data-ttu-id="9e187-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9e187-174">CoreOS</span></span> |<span data-ttu-id="9e187-175">Estável</span><span class="sxs-lookup"><span data-stu-id="9e187-175">Stable</span></span> |<span data-ttu-id="9e187-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="9e187-176">633.1.0</span></span> |
| <span data-ttu-id="9e187-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="9e187-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="9e187-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="9e187-178">DynamicsNAV</span></span> |<span data-ttu-id="9e187-179">2015</span><span class="sxs-lookup"><span data-stu-id="9e187-179">2015</span></span> |<span data-ttu-id="9e187-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="9e187-180">8.0.40459</span></span> |
| <span data-ttu-id="9e187-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="9e187-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="9e187-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="9e187-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="9e187-183">2013</span><span class="sxs-lookup"><span data-stu-id="9e187-183">2013</span></span> |<span data-ttu-id="9e187-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9e187-184">1.0.0</span></span> |
| <span data-ttu-id="9e187-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="9e187-185">msopentech</span></span> |<span data-ttu-id="9e187-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="9e187-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="9e187-187">Standard</span><span class="sxs-lookup"><span data-stu-id="9e187-187">Standard</span></span> |<span data-ttu-id="9e187-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9e187-188">1.0.0</span></span> |
| <span data-ttu-id="9e187-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="9e187-189">msopentech</span></span> |<span data-ttu-id="9e187-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="9e187-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="9e187-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="9e187-191">Enterprise</span></span> |<span data-ttu-id="9e187-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9e187-192">1.0.0</span></span> |
| <span data-ttu-id="9e187-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="9e187-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="9e187-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="9e187-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="9e187-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="9e187-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="9e187-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="9e187-196">12.0.2430</span></span> |
| <span data-ttu-id="9e187-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="9e187-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="9e187-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="9e187-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="9e187-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="9e187-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="9e187-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="9e187-200">12.0.2430</span></span> |
| <span data-ttu-id="9e187-201">Canônico</span><span class="sxs-lookup"><span data-stu-id="9e187-201">Canonical</span></span> |<span data-ttu-id="9e187-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9e187-202">UbuntuServer</span></span> |<span data-ttu-id="9e187-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="9e187-203">12.04.5-LTS</span></span> |<span data-ttu-id="9e187-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="9e187-204">12.04.201504230</span></span> |
| <span data-ttu-id="9e187-205">Canônico</span><span class="sxs-lookup"><span data-stu-id="9e187-205">Canonical</span></span> |<span data-ttu-id="9e187-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9e187-206">UbuntuServer</span></span> |<span data-ttu-id="9e187-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="9e187-207">14.04.2-LTS</span></span> |<span data-ttu-id="9e187-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="9e187-208">14.04.201503090</span></span> |
| <span data-ttu-id="9e187-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9e187-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9e187-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9e187-210">WindowsServer</span></span> |<span data-ttu-id="9e187-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9e187-211">2012-Datacenter</span></span> |<span data-ttu-id="9e187-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="9e187-212">3.0.201503</span></span> |
| <span data-ttu-id="9e187-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9e187-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9e187-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9e187-214">WindowsServer</span></span> |<span data-ttu-id="9e187-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9e187-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="9e187-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="9e187-216">4.0.201503</span></span> |
| <span data-ttu-id="9e187-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9e187-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9e187-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9e187-218">WindowsServer</span></span> |<span data-ttu-id="9e187-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="9e187-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="9e187-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="9e187-220">5.0.201504</span></span> |
| <span data-ttu-id="9e187-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9e187-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="9e187-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9e187-222">WindowsServerEssentials</span></span> |<span data-ttu-id="9e187-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9e187-223">WindowsServerEssentials</span></span> |<span data-ttu-id="9e187-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="9e187-224">1.0.141204</span></span> |
| <span data-ttu-id="9e187-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="9e187-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="9e187-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="9e187-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="9e187-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="9e187-227">2012R2</span></span> |<span data-ttu-id="9e187-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="9e187-228">4.3.4665</span></span> |

<span data-ttu-id="9e187-229">Crie sua VM inserindo Olá `azure vm quick-create` comando e a se preparar para Olá prompts.</span><span class="sxs-lookup"><span data-stu-id="9e187-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="9e187-230">O resultado deve ser semelhante a esse:</span><span class="sxs-lookup"><span data-stu-id="9e187-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="9e187-231">E, assim, você obtém sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="9e187-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="9e187-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Tarefa: implantar uma VM no Azure a partir de um modelo</span><span class="sxs-lookup"><span data-stu-id="9e187-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="9e187-233">Use as instruções de saudação toodeploy essas seções uma nova VM do Azure usando um modelo com hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e187-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="9e187-234">Este modelo cria uma única máquina virtual em uma nova rede virtual com uma única sub-rede e, diferentemente do `azure vm quick-create`, permite que você toodescribe o que você deseja com precisão e repeti-la sem erros.</span><span class="sxs-lookup"><span data-stu-id="9e187-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="9e187-235">Aqui está o que o modelo cria:</span><span class="sxs-lookup"><span data-stu-id="9e187-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="9e187-236">Etapa 1: Examine o arquivo JSON de Olá Olá para parâmetros de modelo</span><span class="sxs-lookup"><span data-stu-id="9e187-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="9e187-237">Aqui estão Olá conteúdo do hello JSON arquivo de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e187-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="9e187-238">(modelo de saudação também está localizado em [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="9e187-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="9e187-239">Modelos são flexíveis, para que designer Olá tenha escolhido toogive muita parâmetros ou escolhido toooffer apenas alguns ao criar um modelo que mais é fixo.</span><span class="sxs-lookup"><span data-stu-id="9e187-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="9e187-240">Em informações de pedidos toocollect Olá é necessário o modelo de saudação toopass como parâmetros, abrir o arquivo de modelo de saudação (Este tópico tem um modelo embutido, abaixo) e examine Olá **parâmetros** valores.</span><span class="sxs-lookup"><span data-stu-id="9e187-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="9e187-241">Nesse caso, o modelo de saudação abaixo pedirá para:</span><span class="sxs-lookup"><span data-stu-id="9e187-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="9e187-242">Um nome de conta de armazenamento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9e187-242">A unique storage account name.</span></span>
* <span data-ttu-id="9e187-243">Um nome de usuário de administrador para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9e187-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="9e187-244">Uma senha.</span><span class="sxs-lookup"><span data-stu-id="9e187-244">A password.</span></span>
* <span data-ttu-id="9e187-245">Um nome de domínio para Olá fora toouse do mundo.</span><span class="sxs-lookup"><span data-stu-id="9e187-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="9e187-246">Um número de versão do Servidor do Ubuntu, mas apenas um de uma lista será aceito.</span><span class="sxs-lookup"><span data-stu-id="9e187-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="9e187-247">Veja mais sobre os [requisitos de nome de usuário e senha](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="9e187-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="9e187-248">Depois que você decidir sobre esses valores, você está pronto toocreate um grupo e implanta este modelo em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e187-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="9e187-249">Etapa 2: Criar a máquina virtual de saudação usando o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="9e187-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="9e187-250">Uma vez que os valores de parâmetro prontos, você deve criar um grupo de recursos para sua implantação de modelo e, em seguida, implante o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e187-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="9e187-251">grupo de recursos toocreate hello, tipo `azure group create <group name> <location>` com o nome de saudação do grupo de saudação desejado e localização do datacenter Olá no qual você deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9e187-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="9e187-252">Isso acontece rapidamente:</span><span class="sxs-lookup"><span data-stu-id="9e187-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9e187-253">Implantação de saudação toocreate agora, chamada `azure group deployment create` e passar:</span><span class="sxs-lookup"><span data-stu-id="9e187-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="9e187-254">arquivo de modelo de saudação (se você salvou Olá acima arquivo local do JSON modelo tooa).</span><span class="sxs-lookup"><span data-stu-id="9e187-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="9e187-255">Um modelo de URI (se você deseja toopoint no arquivo hello no GitHub ou algum outro endereço da web).</span><span class="sxs-lookup"><span data-stu-id="9e187-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="9e187-256">grupo de recursos Olá no qual você deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9e187-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="9e187-257">E um nome de implantação opcional.</span><span class="sxs-lookup"><span data-stu-id="9e187-257">An optional deployment name.</span></span>

<span data-ttu-id="9e187-258">Será solicitada toosupply Olá valores de parâmetros na seção "parâmetros" hello arquivo JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e187-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="9e187-259">Quando você tiver especificado a todos os valores de parâmetro hello, sua implantação começará.</span><span class="sxs-lookup"><span data-stu-id="9e187-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="9e187-260">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="9e187-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="9e187-261">Olá, tipo de informações a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="9e187-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="9e187-262"><a id="create-a-custom-vm-image"></a>Tarefa: Criar uma imagem de VM personalizada</span><span class="sxs-lookup"><span data-stu-id="9e187-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="9e187-263">Você viu o uso básico de saudação de modelos acima, portanto, agora podemos usar toocreate semelhante de instruções uma VM personalizada de um arquivo. vhd específico no Azure usando um modelo por meio de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e187-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="9e187-264">diferença de saudação aqui é que este modelo cria uma única máquina virtual de um disco rígido virtual (VHD) especificado.</span><span class="sxs-lookup"><span data-stu-id="9e187-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="9e187-265">Etapa 1: Examine Olá JSON no arquivo de modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="9e187-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="9e187-266">Aqui estão Olá conteúdo do hello JSON arquivo de modelo de saudação que esta seção usa como exemplo.</span><span class="sxs-lookup"><span data-stu-id="9e187-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="9e187-267">(modelo de saudação também está localizado em [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="9e187-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="9e187-268">Novamente, você precisará de valores de saudação toofind você deseja tooenter para parâmetros de saudação que não têm valores padrão.</span><span class="sxs-lookup"><span data-stu-id="9e187-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="9e187-269">Quando você executa Olá `azure group deployment create` comando, Olá CLI do Azure solicitará que você tooenter esses valores.</span><span class="sxs-lookup"><span data-stu-id="9e187-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="9e187-270">Etapa 2: Obter Olá VHD</span><span class="sxs-lookup"><span data-stu-id="9e187-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="9e187-271">Obviamente, você precisará de um .vhd para isso.</span><span class="sxs-lookup"><span data-stu-id="9e187-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="9e187-272">Você pode usar um que já tenha no Azure ou pode carregar um.</span><span class="sxs-lookup"><span data-stu-id="9e187-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="9e187-273">Para uma máquina virtual com base em Windows, consulte [criar e carregar um VHD do Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e187-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="9e187-274">Para uma máquina virtual com base em Linux, consulte [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e187-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="9e187-275">Etapa 3: Criar a máquina virtual de saudação usando o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="9e187-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="9e187-276">Agora você está pronto toocreate uma nova máquina virtual com base em. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e187-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="9e187-277">Criar um toodeploy de grupo, usando `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="9e187-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9e187-278">Criar implantação hello usando Olá `--template-uri` toocall opção no modelo de saudação diretamente (ou você pode usar o hello `--template-file` opção toouse um arquivo que você salvou localmente).</span><span class="sxs-lookup"><span data-stu-id="9e187-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="9e187-279">Observe que, como modelo Olá tem padrões especificados, você será solicitado para apenas algumas coisas.</span><span class="sxs-lookup"><span data-stu-id="9e187-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="9e187-280">Se você implantar o modelo de saudação em locais diferentes, você pode achar que alguns colisões de nomenclatura ocorrerem com valores padrão de saudação (particularmente Olá nome DNS criar).</span><span class="sxs-lookup"><span data-stu-id="9e187-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="9e187-281">Saída parecida com hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e187-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="9e187-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Tarefa: implantar um aplicativo com várias VMs que usa uma rede virtual e um balanceador externo de carga</span><span class="sxs-lookup"><span data-stu-id="9e187-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="9e187-283">Este modelo permite que você toocreate duas máquinas virtuais em um balanceador de carga e configurar uma regra de balanceamento de carga na porta 80.</span><span class="sxs-lookup"><span data-stu-id="9e187-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="9e187-284">Esse modelo também implanta uma Conta de Armazenamento, Rede Virtual, Endereço IP Público, Conjunto de Disponibilidade e Interfaces de Rede.</span><span class="sxs-lookup"><span data-stu-id="9e187-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="9e187-285">Siga essas etapas toodeploy um aplicativo de várias VMs que usa uma rede virtual e um balanceador de carga usando um modelo de Gerenciador de recursos no repositório de modelos do GitHub Olá através de comandos do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e187-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="9e187-286">Etapa 1: Examine Olá JSON no arquivo de modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="9e187-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="9e187-287">Aqui estão Olá conteúdo do hello JSON arquivo de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e187-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="9e187-288">Se desejar que a versão mais recente do hello, ele localizou [no repositório do GitHub Olá para modelos de](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9e187-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="9e187-289">Este tópico usa Olá `--template-uri` toocall de comutador no modelo hello, mas você também pode usar o hello `--template-file` alternar toopass uma versão local.</span><span class="sxs-lookup"><span data-stu-id="9e187-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="9e187-290">Etapa 2: Criar a implantação de saudação usando o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="9e187-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="9e187-291">Criar um grupo de recursos para o modelo de saudação usando `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="9e187-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="9e187-292">Em seguida, crie uma implantação para esse grupo de recursos usando `azure group deployment create` e passando o grupo de recursos hello, passando um nome de implantação e responder a prompts Olá para parâmetros de modelo de saudação que não possuem valores padrão.</span><span class="sxs-lookup"><span data-stu-id="9e187-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="9e187-293">Agora use Olá `azure group deployment create` comando e hello `--template-uri` modelo de saudação toodeploy opção.</span><span class="sxs-lookup"><span data-stu-id="9e187-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="9e187-294">Esteja pronto para fornecer os valores de parâmetros quando eles forem solicitados, conforme mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e187-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="9e187-295">Observe que esse modelo implanta uma imagem do Windows Server. No entanto, ela poderia ser facilmente substituída por qualquer imagem do Linux.</span><span class="sxs-lookup"><span data-stu-id="9e187-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="9e187-296">Deseja toocreate um cluster do Docker com vários gerenciadores de por nuvem?</span><span class="sxs-lookup"><span data-stu-id="9e187-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="9e187-297">[Você consegue](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="9e187-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="9e187-298"><a id="remove-a-resource-group"></a>Tarefa: Remover um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e187-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="9e187-299">Lembre-se de que você pode reutilizar o grupo de recursos de tooa, mas se você tiver terminado com um, você poderá excluí-la usando `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="9e187-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="9e187-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Tarefa: Mostrar log Olá para uma implantação de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e187-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="9e187-301">Essa é uma tarefa comum ao se criar ou usar modelos.</span><span class="sxs-lookup"><span data-stu-id="9e187-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="9e187-302">implantação de Olá Olá chamada toodisplay logs para um grupo é `azure group log show <groupname>`, que exibe uma grande quantidade de informações que são úteis para entender por que algo aconteceu – ou não.</span><span class="sxs-lookup"><span data-stu-id="9e187-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="9e187-303">(Para obter mais informações sobre como solucionar problemas em suas implantações, bem como outras informações sobre problemas, confira [Solução de problemas comuns de implantação do Azure com o Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md)).</span><span class="sxs-lookup"><span data-stu-id="9e187-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="9e187-304">falhas de tootarget específico, por exemplo, você pode usar ferramentas como **jq** tooquery coisas um pouco mais precisamente, como quais falhas individuais, você precisa toocorrect.</span><span class="sxs-lookup"><span data-stu-id="9e187-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="9e187-305">Olá exemplo a seguir usa **jq** tooparse de log para uma implantação **lbgroup**, procura a falhas.</span><span class="sxs-lookup"><span data-stu-id="9e187-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="9e187-306">Você pode descobrir rapidamente qual foi o problema, corrigi-lo e tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="9e187-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="9e187-307">Olá caso a seguir, modelo Olá tinha foi criando duas VMs em Olá mesmo tempo, que é criado um bloqueio em. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e187-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="9e187-308">(Depois que modificamos modelo hello, Olá implantação bem-sucedida rapidamente.)</span><span class="sxs-lookup"><span data-stu-id="9e187-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="9e187-309"><a id="display-information-about-a-virtual-machine"></a>Tarefa: Exibir informações sobre uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9e187-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="9e187-310">Você pode ver informações sobre máquinas virtuais específicas no seu grupo de recursos usando Olá `azure vm show <groupname> <vmname>` comando.</span><span class="sxs-lookup"><span data-stu-id="9e187-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="9e187-311">Se você tiver mais de uma máquina virtual em seu grupo, talvez seja necessário primeiro Olá toolist VMs em um grupo usando `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="9e187-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="9e187-312">E, em seguida, procurar por myVM1:</span><span class="sxs-lookup"><span data-stu-id="9e187-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="9e187-313">Se você quiser tooprogrammatically repositório e manipular a saída de hello dos seus comandos de console, convém toouse uma análise JSON ferramenta como  **[jq](https://github.com/stedolan/jq)**  ou  **[jsawk](https://github.com/micha/jsawk)** , ou bibliotecas de idioma que são bons para tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e187-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="9e187-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Tarefa: Faça logon na máquina virtual baseados em Linux de tooa</span><span class="sxs-lookup"><span data-stu-id="9e187-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="9e187-315">Normalmente máquinas Linux são conectado toothrough SSH.</span><span class="sxs-lookup"><span data-stu-id="9e187-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="9e187-316">Para obter mais informações, consulte [como toouse SSH com Linux no Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e187-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="9e187-317"><a id="stop-a-virtual-machine"></a>Tarefa: Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="9e187-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="9e187-318">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9e187-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="9e187-319">Use este parâmetro tookeep Olá IP virtual (VIP) de rede virtual de saudação caso ela seja Olá última VM nessa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9e187-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="9e187-320">Se você usar o hello `StayProvisioned` parâmetro, você ainda será cobrado por Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9e187-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="9e187-321"><a id="start-a-virtual-machine"></a>Tarefa: iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="9e187-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="9e187-322">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9e187-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="9e187-323"><a id="attach-a-data-disk"></a>Tarefa: Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="9e187-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="9e187-324">Você também precisará toodecide se tooattach um novo disco ou uma que contém dados.</span><span class="sxs-lookup"><span data-stu-id="9e187-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="9e187-325">Para um novo disco, o comando de saudação cria o arquivo. vhd de saudação e anexa-o no hello mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="9e187-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="9e187-326">tooattach um novo disco, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9e187-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="9e187-327">tooattach um disco de dados existente, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="9e187-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="9e187-328">Em seguida, você precisará toomount disco de Olá, como faria normalmente no Linux.</span><span class="sxs-lookup"><span data-stu-id="9e187-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e187-329">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e187-329">Next steps</span></span>
<span data-ttu-id="9e187-330">Para obter mais exemplos de uso da CLI do Azure com hello **arm** modo, consulte [hello usando a CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9e187-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="9e187-331">toolearn mais sobre os recursos do Azure e seus conceitos, consulte [visão geral do Gerenciador de recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e187-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="9e187-332">Para obter mais modelos que você pode usar, confira [Modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) e [Estruturas de aplicativos usando modelos](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e187-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
