---
title: aaaAzure exemplo de Script do PowerShell - criar um cluster do Service Fabric | Microsoft Docs
description: "Exemplo de script do Azure PowerShell – criar um cluster do Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>Criar um cluster do Service Fabric

Esse script de exemplo cria um cluster do Service Fabric, um cluster de cinco nós protegido com um certificado X.509.  comando Olá cria um certificado autoassinado e carrega-tooa novo cofre de chave. certificado de Olá também é um diretório local tooa copiado.  Saudação de conjunto *-OS* versão de saudação do parâmetro toochoose do Windows ou Linux que é executado em nós de cluster de saudação.  Personalize parâmetros Olá conforme necessário.

Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure. 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, cluster e recursos todos relacionados.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [New-AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Cria um novo cluster do Service Fabric. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos adicionais do Azure Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).
