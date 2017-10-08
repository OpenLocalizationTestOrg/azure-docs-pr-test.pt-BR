---
title: aaaDesign do Azure primeiro banco de dados para o banco de dados MySQL - CLI do Azure | Microsoft Docs
description: "Este tutorial explica como toocreate e gerenciar o banco de dados do Azure para o MySQL server e banco de dados usando o Azure CLI 2.0 na linha de comando de saudação."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Projetar seu primeiro Banco de Dados do Azure para o banco de dados MySQL

Banco de dados do Azure para MySQL é um serviço de banco de dados relacional na nuvem da Microsoft com base no mecanismo de banco de dados MySQL Community Edition de saudação. Neste tutorial, você usar Azure CLI (interface de linha de comando) e outros utilitários toolearn como para:

> [!div class="checklist"]
> * Criar um Banco de Dados do Azure para MySQL
> * Configurar o firewall do servidor de saudação
> * Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate um banco de dados
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
Crie um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) com o comando [az group create](https://docs.microsoft.com/cli/azure/group#create). Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.

Olá, exemplo a seguir cria um grupo de recursos denominado `mycliresource` em Olá `westus` local.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Criar um servidor de Banco de Dados do Azure para MySQL
Crie um banco de dados do Azure para o servidor MySQL com do mysql server Olá az criar comando. Um servidor pode gerenciar vários bancos de dados. Normalmente, um banco de dados separado é usado para cada projeto ou para cada usuário.

Olá, exemplo a seguir cria um banco de dados do Azure para o MySQL server localizado em `westus` no grupo de recursos de saudação `mycliresource` com o nome `mycliserver`. servidor de saudação tem um logon de administrador denominado `myadmin` e a senha `Password01!`. servidor de saudação é criado com **básica** nível de desempenho e **50** unidades compartilhadas entre todos os bancos de dados de Olá no servidor de saudação de computação. Você pode escalonar a computação e armazenamento para cima ou para baixo dependendo das necessidades do aplicativo hello.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurar regra de firewall
Crie um banco de dados do Azure para o comando de criar a regra de firewall no nível do servidor MySQL com hello az mysql server-regra de firewall. Uma regra de firewall de nível de servidor permite que um aplicativo externo, como **mysql** ferramenta de linha de comando ou o servidor de tooyour de tooconnect do MySQL Workbench através do firewall de serviço do Azure MySQL hello. 

Olá, exemplo a seguir cria uma regra de firewall para um intervalo de endereços predefinidos. Este exemplo mostra Olá todo possíveis intervalo de endereços IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Obter informações de conexão Olá

tooconnect tooyour server, você precisa ter credenciais de acesso e informações de host de tooprovide.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

resultado de saudação está no formato JSON. Anote Olá **fullyQualifiedDomainName** e **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a>Conecte-se o servidor toohello usando mysql
Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour uma conexão banco de dados do Azure para o MySQL server. Neste exemplo, o comando de saudação é:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Criar um banco de dados vazio
Quando estiver conectado toohello server, crie um banco de dados em branco.
```sql
mysql> CREATE DATABASE mysampledb;
```

No prompt de hello, execute Olá banco de dados do comando tooswitch Olá conexão toothis recém-criado a seguir:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Criar tabelas no banco de dados de saudação
Agora que você sabe como tooconnect toohello banco de dados para o banco de dados MySQL, podemos ir como toocomplete algumas tarefas básicas.

Primeiro, criamos uma tabela e a carregamos com alguns dados. Vamos criar uma tabela que armazena informações de inventário.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Carregar dados em tabelas de saudação
Agora que temos uma tabela, podemos inserir alguns dados nela. Na janela de prompt de comando aberta hello, execute Olá tooinsert de consulta a seguir algumas linhas de dados.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Agora você tem duas linhas de dados de exemplo na tabela de saudação criado anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar e atualizar dados Olá nas tabelas de saudação
Execute Olá consultar tooretrieve informações a seguir da tabela de banco de dados de saudação.
```sql
SELECT * FROM inventory;
```

Você também pode atualizar dados Olá nas tabelas de saudação.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

linha de saudação obtém atualizada quando você recuperar dados.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar um ponto anterior do banco de dados tooa no tempo
Imagine que você excluiu acidentalmente essa tabela. Isso é algo que você não pode se recuperar facilmente. Banco de dados do Azure para MySQL permite que você toogo tooany back ponto no tempo no hello última até too35 dias e esse ponto no novo servidor tooa do tempo de restauração. Você pode usar esse novo toorecover de servidor os dados excluídos. Olá etapas Olá exemplo server tooa ponto de restauração da seguir antes de saudação tabela foi adicionada.

Olá restauração é necessário Olá informações a seguir:

- Ponto de restauração: selecione um point-in-time que ocorre antes que o servidor de saudação foi alterado. Deve ser maior que ou igual ao valor de backup mais antigo toohello origem do banco de dados.
- Servidor de destino: forneça um novo nome de servidor que você deseja toorestore para
- Servidor de origem: fornecer nome de saudação do servidor de saudação desejado toorestore de
- Local: Não é possível selecionar região hello, por padrão, ele é igual ao servidor de origem Olá

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

servidor de saudação toorestore e [restauração point-in-time tooa](./howto-restore-server-portal.md) antes Olá tabela foi excluída. Restaurar o servidor tooa outro ponto no tempo cria um duplicado novo servidor como servidor de saudação original como de saudação ponto no tempo especificado, desde que está dentro do período de retenção de saudação de seu [camada de serviço](./concepts-service-tiers.md).

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu a:
> [!div class="checklist"]
> * Criar um Banco de Dados do Azure para MySQL
> * Configurar o firewall do servidor de saudação
> * Use [ferramenta de linha de comando do mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate um banco de dados
> * Carregar dados de exemplo
> * Consultar dados
> * Atualizar dados
> * Restaurar dados

> [!div class="nextstepaction"]
> [Banco de Dados do Azure para MySQL - Exemplos da CLI do Azure](./sample-scripts-azure-cli.md)
