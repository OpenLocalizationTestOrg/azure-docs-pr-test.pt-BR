---
title: "Exemplo de script da CLI do Azure - Criar um aplicativo Web do ASP.NET Core em um contêiner de encaixe | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Criar um aplicativo Web do ASP.NET Core em um contêiner de encaixe"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5d1e2c7d2815df5fb9c176ec290a18d330ea3f7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a>Criar um aplicativo Web do ASP.NET Core em um contêiner do Docker

Nesse cenário, você aprenderá como criar um grupo de recursos, o Plano do Serviço de Aplicativo do Linux e o aplicativo Web e implantar um aplicativo ASP.NET Core usando um contêiner de encaixe.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior. Execute `az --version` para encontrar a versão. Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Docker do Linux")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos para criar um grupo de recursos, um aplicativo Web e todos os recursos relacionados. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um Plano do Serviço de Aplicativo. Isso é como um farm de servidores para seu aplicativo Web do Azure. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Cria um aplicativo Web do Azure. |
| [az webapp config container set](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | Define o contêiner do Docker para o aplicativo Web do Azure. |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).
