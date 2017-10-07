---
title: AAA "CLI do Azure Script - criar um banco de dados do Azure para PostgreSQL | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – cria um Banco de Dados do Azure para servidor PostgreSQL e configura uma regra de firewall no nível do servidor."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>Criar um banco de dados do Azure para o servidor PostgreSQL e configurar uma regra de firewall usando Olá CLI do Azure
Este exemplo de script da CLI cria um Banco de Dados do Azure para servidor PostgreSQL e configura uma regra de firewall no nível do servidor. Depois que o script hello foi executado com êxito, servidor de PostgreSQL Olá pode ser acessado de todos os serviços do Azure e Olá configurado o endereço IP.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo
Esse script de exemplo, edite Olá realçado linhas toocustomize Olá administrador username e password.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Limpar implantação
Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Explicação sobre o script
Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| **Comando** | **Observações** |
|---|---|
| [az group create](/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az postgres server create](/cli/azure/postgres/server#create) | Cria um servidor PostgreSQL que hospeda os bancos de dados de saudação. |
| [az postgres server firewall create](/cli/azure/postgres/server/firewall-rule#create) | Cria um servidor de toohello de acesso do firewall regra tooallow e bancos de dados sob ele do intervalo de endereços IP hello inserido. |
| [az group delete](/cli/azure/group#delete) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas
- Para obter mais informações sobre Olá CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview)
- Experimente scripts adicionais: [Exemplos da CLI do Azure para o Banco de Dados do Azure para PostgreSQL](../sample-scripts-azure-cli.md)
