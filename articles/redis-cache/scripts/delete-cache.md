---
title: aaaAzure exemplo de Script CLI - excluir um Cache Redis do Azure | Microsoft Docs
description: "Exemplo de Script da CLI do Azure – excluir um Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 788277f6464d40fedc597ce7f3041130312c07a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-azure-redis-cache"></a>Excluir um Cache Redis do Azure

Nesse cenário, você aprenderá como toodelete um Cache Redis do Azure.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toodelete uma instância de Cache Redis do Azure a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [exclusão de redis az](https://docs.microsoft.com/cli/azure/redis#delete) | Excluir uma instância do Cache Redis. |


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI do Azure Redis Cache adicionais podem ser encontrados no hello [documentação do Cache Redis do Azure](../cli-samples.md).
