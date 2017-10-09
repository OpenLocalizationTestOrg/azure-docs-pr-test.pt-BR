---
title: "aaaAzure exemplo remover serviço malha CLI do Script"
description: "Remover um aplicativo de um cluster do Azure Service Fabric usando Olá CLI de malha do serviço do Azure"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="7b90e-103">Remover um aplicativo de um cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7b90e-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="7b90e-104">Esse script de exemplo exclui uma instância de aplicativo de malha do serviço em execução, cancela o registro de um tipo de aplicativo e a versão do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7b90e-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster.</span></span>  <span data-ttu-id="7b90e-105">Excluindo instância de aplicativo hello também exclui Olá todas as instâncias de serviço associadas a esse aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="7b90e-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="7b90e-106">Em seguida, os arquivos de aplicativo hello são excluídos saudação do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="7b90e-106">Next, hello application files are deleted from hello image store.</span></span> 

<span data-ttu-id="7b90e-107">Se necessário, instale Olá [CLI de malha do serviço](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7b90e-107">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="7b90e-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="7b90e-108">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a><span data-ttu-id="7b90e-109">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b90e-109">Next steps</span></span>

<span data-ttu-id="7b90e-110">Para obter mais informações, consulte Olá [documentação CLI de malha do serviço](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7b90e-110">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="7b90e-111">Exemplos adicionais de CLI de malha do serviço para serviço de malha do Azure podem ser encontrados no hello [exemplos de CLI de malha do serviço](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7b90e-111">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
