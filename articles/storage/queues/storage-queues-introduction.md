---
title: aaaIntroduction tooAzure armazenamento de fila | Microsoft Docs
description: "Introdução tooAzure armazenamento de fila"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="c3ff2-103">Introdução tooQueues</span><span class="sxs-lookup"><span data-stu-id="c3ff2-103">Introduction tooQueues</span></span>

<span data-ttu-id="c3ff2-104">Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="c3ff2-105">Uma mensagem da fila única pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="c3ff2-106">Usos comuns</span><span class="sxs-lookup"><span data-stu-id="c3ff2-106">Common uses</span></span>

<span data-ttu-id="c3ff2-107">Usos comuns de Armazenamento de filas incluem:</span><span class="sxs-lookup"><span data-stu-id="c3ff2-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="c3ff2-108">Criando uma lista de pendências de trabalho tooprocess assincronamente</span><span class="sxs-lookup"><span data-stu-id="c3ff2-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="c3ff2-109">Transmissão de mensagens de uma função de trabalho do Azure de tooan de função web do Azure</span><span class="sxs-lookup"><span data-stu-id="c3ff2-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="c3ff2-110">Conceitos do serviço Fila</span><span class="sxs-lookup"><span data-stu-id="c3ff2-110">Queue service concepts</span></span>

<span data-ttu-id="c3ff2-111">Olá serviço fila contém Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3ff2-111">hello Queue service contains hello following components:</span></span>

![Conceitos de fila](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="c3ff2-113">**Formato de URL:** filas são acessadas usando Olá formato de URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3ff2-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="c3ff2-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="c3ff2-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="c3ff2-115">Olá URL a seguir aborda uma fila no diagrama de saudação:</span><span class="sxs-lookup"><span data-stu-id="c3ff2-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="c3ff2-116">**Conta de armazenamento:** todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="c3ff2-117">Consulte [Escalabilidade e Metas de Desempenho do Armazenamento do Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) para obter detalhes sobre a capacidade da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="c3ff2-118">**Fila:** uma fila contém um conjunto de mensagens.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="c3ff2-119">Todas as mensagens devem estar em uma fila.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-119">All messages must be in a queue.</span></span> <span data-ttu-id="c3ff2-120">Observe que nome de fila Olá deve ser todas minúscula.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="c3ff2-121">Para saber mais sobre filas de nomenclatura, confira [Nomenclatura de filas e metadados](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3ff2-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="c3ff2-122">**Mensagem:** A mensagem, em qualquer formato de backup too64 KB.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="c3ff2-123">tempo máximo de saudação que uma mensagem pode permanecer na fila de saudação é de sete dias.</span><span class="sxs-lookup"><span data-stu-id="c3ff2-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ff2-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3ff2-124">Next steps</span></span>

* [<span data-ttu-id="c3ff2-125">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c3ff2-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="c3ff2-126">Introdução às filas usando .NET</span><span class="sxs-lookup"><span data-stu-id="c3ff2-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
