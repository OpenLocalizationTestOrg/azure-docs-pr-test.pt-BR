---
title: "AAA \"pool do Azure Batch Excluir evento concluída | Microsoft Docs\""
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="31a9b-103">Evento de conclusão de exclusão de pool</span><span class="sxs-lookup"><span data-stu-id="31a9b-103">Pool delete complete event</span></span>

 <span data-ttu-id="31a9b-104">Esse evento é emitido quando uma operação de exclusão de pool é concluída.</span><span class="sxs-lookup"><span data-stu-id="31a9b-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="31a9b-105">Olá, exemplo a seguir mostra o corpo de saudação de um evento de conclusão de excluir pool.</span><span class="sxs-lookup"><span data-stu-id="31a9b-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="31a9b-106">Elemento</span><span class="sxs-lookup"><span data-stu-id="31a9b-106">Element</span></span>|<span data-ttu-id="31a9b-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="31a9b-107">Type</span></span>|<span data-ttu-id="31a9b-108">Observações</span><span class="sxs-lookup"><span data-stu-id="31a9b-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="31a9b-109">ID</span><span class="sxs-lookup"><span data-stu-id="31a9b-109">id</span></span>|<span data-ttu-id="31a9b-110">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="31a9b-110">String</span></span>|<span data-ttu-id="31a9b-111">id de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="31a9b-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="31a9b-112">startTime</span><span class="sxs-lookup"><span data-stu-id="31a9b-112">startTime</span></span>|<span data-ttu-id="31a9b-113">Datetime</span><span class="sxs-lookup"><span data-stu-id="31a9b-113">DateTime</span></span>|<span data-ttu-id="31a9b-114">tempo de saudação excluir pool Olá iniciado.</span><span class="sxs-lookup"><span data-stu-id="31a9b-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="31a9b-115">endTime</span><span class="sxs-lookup"><span data-stu-id="31a9b-115">endTime</span></span>|<span data-ttu-id="31a9b-116">Datetime</span><span class="sxs-lookup"><span data-stu-id="31a9b-116">DateTime</span></span>|<span data-ttu-id="31a9b-117">Olá tempo excluir pool Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="31a9b-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="31a9b-118">Comentários</span><span class="sxs-lookup"><span data-stu-id="31a9b-118">Remarks</span></span>
<span data-ttu-id="31a9b-119">Para obter mais informações sobre estados e códigos de erro para a operação de redimensionamento do pool, consulte [Excluir um pool de uma conta](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="31a9b-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>