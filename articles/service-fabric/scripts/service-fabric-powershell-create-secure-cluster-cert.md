---
title: "Exemplo de script do Azure PowerShell – criar um cluster do Service Fabric | Microsoft Docs"
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
ms.openlocfilehash: 7cbeb3da695af3815ba660f9cc2e3388abb6f87d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="b5973-103">Criar um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b5973-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="b5973-104">Esse script de exemplo cria um cluster do Service Fabric, um cluster de cinco nós protegido com um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="b5973-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="b5973-105">O comando cria um certificado autoassinado e o carrega em um novo cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b5973-105">The command creates a self-signed certificate and uploads it to a new key vault.</span></span> <span data-ttu-id="b5973-106">O certificado também é copiado para um diretório local.</span><span class="sxs-lookup"><span data-stu-id="b5973-106">The certificate is also copied to a local directory.</span></span>  <span data-ttu-id="b5973-107">Defina o parâmetro *-OS* para escolher a versão do Windows ou Linux que é executada nos nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="b5973-107">Set the *-OS* parameter to choose the version of Windows or Linux that runs on the cluster nodes.</span></span>  <span data-ttu-id="b5973-108">Personalize os parâmetros conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="b5973-108">Customize the parameters as needed.</span></span>

<span data-ttu-id="b5973-109">Se necessário, instale o Azure PowerShell usando as instruções encontradas no [Guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="b5973-109">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b5973-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b5973-110">Sample script</span></span>

<span data-ttu-id="b5973-111">[!code-powershell[principal](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Criar um cluster do Service Fabric")]</span><span class="sxs-lookup"><span data-stu-id="b5973-111">[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b5973-112">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="b5973-112">Clean up deployment</span></span> 

<span data-ttu-id="b5973-113">Após a execução do exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos, o cluster e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b5973-113">After the script sample has been run, the following command can be used to remove the resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="b5973-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b5973-114">Script explanation</span></span>

<span data-ttu-id="b5973-115">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="b5973-115">This script uses the following commands.</span></span> <span data-ttu-id="b5973-116">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="b5973-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b5973-117">Command</span><span class="sxs-lookup"><span data-stu-id="b5973-117">Command</span></span> | <span data-ttu-id="b5973-118">Observações</span><span class="sxs-lookup"><span data-stu-id="b5973-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b5973-119">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="b5973-119">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="b5973-120">Cria um novo cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b5973-120">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5973-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5973-121">Next steps</span></span>

<span data-ttu-id="b5973-122">Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5973-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b5973-123">Mais exemplos do Azure PowerShell para o Azure Service Fabric podem ser encontrados nos [exemplos do Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b5973-123">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
