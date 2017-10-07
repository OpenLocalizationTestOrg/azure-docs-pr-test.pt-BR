---
title: Projetar seu primeiro Banco de Dados do Azure para PostgreSQL usando a CLI do Azure | Microsoft Docs
description: Este tutorial mostra como tooDesign do Azure primeiro banco de dados para PostgreSQL usando a CLI do Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Criar seu primeiro Banco de Dados do Azure para PostgreSQL usando a CLI do Azure 
Neste tutorial, você usar Azure CLI (interface de linha de comando) e outros utilitários toolearn como para:
> [!div class="checklist"]
> * Criar um Banco de Dados do Azure para o PostgreSQL
> * Configurar o firewall do servidor de saudação
> * Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilitário um banco de dados
> * Carregar dados de exemplo
> * Consultar dados
> * Atualizar dados
> * Restaurar dados

Você pode usar o hello Shell de nuvem do Azure no navegador hello, ou [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli) em seus próprios blocos de código do computador toorun Olá neste tutorial.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se você tiver várias assinaturas, escolha Olá a assinatura de apropriado no qual o recurso de saudação existe ou é cobrado por. Selecione uma ID da assinatura específica em sua conta usando o comando [az account set](/cli/azure/account#set).
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

Olá, exemplo a seguir cria um servidor chamado `mypgserver-20170401` em seu grupo de recursos `myresourcegroup` com logon de administrador de servidor `mylogin`. Nome de um servidor mapeia o nome tooDNS e, portanto, é necessário toobe globalmente exclusivo no Azure. Olá substituto `<server_admin_password>` com seu próprio valor.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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
>

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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Conecte-se tooAzure banco de dados para o banco de dados PostgreSQL usando psql
Se o computador cliente tem PostgreSQL instalado, você pode usar uma instância local do [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), ou Olá Console de nuvem do Azure tooconnect tooan PostgreSQL Azure server. Agora vamos usar Olá psql utilitário de linha de comando tooconnect toohello banco de dados para o servidor PostgreSQL.

1. Executar Olá psql comando tooconnect tooan banco de dados PostgreSQL servidor a seguir
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Por exemplo, Olá comando a seguir conecta o banco de dados padrão toohello chamado **postgres** no seu servidor PostgreSQL **mypgserver 20170401.postgres.database.azure.com** usando as credenciais de acesso. Digite hello `<server_admin_password>` você escolheu quando solicitado para a senha.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  Quando estiver conectado toohello server, crie um banco de dados em branco no prompt de saudação.
```sql
CREATE DATABASE mypgsqldb;
```

3.  No prompt de hello, execute Olá após o banco de dados do comando tooswitch conexão toohello recém-criado **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Criar tabelas no banco de dados de saudação
Agora que você sabe como tooconnect toohello banco de dados do Azure para PostgreSQL, podemos ir como toocomplete algumas tarefas básicas.

Primeiro, criamos uma tabela e a carregamos com alguns dados. Vamos criar uma tabela que rastreia informações de inventário.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Você pode ver Olá recém-criado tabela na lista de saudação de tabelas agora digitando:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Carregar dados em tabelas de saudação
Agora que temos uma tabela, podemos inserir alguns dados nela. Na janela de prompt de comando aberta hello, executar Olá tooinsert de consulta a seguir algumas linhas de dados
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Você tem agora duas linhas de dados de exemplo na tabela de saudação criado anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar e atualizar dados Olá nas tabelas de saudação
Execute Olá consultar tooretrieve informações a seguir da tabela de banco de dados de saudação. 
```sql
SELECT * FROM inventory;
```

Você também pode atualizar dados Olá nas tabelas de saudação
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

linha de saudação obtém atualizada quando você recuperar dados.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar um ponto anterior do banco de dados tooa no tempo
Imagine que você excluiu acidentalmente uma tabela. Isso é algo que você não pode se recuperar facilmente. Banco de dados do Azure para PostgreSQL permite voltar tooany de toogo point-in-time (em Olá última too7 dias (Basic) e 35 dias (padrão)) e restaurar esse point-in-time tooa novo servidor. Você pode usar esse novo toorecover de servidor os dados excluídos. Olá etapas Olá exemplo server tooa ponto de restauração da seguir antes de saudação tabela foi adicionada.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Olá `az postgres server restore` comando precisa Olá parâmetros a seguir:
| Configuração | Valor sugerido | Descrição  |
| --- | --- | --- |
| --resource-group |  myResourceGroup |  O grupo de recursos no qual Olá o servidor de origem existe.  |
| --nome | restaurado mypgserver | nome de Olá do novo servidor de saudação é criado pelo comando de restauração de saudação. |
| Restauração-point-in-time | 2017-04-13T13:59:00Z | Selecione um toorestore point-in-time para. Essa data e hora devem ser dentro do período de retenção de backup do servidor de origem hello. Use o formato ISO8601 de data e hora. Por exemplo, você pode usar seu próprio fuso horário local, como `2017-04-13T05:59:00-08:00`, ou usar o formato UTC Zulu `2017-04-13T13:59:00Z`. |
| --servidor de origem | mypgserver-20170401 | nome de saudação ou ID do hello toorestore de servidor de origem do. |

Restaurar um servidor tooa point-in-time cria um novo servidor, copiando como servidor de saudação original a partir do ponto de saudação no horário especificado. local de saudação e preços valores nível para o servidor de saudação restaurada são Olá mesmo que o servidor de origem hello.

comando Olá é síncrono e retornará depois Olá servidor for restaurado. Quando termina de restauração hello, localize o servidor de novo Olá que foi criado. Verifique se Olá dados foi restaurados conforme o esperado.


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toouse Azure CLI (interface de linha de comando) e outros utilitários para:
> [!div class="checklist"]
> * Criar um Banco de Dados do Azure para o PostgreSQL
> * Configurar o firewall do servidor de saudação
> * Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilitário um banco de dados
> * Carregar dados de exemplo
> * Consultar dados
> * Atualizar dados
> * Restaurar dados

Em seguida, Aprenda como toouse Olá tarefas semelhantes toodo portal do Azure, examine este tutorial: [criar seu primeiro banco de dados do Azure para PostgreSQL usando Olá portal do Azure](tutorial-design-database-using-azure-portal.md)
