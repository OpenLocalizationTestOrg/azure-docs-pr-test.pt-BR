---
title: "aaaAzure exemplo de Script CLI - criar um aplicativo de função em um plano de serviço de aplicativo | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um Aplicativo de funções em um Plano do Serviço de Aplicativo"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a>Criar um Aplicativo de funções em um Plano do Serviço de Aplicativo

Este exemplo de script cria um Aplicativo de funções do Azure, que é um contêiner para suas funções. saudação de função de aplicativo é criada usando um plano de serviço de aplicativo dedicado, que significa que os recursos do servidor estão sempre ativados.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

Esse script cria um Aplicativo de funções do Azure usando um [plano do Serviço de Aplicativo](../functions-scale.md#app-service-plan) dedicado.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação sobre o script

Cada comando na documentação específica do toocommand Olá tabela links. Esse script usa Olá comandos a seguir:

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Cria uma conta de armazenamento do Azure. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appserviceplan#create) | Cria um Plano do Serviço de Aplicativo. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#delete) | Cria um Aplicativo de funções do Azure. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI do Azure funções adicionais podem ser encontrados no hello [documentação de funções do Azure](../functions-cli-samples.md).
