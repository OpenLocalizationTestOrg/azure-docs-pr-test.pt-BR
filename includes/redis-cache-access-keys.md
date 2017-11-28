<span data-ttu-id="2be39-101">Para se conectar a uma instância de Cache Redis do Azure, os clientes de cache precisam do nome de host, das portas e das chaves do cache.</span><span class="sxs-lookup"><span data-stu-id="2be39-101">To connect to an Azure Redis Cache instance, cache clients need the host name, ports, and keys of the cache.</span></span> <span data-ttu-id="2be39-102">Alguns clientes podem se referir a esses itens por nomes um pouco diferentes.</span><span class="sxs-lookup"><span data-stu-id="2be39-102">Some clients may refer to these items by slightly different names.</span></span> <span data-ttu-id="2be39-103">Você pode recuperar essas informações no portal do Azure ou usando as ferramentas da linha de comando, como a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2be39-103">You can retrieve this information in the Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-the-azure-portal"></a><span data-ttu-id="2be39-104">Recuperar o nome de host, portas e chaves de acesso usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2be39-104">Retrieve host name, ports, and access keys using the Azure Portal</span></span>
<span data-ttu-id="2be39-105">Para recuperar o nome de host, portas e acesso chaves usando o Portal do Azure, [navegue](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) até o cache no [portal do Azure](https://portal.azure.com) e clique em **Chaves de acesso** e **Propriedades** no **menu Recurso**.</span><span class="sxs-lookup"><span data-stu-id="2be39-105">To retrieve host name, ports, and access keys using the Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) to your cache in the [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in the **Resource menu**.</span></span> 

![Configurações de Cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="2be39-107">Recuperar o nome de host, portas e chaves de acesso usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2be39-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="2be39-108">Para recuperar o nome de host e as portas usando a CLI do Azure 2.0, você pode chamar [az redis show](https://docs.microsoft.com/cli/azure/redis#show) e para recuperar as chaves, pode chamar [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="2be39-108">To retrieve the host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and to retrieve the keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="2be39-109">O script a seguir chama esses dois comandos e repete o nome de host, portas e chaves no console.</span><span class="sxs-lookup"><span data-stu-id="2be39-109">The following script calls these two commands and echos the hostname, ports, and keys to the console.</span></span>

```azurecli
#/bin/bash

# Retrieve the hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve the hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve the keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display the retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="2be39-110">Para obter mais informações sobre esse script, consulte [Obter o nome de host, portas e chaves para o Cache Redis do Azure](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="2be39-110">For more information about this script, see [Get the hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="2be39-111">Para obter mais informações sobre a CLI do Azure 2.0, consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) e [Começar com a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2be39-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
