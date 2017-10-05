---
title: "Como criar um namespace do Barramento de Serviço no portal do Azure | Microsoft Docs"
description: "Crie um namespace do Barramento de Serviço usando o Portal do Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c8654ed547a9001e2e968d2a45d990a73ef27d3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-service-bus-namespace-using-the-azure-portal"></a><span data-ttu-id="bcbff-103">Criar um namespace do Barramento de Serviço usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bcbff-103">Create a Service Bus namespace using the Azure portal</span></span>

<span data-ttu-id="bcbff-104">Um namespace é um contêiner de escopo para todos os componentes de mensagem.</span><span class="sxs-lookup"><span data-stu-id="bcbff-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="bcbff-105">Várias filas e tópicos podem residir em um único namespace e os namespaces geralmente servem como contêineres de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bcbff-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="bcbff-106">Existem duas maneiras diferentes de criar um namespace de Barramento de Serviço:</span><span class="sxs-lookup"><span data-stu-id="bcbff-106">There are two different ways to create a Service Bus namespace:</span></span>

1. <span data-ttu-id="bcbff-107">Portal do Azure (este artigo)</span><span class="sxs-lookup"><span data-stu-id="bcbff-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="bcbff-108">[Modelos do Gerenciador de Recursos][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="bcbff-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-the-azure-portal"></a><span data-ttu-id="bcbff-109">Criar um namespace no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bcbff-109">Create a namespace in the Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="bcbff-110">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="bcbff-110">Congratulations!</span></span> <span data-ttu-id="bcbff-111">Agora você criou um namespace Mensagens do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="bcbff-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcbff-112">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bcbff-112">Next steps</span></span>

<span data-ttu-id="bcbff-113">Confira nossos [exemplos do GitHub][github-samples], que mostram alguns dos recursos mais avançados de Mensagens do Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcbff-113">Check out our [GitHub samples][github-samples], which show some of the more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
