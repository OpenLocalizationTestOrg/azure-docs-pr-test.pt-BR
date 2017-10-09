---
title: 'CLI do Azure: Criar um banco de dados SQL | Microsoft Docs'
description: "Saiba como toocreate um servidor lógico do banco de dados SQL, a regra de firewall de nível de servidor e bancos de dados usando Olá CLI do Azure."
keywords: tutorial do banco de dados SQL, criar um banco de dados SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Criar um único banco de dados SQL do Azure usando Olá CLI do Azure

Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts. Este guia de detalhes usando Olá CLI do Azure toodeploy um banco de dados do SQL Azure em uma [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) em uma [servidor lógico do banco de dados SQL](sql-database-features.md).

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Definir variáveis

Defina variáveis para uso em scripts Olá esse início rápido.

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando Olá [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo. Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` local.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Criar um servidor lógico

Criar um [servidor lógico do banco de dados do Azure SQL](sql-database-features.md) usando Olá [az sql server criar](/cli/azure/sql/server#create) comando. Um servidor lógico contém um grupo de bancos de dados gerenciados conjuntamente. Olá exemplo a seguir cria um servidor nomeado aleatoriamente em seu grupo de recursos com um logon de administrador denominado `ServerAdmin` e uma senha de `ChangeYourAdminPassword1`. Substitua esses valores predefinidos como desejado.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Configurar uma regra de firewall de servidor

Criar um [regra de firewall de nível de servidor de banco de dados do Azure SQL](sql-database-firewall-configure.md) usando Olá [firewall do servidor sql az criar](/cli/azure/sql/server/firewall-rule#create) comando. Uma regra de firewall de nível de servidor permite que um aplicativo externo, como SQL Server Management Studio ou hello SQLCMD utilitário tooconnect tooa banco de dados SQL por meio do firewall do serviço de banco de dados SQL hello. No hello exemplo a seguir, o firewall Olá só é aberto para outros recursos do Azure. conectividade externa tooenable, change Olá IP endereço tooan apropriado para seu ambiente. tooopen todos os endereços IP, use 0.0.0.0 como Olá Iniciando endereço IP e 255.255.255.255 como Olá endereço final.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> O Banco de Dados SQL se comunica pela porta 1433. Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 1433 talvez não consigam pelo firewall da rede. Nesse caso, não será tooconnect capaz de servidor de banco de dados SQL de tooyour, a menos que o departamento de TI abre a porta 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Criar um banco de dados no servidor de saudação com dados de exemplo

Criar um banco de dados com um [nível de desempenho S0](sql-database-service-tiers.md) no servidor de saudação usando Olá [criar banco de dados de sql az](/cli/azure/sql/db#create) comando. Olá, exemplo a seguir cria um banco de dados chamado `mySampleDatabase` e carrega Olá dados de exemplo AdventureWorksLT para este banco de dados. Substituir essas predefinidos valores conforme desejado (outros inícios rápidos nesta compilação da coleção após valores hello esse início rápido).

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Limpar recursos

Outros inícios rápidos nessa coleção aproveitam esse início rápido. 

> [!TIP]
> Se você planeja toocontinue toowork com inícios rápidos subsequentes, não limpar os recursos de saudação criados nesse rápido inicie. Se você não planeja toocontinue, use Olá seguindo as etapas toodelete todos os recursos criados por esse início rápido no portal do Azure de saudação.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um banco de dados, você pode se conectar e consultar usando suas ferramentas favoritas. Saiba mais escolhendo sua ferramenta abaixo:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

