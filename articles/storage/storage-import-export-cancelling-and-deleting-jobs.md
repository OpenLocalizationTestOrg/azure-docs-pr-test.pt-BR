---
title: "Cancelar e excluir um trabalho de Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como cancelar e excluir trabalhos do serviço de Importação/Exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="468f7-103">Cancelando e excluindo trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="468f7-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="468f7-104">É possível solicitar que um trabalho seja cancelado antes que ele entre no estado `Packaging` chamando a operação [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) e definindo o elemento `CancelRequested` como `true`.</span><span class="sxs-lookup"><span data-stu-id="468f7-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="468f7-105">O trabalho será cancelado com os melhores esforços.</span><span class="sxs-lookup"><span data-stu-id="468f7-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="468f7-106">Se as unidades estiverem transferindo dados, os dados poderão continuar sendo transferidos mesmo depois que o cancelamento tiver sido solicitado.</span><span class="sxs-lookup"><span data-stu-id="468f7-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="468f7-107">Um trabalho cancelado será movido para o estado `Completed` e mantido por 90 dias, período após o qual ele será excluído.</span><span class="sxs-lookup"><span data-stu-id="468f7-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="468f7-108">Para excluir um trabalho, chame a operação [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) antes que o trabalho seja enviado (*ou seja*, enquanto o trabalho está no estado `Creating`).</span><span class="sxs-lookup"><span data-stu-id="468f7-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="468f7-109">Também é possível excluir um trabalho quando ele está no estado `Completed`.</span><span class="sxs-lookup"><span data-stu-id="468f7-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="468f7-110">Após a exclusão de um trabalho, suas informações e seu status não são mais acessíveis por meio da API REST ou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="468f7-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="468f7-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="468f7-111">Next steps</span></span>

* [<span data-ttu-id="468f7-112">Usando a API REST do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="468f7-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
