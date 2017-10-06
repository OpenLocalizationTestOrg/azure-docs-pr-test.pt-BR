---
title: aaaAzure exemplo de Script CLI - dimensionar um aplicativo Web manualmente usando o Azure CLI 2.0 | Microsoft Docs
description: Exemplo de Script CLI do Azure - Dimensionar um aplicativo Web manualmente usando a CLI do Azure 2.0
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a>Dimensionar manualmente um aplicativo Web

Nesse cenário, você aprenderá toocreate um grupo de recursos, aplicativo de serviço web e o plano de aplicativo. Em seguida, você será dimensionado Olá plano do serviço de aplicativo de instâncias de toomultiple uma única instância.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web e relacionados com todos os recursos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um Plano do Serviço de Aplicativo. Isso é como um farm de servidores para seu aplicativo Web do Azure. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Cria um aplicativo Web do Azure. |
| [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) | Atualiza as propriedades de saudação plano de serviço de aplicativo. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).
