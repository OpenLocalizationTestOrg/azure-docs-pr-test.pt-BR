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
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="bb59a-103">Fazer upgrade de um aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bb59a-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="bb59a-104">Esse exemplo de script faz upgrade de uma instância de aplicativo do Service Fabric em execução para a versão 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="bb59a-104">This sample script upgrades a running Service Fabric application instance to version 1.3.0.</span></span> <span data-ttu-id="bb59a-105">O script copia o novo pacote de aplicativos para o repositório de imagens de cluster, registra o tipo de aplicativo, inicia um upgrade monitorado e verifica o status do upgrade continuamente até que o upgrade seja concluído ou revertido.</span><span class="sxs-lookup"><span data-stu-id="bb59a-105">The script copies the new application package to the cluster image store, registers the application type, starts a monitored upgrade, and continuously checks the upgrade status until the upgrade completes or rolls back.</span></span> <span data-ttu-id="bb59a-106">Personalize os parâmetros conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="bb59a-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="bb59a-107">Se necessário, instale o módulo Service Fabric do PowerShell com o [SDK do Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb59a-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bb59a-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="bb59a-108">Sample script</span></span>

<span data-ttu-id="bb59a-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade de um aplicativo")]</span><span class="sxs-lookup"><span data-stu-id="bb59a-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="bb59a-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="bb59a-110">Script explanation</span></span>

<span data-ttu-id="bb59a-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="bb59a-111">This script uses the following commands.</span></span> <span data-ttu-id="bb59a-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="bb59a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bb59a-113">Command</span><span class="sxs-lookup"><span data-stu-id="bb59a-113">Command</span></span> | <span data-ttu-id="bb59a-114">Observações</span><span class="sxs-lookup"><span data-stu-id="bb59a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bb59a-115">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="bb59a-115">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="bb59a-116">Obtém todos os aplicativos no cluster do Service Fabric ou um aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="bb59a-116">Gets all the applications in the Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="bb59a-117">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="bb59a-117">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="bb59a-118">Obtém o status do upgrade de um aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb59a-118">Gets the status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="bb59a-119">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="bb59a-119">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="bb59a-120">Obtém os tipos de aplicativo do Service Fabric registrados no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb59a-120">Gets the Service Fabric application types registered on the Service Fabric cluster.</span></span> |
| [<span data-ttu-id="bb59a-121">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="bb59a-121">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="bb59a-122">Cancela o registro de um tipo de aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb59a-122">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="bb59a-123">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="bb59a-123">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="bb59a-124">Copia um pacote de aplicativos do Service Fabric para o repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="bb59a-124">Copies a Service Fabric application package to the image store.</span></span>  |
| [<span data-ttu-id="bb59a-125">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="bb59a-125">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="bb59a-126">Registra um tipo de aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb59a-126">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="bb59a-127">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="bb59a-127">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="bb59a-128">Faz upgrade de um aplicativo do Service Fabric para a versão do tipo de aplicativo especificado.</span><span class="sxs-lookup"><span data-stu-id="bb59a-128">Upgrades a Service Fabric application to the specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="bb59a-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb59a-129">Next steps</span></span>

<span data-ttu-id="bb59a-130">Para obter mais informações sobre o módulo do PowerShell do Service Fabric, confira [Documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="bb59a-130">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="bb59a-131">Mais exemplos do PowerShell para o Azure Service Fabric podem ser encontrados nos [exemplos do Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bb59a-131">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
