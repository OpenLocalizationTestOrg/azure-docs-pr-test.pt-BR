---
title: aaaCreate e gerenciar o banco de dados MySQL para regras de firewall usando a CLI do Azure | Microsoft Docs
description: Este artigo descreve como toocreate e gerenciar o banco de dados MySQL para regras de firewall usando a linha de comando CLI do Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando a CLI do Azure
Regras de firewall de nível de servidor Habilitar administradores toomanage acesso tooan banco de dados do Azure para MySQL Server de um endereço IP específico ou intervalo de endereços IP. Usando os comandos de CLI do Azure convenientes, você pode criar, atualizar, excluir, lista e mostrar toomanage de regras de firewall em seu servidor. Para obter uma visão geral dos firewalls do Banco de Dados do Azure para MySQL, confira [Regras de firewall do servidor de Banco de Dados do Azure para MySQL](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>Pré-requisitos
* [Instalar a CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Instalar o SDK do Azure Python para os serviços PostgreSQL e MySQL
* Instalar o componente de CLI do Azure Olá para serviços PostgreSQL e MySQL
* Criar um servidor de Banco de Dados do Azure para MySQL

## <a name="firewall-rule-commands"></a>Comandos de regra de firewall:
Olá **regra de firewall de servidor de mysql de az** comando é usado da CLI do Azure toocreate, excluir, listar, mostrar e atualizar regras de firewall.

Comandos:
- **create**: crie uma regra de firewall de servidor MySQL do Azure.
- **delete**: exclua uma regra de firewall de servidor MySQL do Azure.
- **lista** : lista de regras de firewall de servidor hello Azure MySQL.
- **Mostrar** : Mostrar detalhes de saudação de um servidor MySQL Azure regra de firewall.
- **update**: atualize uma regra de firewall de servidor MySQL do Azure.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>Logon tooAzure e lista o banco de dados do Azure para servidores de MySQL
Conecte com segurança à CLI do Azure com sua conta do Azure. Saudação de uso **logon az** comando toodo isso.

1. Execute Olá comando a seguir na linha de comando hello.
```azurecli
az login
```
Este comando produzirá um toouse de código na próxima etapa do hello.

2. Use um navegador da web página da saudação tooopen [https://aka.ms/devicelogin](https://aka.ms/devicelogin) e insira o código de saudação.

3. No prompt de hello, faça logon usando suas credenciais do Azure.

4. Depois que o seu logon for autorizado, uma lista de assinaturas será impressa no console de saudação. Copie a id de saudação do hello desejado assinatura tooset Olá atual assinatura toobe usada no futuro.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Se você não tiver certeza dos nomes de saudação, lista hello bancos de dados do Azure para servidores de MySQL para sua assinatura e grupo de recursos.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Observe o atributo de nome de saudação no hello listando, que será usado toospecify quais toowork do servidor MySQL no. Se necessário, confirme os detalhes de saudação para esse servidor toousing Olá atributo tooconfirm nome está correto:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Listar regras de firewall no servidor de Banco de Dados do Azure para MySQL 
Usando o nome do servidor de saudação e nome do grupo de recursos hello, lista Olá servidor regras de firewall existentes no servidor de saudação. Observe que esse atributo de nome de servidor de saudação é especificado no hello **– servidor** alternar e não Olá **– nome** alternar.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
saída de Hello lista regras Olá se houver, por padrão em JSON de formato. Você pode usar o comutador hello **– tabela de saída** para um formato mais legível da tabela como saída de hello.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Criar uma regra de firewall no servidor de Banco de Dados do Azure para MySQL
Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, crie uma nova regra de firewall no servidor de saudação. Forneça um nome para a regra Olá Olá IP de início e IP final para a regra de saudação toocover um acesso de tooallow de endereços IP do intervalo.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Para um único endereço IP toobe permissão de acesso, forneça Olá mesmo endereço como Olá IP inicial e final de IP, como neste exemplo.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Ao ser bem-sucedido, a saída do comando Olá listará detalhes Olá Olá de regra de firewall criadas por padrão no formato JSON. Se houver uma falha, saída de hello mostrará texto da mensagem de erro.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Atualizar uma regra de firewall no servidor de Banco de Dados do Azure para MySQL 
Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, atualize uma regra de firewall existente no servidor de saudação. Forneça o nome de saudação da regra de firewall existente hello como entrada e a saudação inicial IP e término IP atributos tooupdate.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Ao ser bem-sucedido, a saída do comando Olá listará detalhes Olá Olá de regra de firewall atualizado, por padrão, no formato JSON. Se houver uma falha, saída de hello mostrará texto da mensagem de erro.

> [!NOTE]
> Se a regra de firewall de saudação não existir, ele será criado pelo comando de atualização de saudação.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Mostrar detalhes de uma regra de firewall no servidor de Banco de Dados do Azure para MySQL
Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, mostre Olá existente firewall detalhes da regra do servidor de saudação. Forneça o nome de saudação da regra de firewall existente hello como entrada.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Ao ser bem-sucedido, a saída do comando Olá listará detalhes Olá Olá de regra de firewall especificado, por padrão, no formato JSON. Se houver uma falha, saída de hello mostrará texto da mensagem de erro.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Excluir uma regra de firewall no servidor de Banco de Dados do Azure para MySQL
Usando o nome do servidor MySQL Azure hello e nome do grupo de recursos hello, remova uma regra de firewall existente do servidor de saudação. Forneça o nome de Olá Olá existente de regra de firewall.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Após o êxito, não haverá saída. Em caso de falha, o texto de mensagem de erro de saudação será retornado.

## <a name="next-steps"></a>Próximas etapas
- Entenda mais sobre [Regras de firewall do servidor de Banco de Dados do Azure para MySQL](./concepts-firewall-rules.md)
- [Criar e gerenciar o banco de dados MySQL para regras de firewall usando Olá portal do Azure](./howto-manage-firewall-using-portal.md)
