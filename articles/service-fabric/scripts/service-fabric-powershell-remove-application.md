---
title: Exemplo de Script do PowerShell - remover aplicativo de um cluster de aaaAzure | Microsoft Docs
description: "Exemplo de script do Azure PowerShell – remover um aplicativo de um cluster do Service Fabric."
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Remover um aplicativo de um cluster do Service Fabric

Esse script de exemplo exclui uma instância de aplicativo de malha do serviço em execução, cancela o registro de um tipo de aplicativo e a versão do cluster hello e exclui o pacote de aplicativo Olá Olá cluster do repositório de imagens.  Excluindo instância de aplicativo hello também exclui Olá todas as instâncias de serviço associadas a esse aplicativo em execução. Personalize parâmetros Olá conforme necessário. 

Se necessário, instale o módulo do PowerShell do Service Fabric Olá com hello [SDK do Service Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Remove uma instância em execução de aplicativo de malha do serviço de cluster hello.  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Cancela o registro de um tipo de aplicativo de malha do serviço e a versão do cluster hello. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Remove um pacote de aplicativo do Service Fabric saudação do repositório de imagens.|

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Service Fabric hello, consulte [documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Exemplos adicionais do Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).
