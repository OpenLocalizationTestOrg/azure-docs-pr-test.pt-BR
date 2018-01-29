---
title: "Exemplo de CLI para mover um pool elástico do banco de dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo da CLI do Azure para mover um banco de dados SQL em um pool elástico do SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune, mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 6da859530cd692d80f82270cb599483041612db7
ms.sourcegitcommit: 4ac89872f4c86c612a71eb7ec30b755e7df89722
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a>Usar a CLI para mover um banco de dados SQL do Azure em um pool elástico do SQL

Este exemplo de script da CLI do Azure cria dois pools elásticos e move um banco de dados SQL do Azure de um pool elástico do SQL para outro pool elástico do SQL, depois move um banco de dados de um pool elástico para um nível de desempenho de banco de dados individual. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior. Execute `az --version` para encontrar a versão. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Limpar implantação

Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#az_sql_server_create) | Cria um servidor lógico que hospeda um banco de dados ou pool elástico. |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pool#az_sql_elastic_pool_create) | Cria um pool elástico dentro do servidor lógico. |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#az_sql_db_create) | Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool. |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#az_sql_db_update) | Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Os exemplos de script da CLI do Banco de Dados SQL adicionais podem ser encontrados na [documentação do Banco de Dados SQL do Azure](../sql-database-cli-samples.md).


