---
title: "aaaAzure exemplo de Script CLI - rotear o tráfego para alta disponibilidade de aplicativos | Microsoft Docs"
description: "Exemplo de script da CLI do Azure - Rotear o tráfego para alta disponibilidade de aplicativos"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Rotear o tráfego para alta disponibilidade de aplicativos

Este script cria um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego. Traffic Manager direciona o aplicativo de toohello de tráfego em uma região, como região primária hello e região secundária toohello quando o aplicativo hello na região primária Olá não está disponível. Antes de executar o script hello, você deve alterar Olá MyWebApp, MyWebAppL1 e MyWebAppL2 valores toounique valores no Azure. Depois de executar o script hello, você pode acessar o aplicativo de saudação em região primária Olá Olá URL mywebapp.trafficmanager.net.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>Limpar implantação 

Após a execução do exemplo de script hello, Olá siga comando pode ser usado tooremove grupo de recursos de saudação, aplicativo de serviço de aplicativo e recursos todos relacionados.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, o aplicativo web, o perfil do Gerenciador de tráfego a seguir, e todos os recursos relacionados. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um Plano do Serviço de Aplicativo. Isso é como um farm de servidores para seu aplicativo Web do Azure. |
| [az appservice web create](https://docs.microsoft.com/cli/azure/appservice/web#create) | Cria um aplicativo web do Azure em Olá plano de serviço de aplicativo. |
| [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Cria um perfil de Gerenciador de Tráfego do Azure. |
| [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Adiciona um ponto de extremidade tooan perfil do Gerenciador de tráfego do Azure. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação de rede do Azure](../cli-samples.md).
