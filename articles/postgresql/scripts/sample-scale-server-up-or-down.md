---
title: AAA "banco de dados no Azure de escala de Script CLI do Azure para PostgreSQL | Microsoft Docs"
description: "Exemplo de Script do Azure CLI - escala banco de dados para o nível de desempenho diferentes de tooa PostgreSQL servidor depois de consultar as métricas de saudação."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Monitore e dimensione um único servidor PostgreSQL usando a CLI do Azure
Esse exemplo de script CLI dimensiona um único banco de dados do Azure para o nível de desempenho diferentes PostgreSQL servidor tooa depois de consultar as métricas de saudação. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo
No script de exemplo, altere Olá realçado linhas toocustomize Olá administrador username e password. Substitua a id de assinatura de saudação em Olá az monitor comandos com sua id de assinatura.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Limpar implantação
Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Explicação sobre o script
Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| **Comando** | **Observações** |
|---|---|
| [az group create](/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az postgres server create](/cli/azure/postgres/server#create) | Cria um servidor PostgreSQL que hospeda os bancos de dados de saudação. |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | Lista o valor de métrica Olá para recursos de saudação. |
| [az group delete](/cli/azure/group#delete) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas
- Para obter mais informações sobre Olá CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview)
- Experimente scripts adicionais: [Exemplos da CLI do Azure para o Banco de Dados do Azure para PostgreSQL](../sample-scripts-azure-cli.md)
- Leia mais informações sobre dimensionamento: [Camadas de serviço](../concepts-service-tiers.md) e [Unidades de computação e unidades de armazenamento](../concepts-compute-unit-and-storage.md)
