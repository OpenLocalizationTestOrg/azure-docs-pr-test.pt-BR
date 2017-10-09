---
title: "parâmetros de serviço Olá aaaConfigure no banco de dados do Azure para PostgreSQL | Microsoft Docs"
description: "Este artigo descreve como parâmetros de serviço de saudação tooconfigure no banco de dados do Azure para usar PostgreSQL Olá a linha de comando CLI do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Personalizar os parâmetros de configuração do servidor usando a CLI do Azure
Você pode listar, mostrar e atualizar os parâmetros de configuração para um servidor do Azure PostgreSQL usando Olá Interface de linha de comando (CLI do Azure). No entanto, somente um subconjunto de configurações de mecanismo é exposto no nível do servidor e pode ser modificado. 

## <a name="prerequisites"></a>Pré-requisitos
toostep por este tooguide como, você precisa:
- Um servidor e um banco de dados [Criar um Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Instalar [2.0 do CLI do Azure](/cli/azure/install-azure-cli) linha de comando utilitário ou use Olá Shell de nuvem do Azure no navegador de saudação.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Listar os parâmetros de configuração de servidor para o bando de dados do Azure para servidor PostgreSQL
execução de todos os parâmetros modificáveis em um servidor e seus valores, toolist Olá [lista de configuração de servidor az postgres](/cli/azure/postgres/server/configuration#list) comando.

Você pode listar os parâmetros de configuração de servidor Olá para o servidor de saudação **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Mostrar detalhes do parâmetro de configuração do servidor
tooshow detalhes sobre um parâmetro de configuração específico para um servidor, execute Olá [Mostrar de configuração de servidor az postgres](/cli/azure/postgres/server/configuration#show) comando.

Este exemplo mostra detalhes de saudação **log\_min\_mensagens** parâmetro de configuração de servidor para servidor **mypgserver 20170401.postgres.database.azure.com** em grupo de recursos **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Modificar o valor do parâmetro de configuração do servidor
Você também pode modificar o valor de saudação de um determinado parâmetro de configuração do servidor, e isso atualiza o valor de configuração subjacentes Olá para o mecanismo do hello PostgreSQL server. saudação de uso de configuração de Olá tooupdate [conjunto de configurações de servidor az postgres](/cli/azure/postgres/server/configuration#set) comando. 

Olá tooupdate **log\_min\_mensagens** parâmetro de configuração do servidor do servidor **mypgserver 20170401.postgres.database.azure.com** dogrupoderecursos**myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Se você desejar tooreset Olá valor de um parâmetro de configuração, você simplesmente escolher tooleave out Olá opcional `--value` parâmetro e serviço Olá aplicará o valor padrão de saudação. No exemplo acima, ele teria a seguinte aparência:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Isso irá redefinir Olá **log\_min\_mensagens** valor padrão da configuração toohello **aviso**. Para obter mais detalhes sobre a configuração do servidor e os valores permitidos, veja a documentação do PostgreSQL em [Configuração do Servidor](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Próximas etapas
- logs do servidor tooconfigure e acesso, consulte [Logs do servidor no banco de dados do Azure para PostgreSQL](concepts-server-logs.md)
