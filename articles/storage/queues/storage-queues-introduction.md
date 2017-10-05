---
title: "Introdução ao Armazenamento de filas do Azure | Microsoft Docs"
description: "Introdução ao Armazenamento de filas do Azure"
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
ms.openlocfilehash: 4db7552a1b76c89151405c55c8682abbb5326bb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-queues"></a><span data-ttu-id="eef17-103">Introdução às Filas</span><span class="sxs-lookup"><span data-stu-id="eef17-103">Introduction to Queues</span></span>

<span data-ttu-id="eef17-104">O armazenamento de filas do Azure é um serviço para armazenamento de um grande número de mensagens que podem ser acessadas de qualquer lugar do mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eef17-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="eef17-105">Uma única mensagem de fila pode ter até 64 KB de tamanho e uma fila pode conter milhões de mensagens, até o limite de capacidade total de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eef17-105">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="eef17-106">Usos comuns</span><span class="sxs-lookup"><span data-stu-id="eef17-106">Common uses</span></span>

<span data-ttu-id="eef17-107">Usos comuns de Armazenamento de filas incluem:</span><span class="sxs-lookup"><span data-stu-id="eef17-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="eef17-108">Criar uma lista de pendências de trabalho para processar de maneira assíncrona</span><span class="sxs-lookup"><span data-stu-id="eef17-108">Creating a backlog of work to process asynchronously</span></span>
* <span data-ttu-id="eef17-109">Transmitir mensagens de uma função Web do Azure para uma função de Trabalho do Azure</span><span class="sxs-lookup"><span data-stu-id="eef17-109">Passing messages from an Azure web role to an Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="eef17-110">Conceitos do serviço Fila</span><span class="sxs-lookup"><span data-stu-id="eef17-110">Queue service concepts</span></span>

<span data-ttu-id="eef17-111">O serviço Fila contém os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="eef17-111">The Queue service contains the following components:</span></span>

![Conceitos de fila](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="eef17-113">**Formato da URL:** as filas são acessadas usando o seguinte formato de URL:</span><span class="sxs-lookup"><span data-stu-id="eef17-113">**URL format:** Queues are addressable using the following URL format:</span></span>   
    <span data-ttu-id="eef17-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="eef17-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="eef17-115">A URL a seguir endereça um fila no diagrama:</span><span class="sxs-lookup"><span data-stu-id="eef17-115">The following URL addresses a queue in the diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="eef17-116">**Conta de armazenamento:** todo o acesso ao Armazenamento do Azure é feito por meio de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eef17-116">**Storage account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="eef17-117">Consulte [Escalabilidade e Metas de Desempenho do Armazenamento do Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) para obter detalhes sobre a capacidade da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eef17-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="eef17-118">**Fila:** uma fila contém um conjunto de mensagens.</span><span class="sxs-lookup"><span data-stu-id="eef17-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="eef17-119">Todas as mensagens devem estar em uma fila.</span><span class="sxs-lookup"><span data-stu-id="eef17-119">All messages must be in a queue.</span></span> <span data-ttu-id="eef17-120">Observe que o nome da fila deve estar em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="eef17-120">Note that the queue name must be all lowercase.</span></span> <span data-ttu-id="eef17-121">Para saber mais sobre filas de nomenclatura, confira [Nomenclatura de filas e metadados](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="eef17-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="eef17-122">**Mensagem:** uma mensagem, em qualquer formato, de até 64 KB.</span><span class="sxs-lookup"><span data-stu-id="eef17-122">**Message:** A message, in any format, of up to 64 KB.</span></span> <span data-ttu-id="eef17-123">O tempo máximo que uma mensagem pode ficar na fila é de sete dias.</span><span class="sxs-lookup"><span data-stu-id="eef17-123">The maximum time that a message can remain in the queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eef17-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eef17-124">Next steps</span></span>

* [<span data-ttu-id="eef17-125">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="eef17-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="eef17-126">Introdução às filas usando .NET</span><span class="sxs-lookup"><span data-stu-id="eef17-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
