---
title: "Evento de exclusão de pool – Azure | Microsoft Docs"
description: "Referência de exclusão do pool de lote evento inicial."
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
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="5cac1-103">Evento de conclusão de exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="5cac1-103">Pool delete complete event</span></span>

 <span data-ttu-id="5cac1-104">Esse evento é emitido quando uma operação de exclusão de pool é concluída.</span><span class="sxs-lookup"><span data-stu-id="5cac1-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="5cac1-105">O exemplo a seguir mostra o corpo de um evento de conclusão de exclusão de pool.</span><span class="sxs-lookup"><span data-stu-id="5cac1-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="5cac1-106">Elemento</span><span class="sxs-lookup"><span data-stu-id="5cac1-106">Element</span></span>|<span data-ttu-id="5cac1-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="5cac1-107">Type</span></span>|<span data-ttu-id="5cac1-108">Observações</span><span class="sxs-lookup"><span data-stu-id="5cac1-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="5cac1-109">ID</span><span class="sxs-lookup"><span data-stu-id="5cac1-109">id</span></span>|<span data-ttu-id="5cac1-110">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5cac1-110">String</span></span>|<span data-ttu-id="5cac1-111">A ID do pool.</span><span class="sxs-lookup"><span data-stu-id="5cac1-111">The id of the pool.</span></span>|
|<span data-ttu-id="5cac1-112">startTime</span><span class="sxs-lookup"><span data-stu-id="5cac1-112">startTime</span></span>|<span data-ttu-id="5cac1-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="5cac1-113">DateTime</span></span>|<span data-ttu-id="5cac1-114">A hora de início da exclusão do pool.</span><span class="sxs-lookup"><span data-stu-id="5cac1-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="5cac1-115">endTime</span><span class="sxs-lookup"><span data-stu-id="5cac1-115">endTime</span></span>|<span data-ttu-id="5cac1-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="5cac1-116">DateTime</span></span>|<span data-ttu-id="5cac1-117">A hora de conclusão da exclusão do pool.</span><span class="sxs-lookup"><span data-stu-id="5cac1-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="5cac1-118">Comentários</span><span class="sxs-lookup"><span data-stu-id="5cac1-118">Remarks</span></span>
<span data-ttu-id="5cac1-119">Para obter mais informações sobre estados e códigos de erro para a operação de redimensionamento do pool, consulte [Excluir um pool de uma conta](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="5cac1-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>