---
title: "aaaHow toocreate um namespace de barramento de serviço no portal do Azure de saudação | Microsoft Docs"
description: "Crie um namespace de barramento de serviço usando Olá portal do Azure."
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
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a><span data-ttu-id="e4f65-103">Criar um namespace de barramento de serviço usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e4f65-103">Create a Service Bus namespace using hello Azure portal</span></span>

<span data-ttu-id="e4f65-104">Um namespace é um contêiner de escopo para todos os componentes de mensagem.</span><span class="sxs-lookup"><span data-stu-id="e4f65-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="e4f65-105">Várias filas e tópicos podem residir em um único namespace e os namespaces geralmente servem como contêineres de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e4f65-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="e4f65-106">Há duas maneiras diferentes toocreate um namespace de barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="e4f65-106">There are two different ways toocreate a Service Bus namespace:</span></span>

1. <span data-ttu-id="e4f65-107">Portal do Azure (este artigo)</span><span class="sxs-lookup"><span data-stu-id="e4f65-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="e4f65-108">[Modelos do Gerenciador de Recursos][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="e4f65-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-hello-azure-portal"></a><span data-ttu-id="e4f65-109">Criar um namespace no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e4f65-109">Create a namespace in hello Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="e4f65-110">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e4f65-110">Congratulations!</span></span> <span data-ttu-id="e4f65-111">Agora você criou um namespace Mensagens do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="e4f65-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4f65-112">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4f65-112">Next steps</span></span>

<span data-ttu-id="e4f65-113">Confira nosso [GitHub exemplos][github-samples], que mostram algumas das hello mais avançados recursos de mensagens do barramento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f65-113">Check out our [GitHub samples][github-samples], which show some of hello more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
