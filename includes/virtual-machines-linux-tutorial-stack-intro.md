## <a name="create-a-resource-group"></a><span data-ttu-id="9e906-101">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9e906-101">Create a resource group</span></span>

<span data-ttu-id="9e906-102">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9e906-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9e906-103">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9e906-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="9e906-104">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="9e906-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="9e906-105">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9e906-105">Create a virtual machine</span></span>

<span data-ttu-id="9e906-106">Criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9e906-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="9e906-107">Olá, exemplo a seguir cria uma VM denominada *myVM* e cria as chaves de SSH se eles ainda não existir em um local de chave padrão.</span><span class="sxs-lookup"><span data-stu-id="9e906-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="9e906-108">toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.</span><span class="sxs-lookup"><span data-stu-id="9e906-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="9e906-109">Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e906-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="9e906-110">Anote Olá `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="9e906-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="9e906-111">Esse endereço é usado tooaccess Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9e906-111">This address is used tooaccess hello VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="9e906-112">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="9e906-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="9e906-113">Por padrão, somente as conexões de SSH têm permissão em VMs Linux implantadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="9e906-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="9e906-114">Como essa VM toobe um servidor web, você precisa tooopen porta 80 de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="9e906-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="9e906-115">Saudação de uso [az vm abrir portas](/cli/azure/vm#open-port) saudação do comando tooopen desejado de porta.</span><span class="sxs-lookup"><span data-stu-id="9e906-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="9e906-116">SSH em sua VM</span><span class="sxs-lookup"><span data-stu-id="9e906-116">SSH into your VM</span></span>


<span data-ttu-id="9e906-117">Se você não souber Olá endereço IP público da VM, execute Olá [lista de ip público de rede az](/cli/azure/network/public-ip#list) comando:</span><span class="sxs-lookup"><span data-stu-id="9e906-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="9e906-118">A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e906-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="9e906-119">Substituir saudação correto endereço IP público de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9e906-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="9e906-120">Neste exemplo, o endereço IP de saudação é *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="9e906-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

