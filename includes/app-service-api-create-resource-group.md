<span data-ttu-id="91d1d-101">Crie um grupo de recursos com o comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="91d1d-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="91d1d-102">O seguinte exemplo cria um grupo de recursos chamado *myResourceGroup* no local *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="91d1d-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="91d1d-103">Para ver os locais disponíveis, execute o comando `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="91d1d-103">To see the available locations, run the `az appservice list-locations` command.</span></span> <span data-ttu-id="91d1d-104">Geralmente, você cria recursos em uma região perto de você.</span><span class="sxs-lookup"><span data-stu-id="91d1d-104">You generally create resources in a region near you.</span></span>
