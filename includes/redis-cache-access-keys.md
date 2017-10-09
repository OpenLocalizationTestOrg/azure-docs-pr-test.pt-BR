instância de Cache Redis do Azure de tooan tooconnect, os clientes de cache necessário Olá host, portas e chaves de cache de saudação. Alguns clientes podem se referir a itens de toothese por nomes um pouco diferentes. Você pode recuperar essas informações no hello portal do Azure ou usando ferramentas de linha de comando como CLI do Azure.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Recuperar o nome de host, portas e chaves de acesso usando Olá Portal do Azure
tooretrieve host nome, portas e chaves de acesso usando Olá Portal do Azure, [procurar](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache Olá [portal do Azure](https://portal.azure.com) e clique em **chaves de acesso** e  **Propriedades** em Olá **menu recursos**. 

![Configurações de Cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Recuperar o nome de host, portas e chaves de acesso usando a CLI do Azure
nome de host tooretrieve hello e portas usando o Azure 2.0 do CLI que você pode chamar [Mostrar do redis az](https://docs.microsoft.com/cli/azure/redis#show)e as chaves de saudação tooretrieve você pode chamar [az redis lista chaves](https://docs.microsoft.com/cli/azure/redis#list-keys). Olá, script a seguir chama esses dois comandos e ecos Olá nome de host, portas e console de toohello de chaves.

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

Para obter mais informações sobre esse script, consulte [obter Olá nome de host, portas e chaves de Cache Redis do Azure](../articles/redis-cache/scripts/cache-keys-ports.md). Para obter mais informações sobre a CLI do Azure 2.0, consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) e [Começar com a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).
