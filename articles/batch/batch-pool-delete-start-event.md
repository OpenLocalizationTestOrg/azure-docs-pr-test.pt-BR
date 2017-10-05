---
title: "Iniciar eventos de exclusão de pool lote do Azure | Documentos do Microsoft"
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
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="b290c-103">Evento inicial de exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="b290c-103">Pool delete start event</span></span>

 <span data-ttu-id="b290c-104">Esse evento é emitido quando uma operação de exclusão de pool é iniciada.</span><span class="sxs-lookup"><span data-stu-id="b290c-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="b290c-105">Como a exclusão do pool é um evento assíncrono, você pode esperar que um evento completo de conclusão de exclusão de pool seja emitido quando a operação de exclusão é concluída.</span><span class="sxs-lookup"><span data-stu-id="b290c-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="b290c-106">O exemplo a seguir mostra o corpo de um evento de início de exclusão de pool.</span><span class="sxs-lookup"><span data-stu-id="b290c-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="b290c-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="b290c-107">Element</span></span>|<span data-ttu-id="b290c-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="b290c-108">Type</span></span>|<span data-ttu-id="b290c-109">Observações</span><span class="sxs-lookup"><span data-stu-id="b290c-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="b290c-110">ID</span><span class="sxs-lookup"><span data-stu-id="b290c-110">id</span></span>|<span data-ttu-id="b290c-111">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b290c-111">String</span></span>|<span data-ttu-id="b290c-112">A ID do pool.</span><span class="sxs-lookup"><span data-stu-id="b290c-112">The id of the pool.</span></span>|