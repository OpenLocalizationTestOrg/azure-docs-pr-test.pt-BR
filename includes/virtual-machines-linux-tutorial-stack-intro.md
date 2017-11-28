## <a name="create-a-resource-group"></a><span data-ttu-id="5a7b9-101">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5a7b9-101">Create a resource group</span></span>

<span data-ttu-id="5a7b9-102">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5a7b9-102">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5a7b9-103">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5a7b9-104">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *eastus*.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="5a7b9-105">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5a7b9-105">Create a virtual machine</span></span>

<span data-ttu-id="5a7b9-106">Crie uma VM com o comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5a7b9-106">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="5a7b9-107">O exemplo a seguir cria uma VM denominada *myVM* e cria chaves SSH, se elas ainda não existirem em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="5a7b9-108">Para usar um conjunto específico de chaves, use a opção `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="5a7b9-109">Quando a VM tiver sido criada, a CLI do Azure mostra informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-109">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="5a7b9-110">Anote `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-110">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="5a7b9-111">Esse endereço é usado para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-111">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="5a7b9-112">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="5a7b9-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="5a7b9-113">Por padrão, somente as conexões de SSH têm permissão em VMs Linux implantadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="5a7b9-114">Como essa VM será um servidor Web, você precisa abrir a porta 80 na Internet.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-114">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="5a7b9-115">Use o comando [az vm open-port](/cli/azure/vm#open-port) para abrir a porta desejada.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-115">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="5a7b9-116">SSH em sua VM</span><span class="sxs-lookup"><span data-stu-id="5a7b9-116">SSH into your VM</span></span>


<span data-ttu-id="5a7b9-117">Se você ainda não souber o endereço IP público de sua VM, execute o comando [az network public-ip list](/cli/azure/network/public-ip#list):</span><span class="sxs-lookup"><span data-stu-id="5a7b9-117">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="5a7b9-118">Use o seguinte comando para criar uma sessão SSH com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-118">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="5a7b9-119">Substitua o endereço IP público correto de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-119">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="5a7b9-120">Neste exemplo, o endereço IP é *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="5a7b9-120">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

