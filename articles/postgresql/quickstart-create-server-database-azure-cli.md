---
title: "Criar um banco de dados do Azure para PostgreSQL usando Olá CLI do Azure | Microsoft Docs"
description: "Rápido iniciar toocreate guia e gerenciar banco de dados PostgreSQL servidor usando o Azure CLI (interface de linha de comando)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Criar um banco de dados do Azure para PostgreSQL usando Olá CLI do Azure
Banco de dados do Azure para PostgreSQL é um serviço gerenciado que permite que você toorun, gerenciar e dimensionar os bancos de dados PostgreSQL altamente disponíveis na nuvem hello. Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts. Este guia de início rápido mostra como toocreate um Azure banco de dados PostgreSQL servidor em um [grupo de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) usando Olá CLI do Azure.

Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se você tiver várias assinaturas, escolha assinatura apropriada hello, no qual o recurso de saudação será cobrado. Selecione uma ID da assinatura específica em sua conta usando o comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) usando Olá [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo. Olá, exemplo a seguir cria um grupo de recursos denominado `myresourcegroup` em Olá `westus` local.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Criar um Banco de Dados do Azure para o servidor PostgreSQL

Criar um [banco de dados do Azure para o servidor PostgreSQL](overview.md) usando Olá [az postgres server criar](/cli/azure/postgres/server#create) comando. Um servidor contém um grupo de bancos de dados gerenciados conjuntamente. 

Olá, exemplo a seguir cria um servidor chamado `mypgserver-20170401` em seu grupo de recursos `myresourcegroup` com logon de administrador de servidor `mylogin`. nome de saudação de um servidor mapeia o nome tooDNS e, portanto, é necessário toobe globalmente exclusivo no Azure. Olá substituto `<server_admin_password>` com seu próprio valor.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> Olá administrador logon e senha que você especificar aqui são toolog necessária no servidor de toohello e seus bancos de dados mais tarde nesse início rápido. Lembre-se ou registre essas informações para o uso posterior.

Por padrão, o banco de dados **postgres** é criado em seu servidor. Olá [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) banco de dados é um banco de dados padrão devem ser usados pelos usuários, utilitários e aplicativos de terceiros. 


## <a name="configure-a-server-level-firewall-rule"></a>Configurar uma regra de firewall no nível de servidor

Criar uma regra de firewall de nível de servidor do Azure PostgreSQL com hello [criar regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#create) comando. Uma regra de firewall de nível de servidor permite que um aplicativo externo, como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) ou [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server através do firewall de serviço do Azure PostgreSQL hello. 

Você pode definir uma regra de firewall que abrange um tooconnect IP intervalo toobe capaz de sua rede. Olá exemplo a seguir usa [criar regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#create) toocreate uma regra de firewall `AllowAllIps` para um endereço IP, intervalo. tooopen todos os endereços IP, use 0.0.0.0 como Olá Iniciando endereço IP e 255.255.255.255 como Olá endereço final.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> O servidor PostgreSQL do Azure se comunica pela porta 5432. Ao se conectar de dentro de uma rede corporativa, o tráfego de saída pela porta 5432 talvez não seja permitido pelo firewall de sua rede. Ter seu departamento de TI abrir porta 5432 tooconnect tooyour banco de dados SQL server.

## <a name="get-hello-connection-information"></a>Obter informações de conexão Olá

tooconnect tooyour server, você precisa ter credenciais de acesso e informações de host de tooprovide.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

resultado de saudação está no formato JSON. Anote Olá **administratorLogin** e **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-toopostgresql-database-using-psql"></a>Conecte-se o banco de dados de tooPostgreSQL usando psql

Se o computador cliente tem PostgreSQL instalado, você pode usar uma instância local do [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan PostgreSQL Azure server. Agora vamos usar servidor de Azure PostgreSQL Olá psql utilitário de linha de comando tooconnect toohello.

1. Executar Olá psql comando tooconnect tooan banco de dados PostgreSQL servidor a seguir
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Por exemplo, Olá comando a seguir conecta o banco de dados padrão toohello chamado **postgres** no seu servidor PostgreSQL **mypgserver 20170401.postgres.database.azure.com** usando as credenciais de acesso. Digite hello `<server_admin_password>` você escolheu quando solicitado para a senha.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  Quando estiver conectado toohello server, crie um banco de dados em branco no prompt de saudação.
```sql
CREATE DATABASE mypgsqldb;
```

3.  No prompt de hello, execute Olá após o banco de dados do comando tooswitch conexão toohello recém-criado **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Conecte-se o banco de dados de tooPostgreSQL usando pgAdmin

tooconnect tooAzure PostgreSQL server usando a ferramenta Olá GUI _pgAdmin_
1.  Iniciar Olá _pgAdmin_ aplicativo no computador cliente. Você pode instalar o _pgAdmin_ de http://www.pgadmin.org/.
2.  Escolha **adicionar novo servidor** de saudação **Links rápidos** menu.
3.  Em Olá **criar - servidor** caixa de diálogo **geral** , insira um nome amigável exclusivo para o servidor de saudação. Por exemplo, **Servidor PostgreSQL do Azure**.
 ![ferramenta pgAdmin – criar – servidor](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  Em Olá **criar - servidor** caixa de diálogo, **Conexão** guia:
    - Insira o nome totalmente qualificado do servidor de saudação (por exemplo, **mypgserver 20170401.postgres.database.azure.com**) no hello **nome de Host / endereço** caixa. 
    - Insira a porta 5432 em Olá **porta** caixa. 
    - Digite hello **logon de administrador do servidor (user@mypgserver)** obtido anteriormente neste guia de início rápido e a senha fornecidos quando você criou o servidor de saudação em Olá **Username** e **senha** caixas, respectivamente.
    - Selecione **Modo SSL** como **Requerer**. Por padrão, todos os servidores PostgreSQL do Azure são criados com a imposição de SSL ligada. tooturn desativar impondo SSL, consulte os detalhes em [impondo SSL](./concepts-ssl-connection-security.md).

    ![pgAdmin – Criar – Servidor](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  Clique em **Salvar**.
6.  No painel esquerdo do navegador hello, expanda Olá **grupos de servidores**. Escolha o **Servidor PostgreSQL do Azure**.
7.  Escolha Olá **servidor** conectado a e, em seguida, escolha **bancos de dados** sob ele. 
8.  Clique duas vezes em **bancos de dados** tooCreate um banco de dados.
9.  Escolha um nome de banco de dados **mypgsqldb** e proprietário Olá para ela como logon de administrador do servidor **mylogin**.
10. Clique em **salvar** toocreate um banco de dados em branco.
11. Em Olá **navegador**, expanda Olá **servidores** grupo. Expanda servidor Olá que você criou e consulte banco de dados de saudação **mypgsqldb** sob ele.
 ![pgAdmin – Criar – Banco de Dados](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Limpar recursos

Limpar todos os recursos criados no guia de início rápido Olá excluindo Olá [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Outros inícios rápidos nessa coleção aproveitam esse início rápido. Se você planeja toocontinue toowork com subsequentes guias de início rápido, não a limpeza hello recursos criados neste guia de início rápido. Se você não planeja toocontinue, use Olá toodelete as etapas a seguir todos os recursos criados por este guia de início rápido no hello CLI do Azure.

```azurecli-interactive
az group delete --name myresourcegroup
```

Se você apenas deseja toodelete Olá um recém-criado servidor, você pode executar [exclusão do servidor postgres az](/cli/azure/postgres/server#delete) comando.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
