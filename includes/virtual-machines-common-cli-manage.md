<span data-ttu-id="67690-101">Olá 2.0 do CLI do Azure permite que você toocreate e gerenciar seus recursos do Azure no Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="67690-101">hello Azure CLI 2.0 allows you toocreate and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="67690-102">Este artigo detalha algumas Olá toocreate de comandos mais comuns e gerenciar máquinas virtuais (VMs).</span><span class="sxs-lookup"><span data-stu-id="67690-102">This article details some of hello most common commands toocreate and manage virtual machines (VMs).</span></span>

<span data-ttu-id="67690-103">Este artigo requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="67690-103">This article requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="67690-104">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="67690-104">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="67690-105">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="67690-105">If you need tooupgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="67690-106">Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="67690-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="67690-107">Comandos básicos do Azure Resource Manager na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="67690-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="67690-108">Para obter mais ajuda com as opções e opções de linha de comando específico, você pode usar ajuda de comando online hello e opções digitando `az <command> <subcommand> --help`.</span><span class="sxs-lookup"><span data-stu-id="67690-108">For more detailed help with specific command line switches and options, you can use hello online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="67690-109">Criar VMs</span><span class="sxs-lookup"><span data-stu-id="67690-109">Create VMs</span></span>
| <span data-ttu-id="67690-110">Tarefa</span><span class="sxs-lookup"><span data-stu-id="67690-110">Task</span></span> | <span data-ttu-id="67690-111">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="67690-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="67690-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="67690-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="67690-113">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="67690-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="67690-114">Criar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="67690-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="67690-115">Gerenciar o estado da VM</span><span class="sxs-lookup"><span data-stu-id="67690-115">Manage VM state</span></span>
| <span data-ttu-id="67690-116">Tarefa</span><span class="sxs-lookup"><span data-stu-id="67690-116">Task</span></span> | <span data-ttu-id="67690-117">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="67690-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="67690-118">Iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="67690-119">Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="67690-120">Desalocar uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="67690-121">Reiniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="67690-122">Reimplantar uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="67690-123">Excluir uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="67690-124">Obter informações sobre a VM</span><span class="sxs-lookup"><span data-stu-id="67690-124">Get VM info</span></span>
| <span data-ttu-id="67690-125">Tarefa</span><span class="sxs-lookup"><span data-stu-id="67690-125">Task</span></span> | <span data-ttu-id="67690-126">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="67690-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="67690-127">Listar VMs</span><span class="sxs-lookup"><span data-stu-id="67690-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="67690-128">Obter informações sobre uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="67690-129">Conferir o uso dos recursos de VM</span><span class="sxs-lookup"><span data-stu-id="67690-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="67690-130">Conferir todos os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="67690-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="67690-131">Discos e imagens</span><span class="sxs-lookup"><span data-stu-id="67690-131">Disks and images</span></span>
| <span data-ttu-id="67690-132">Tarefa</span><span class="sxs-lookup"><span data-stu-id="67690-132">Task</span></span> | <span data-ttu-id="67690-133">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="67690-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="67690-134">Adicionar um disco de dados tooa VM</span><span class="sxs-lookup"><span data-stu-id="67690-134">Add a data disk tooa VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="67690-135">Remover um disco de dados de uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="67690-136">Redimensionar um disco</span><span class="sxs-lookup"><span data-stu-id="67690-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="67690-137">Instantâneo de um disco</span><span class="sxs-lookup"><span data-stu-id="67690-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="67690-138">Criar imagem de uma VM</span><span class="sxs-lookup"><span data-stu-id="67690-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="67690-139">Criar uma VM com base em uma imagem</span><span class="sxs-lookup"><span data-stu-id="67690-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="67690-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67690-140">Next steps</span></span>
<span data-ttu-id="67690-141">Para obter exemplos adicionais de comandos CLI hello, consulte Olá [criar e gerenciar máquinas virtuais Linux com hello CLI do Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="67690-141">For additional examples of hello CLI commands, see hello [Create and Manage Linux VMs with hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

