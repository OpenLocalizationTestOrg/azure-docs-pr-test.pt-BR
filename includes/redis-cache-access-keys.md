<span data-ttu-id="c3971-101">instância de Cache Redis do Azure de tooan tooconnect, os clientes de cache necessário Olá host, portas e chaves de cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3971-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="c3971-102">Alguns clientes podem se referir a itens de toothese por nomes um pouco diferentes.</span><span class="sxs-lookup"><span data-stu-id="c3971-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="c3971-103">Você pode recuperar essas informações no hello portal do Azure ou usando ferramentas de linha de comando como CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3971-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="c3971-104">Recuperar o nome de host, portas e chaves de acesso usando Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c3971-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="c3971-105">tooretrieve host nome, portas e chaves de acesso usando Olá Portal do Azure, [procurar](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache Olá [portal do Azure](https://portal.azure.com) e clique em **chaves de acesso** e  **Propriedades** em Olá **menu recursos**.</span><span class="sxs-lookup"><span data-stu-id="c3971-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Configurações de Cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="c3971-107">Recuperar o nome de host, portas e chaves de acesso usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c3971-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="c3971-108">nome de host tooretrieve hello e portas usando o Azure 2.0 do CLI que você pode chamar [Mostrar do redis az](https://docs.microsoft.com/cli/azure/redis#show)e as chaves de saudação tooretrieve você pode chamar [az redis lista chaves](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="c3971-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="c3971-109">Olá, script a seguir chama esses dois comandos e ecos Olá nome de host, portas e console de toohello de chaves.</span><span class="sxs-lookup"><span data-stu-id="c3971-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="c3971-110">Para obter mais informações sobre esse script, consulte [obter Olá nome de host, portas e chaves de Cache Redis do Azure](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="c3971-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="c3971-111">Para obter mais informações sobre a CLI do Azure 2.0, consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) e [Começar com a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c3971-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
