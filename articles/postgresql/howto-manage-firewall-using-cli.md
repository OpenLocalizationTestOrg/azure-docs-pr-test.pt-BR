---
title: aaaCreate e gerenciar o banco de dados PostgreSQL para regras de firewall usando a CLI do Azure | Microsoft Docs
description: Este artigo descreve como toocreate e gerenciar o banco de dados PostgreSQL para regras de firewall usando a linha de comando CLI do Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando a CLI do Azure
Regras de firewall de nível de servidor Habilitar administradores toomanage acesso tooan banco de dados do Azure para PostgreSQL Server de um endereço IP específico ou intervalo de endereços IP. Usando os comandos de CLI do Azure convenientes, você pode criar, atualizar, excluir, lista e mostrar toomanage de regras de firewall em seu servidor. Para obter uma visão geral dos firewalls do Banco de Dados do Azure para PostgreSQL, confira [Regras de firewall do servidor de Banco de Dados do Azure para PostgreSQL](concepts-firewall-rules.md)

## <a name="prerequisites"></a>Pré-requisitos
toostep por este tooguide como, você precisa:
- Um [Banco de Dados do Azure para servidor e banco de dados PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Instalar [2.0 do CLI do Azure](/cli/azure/install-azure-cli) linha de comando utilitário ou use Olá Shell de nuvem do Azure no navegador de saudação.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Configurar regras de firewall para o Banco de Dados do Azure para PostgreSQL
Olá [regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule) comandos são regras de firewall de tooconfigure usado.

## <a name="list-firewall-rules"></a>Listar regras de firewall 
toolist Olá existente de regras de firewall de servidor no servidor de saudação, executar Olá [lista de regra de firewall de servidor az postgres](/cli/azure/postgres/server/firewall-rule#list) comando.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
Se houver, por padrão em JSON formatar a saída de Hello lista regras hello. Você pode usar o comutador hello `--output table` para um formato mais legível da tabela como saída de hello.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Criar uma regra de firewall
toocreate uma nova regra de firewall no servidor de saudação, execute Olá [criar regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#create) comando. 

Este exemplo permite que um intervalo de todos os servidores de saudação IP endereços tooaccess **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
fornecer tooallow um tooaccess singular de endereço IP, Olá mesmo endereço como Olá IP inicial e final de IP, como neste exemplo.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
Ao ser bem-sucedido, a saída do comando de saudação lista detalhes Olá Olá de regra de firewall criadas por padrão no formato JSON. Se houver uma falha, o hello saída showserror texto da mensagem.

## <a name="update-firewall-rule"></a>Atualizar uma regra de firewall 
Atualizar uma regra de firewall existente no servidor usando o hello [atualização de regra de firewall de servidor az postgres](/cli/azure/postgres/server/firewall-rule#update) comando. Forneça o nome de saudação da regra de firewall existente hello como entrada e a saudação inicial IP e término IP atributos tooupdate.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
Ao ser bem-sucedido, a saída do comando de saudação lista detalhes Olá Olá de regra de firewall atualizado, por padrão, no formato JSON. Se houver uma falha, o hello saída showserror texto da mensagem.
> [!NOTE]
> Se a regra de firewall de saudação não existir, ele é criado pelo comando de atualização de saudação.

## <a name="show-firewall-rule-details"></a>Mostrar detalhes da regra de firewall
Você também pode exibir detalhes da regra para um servidor de firewall existente Olá executando [Mostrar de regra de firewall de servidor az postgres](/cli/azure/postgres/server/firewall-rule#show) comando.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Ao ser bem-sucedido, a saída do comando de saudação lista detalhes Olá Olá de regra de firewall especificado, por padrão, no formato JSON. Se houver uma falha, o hello saída showserror texto da mensagem.

## <a name="delete-firewall-rule"></a>Excluir regra de firewall
toorevoke acesso para um intervalo IP do servidor de saudação, excluir uma regra de firewall existente executando Olá [Excluir regra de firewall de servidor de postgres de az](/cli/azure/postgres/server/firewall-rule#delete) comando. Forneça o nome de Olá Olá existente de regra de firewall.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Após o êxito, não haverá saída. Em caso de falha, o texto de mensagem de erro de saudação é retornado.

## <a name="next-steps"></a>Próximas etapas
- Da mesma forma, você pode usar um navegador da web muito[criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando Olá portal do Azure](howto-manage-firewall-using-portal.md)
- Entenda mais sobre [Regras de firewall do servidor de Banco de Dados do Azure para PostgreSQL](concepts-firewall-rules.md)
- Para obter ajuda na conexão tooan banco de dados para o servidor PostgreSQL, consulte [bibliotecas de Conexão para o banco de dados do Azure para PostgreSQL](concepts-connection-libraries.md)
