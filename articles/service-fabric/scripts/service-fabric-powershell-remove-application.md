---
title: "Exemplo de script do Azure PowerShell – remover aplicativo de um cluster | Microsoft Docs"
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
ms.openlocfilehash: 05851132c7e5e5877884d29f04bce6c0717ce411
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="b6456-103">Remover um aplicativo de um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b6456-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="b6456-104">Esse script de exemplo exclui uma instância de aplicativo do Service Fabric em execução, cancela o registro do tipo e da versão de um aplicativo do cluster e exclui o pacote de aplicativos do repositório de imagens do cluster.</span><span class="sxs-lookup"><span data-stu-id="b6456-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from the cluster, and deletes the application package from the cluster image store.</span></span>  <span data-ttu-id="b6456-105">A exclusão da instância do aplicativo também exclui todas as instâncias de serviço em execução associadas a esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6456-105">Deleting the application instance also deletes all the running service instances associated with that application.</span></span> <span data-ttu-id="b6456-106">Personalize os parâmetros conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="b6456-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="b6456-107">Se necessário, instale o módulo Service Fabric do PowerShell com o [SDK do Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6456-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b6456-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b6456-108">Sample script</span></span>

<span data-ttu-id="b6456-109">[!code-powershell[principal](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remover um aplicativo de um cluster")]</span><span class="sxs-lookup"><span data-stu-id="b6456-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="b6456-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b6456-110">Script explanation</span></span>

<span data-ttu-id="b6456-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="b6456-111">This script uses the following commands.</span></span> <span data-ttu-id="b6456-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="b6456-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b6456-113">Command</span><span class="sxs-lookup"><span data-stu-id="b6456-113">Command</span></span> | <span data-ttu-id="b6456-114">Observações</span><span class="sxs-lookup"><span data-stu-id="b6456-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b6456-115">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="b6456-115">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="b6456-116">Remove do cluster uma instância de aplicativo do Service Fabric em execução.</span><span class="sxs-lookup"><span data-stu-id="b6456-116">Removes a running Service Fabric application instance from the cluster.</span></span>  |
| [<span data-ttu-id="b6456-117">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="b6456-117">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="b6456-118">Cancela o registro de um tipo e uma versão de aplicativo do Service Fabric do cluster.</span><span class="sxs-lookup"><span data-stu-id="b6456-118">Unregisters a Service Fabric application type and version from the cluster.</span></span> |
| [<span data-ttu-id="b6456-119">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="b6456-119">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="b6456-120">Remove do repositório de imagens um pacote de aplicativos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b6456-120">Removes a Service Fabric application package from the image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="b6456-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6456-121">Next steps</span></span>

<span data-ttu-id="b6456-122">Para obter mais informações sobre o módulo do PowerShell do Service Fabric, confira [Documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b6456-122">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="b6456-123">Mais exemplos do PowerShell para o Azure Service Fabric podem ser encontrados nos [exemplos do Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b6456-123">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
