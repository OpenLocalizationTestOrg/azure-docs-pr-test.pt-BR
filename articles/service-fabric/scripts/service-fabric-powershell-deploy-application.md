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
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="9d240-103">Implantar um cluster do aplicativo tooa Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9d240-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="9d240-104">Esse script de exemplo copia um repositório de imagens de cluster do aplicativo pacote tooa, registra o tipo de aplicativo hello no cluster hello e cria uma instância de aplicativo do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9d240-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="9d240-105">Se todos os serviços padrão foram definidos no manifesto de aplicativo de saudação do tipo de aplicativo de destino hello, esses serviços são criados no momento.</span><span class="sxs-lookup"><span data-stu-id="9d240-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="9d240-106">Personalize parâmetros Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="9d240-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="9d240-107">Se necessário, instale o módulo do PowerShell do Service Fabric Olá com hello [SDK do Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9d240-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9d240-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="9d240-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9d240-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="9d240-109">Clean up deployment</span></span> 

<span data-ttu-id="9d240-110">Após a execução do exemplo de script hello, Olá script [remover um aplicativo](service-fabric-powershell-remove-application.md) pode ser usado tooremove Olá aplicativo instância, cancelar o registro do tipo de aplicativo hello e excluir pacote de aplicativo hello saudação do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="9d240-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="9d240-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="9d240-111">Script explanation</span></span>

<span data-ttu-id="9d240-112">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d240-112">This script uses hello following commands.</span></span> <span data-ttu-id="9d240-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="9d240-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9d240-114">Command</span><span class="sxs-lookup"><span data-stu-id="9d240-114">Command</span></span> | <span data-ttu-id="9d240-115">Observações</span><span class="sxs-lookup"><span data-stu-id="9d240-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d240-116">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="9d240-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="9d240-117">Copie um repositório de imagem do aplicativo pacote toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="9d240-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="9d240-118">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="9d240-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="9d240-119">Registra um tipo de aplicativo e a versão no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9d240-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="9d240-120">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="9d240-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="9d240-121">Cria um aplicativo com base em um tipo de aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="9d240-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d240-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d240-122">Next steps</span></span>

<span data-ttu-id="9d240-123">Para obter mais informações sobre o módulo do PowerShell do Service Fabric hello, consulte [documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="9d240-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="9d240-124">Exemplos adicionais do Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9d240-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
