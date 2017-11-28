<span data-ttu-id="06d22-101">A CLI do Azure 2.0 permite criar e gerenciar os recursos do Azure no Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="06d22-101">The Azure CLI 2.0 allows you to create and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="06d22-102">Este artigo detalha alguns dos comandos mais comuns para criar e gerenciar máquinas virtuais (VMs).</span><span class="sxs-lookup"><span data-stu-id="06d22-102">This article details some of the most common commands to create and manage virtual machines (VMs).</span></span>

<span data-ttu-id="06d22-103">Este tutorial requer a CLI do Azure, versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="06d22-103">This article requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="06d22-104">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="06d22-104">Run `az --version` to find the version.</span></span> <span data-ttu-id="06d22-105">Se você precisar atualizar, confira [Instalar a CLI 2.0 do Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="06d22-105">If you need to upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="06d22-106">Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="06d22-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="06d22-107">Comandos básicos do Azure Resource Manager na CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06d22-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="06d22-108">Para obter ajuda mais detalhada com opções específicas de linha de comando, você pode usar as opções e a ajuda online sobre os comandos digitando `az <command> <subcommand> --help`.</span><span class="sxs-lookup"><span data-stu-id="06d22-108">For more detailed help with specific command line switches and options, you can use the online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="06d22-109">Criar VMs</span><span class="sxs-lookup"><span data-stu-id="06d22-109">Create VMs</span></span>
| <span data-ttu-id="06d22-110">Tarefa</span><span class="sxs-lookup"><span data-stu-id="06d22-110">Task</span></span> | <span data-ttu-id="06d22-111">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06d22-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="06d22-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="06d22-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="06d22-113">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="06d22-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="06d22-114">Criar uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="06d22-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="06d22-115">Gerenciar o estado da VM</span><span class="sxs-lookup"><span data-stu-id="06d22-115">Manage VM state</span></span>
| <span data-ttu-id="06d22-116">Tarefa</span><span class="sxs-lookup"><span data-stu-id="06d22-116">Task</span></span> | <span data-ttu-id="06d22-117">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06d22-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="06d22-118">Iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="06d22-119">Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="06d22-120">Desalocar uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="06d22-121">Reiniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="06d22-122">Reimplantar uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="06d22-123">Excluir uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="06d22-124">Obter informações sobre a VM</span><span class="sxs-lookup"><span data-stu-id="06d22-124">Get VM info</span></span>
| <span data-ttu-id="06d22-125">Tarefa</span><span class="sxs-lookup"><span data-stu-id="06d22-125">Task</span></span> | <span data-ttu-id="06d22-126">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06d22-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="06d22-127">Listar VMs</span><span class="sxs-lookup"><span data-stu-id="06d22-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="06d22-128">Obter informações sobre uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="06d22-129">Conferir o uso dos recursos de VM</span><span class="sxs-lookup"><span data-stu-id="06d22-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="06d22-130">Conferir todos os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="06d22-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="06d22-131">Discos e imagens</span><span class="sxs-lookup"><span data-stu-id="06d22-131">Disks and images</span></span>
| <span data-ttu-id="06d22-132">Tarefa</span><span class="sxs-lookup"><span data-stu-id="06d22-132">Task</span></span> | <span data-ttu-id="06d22-133">Comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06d22-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="06d22-134">Adicionar um disco de dados a uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-134">Add a data disk to a VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="06d22-135">Remover um disco de dados de uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="06d22-136">Redimensionar um disco</span><span class="sxs-lookup"><span data-stu-id="06d22-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="06d22-137">Instantâneo de um disco</span><span class="sxs-lookup"><span data-stu-id="06d22-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="06d22-138">Criar imagem de uma VM</span><span class="sxs-lookup"><span data-stu-id="06d22-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="06d22-139">Criar uma VM com base em uma imagem</span><span class="sxs-lookup"><span data-stu-id="06d22-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="06d22-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06d22-140">Next steps</span></span>
<span data-ttu-id="06d22-141">Para obter exemplos adicionais dos comandos da CLI, consulte o tutorial [Criar e gerenciar VMs do Linux com a CLI do Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="06d22-141">For additional examples of the CLI commands, see the [Create and Manage Linux VMs with the Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

