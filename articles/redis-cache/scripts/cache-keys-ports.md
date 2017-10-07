---
title: aaaAzure exemplo de Script CLI - Get hello nome de host, portas e chaves para Cache Redis do Azure | Microsoft Docs
description: "Exemplo de Script CLI do Azure - Get hello nome do host, portas e chaves para uma instância de Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Obter Olá nome de host, portas e chaves de Cache Redis do Azure

Nesse cenário, você aprenderá como chaves, portas e tooretrieve Olá hostname usado instância de Cache Redis do Azure tooan tooconnect.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos tooretrieve Olá hostname, chaves e portas de uma instância de Cache Redis do Azure a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [apresentação de redis az](https://docs.microsoft.com/cli/azure/redis#show) | Recupere os detalhes de uma instância de Cache Redis do Azure. |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | Recupere chaves de acesso para uma instância de Cache Redis do Azure. |


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI do Azure Redis Cache adicionais podem ser encontrados no hello [documentação do Cache Redis do Azure](../cli-samples.md).
