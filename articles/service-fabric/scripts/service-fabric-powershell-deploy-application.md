---
title: "Exemplo de script do Azure PowerShell – implantar aplicativo em um cluster | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – implantar um aplicativo em um cluster do Service Fabric."
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
ms.openlocfilehash: 2863823205dbd70f63948ecd4af8898220fe1ff8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="ac043-103">Implantar um aplicativo em um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ac043-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="ac043-104">Esse script de exemplo copia um pacote de aplicativos em um repositório de imagens de cluster, registra o tipo de aplicativo no cluster e cria uma instância do aplicativo com base no tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac043-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span>  <span data-ttu-id="ac043-105">Se algum serviço padrão tiver sido definido no manifesto do aplicativo do tipo de aplicativo de destino, ele também será criado nesse momento.</span><span class="sxs-lookup"><span data-stu-id="ac043-105">If any default services were defined in the application manifest of the target application type, then those services are created at this time.</span></span> <span data-ttu-id="ac043-106">Personalize os parâmetros conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="ac043-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="ac043-107">Se necessário, instale o módulo Service Fabric do PowerShell com o [SDK do Service Fabric](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ac043-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ac043-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ac043-108">Sample script</span></span>

<span data-ttu-id="ac043-109">[!code-powershell[principal](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Implantar um aplicativo em um cluster")]</span><span class="sxs-lookup"><span data-stu-id="ac043-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ac043-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ac043-110">Clean up deployment</span></span> 

<span data-ttu-id="ac043-111">Depois que o exemplo de script foi executado, o script em [Remover um aplicativo](service-fabric-powershell-remove-application.md) pode ser usado para remover a instância do aplicativo, cancelar o registro do tipo de aplicativo e excluir o pacote de aplicativos do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="ac043-111">After the script sample has been run, the script in [Remove an application](service-fabric-powershell-remove-application.md) can be used to remove the application instance, unregister the application type, and delete the application package from the image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="ac043-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ac043-112">Script explanation</span></span>

<span data-ttu-id="ac043-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="ac043-113">This script uses the following commands.</span></span> <span data-ttu-id="ac043-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="ac043-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ac043-115">Command</span><span class="sxs-lookup"><span data-stu-id="ac043-115">Command</span></span> | <span data-ttu-id="ac043-116">Observações</span><span class="sxs-lookup"><span data-stu-id="ac043-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac043-117">Copy-ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="ac043-117">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="ac043-118">Copia um pacote de aplicativos para o repositório de imagens de cluster.</span><span class="sxs-lookup"><span data-stu-id="ac043-118">Copy an application package to the cluster image store.</span></span>  |
|[<span data-ttu-id="ac043-119">Register-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="ac043-119">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="ac043-120">Registra o tipo e a versão do aplicativo no cluster.</span><span class="sxs-lookup"><span data-stu-id="ac043-120">Registers an application type and version on the cluster.</span></span> |
|[<span data-ttu-id="ac043-121">New-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="ac043-121">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="ac043-122">Cria um aplicativo com base em um tipo de aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="ac043-122">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac043-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac043-123">Next steps</span></span>

<span data-ttu-id="ac043-124">Para obter mais informações sobre o módulo do PowerShell do Service Fabric, confira [Documentação do Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ac043-124">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="ac043-125">Mais exemplos do PowerShell para o Azure Service Fabric podem ser encontrados nos [exemplos do Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ac043-125">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
