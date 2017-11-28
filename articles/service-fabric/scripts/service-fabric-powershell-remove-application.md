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
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="f2421-103">Remover um aplicativo de um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f2421-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="f2421-104">Esse script de exemplo exclui uma instância de aplicativo de malha do serviço em execução, cancela o registro de um tipo de aplicativo e a versão do cluster hello e exclui o pacote de aplicativo Olá Olá cluster do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="f2421-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="f2421-105">Excluindo instância de aplicativo hello também exclui Olá todas as instâncias de serviço associadas a esse aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="f2421-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="f2421-106">Personalize parâmetros Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f2421-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="f2421-107">Se necessário, instale o módulo do PowerShell do Service Fabric Olá com hello [SDK do Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f2421-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f2421-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="f2421-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="f2421-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="f2421-109">Script explanation</span></span>

<span data-ttu-id="f2421-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f2421-110">This script uses hello following commands.</span></span> <span data-ttu-id="f2421-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="f2421-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f2421-112">Command</span><span class="sxs-lookup"><span data-stu-id="f2421-112">Command</span></span> | <span data-ttu-id="f2421-113">Observações</span><span class="sxs-lookup"><span data-stu-id="f2421-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f2421-114">Remove-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="f2421-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="f2421-115">Remove uma instância em execução de aplicativo de malha do serviço de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f2421-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="f2421-116">Unregister-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="f2421-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="f2421-117">Cancela o registro de um tipo de aplicativo de malha do serviço e a versão do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f2421-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="f2421-118">Remove-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="f2421-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="f2421-119">Remove um pacote de aplicativo do Service Fabric saudação do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="f2421-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f2421-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2421-120">Next steps</span></span>

<span data-ttu-id="f2421-121">Para obter mais informações sobre o módulo do PowerShell do Service Fabric hello, consulte [documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f2421-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="f2421-122">Exemplos adicionais do Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f2421-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
