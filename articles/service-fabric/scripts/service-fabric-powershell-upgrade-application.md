---
title: Exemplo de script do Azure PowerShell - Fazer upgrade de um aplicativo do Service Fabric | Microsoft Docs
description: Exemplo de script do Azure PowerShell - Fazer upgrade de um aplicativo do Service Fabric.
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 454849f82ddb23ddb9d71459f86e3cf5a1589254
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Fazer upgrade de um aplicativo do Service Fabric

Esse exemplo de script faz upgrade de uma instância de aplicativo do Service Fabric em execução para a versão 1.3.0. O script copia o novo pacote de aplicativos para o repositório de imagens de cluster, registra o tipo de aplicativo, inicia um upgrade monitorado e verifica o status do upgrade continuamente até que o upgrade seja concluído ou revertido. Personalize os parâmetros conforme necessário. 

Se necessário, instale o módulo Service Fabric do PowerShell com o [SDK do Service Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade de um aplicativo")]

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Obtém todos os aplicativos no cluster do Service Fabric ou um aplicativo específico.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Obtém o status do upgrade de um aplicativo do Service Fabric. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Obtém os tipos de aplicativo do Service Fabric registrados no cluster do Service Fabric. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Cancela o registro de um tipo de aplicativo do Service Fabric.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copia um pacote de aplicativos do Service Fabric para o repositório de imagens.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Registra um tipo de aplicativo do Service Fabric. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Faz upgrade de um aplicativo do Service Fabric para a versão do tipo de aplicativo especificado. |


## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Service Fabric, confira [Documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Mais exemplos do PowerShell para o Azure Service Fabric podem ser encontrados nos [exemplos do Azure PowerShell](../service-fabric-powershell-samples.md).
