---
title: "AAA \"evento de início do lote do Azure pool delete | Microsoft Docs\""
description: "Referência para excluir um pool de lote evento inicial."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="30f5e-103">Evento inicial de exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="30f5e-103">Pool delete start event</span></span>

 <span data-ttu-id="30f5e-104">Esse evento é emitido quando uma operação de exclusão de pool é iniciada.</span><span class="sxs-lookup"><span data-stu-id="30f5e-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="30f5e-105">Desde que a exclusão do pool de saudação é um evento assíncrono, você pode esperar um toobe de evento de conclusão de excluir pool emitido depois que a operação de exclusão de saudação for concluída.</span><span class="sxs-lookup"><span data-stu-id="30f5e-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="30f5e-106">Olá, exemplo a seguir mostra Olá corpo de um evento de início de exclusão do pool.</span><span class="sxs-lookup"><span data-stu-id="30f5e-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="30f5e-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="30f5e-107">Element</span></span>|<span data-ttu-id="30f5e-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="30f5e-108">Type</span></span>|<span data-ttu-id="30f5e-109">Observações</span><span class="sxs-lookup"><span data-stu-id="30f5e-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="30f5e-110">ID</span><span class="sxs-lookup"><span data-stu-id="30f5e-110">id</span></span>|<span data-ttu-id="30f5e-111">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="30f5e-111">String</span></span>|<span data-ttu-id="30f5e-112">id de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="30f5e-112">hello id of hello pool.</span></span>|
