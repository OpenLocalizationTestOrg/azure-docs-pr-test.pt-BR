---
title: "aaaAzure exemplo de Script do PowerShell - atualizar um aplicativo de malha do serviço | Microsoft Docs"
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
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="25303-103">Fazer upgrade de um aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="25303-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="25303-104">Esse script de exemplo atualiza um tooversion da instância de aplicativo do Service Fabric em execução 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="25303-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="25303-105">script Hello copia Olá novo aplicativo toohello cluster imagem repositório do pacote, registra o tipo de aplicativo hello, inicia uma atualização monitorada e verifica continuamente o status da atualização Olá até que a atualização Olá é concluída ou revertida.</span><span class="sxs-lookup"><span data-stu-id="25303-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="25303-106">Personalize parâmetros Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="25303-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="25303-107">Se necessário, instale o módulo do PowerShell do Service Fabric Olá com hello [SDK do Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="25303-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="25303-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="25303-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="25303-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="25303-109">Script explanation</span></span>

<span data-ttu-id="25303-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="25303-110">This script uses hello following commands.</span></span> <span data-ttu-id="25303-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="25303-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="25303-112">Command</span><span class="sxs-lookup"><span data-stu-id="25303-112">Command</span></span> | <span data-ttu-id="25303-113">Observações</span><span class="sxs-lookup"><span data-stu-id="25303-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25303-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="25303-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="25303-115">Obtém todos os aplicativos de saudação no cluster do Service Fabric hello ou um aplicativo específico.</span><span class="sxs-lookup"><span data-stu-id="25303-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="25303-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="25303-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="25303-117">Obtém o status de saudação de uma atualização de aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25303-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="25303-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="25303-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="25303-119">Obtém os tipos de aplicativos do Service Fabric Olá registrados no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="25303-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="25303-120">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="25303-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="25303-121">Cancela o registro de um tipo de aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25303-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="25303-122">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="25303-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="25303-123">Copia uma imagem de toohello do pacote de aplicativo do Service Fabric repositório.</span><span class="sxs-lookup"><span data-stu-id="25303-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="25303-124">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="25303-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="25303-125">Registra um tipo de aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="25303-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="25303-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="25303-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="25303-127">Atualiza uma versão de tipo do Service Fabric application toohello aplicativo especificado.</span><span class="sxs-lookup"><span data-stu-id="25303-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="25303-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25303-128">Next steps</span></span>

<span data-ttu-id="25303-129">Para obter mais informações sobre o módulo do PowerShell do Service Fabric hello, consulte [documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="25303-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="25303-130">Exemplos adicionais do Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="25303-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
