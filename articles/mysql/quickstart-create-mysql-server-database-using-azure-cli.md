---
title: "Início rápido: criar um servidor do Banco de Dados do Azure para MySQL – CLI do Azure | Microsoft Docs"
description: "Este guia de início rápido descreve como toouse Olá CLI do Azure toocreate um banco de dados do Azure para o MySQL server em um grupo de recursos do Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Criar um servidor de Banco de Dados do Azure para MySQL usando a CLI do Azure
Este guia de início rápido descreve como toouse Olá CLI do Azure toocreate um banco de dados do Azure para o MySQL server em um grupo de recursos do Azure em cerca de cinco minutos. Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.

Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se você tiver várias assinaturas, escolha Olá a assinatura de apropriado no qual o recurso de saudação existe ou é cobrado por. Selecione uma ID da assinatura específica em sua conta usando o comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Criar um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) usando Olá [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.

Olá, exemplo a seguir cria um grupo de recursos denominado `myresourcegroup` em Olá `westus` local.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Criar um servidor de Banco de Dados do Azure para MySQL
Criar um banco de dados do Azure para o MySQL server com hello **az mysql server criar** comando. Um servidor pode gerenciar vários bancos de dados. Normalmente, um banco de dados separado é usado para cada projeto ou para cada usuário.

Olá, exemplo a seguir cria um banco de dados do Azure para o MySQL server localizado em `westus` no grupo de recursos de saudação `myresourcegroup` com o nome `myserver4demo`. servidor de saudação tem um logon de administrador denominado `myadmin` e a senha `Password01!`. servidor de saudação é criado com **básica** nível de desempenho e **50** unidades compartilhadas entre todos os bancos de dados de Olá no servidor de saudação de computação. Você pode escalonar a computação e armazenamento para cima ou para baixo dependendo das necessidades do aplicativo hello.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurar regra de firewall
Criar um banco de dados do Azure para a regra de firewall no nível do servidor MySQL usando Olá **criar regra de firewall de servidor de mysql de az** comando. Uma regra de firewall de nível de servidor permite que um aplicativo externo, como Olá **mysql.exe** ferramenta de linha de comando ou o servidor de tooyour de tooconnect do MySQL Workbench através do firewall de serviço do Azure MySQL hello. 

Olá, exemplo a seguir cria uma regra de firewall para um intervalo de endereços predefinido, que neste exemplo é Olá todo possíveis intervalo de endereços IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Configurar definições de SSL
Por padrão, as conexões SSL entre o servidor e os aplicativos cliente são impostas.  Isso garante a segurança de "em movimento" Olá de dados criptografando o fluxo de dados Olá através da internet.  toomake esse rápido iniciar mais fácil, Desabilitaremos conexões SSL para o servidor.  Isso não é recomendável para servidores de produção.  Para obter mais informações, consulte [conectividade de configurar SSL em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL](./howto-configure-ssl.md).

Olá, exemplo a seguir desabilita impor SSL em seu servidor MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Obter informações de conexão Olá

tooconnect tooyour server, você precisa ter credenciais de acesso e informações de host de tooprovide.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

resultado de saudação está no formato JSON. Anote Olá **fullyQualifiedDomainName** e **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Conectar usando a ferramenta de linha de comando de mysql.exe de saudação do servidor de toohello
Conectar usando a saudação do servidor de tooyour **mysql.exe** ferramenta de linha de comando. Você pode baixar o MySQL [daqui](https://dev.mysql.com/downloads/) e instalá-lo em seu computador. Em vez disso, você também pode clicar Olá **Experimente** botão exemplos de código ou Olá `>_` botão de Olá superior direita barra de ferramentas do hello portal do Azure e inicialização Olá **Shell de nuvem do Azure**.

Digite os comandos a próxima hello: 

1. Conecte-se usando o servidor toohello **mysql** ferramenta de linha de comando:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Exibir o status do servidor:
```sql
 mysql> status
```
Se tudo correr bem, a ferramenta de linha de comando Olá deve gerar Olá texto a seguir:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> Para saber mais sobre outros comandos, veja [Manual de Referência do MySQL 5.7 – Capítulo 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Conecte-se o servidor toohello usando a ferramenta de GUI do MySQL Workbench Olá
1.  Inicie Olá aplicativo MySQL Workbench no computador cliente. É possível baixar e instalar o MySQL Workbench [aqui](https://dev.mysql.com/downloads/workbench/).

2.  Em Olá **Conexão nova instalação** caixa de diálogo, digite Olá seguintes informações sobre **parâmetros** guia:

   ![configurar nova conexão](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Configuração** | **Valor Sugerido** | **Descrição** |
|---|---|---|
|   Nome da Conexão | Minha Conexão | Especifique um nome para essa conexão (pode ser qualquer nome) |
| Método de Conexão | escolha o Padrão (TCP/IP) | Usar o TCP/IP protocolo tooconnect tooAzure banco de dados para MySQL > |
| Nome do host | myserver4demo.mysql.database.azure.com | O nome do servidor que você anotou anteriormente. |
| Porta | 3306 | porta padrão Olá MySQL é usada. |
| Nome de Usuário | myadmin@myserver4demo | logon de administrador de servidor Olá observado anteriormente. |
| Senha | **** | Use a senha de conta de administrador Olá configurados anteriormente. |

Clique em **Conexão de teste** tootest se todos os parâmetros estão configurados corretamente.
Agora, você pode clicar em conexão Olá toosuccessfully conectar toohello server.

## <a name="clean-up-resources"></a>Limpar recursos
Se você não precisa desses recursos para outro/tutorial de início rápido, você pode excluí-los fazendo Olá comando a seguir: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Como criar um banco de dados MySQL com a CLI do Azure](./tutorial-design-database-using-cli.md)
