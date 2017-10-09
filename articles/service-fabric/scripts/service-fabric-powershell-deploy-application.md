---
title: aaaAzure exemplo de Script do PowerShell - implantar aplicativo tooa cluster | Microsoft Docs
description: "Script do PowerShell do Azure de exemplo: implantar um cluster de malha do serviço do aplicativo tooa."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Implantar um cluster do aplicativo tooa Service Fabric

Esse script de exemplo copia um repositório de imagens de cluster do aplicativo pacote tooa, registra o tipo de aplicativo hello no cluster hello e cria uma instância de aplicativo do tipo de aplicativo hello.  Se todos os serviços padrão foram definidos no manifesto de aplicativo de saudação do tipo de aplicativo de destino hello, esses serviços são criados no momento. Personalize parâmetros Olá conforme necessário. 

Se necessário, instale o módulo do PowerShell do Service Fabric Olá com hello [SDK do Service Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Após a execução do exemplo de script hello, Olá script [remover um aplicativo](service-fabric-powershell-remove-application.md) pode ser usado tooremove Olá aplicativo instância, cancelar o registro do tipo de aplicativo hello e excluir pacote de aplicativo hello saudação do repositório de imagens.

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copie um repositório de imagem do aplicativo pacote toohello cluster.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Registra um tipo de aplicativo e a versão no cluster hello. |
|[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Cria um aplicativo com base em um tipo de aplicativo registrado. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Service Fabric hello, consulte [documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Exemplos adicionais do Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).
