---
title: "Criar uma Função do Azure que se conecta a um armazenamento Azure | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Criar uma função do Azure que se conecta a um armazenamento Azure"
services: functions
documentationcenter: functions
author: ggailey777
manager: cfowler
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 363a3fd1c80538495658720274840b921baa8675
ms.sourcegitcommit: 29bac59f1d62f38740b60274cb4912816ee775ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a>Integrar o Aplicativo de funções à conta de armazenamento do Azure

Este exemplo de script cria um Aplicativo de funções e uma Conta de armazenamento.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você usar a CLI localmente, garanta que está executando a versão 2.0 ou posteriores da CLI do Azure. Para saber qual é a versão, execute `az --version`. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure](/cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

Este exemplo cria um Aplicativo de funções do Azure e adiciona a cadeia de conexão de armazenamento para uma configuração de aplicativo.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a>Limpar implantação

Após executar o exemplo de script, execute o comando a seguir para remover o grupo de recursos e todos os recursos relacionados:

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | Fazer logon no Azure. |
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | Criar um grupo de recursos com local |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | Criar uma conta de armazenamento |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#az_functionapp_create) | Criar um novo aplicativo de funções |
| [az group delete](https://docs.microsoft.com/cli/azure/group#az_group_delete) | Limpar |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos adicionais de scripts da CLI do Azure Functions podem ser encontrados na [Documentação do Azure Functions](../functions-cli-samples.md).
