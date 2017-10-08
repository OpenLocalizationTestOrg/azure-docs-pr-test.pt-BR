---
title: "aaaCreate uma função do Azure que se conecta tooan banco de dados do Azure Cosmos | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma função do Azure que se conecta tooan Azure Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a>Criar uma função do Azure que se conecta tooan Azure Cosmos DB

Esse script de exemplo cria um aplicativo de função do Azure e conecta-se o banco de dados de banco de dados do Azure Cosmos tooan.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

Este exemplo cria um aplicativo de função do Azure e adiciona uma configuração de chave tooapp Cosmos DB ponto de extremidade e acesso.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Limpar implantação

Após a execução do exemplo de script hello, Olá acompanhamento pode ser usado tooremove grupo de recursos de saudação e todos os recursos relacionados.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | TooAzure de logon. |
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Criar um grupo de recursos com local |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | Criar uma conta de armazenamento |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#create) | Criar um novo aplicativo de funções |
| [az documentdb create](https://docs.microsoft.com/cli/azure/documentdb#create) | Criar banco de dados do documentdb |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Limpar |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).




