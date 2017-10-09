Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

toosee Olá locais disponíveis, executados Olá `az appservice list-locations` comando. Geralmente, você cria recursos em uma região perto de você.
