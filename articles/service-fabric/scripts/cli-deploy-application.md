---
title: "Exemplo de implantação do serviço malha Script CLI do aaaAzure"
description: "Implantar um cluster de Azure Service Fabric do aplicativo tooan usando Olá CLI de malha do serviço do Azure"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Implantar um cluster do aplicativo tooa Service Fabric

Esse script de exemplo copia um repositório de imagens de cluster do aplicativo pacote tooa, registra o tipo de aplicativo hello no cluster hello e cria uma instância de aplicativo do tipo de aplicativo hello. Todos os serviços padrão também são criados nesse momento.

Se necessário, instale Olá [CLI de malha do serviço](../service-fabric-cli.md).

## <a name="sample-script"></a>Script de exemplo

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Limpar implantação

Quando terminar, Olá [remover](cli-remove-application.md) script pode ser usado tooremove Olá aplicativo. script de remoção de saudação exclui a instância do aplicativo hello, cancela o registro de tipo de aplicativo hello e exclui o pacote de aplicativo de saudação do armazenamento de imagem.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte Olá [documentação CLI de malha do serviço](../service-fabric-cli.md).

Exemplos adicionais de CLI de malha do serviço para serviço de malha do Azure podem ser encontrados no hello [exemplos de CLI de malha do serviço](../samples-cli.md).
