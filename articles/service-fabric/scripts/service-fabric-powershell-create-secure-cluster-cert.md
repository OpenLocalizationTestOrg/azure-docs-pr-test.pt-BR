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
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="11726-103">Criar um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="11726-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="11726-104">Esse script de exemplo cria um cluster do Service Fabric, um cluster de cinco nós protegido com um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="11726-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="11726-105">comando Olá cria um certificado autoassinado e carrega-tooa novo cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="11726-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="11726-106">certificado de Olá também é um diretório local tooa copiado.</span><span class="sxs-lookup"><span data-stu-id="11726-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="11726-107">Saudação de conjunto *-OS* versão de saudação do parâmetro toochoose do Windows ou Linux que é executado em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="11726-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="11726-108">Personalize parâmetros Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="11726-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="11726-109">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="11726-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="11726-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="11726-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="11726-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="11726-111">Clean up deployment</span></span> 

<span data-ttu-id="11726-112">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, cluster e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="11726-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="11726-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="11726-113">Script explanation</span></span>

<span data-ttu-id="11726-114">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="11726-114">This script uses hello following commands.</span></span> <span data-ttu-id="11726-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="11726-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="11726-116">Command</span><span class="sxs-lookup"><span data-stu-id="11726-116">Command</span></span> | <span data-ttu-id="11726-117">Observações</span><span class="sxs-lookup"><span data-stu-id="11726-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="11726-118">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="11726-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="11726-119">Cria um novo cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="11726-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="11726-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11726-120">Next steps</span></span>

<span data-ttu-id="11726-121">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="11726-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="11726-122">Exemplos adicionais do Azure Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="11726-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
