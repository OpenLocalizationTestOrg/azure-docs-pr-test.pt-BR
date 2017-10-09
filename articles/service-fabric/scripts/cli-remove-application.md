---
title: "aaaAzure exemplo remover serviço malha CLI do Script"
description: "Remover um aplicativo de um cluster do Azure Service Fabric usando Olá CLI de malha do serviço do Azure"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Remover um aplicativo de um cluster do Service Fabric

Esse script de exemplo exclui uma instância de aplicativo de malha do serviço em execução, cancela o registro de um tipo de aplicativo e a versão do cluster hello.  Excluindo instância de aplicativo hello também exclui Olá todas as instâncias de serviço associadas a esse aplicativo em execução. Em seguida, os arquivos de aplicativo hello são excluídos saudação do repositório de imagens. 

Se necessário, instale Olá [CLI de malha do serviço](../service-fabric-cli.md).

## <a name="sample-script"></a>Script de exemplo

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte Olá [documentação CLI de malha do serviço](../service-fabric-cli.md).

Exemplos adicionais de CLI de malha do serviço para serviço de malha do Azure podem ser encontrados no hello [exemplos de CLI de malha do serviço](../samples-cli.md).
