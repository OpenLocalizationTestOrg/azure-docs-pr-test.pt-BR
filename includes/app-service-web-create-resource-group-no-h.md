Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.

[!INCLUDE [resource group intro text](resource-group.md)]

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Você geralmente criar o recurso hello e grupo de recursos em uma região de perto de você. locais de todos os toosee com suporte para aplicativos da Web do Azure, execute Olá `az appservice list-locations` comando. 
