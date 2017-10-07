---
title: "Exemplo de implantação do serviço malha Script CLI do aaaAzure"
description: "Implantar um cluster de Azure Service Fabric do aplicativo tooan usando Olá CLI de malha do serviço do Azure"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="6e785-103">Implantar um cluster do aplicativo tooa Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e785-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="6e785-104">Esse script de exemplo copia um repositório de imagens de cluster do aplicativo pacote tooa, registra o tipo de aplicativo hello no cluster hello e cria uma instância de aplicativo do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6e785-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="6e785-105">Todos os serviços padrão também são criados nesse momento.</span><span class="sxs-lookup"><span data-stu-id="6e785-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="6e785-106">Se necessário, instale Olá [CLI de malha do serviço](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6e785-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="6e785-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6e785-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6e785-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="6e785-108">Clean up deployment</span></span>

<span data-ttu-id="6e785-109">Quando terminar, Olá [remover](cli-remove-application.md) script pode ser usado tooremove Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e785-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="6e785-110">script de remoção de saudação exclui a instância do aplicativo hello, cancela o registro de tipo de aplicativo hello e exclui o pacote de aplicativo de saudação do armazenamento de imagem.</span><span class="sxs-lookup"><span data-stu-id="6e785-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e785-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e785-111">Next steps</span></span>

<span data-ttu-id="6e785-112">Para obter mais informações, consulte Olá [documentação CLI de malha do serviço](../service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6e785-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="6e785-113">Exemplos adicionais de CLI de malha do serviço para serviço de malha do Azure podem ser encontrados no hello [exemplos de CLI de malha do serviço](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6e785-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
