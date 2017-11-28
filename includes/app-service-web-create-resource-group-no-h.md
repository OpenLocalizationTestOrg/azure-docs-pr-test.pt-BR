<span data-ttu-id="d1979-101">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="d1979-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="d1979-102">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.</span><span class="sxs-lookup"><span data-stu-id="d1979-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="d1979-103">Você geralmente criar o recurso hello e grupo de recursos em uma região de perto de você.</span><span class="sxs-lookup"><span data-stu-id="d1979-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="d1979-104">locais de todos os toosee com suporte para aplicativos da Web do Azure, execute Olá `az appservice list-locations` comando.</span><span class="sxs-lookup"><span data-stu-id="d1979-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
