<span data-ttu-id="e4b02-101">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e4b02-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="e4b02-102">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.</span><span class="sxs-lookup"><span data-stu-id="e4b02-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="e4b02-103">toosee Olá locais disponíveis, executados Olá `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="e4b02-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="e4b02-104">Geralmente, você cria recursos em uma região perto de você.</span><span class="sxs-lookup"><span data-stu-id="e4b02-104">You generally create resources in a region near you.</span></span>
