---
title: "banco de dados do SQL Azure aaaCLI exemplo-monitor escala único | Microsoft Docs"
description: "Toomonitor de script de exemplo CLI do Azure e a escala de um único banco de dados do SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a>Use toomonitor CLI e dimensionar um único banco de dados SQL

Este exemplo de script CLI do Azure é dimensionado um único nível de desempenho diferentes de tooa de banco de dados SQL do Azure depois de consultar informações sobre o tamanho do banco de dados de saudação hello. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a>Limpar implantação

Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Cria um servidor lógico que hospeda um banco de dados. |
| [az sql db show-usage](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | Mostra informações de uso de tamanho de saudação para um banco de dados. |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#update) | Atualiza as propriedades do banco de dados (como Olá camadas ou desempenho do nível de serviço) ou move um banco de dados em, em ou entre pools elásticos. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |
|||

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI do banco de dados SQL adicionais podem ser encontrados no hello [documentação de banco de dados do Azure SQL](../sql-database-cli-samples.md).
